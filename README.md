<div align="center">

# PointagePro

### La gestion de présence, réinventée.

QR Code · Géolocalisation · 100% Offline-First · Zéro friction

[![PWA](https://img.shields.io/badge/PWA-Ready-5A0FC8?style=for-the-badge&logo=googlechrome&logoColor=white)](#)
[![Offline First](https://img.shields.io/badge/Offline-First-00C853?style=for-the-badge&logo=cloudflare&logoColor=white)](#)
[![Cross Platform](https://img.shields.io/badge/Cross--Platform-Mobile%20|%20Tablette%20|%20PC-2563EB?style=for-the-badge&logo=devbox&logoColor=white)](#)
[![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge&logo=opensourceinitiative&logoColor=white)](#)

*Une seule application, déployable sur mobile, tablette et desktop, sans dépendre d'une connexion permanente.*

</div>

---

## Pourquoi PointagePro

Fini les feuilles de présence papier, les badgeuses hors de prix et les systèmes qui plantent dès que le wifi tousse. PointagePro transforme n'importe quel smartphone en terminal de pointage professionnel — scan QR, position GPS vérifiée, et ça continue de fonctionner même sans connexion internet.

Que vous soyez une PME, une école ou une équipe terrain, l'app s'installe en 30 secondes et s'utilise sans formation.

---

## Fonctionnalités

<table>
<tr>
<th width="50%">Pour les employés</th>
<th width="50%">Pour les managers RH</th>
</tr>
<tr>
<td valign="top">

- Scanner QR Code instantané *(simulé en démo — remplacer par jsQR ou ZXing en production)*
- Géolocalisation GPS automatique
- Historique de pointage filtrable
- Profil éditable
- Thème clair / sombre

</td>
<td valign="top">

- Dashboard temps réel
- Export CSV & Excel en un clic
- Connexion sécurisée à session persistante
- Notifications toast en direct
- Vue d'ensemble des présences

</td>
</tr>
</table>

**Sous le capot**

| Capacité | Détail |
|---|---|
| Mode Offline-First | Les pointages s'enregistrent localement et se synchronisent automatiquement dès le retour du réseau |
| Progressive Web App | S'installe comme une vraie application, sans passer par un store |
| Responsive natif | Mobile, tablette, desktop — une seule base de code |
| Interface | Animations fluides pensées pour une expérience premium |

---

## Démarrage rapide

**Option 1 — Le plus simple**

Ouvrir `index.html` directement dans le navigateur.

**Option 2 — Serveur local** *(recommandé pour tester le mode PWA)*

```bash
# Avec Python 3
python -m http.server 8080

# Avec Node.js
npx serve .
```
Puis ouvrir [http://localhost:8080](http://localhost:8080)

**Option 3 — Installer comme une application**

1. Ouvrir le projet dans Chrome
2. Cliquer sur l'icône Installer dans la barre d'adresse
3. Confirmer — l'app se comporte désormais comme une application native

**Option 4 — Version desktop (Electron)**

```bash
npm install
npm run electron

# Générer un exécutable Windows
npm run build:win
```

---

## Comptes de démonstration

| Nom | Rôle | Accès |
|---|---|---|
| Jean Dupont | Employé | Pointage QR Code |
| Marie Martin | Manager RH | Dashboard complet + Export |

---

## Architecture du projet

```
pointagepro/
├── index.html        Application complète (tout-en-un)
├── manifest.json      Configuration PWA
├── sw.js               Service Worker (moteur du mode offline)
├── package.json       Configuration Electron (build desktop)
└── README.md          Documentation
```

---

## Stack technique

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](#)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](#)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](#)
[![Service Workers](https://img.shields.io/badge/Service_Workers-4285F4?style=flat-square&logo=googlechrome&logoColor=white)](#)
[![IndexedDB](https://img.shields.io/badge/IndexedDB-FF6B00?style=flat-square&logo=databricks&logoColor=white)](#)
[![Electron](https://img.shields.io/badge/Electron-47848F?style=flat-square&logo=electron&logoColor=white)](#)

---

## Feuille de route production

Le projet est fonctionnel en démonstration. Étapes recommandées pour un déploiement à grande échelle :

- [ ] Remplacer le scanner simulé par **jsQR** ou **ZXing**
- [ ] Connecter le backend à **Firebase Firestore** ou **Supabase**
- [ ] Activer le **Background Sync** via le Service Worker
- [ ] Basculer le stockage offline vers **IndexedDB** (via `idb-keyval`)

---

## Contexte du projet

PointagePro a été développé dans le cadre d'un ideathon, comme réponse au problème du suivi de présence dans des environnements à connectivité instable (terrain, zones rurales, sites décentralisés). L'accent a été mis sur une architecture offline-first et une installation sans dépendance lourde, afin de rester déployable rapidement dans des contextes réels.
