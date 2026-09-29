# Ciné à deux — version GitHub Pages

Ce site fonctionne comme la version précédente (créer une salle, obtenir un code,
le partager, regarder une vidéo synchronisée à deux) mais s'héberge tout seul,
sans dépendre de claude.ai. La synchronisation passe par **Firebase Realtime
Database** (gratuit pour cet usage).

## 1. Créer le projet Firebase (5 minutes, gratuit)

1. Allez sur https://console.firebase.google.com et connectez-vous avec un
   compte Google.
2. Cliquez sur **Ajouter un projet**, donnez-lui un nom (ex. `cine-a-deux`),
   passez les étapes suivantes (Google Analytics n'est pas nécessaire).
3. Dans le menu de gauche, ouvrez **Créer > Realtime Database**, cliquez sur
   **Créer une base de données**, choisissez un emplacement, puis démarrez
   **en mode test**.
4. Une fois créée, ouvrez l'onglet **Règles** de la base et remplacez le
   contenu par :

   ```json
   {
     "rules": {
       "rooms": {
         "$code": {
           ".read": true,
           ".write": true
         }
       }
     }
   }
   ```

   Cliquez sur **Publier**. (Ces règles laissent n'importe qui lire/écrire
   dans une salle s'il connaît le code à 6 caractères — suffisant pour un
   usage entre amis, sans compte à créer.)

5. Revenez à la page d'accueil du projet, cliquez sur l'icône **`</>`** (Ajouter
   une application Web), donnez-lui un nom, puis **Enregistrer**. Firebase
   affiche un bloc `firebaseConfig = { ... }` : copiez ces valeurs.

## 2. Configurer le site

Ouvrez `index.html`, tout en haut du `<script>` en bas du fichier, et collez
vos valeurs à la place des `"REMPLACEZ_MOI"` :

```js
const firebaseConfig = {
  apiKey: "...",
  authDomain: "...",
  databaseURL: "...",
  projectId: "..."
};
```

## 3. Mettre en ligne sur GitHub Pages

1. Créez un nouveau dépôt GitHub (ou utilisez-en un existant).
2. Ajoutez `index.html` à la racine du dépôt (ou dans un dossier `docs/`).
3. Dans **Settings > Pages** du dépôt, choisissez la branche et le dossier où
   se trouve `index.html`, puis enregistrez.
4. GitHub vous donne une adresse du type
   `https://votre-pseudo.github.io/votre-repo/` — c'est ce lien que vous
   partagez avec votre ami·e.

## Utilisation

- La première personne ouvre le lien, clique sur **Créer ma salle**, charge
  le lien de la vidéo (.mp4 direct ou lien YouTube), et obtient un code.
- Elle envoie ce code à son ami·e (le lien du site suffit, le code est à
  transmettre séparément).
- L'ami·e ouvre le même lien, va dans **J'ai un code**, saisit le code : la
  vidéo apparaît et la lecture se synchronise automatiquement.
