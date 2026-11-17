# Agenda de devoirs de Chloé : installation

L'app est un seul fichier (`index.html`) hébergé gratuitement sur **GitHub Pages**.
Les données sont gardées dans **Firebase** (gratuit, Google), partagées entre papa, Chloé et maman.
Connexion sans mot de passe : un lien reçu par courriel. Seules 3 adresses ont accès.

Compter environ 20 minutes, une seule fois.

---

## 1. Créer la base de données (Firebase)

1. Va sur https://console.firebase.google.com et connecte-toi avec ton compte Google.
2. **Ajouter un projet** → nom : `agenda-chloe` → tu peux désactiver Google Analytics → **Créer**.
3. Dans le projet, clique sur l'icône **`</>` (Web)** pour ajouter une app web.
   - Nom : `agenda` → **Enregistrer** (ne coche pas « Firebase Hosting »).
   - Firebase affiche un bloc `const firebaseConfig = { ... }`. **Copie-le**, on s'en sert à l'étape 3.

### Activer la connexion par courriel
4. Menu de gauche : **Authentication** → **Commencer**.
5. Onglet **Sign-in method** → **E-mail/Mot de passe** → active **les deux** interrupteurs
   (« E-mail/Mot de passe » et « Lien envoyé par e-mail (connexion sans mot de passe) ») → **Enregistrer**.
6. Onglet **Settings** → **Domaines autorisés** → **Ajouter un domaine** → `TON-NOM-GITHUB.github.io`.

### Créer la base et la protéger
7. Menu de gauche : **Firestore Database** → **Créer une base de données**
   → emplacement `northamerica-northeast1 (Montréal)` → **mode production** → **Créer**.
8. Onglet **Règles** : remplace tout par le contenu du fichier `firestore.rules`,
   **en mettant vos 3 vraies adresses courriel** à la place des exemples → **Publier**.

## 2. Mettre l'app sur GitHub

1. Sur GitHub, crée un dépôt (ex. `agenda-chloe`). Il peut être public : aucune donnée n'est dans le code.
2. Ajoute tout le contenu du zip : `index.html`, le dossier `img/` (icônes), `firestore.rules` et `LISEZ-MOI.md`.
3. **Settings → Pages** → Source : « Deploy from a branch », branche `main`, dossier `/ (root)` → **Save**.
4. Après 1 à 2 minutes, l'app est en ligne à `https://TON-NOM-GITHUB.github.io/agenda-chloe/`.

## 3. Brancher l'app à Firebase

Dans `index.html`, tout en haut du script, remplace :

```js
const FIREBASE_CONFIG = null;
```

par le bloc copié à l'étape 1.3, par exemple :

```js
const FIREBASE_CONFIG = {
  apiKey: "AIza...",
  authDomain: "agenda-chloe.firebaseapp.com",
  projectId: "agenda-chloe",
  storageBucket: "agenda-chloe.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

Enregistre (commit). Ces valeurs ne sont pas secrètes : c'est l'étape 1.8 (les règles) qui protège les données.

## 4. Première connexion (chacun sur son téléphone)

1. Ouvre `https://TON-NOM-GITHUB.github.io/agenda-chloe/`.
2. Entre ton courriel → **Recevoir un lien de connexion**.
3. Ouvre le courriel **sur le même appareil** et touche le lien (regarde dans les indésirables la première fois).
4. Ajoute la page à l'écran d'accueil :
   - iPhone (Safari) : bouton Partager → **Sur l'écran d'accueil**.
   - Android (Chrome) : menu ⋮ → **Ajouter à l'écran d'accueil**.

On reste connecté ensuite. La version gratuite de Firebase limite le nombre de liens envoyés par jour : ne pas se déconnecter inutilement. Pour ajouter ou retirer quelqu'un : modifier la liste d'adresses dans les **Règles** Firestore.

## Récupérer les données de la version Claude

Si Chloé a déjà commencé dans la version sur claude.ai :
Réglages → Sauvegarde → **Télécharger une copie**, puis dans la nouvelle app : Réglages → Sauvegarde → **Restaurer une copie**.

## Mettre à jour l'app plus tard

Remplacer `index.html` sur GitHub (en gardant le bloc `FIREBASE_CONFIG`). Les données restent dans Firebase et ne sont jamais touchées par une mise à jour.
