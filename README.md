<div align="center">

# PointagePro

### La gestion de présence, réinventée.

QR Code · Géolocalisation · 100% Offline-First · Multi-plateforme

[![PWA](https://img.shields.io/badge/PWA-Ready-5A0FC8?style=for-the-badge&logo=googlechrome&logoColor=white)](#)
[![Android](https://img.shields.io/badge/Android-APK-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#)
[![Desktop](https://img.shields.io/badge/Desktop-Electron-47848F?style=for-the-badge&logo=electron&logoColor=white)](#)
[![Offline First](https://img.shields.io/badge/Offline-First-00C853?style=for-the-badge&logo=cloudflare&logoColor=white)](#)
[![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge&logo=opensourceinitiative&logoColor=white)](#)

*Une seule base de code, déployée en PWA, en application Android (APK) et en application desktop (Windows), sans dépendre d'une connexion permanente.*

**Équipe HexSec** — Meddy · Rajo · Mario · Kiady · Rio
Projet réalisé dans le cadre du **Data Day 2026 — Hackathon Dev**.

</div>

---

## Liens du projet

| Ressource | Lien |
|---|---|
| 🎥 Démo vidéo | [À COMPLÉTER — lien YouTube/Drive non répertorié, ou "voir démonstration en direct le jour du jury"] |
| 📱 APK Android | [À COMPLÉTER — pas encore déposée, voir "Feuille de route" ci-dessous] |
| 📊 Pitch (PowerPoint) | [`PointagePro_DataDay2026.pptx`](./PointagePro_DataDay2026.pptx) |

> ⚠️ Tous les livrables sont à la racine du repo (pas de sous-dossier `deliverables/`). Dès que l'APK compilée est ajoutée, mets à jour la ligne ci-dessus avec son nom de fichier exact.

---

## Pourquoi PointagePro

Fini les feuilles de présence papier, les badgeuses hors de prix et les systèmes qui plantent dès que le réseau tousse. PointagePro transforme n'importe quel smartphone ou ordinateur en terminal de pointage — scan QR, position GPS, et ça continue de fonctionner même sans connexion internet grâce à une base de données locale qui se synchronise automatiquement au retour du réseau.

Conçu pour des contextes à connectivité instable (terrain, zones rurales, sites décentralisés), le projet a été développé par l'équipe **HexSec** dans le cadre d'un ideathon.

---

## Fonctionnalités

<table>
<tr>
<th width="50%">Pour les employés</th>
<th width="50%">Pour les managers RH</th>
</tr>
<tr>
<td valign="top">

- Scan QR Code en caméra native (Android) ou navigateur
- Génération de QR Code personnel téléchargeable (PNG)
- Géolocalisation automatique au pointage
- Création de compte et connexion sécurisée
- Thème clair / sombre
- Notifications en temps réel (toasts)

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
| Base de données locale | IndexedDB via **Dexie.js** — les pointages sont écrits localement puis marqués `synchro` ou `en_attente` |
| Mode Offline-First | Détection automatique de la perte/reprise de connexion, avec synchronisation différée des pointages en attente |
| Géolocalisation | Position GPS récupérée via `navigator.geolocation`, avec coordonnées de repli en cas de refus de permission |
| Progressive Web App | Installable depuis le navigateur, fonctionne hors-ligne via Service Worker |

---

## Mode d'emploi — démarrage rapide

**Option 1 — Navigateur direct**

Ouvrir `index.html` dans Chrome, Firefox ou Safari.

**Option 2 — Serveur local** *(recommandé pour tester le mode PWA et le scanner caméra)*

```bash
# Avec Python 3
python -m http.server 8080

# Avec Node.js
npx serve .
```
Puis ouvrir [http://localhost:8080](http://localhost:8080)

**Option 3 — Installer comme application (PWA)**

1. Ouvrir le projet dans Chrome
2. Cliquer sur l'icône Installer dans la barre d'adresse
3. Confirmer — l'app se comporte désormais comme une application native

**Option 4 — Application desktop (Electron)**

```bash
npm install
npm start

# Générer l'exécutable Windows (.exe)
npm run build:win
```

**Option 5 — Application Android (Capacitor)**

Le projet Android est déjà généré dans le dossier `android/`. Pour compiler l'APK :

```bash
npx cap sync android
npx cap open android
```
Puis lancer le build depuis Android Studio.

Sinon, pour tester directement sans compiler : une APK prête à installer sera déposée à la racine du repo avant le dépôt final (source inconnue autorisée dans les paramètres Android).

---

## Comptes de démonstration

| Nom | Rôle | Accès |
|---|---|---|
| Jean Dupont | Employé | Pointage QR Code |
| Marie Martin | Manager RH | Dashboard complet + Export |

La création de compte est également disponible directement depuis l'application.

---

## Architecture du projet

```
pointagepro/
├── index.html               Application complète (interface + logique)
├── app.js                    Logique métier (scanner, base de données, synchronisation)
├── main.js                   Processus principal Electron
├── preload.js                Pont sécurisé Electron
├── sw.js                     Service Worker (mode offline PWA)
├── manifest.json              Configuration PWA
├── capacitor.config.ts        Configuration Capacitor (Android)
├── android/                   Projet Android natif généré par Capacitor
├── html5-qrcode.min.js         Scanner QR pour navigateur
├── qrcode.min.js               Génération de QR Code
├── dexie.min.js                 Wrapper IndexedDB pour le stockage offline
├── build-win.ps1              Script de build Windows
├── package.json               Dépendances et scripts (npm, Electron, Capacitor)
├── PointagePro_DataDay2026.pptx  Pitch de présentation (dépôt hackathon)
├── PointagePro.apk             APK compilée — à ajouter avant le dépôt final
└── README.md                  Documentation
```

---

## Stack technique

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](#)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](#)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](#)
[![Dexie.js](https://img.shields.io/badge/Dexie.js-IndexedDB-FF6B00?style=flat-square&logo=databricks&logoColor=white)](#)
[![Capacitor](https://img.shields.io/badge/Capacitor-Android-119EFF?style=flat-square&logo=capacitor&logoColor=white)](#)
[![Electron](https://img.shields.io/badge/Electron-Desktop-47848F?style=flat-square&logo=electron&logoColor=white)](#)
[![Service Workers](https://img.shields.io/badge/Service_Workers-PWA-4285F4?style=flat-square&logo=googlechrome&logoColor=white)](#)

---

## Feuille de route production

Le cœur de l'application (scan, stockage offline, synchronisation, exports) est fonctionnel. Étapes recommandées pour un déploiement à grande échelle :

- [ ] Remplacer l'authentification côté client par un backend avec API sécurisée
- [ ] Connecter la synchronisation à un service distant (Firebase Firestore ou Supabase) au lieu d'un stockage purement local
- [ ] Publier l'APK sur le Google Play Store (signature, révision des permissions Capacitor)
- [ ] Ajouter des tests automatisés sur la logique de synchronisation offline/online

---

## Équipe & contexte du projet

**HexSec**
Meddy · Rajo · Mario · Kiady · Rio

PointagePro a été développé par l'équipe HexSec dans le cadre d'un ideathon (Data Day 2026), comme réponse au problème du suivi de présence dans des environnements à connectivité instable. L'accent a été mis sur une architecture offline-first fonctionnant sur trois plateformes (web, Android, desktop) à partir d'une base de code unique.
