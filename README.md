[README.md](https://github.com/user-attachments/files/34365701/README.md)
# TerrainSync – mise en ligne (Mac)

## 1. Créer le projet Firebase (navigateur)
1. console.firebase.google.com → Ajouter un projet (nom : terrainsync).
2. Build → Authentication → Commencer → activer « E-mail/Mot de passe ».
3. Build → Firestore Database → Créer (mode production, région europe-west).
3b. Build → Storage → Commencer (région europe-west). Cette fonction peut demander le forfait Firebase avec facturation à l’usage : vérifie les conditions sur la page tarifs de Firebase.
4. Paramètres du projet → Vos applications → icône Web « </> » → copier `firebaseConfig` dans `public/auth.js`.

## 2. Premier administrateur
1. Authentication → Utilisateurs → Ajouter un utilisateur (ton e-mail + mot de passe). Copie son UID.
2. Firestore → Démarrer une collection `users` → ID du document = l’UID. Champs : `email` (texte), `name` (texte, prénom et nom, ex. Jean Dupont), `role` = `admin`, `org` = `mon-entreprise`, `active` = true (booléen).

## 3. Outils sur ton Mac (Terminal, ⌘ + Espace puis « Terminal »)
```
brew install node        # ou télécharge Node.js sur nodejs.org
npm install -g firebase-tools
firebase login
cd ~/Downloads/terrainsync-firebase
firebase use --add       # choisis ton projet
firebase deploy --only hosting,firestore:rules,storage
```
L’adresse du site s’affiche à la fin. Ouvre-la sur le téléphone → « Ajouter à l’écran d’accueil ».

## 4. Utilisation
- Admin : bouton « 👥 Équipe » → invite un e-mail avec un rôle. L’invité clique « Créer mon compte (invité) », choisit un mot de passe, puis son PIN.
- Hors ligne : les modifications sont gardées sur l’appareil et envoyées au retour du réseau.

## Limites de cette version
- Photos stockées dans la fiche (limite ~1 Mo par fiche). Les fichiers joints (plans, DXF, PDF, jusqu’à 50 Mo) vont dans Firebase Storage ; sans réseau, le fichier est gardé sur l’appareil (⏳) et envoyé au retour de la connexion.
- Le PIN verrouille l’appli sur l’appareil ; la vraie sécurité vient des règles Firestore.
- L’assistant IA affiche le guide fixe tant qu’aucun service IA n’est branché.
- Les intervenants proposés dans les tâches viennent des comptes actifs de l’équipe (liste publiée par l’administrateur à chaque ouverture et à chaque invitation).
