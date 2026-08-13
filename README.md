# HIIT Perso

Une application web (PWA) autonome pour créer et suivre des séances de HIIT (High Intensity Interval Training), pensée pour être utilisée **sans regarder l'écran** : tout est annoncé à voix haute.

Tout tient dans un seul fichier `index.html` — aucune installation, aucun compte, aucun serveur. Les données (programmes, historique) restent uniquement sur l'appareil de chaque utilisateur.

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
- **Réglages vocaux** : vitesse, énergie (pitch), choix de la voix, nombre de secondes de décompte, avec un bouton pour tester la voix.

## Utilisation

### Option 1 — Ouvrir le fichier directement

Ouvre `index.html` avec Chrome sur Android, puis menu **⋮ → Ajouter à l'écran d'accueil** pour obtenir une icône comme une vraie app.

> ⚠️ En local (`file://`), tout fonctionne **sauf** la dictée vocale 🎤 et le blocage automatique de l'écran, que Chrome réserve aux pages servies en HTTPS. Héberger le fichier (voir ci-dessous) débloque ces deux points.

### Option 2 — Version hébergée (recommandé)

Une fois publiée sur GitHub Pages, l'app est disponible à une URL fixe, par exemple :

```
https://IGNF-Xavier.github.io/hiit-app/
```

Ouvre ce lien dans Chrome, puis **Ajouter à l'écran d'accueil**. Toutes les fonctionnalités sont alors actives, y compris le micro et l'anti-veille pendant la séance.

## Héberger sur GitHub Pages

1. Crée un nouveau dépôt GitHub, par exemple `hiit-app` (public).
2. Ajoute le fichier `index.html` à la racine du dépôt (glisser-déposer via **Add file → Upload files**, ou `git push`).
3. Va dans **Settings → Pages**.
4. Sous *Build and deployment*, choisis **Source : Deploy from a branch**, puis **Branch : main / (root)**, et sauvegarde.
5. Après environ une minute, l'URL du site apparaît en haut de la page Pages.

## Confidentialité et stockage des données

L'application n'a **aucun serveur ni base de données**. Programmes, bibliothèque d'exercices et historique sont stockés uniquement dans le `localStorage` du navigateur qui l'utilise. Deux personnes qui ouvrent le même lien ont chacune leurs propres données, invisibles l'une pour l'autre. Pour sauvegarder ou transférer ses données manuellement, utiliser l'export/import JSON dans les réglages.

## Aspects techniques

- Fichier HTML unique, CSS et JavaScript intégrés, aucune dépendance externe, aucun build.
- Web Speech API (`speechSynthesis` / `SpeechRecognition`) pour la voix.
- Web Audio API pour les bips.
- `localStorage` pour la persistance des données.
- Wake Lock API (meilleur effort) pour empêcher la mise en veille pendant une séance.
- Compatible hors-ligne dès que la page a été chargée une première fois (pas d'appel réseau après le chargement initial).

## Licence

Projet personnel, libre d'utilisation et de modification.
