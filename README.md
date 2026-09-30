[READMEflme.md](https://github.com/user-attachments/files/32872799/READMEflme.md)
# Flux à deux — version GitHub Pages (Supabase)

Une personne partage son écran ou sa caméra en direct, l'autre la voit — comme
un appel vidéo. La connexion audio/vidéo passe directement entre les deux
appareils (WebRTC) ; **Supabase** sert uniquement à échanger les informations
de connexion au tout début (signalisation), via ses canaux Realtime — pas
besoin de créer de table ni de base de données.

## 1. Créer le projet Supabase (5 minutes, gratuit)

1. Allez sur https://supabase.com, connectez-vous (ou créez un compte),
   cliquez sur **New project**.
2. Donnez-lui un nom, choisissez un mot de passe de base de données
   (pas utilisé ici mais demandé à la création) et une région, puis
   **Create new project**. Patientez une minute pendant la mise en place.
3. Une fois le projet prêt, allez dans **Project Settings > API**.
4. Copiez les deux valeurs :
   - **Project URL**
   - **anon public** (clé sous "Project API keys")

## 2. Configurer le site

Ouvrez `index.html`, tout en haut du `<script>` en bas du fichier, et collez
vos valeurs :

```js
const SUPABASE_URL = "https://xxxxx.supabase.co";
const SUPABASE_ANON_KEY = "eyJhbGciOi...";
```

Le Realtime broadcast est activé par défaut sur un nouveau projet Supabase,
aucune autre configuration n'est nécessaire.

## 3. Mettre en ligne sur GitHub Pages

1. Créez un nouveau dépôt GitHub (ou utilisez-en un existant).
2. Ajoutez `index.html` à la racine du dépôt (ou dans un dossier `docs/`).
3. Dans **Settings > Pages** du dépôt, choisissez la branche et le dossier où
   se trouve `index.html`, puis enregistrez.
4. GitHub vous donne une adresse du type
   `https://votre-pseudo.github.io/votre-repo/` — c'est ce lien que vous
   partagez avec votre ami·e.

## Utilisation

- La première personne ouvre le lien, clique sur **Créer ma salle**, obtient
  un code, puis choisit **Mon écran** ou **Ma caméra** et accepte
  l'autorisation du navigateur.
- Elle envoie le code à son ami·e (par SMS, WhatsApp...).
- L'ami·e ouvre le même lien, va dans **J'ai un code**, saisit le code : le
  flux apparaît automatiquement en direct.

## Limite à connaître

La connexion est directe entre les deux appareils (pas de serveur relais
TURN). Cela fonctionne bien sur la plupart des connexions domestiques, mais
peut échouer si l'un des deux est derrière un réseau très restrictif (Wi-Fi
d'entreprise, certains réseaux mobiles).
