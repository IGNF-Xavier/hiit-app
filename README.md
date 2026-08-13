# HIIT Perso 🏋️

Une application web (PWA) pour créer et suivre des séances de HIIT (High Intensity Interval Training), pensée pour être utilisée **sans regarder l'écran** : tout est annoncé à voix haute.

Aucune installation depuis un store, aucun compte, aucun serveur. Les données (programmes, historique) restent uniquement sur l'appareil de chaque utilisateur.

**Version en ligne :** https://ignf-xavier.github.io/hiit-app/

## Fonctionnalités

- **Plusieurs programmes enregistrés** : nom, liste d'exercices, durée de travail, repos entre exercices, repos entre rounds, nombre de rounds, échauffement, retour au calme.
- **Préréglages rapides** : Tabata 20/10 (×8), 30/15, 40/20, 45/15.
- **Écran de séance plein écran**, code couleur par phase (vert = exercice, orange = repos, bleu = échauffement, violet = retour au calme), minuteur géant lisible du coin de l'œil.
- **Annonces vocales (TTS)** façon coach : nom de l'exercice au début, encouragements à mi-effort, annonce du repos et de l'exercice suivant, message de fin de séance — variés à chaque fois pour ne pas être répétitifs.
- **Bips de décompte** (3-2-1) avant chaque transition, réglables.
- **Vibrations** aux changements de phase.
- **Dictée vocale** 🎤 pour ajouter un nouvel exercice au clavier ou à la voix, avec une bibliothèque d'exercices réutilisables d'un programme à l'autre.
- **Pause / reprise, +10s / -10s, passer l'étape, plein écran.**
- **Historique des séances** effectuées (date, durée, programme).
- **Export / import JSON** pour sauvegarder ou transférer ses programmes.
- **Partage d'un programme via un lien** 🔗 : le programme est encodé directement dans l'URL, aucun serveur requis. La personne qui ouvre le lien voit un aperçu et peut l'importer en un clic.
- **Installation en un tap** 📲 : un bouton « Installer » déclenche directement la popup native d'Android/Chrome (voir ci-dessous).
- **Fonctionne hors-ligne** une fois chargée une première fois, grâce au service worker.
- **Réglages vocaux** : vitesse, énergie (pitch), choix de la voix, nombre de secondes de décompte, avec un bouton pour tester la voix.

## Utilisation

### Version en ligne (recommandé)

1. Ouvre https://ignf-xavier.github.io/hiit-app/ dans Chrome (Android).
2. Un bouton **📲 Installer** apparaît en haut de l'écran d'accueil dès que le navigateur juge le site installable (parfois après quelques secondes) : appuie dessus, confirme, et l'app s'ajoute directement, comme depuis un store.
3. Si le bouton n'apparaît pas (autre navigateur, ou iPhone), utilise le menu du navigateur : **⋮ → Ajouter à l'écran d'accueil** sur Chrome Android, ou **Partager → Sur l'écran d'accueil** sur Safari iOS.

Toutes les fonctionnalités sont actives sur la version en ligne (HTTPS), y compris le micro pour la dictée vocale et l'anti-veille pendant la séance.

### Ouvrir le fichier directement (sans hébergement)

Il est aussi possible d'ouvrir `index.html` en local dans Chrome. Le cœur de l'app fonctionne pareil (minuteur, annonces vocales, bips, sauvegarde des programmes), mais :

- le bouton d'installation automatique ne s'affiche pas (il dépend du manifest + service worker, qui nécessitent HTTPS) ;
- la dictée vocale 🎤 et le blocage automatique de l'écran sont désactivés, Chrome les réservant aux pages en HTTPS.

## Héberger sur GitHub Pages

1. Crée un nouveau dépôt GitHub, par exemple `hiit-app` (public).
2. Ajoute à la racine du dépôt les 5 fichiers du projet : `index.html`, `manifest.json`, `service-worker.js`, `icon-192.png`, `icon-512.png` (glisser-déposer via **Add file → Upload files**, ou `git push`).
3. Va dans **Settings → Pages**.
4. Sous *Build and deployment*, choisis **Source : Deploy from a branch**, puis **Branch : main / (root)**, et sauvegarde.
5. Après environ une minute, l'URL du site apparaît en haut de la page Pages.

## Structure du projet

```
index.html          l'application (HTML + CSS + JS, tout intégré)
manifest.json        nom, icônes et couleurs de l'app installée
service-worker.js    mise en cache pour le fonctionnement hors-ligne
icon-192.png          icône de l'app (192×192)
icon-512.png          icône de l'app (512×512)
```

## Confidentialité et stockage des données

L'application n'a **aucun serveur ni base de données**. Programmes, bibliothèque d'exercices et historique sont stockés uniquement dans le `localStorage` du navigateur qui l'utilise. Deux personnes qui ouvrent le même lien ont chacune leurs propres données, invisibles l'une pour l'autre. Pour sauvegarder ou transférer ses données manuellement, utiliser l'export/import JSON dans les réglages.

## Aspects techniques

- HTML/CSS/JS écrits à la main, aucune dépendance externe, aucun build.
- Web App Manifest (`manifest.json`) + service worker (`service-worker.js`) pour l'installabilité et le fonctionnement hors-ligne.
- `beforeinstallprompt` capté en JavaScript pour proposer un bouton d'installation natif sur Android/Chrome (Safari iOS ne supporte pas cette API, d'où le repli manuel sur ce navigateur).
- Web Speech API (`speechSynthesis` / `SpeechRecognition`) pour la voix.
- Web Audio API pour les bips.
- `localStorage` pour la persistance des données.
- Wake Lock API (meilleur effort) pour empêcher la mise en veille pendant une séance.

## Licence

Projet personnel, libre d'utilisation et de modification.
