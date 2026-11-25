# Site de réservation RDV InBody : Magic Fit, pôle santé

## Ce que contient le dossier

| Fichier | Rôle |
|---|---|
| `public/index.html` | Page adhérents : choix du créneau de 15 min, formulaire, confirmation, annulation par code |
| `public/accueil.html` | Espace accueil (mot de passe) : planning du jour, réserver pour un adhérent, bloquer un créneau, annuler, réglages |
| `netlify/functions/api.mjs` | Le serveur (API) qui enregistre les réservations |
| `netlify.toml`, `package.json` | Configuration Netlify, à ne pas modifier |

Les réservations sont stockées dans **Netlify Blobs**, inclus gratuitement avec Netlify. Il n'y a aucune base de données à créer. Un créneau ne peut être enregistré qu'une seule fois : si deux adhérents cliquent en même temps, un seul l'obtient. L'autre voit un message et la liste se met à jour.

## Mise en ligne sur Netlify (environ 15 min)

> ⚠️ Le simple glisser-déposer d'un dossier sur Netlify (« Netlify Drop ») ne déploie que les pages, pas le serveur : les réservations ne marcheraient pas. Il faut passer par GitHub, comme ci-dessous.

### 1. Mettre les fichiers sur GitHub
1. Créez un compte gratuit sur https://github.com si vous n'en avez pas.
2. Cliquez sur **New repository**. Nom : `magicfit-rdv-inbody`, cochez **Private**, puis **Create repository**.
3. Cliquez sur **uploading an existing file**.
4. Dézippez le fichier reçu, ouvrez le dossier `magicfit-rdv-inbody`, puis **glissez tout son contenu** dans la page : les dossiers `public` et `netlify`, ainsi que `netlify.toml`, `package.json` et ce fichier.
5. Cliquez sur **Commit changes**.

### 2. Brancher Netlify
1. Sur https://app.netlify.com, cliquez sur **Add new site → Import an existing project → GitHub**.
2. Autorisez Netlify et choisissez le dépôt `magicfit-rdv-inbody`.
3. Laissez tous les réglages tels quels (ils sont lus dans `netlify.toml`) et cliquez sur **Deploy**.

### 3. Choisir le mot de passe de l'accueil (obligatoire)
1. Dans Netlify, ouvrez **Site configuration → Environment variables → Add a variable**.
2. Clé : `ADMIN_PASSWORD`. Valeur : un mot de passe d'au moins 6 caractères, que vous donnerez à l'équipe.
3. Ouvrez **Deploys → Trigger deploy → Deploy site** pour qu'il soit pris en compte.

### 4. Vérifier
- `https://VOTRE-SITE.netlify.app` : page adhérents. Faites une réservation test.
- `https://VOTRE-SITE.netlify.app/accueil.html` : espace accueil. Le RDV test doit apparaître. Annulez-le.
- Dans **Réglages**, mettez les vrais horaires du pôle santé. Les horaires par défaut (lun.–ven. 10h–12h / 14h–19h, sam. 10h–12h) sont des exemples.

### 5. Partager
- Pour changer l'adresse, allez dans **Domain management** : vous pouvez renommer `xxx.netlify.app` (ex. `magicfit-inbody.netlify.app`) ou brancher votre propre nom de domaine.
- Mettez le lien sur votre site, votre Instagram ou vos mails, ou faites-en un QR code à afficher à l'accueil.

## Règles appliquées
- Un créneau réservé ou bloqué disparaît aussitôt de la page adhérents.
- Un adhérent ne peut avoir qu'**un seul RDV à venir** par numéro de téléphone. L'accueil, lui, peut en ajouter sans limite.
- Pas de réservation en ligne à moins de 60 min ni à plus de 21 jours. Ces deux valeurs se règlent dans Réglages.
- Chaque RDV a un **code d'annulation** (ex. `20261126-1015-K7P3QX`). L'adhérent peut annuler en ligne avec ce code, et le créneau redevient libre. Sans code, l'accueil annule depuis le planning.
- L'adhérent peut ajouter le RDV à son agenda (fichier .ics).
- La page adhérents se rafraîchit toutes les 30 s, et l'espace accueil aussi.

## Modifier plus tard
Pour modifier un texte ou une couleur, éditez le fichier sur GitHub (icône crayon). Netlify remet le site à jour tout seul en 1 minute.
Les couleurs se trouvent en haut de `public/index.html`, dans `--accent:#ff4d1a`.

## Données personnelles
Le site ne collecte que le prénom, le nom, le téléphone, l'e-mail (facultatif) et la note. Seuls les détenteurs du mot de passe accueil peuvent les consulter. Pensez à mentionner ce traitement dans votre politique de confidentialité.
