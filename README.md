<div align="center">

# PointagePro
## L'équipe

<div align="center">

### HexSec

**Rajo** · **Meddy** · **Mihajasoa** · **Kiady**

Projet conçu et développé dans le cadre du **Data Day 2026 — Hackathon Dev**.

</div>
### La gestion de présence, réinventée.

**QR Code · Géolocalisation · 100 % Offline-First · Multi-plateforme**

[![PWA](https://img.shields.io/badge/PWA-Ready-5A0FC8?style=for-the-badge&logo=googlechrome&logoColor=white)](#)
[![Android](https://img.shields.io/badge/Android-APK-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#)
[![Desktop](https://img.shields.io/badge/Desktop-Electron-47848F?style=for-the-badge&logo=electron&logoColor=white)](#)
[![Offline First](https://img.shields.io/badge/Offline-First-00C853?style=for-the-badge&logo=cloudflare&logoColor=white)](#)
[![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge&logo=opensourceinitiative&logoColor=white)](#)

**Une seule base de code. Trois plateformes. Zéro dépendance au réseau.**
*Web (PWA) · Android (APK) · Desktop (Windows)*

[Démo](#-liens-du-projet) · [Fonctionnalités](#-fonctionnalités) · [Installation](#-installation) · [Architecture](#-architecture) · [Stack technique](#-stack-technique) · [Équipe](#-léquipe)

</div>

<br>

## Le problème

Le papier se perd. Les badgeuses coûtent cher et tombent en panne dès qu'un site est isolé. Le numérique classique exige une connexion permanente — un luxe que beaucoup de terrains n'ont pas. Résultat : des présences perdues, du temps perdu, de la confiance perdue.

**PointagePro** transforme n'importe quel smartphone ou ordinateur en terminal de pointage complet — scan QR, géolocalisation automatique — et continue de fonctionner même sans connexion internet, grâce à une base de données locale qui se synchronise dès que le réseau revient.

Conçu pour les environnements à connectivité instable (terrain, zones rurales, sites décentralisés), et développé par l'équipe **HexSec**.

<br>

## Liens du projet

| Ressource | Accès |
|---|---|
| **Application Android (APK)** | [`app-debug.apk`](https://github.com/otsutsukirajo-dev/Hexsec_-_Ideathon/releases/download/v1.0.0/app-debug.apk) |
| **Application Desktop (Windows)** | [`PointagePro.Setup.1.0.0.exe`](https://github.com/otsutsukirajo-dev/Hexsec_-_Ideathon/releases/download/v1.0.0/PointagePro.Setup.1.0.0.exe) |
| **Pitch (PowerPoint)** | [`PointagePro_DataDay2026.pptx`](./PointagePro_DataDay2026.pptx) |
| **Version web (PWA)** | Ouvrir `index.html`, ou suivre la section [Installation](#-installation) |

*L'APK Android et l'exécutable Windows sont distribués via GitHub Releases.*

<br>

## Fonctionnalités

<table>
<tr>
<th width="50%">Pour les employés</th>
<th width="50%">Pour les managers RH</th>
</tr>
<tr>
<td valign="top">

- Scan QR Code en caméra native (Android) ou navigateur
- QR Code personnel généré et téléchargeable (PNG)
- Géolocalisation automatique à chaque pointage
- Connexion et compte sécurisés
- Thème clair / sombre
- Confirmation en temps réel à chaque pointage

</td>
<td valign="top">

- Dashboard avec statistiques de présence par employé
- Export des rapports en CSV
- Export des rapports en Excel (.xls)
- Suivi du statut de synchronisation (synchronisé / en attente)
- Calcul automatique du taux de présence

</td>
</tr>
</table>

**Sous le capot**

| Capacité | Détail |
|---|---|
| Scanner QR double moteur | Scanner natif via Capacitor sur Android (APK), avec repli automatique sur `html5-qrcode` dans un navigateur classique |
| Base de données locale | IndexedDB via **Dexie.js** — chaque pointage est écrit localement puis marqué `synchro` ou `en_attente` |
| Mode Offline-First | Détection automatique de la perte et de la reprise de connexion, avec synchronisation différée des pointages en attente |
| Géolocalisation | Position GPS récupérée via `navigator.geolocation`, avec coordonnées de repli en cas de refus de permission |
| Progressive Web App | Installable depuis le navigateur, fonctionne hors-ligne via Service Worker |

<br>

## Installation

**Navigateur direct**
Ouvrir `index.html` dans Chrome, Firefox ou Safari.

**Serveur local** *(recommandé pour tester le mode PWA et le scanner caméra)*
```bash
python -m http.server 8080     # avec Python 3
npx serve .                    # avec Node.js
```
Puis ouvrir [http://localhost:8080](http://localhost:8080)

**Installer comme application (PWA)**
1. Ouvrir le projet dans Chrome
2. Cliquer sur l'icône Installer dans la barre d'adresse
3. Confirmer — l'app se comporte désormais comme une application native

**Application desktop (Electron)**
Installer directement [`PointagePro.Setup.1.0.0.exe`](https://github.com/otsutsukirajo-dev/Hexsec_-_Ideathon/releases/download/v1.0.0/PointagePro.Setup.1.0.0.exe), ou compiler depuis les sources :
```bash
npm install
npm start
npm run build:win     # génère l'exécutable Windows (.exe)
```

**Application Android**
Installer directement [`app-debug.apk`](https://github.com/otsutsukirajo-dev/Hexsec_-_Ideathon/releases/download/v1.0.0/app-debug.apk) sur un appareil Android.
Pour recompiler depuis les sources :
```bash
npx cap sync android
npx cap open android   # puis lancer le build depuis Android Studio
```

<br>

## Comptes de démonstration

| Nom | Rôle | Accès |
|---|---|---|
| Jean Dupont | Employé | Pointage QR Code |
| Marie Martin | Manager RH | Dashboard complet + Export |

La création de compte est également disponible directement depuis l'application.

<br>

## Architecture

```
pointagepro/
├── index.html                    Application complète (interface + logique)
├── app.js                        Logique métier — scanner, base de données, synchronisation
├── main.js                       Processus principal Electron
├── preload.js                    Pont sécurisé Electron
├── sw.js                         Service Worker — mode offline PWA
├── manifest.json                 Configuration PWA
├── capacitor.config.ts           Configuration Capacitor (Android)
├── android/                      Projet Android natif généré par Capacitor
├── html5-qrcode.min.js           Scanner QR pour navigateur
├── qrcode.min.js                 Génération de QR Code
├── dexie.min.js                  Wrapper IndexedDB pour le stockage offline
├── build-win.ps1                 Script de build Windows
├── package.json                  Dépendances et scripts (npm, Electron, Capacitor)
├── PointagePro_DataDay2026.pptx  Pitch de présentation
└── README.md
```

<br>

## Stack technique

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](#)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](#)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](#)
[![Dexie.js](https://img.shields.io/badge/Dexie.js-IndexedDB-FF6B00?style=flat-square&logo=databricks&logoColor=white)](#)
[![Capacitor](https://img.shields.io/badge/Capacitor-Android-119EFF?style=flat-square&logo=capacitor&logoColor=white)](#)
[![Electron](https://img.shields.io/badge/Electron-Desktop-47848F?style=flat-square&logo=electron&logoColor=white)](#)
[![Service Workers](https://img.shields.io/badge/Service_Workers-PWA-4285F4?style=flat-square&logo=googlechrome&logoColor=white)](#)

<br>

## Feuille de route

Le cœur de l'application — scan, stockage offline, synchronisation, exports — est fonctionnel dès aujourd'hui. Prochaines étapes pour un déploiement à grande échelle :

- Remplacer l'authentification côté client par un backend avec API sécurisée
- Connecter la synchronisation à un service distant (Firebase Firestore ou Supabase)
- Publier l'application sur le Google Play Store
- Ajouter des tests automatisés sur la logique de synchronisation offline/online

<br>

## L'équipe

<div align="center">

### HexSec

**Meddy** · **Rajo** · **Mario** · **Kiady** · **Rio**

Projet conçu et développé dans le cadre du **Data Day 2026 — Hackathon Dev**.

</div>

<br>

<div align="center">

*PointagePro — le pointage qui n'attend pas le réseau pour exister.*

</div>
