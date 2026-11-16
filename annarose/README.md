# 🎄 Liste de Noël d'Ana & Rose

- `index.html` : le site, à mettre en ligne dans le dossier `anarose/` du dépôt GitHub
- `apps-script/Code.gs` : l'API (lecture, réservation, ajout protégé par mot de passe)

## 1. Créer le Google Sheet
1. Sur https://sheets.google.com, crée une **nouvelle feuille vide**, par exemple « Liste Noël Ana & Rose ».
2. Ne remplis rien. Les en-têtes se créent tout seuls au premier appel de l'API :
   `id | pour | nom | prioritaire | commentaire | occasion | images | liens | reserve_par | reserve_le`

## 2. Ajouter le script
1. Dans le Sheet, ouvre **Extensions → Apps Script**.
2. Remplace le contenu de `Code.gs` par celui de `apps-script/Code.gs`, puis enregistre.
3. **Mot de passe pour l'ajout** : ouvre ⚙️ **Paramètres du projet**, tout en bas **Propriétés du script**, puis **Ajouter une propriété** :
   - Propriété : `ADMIN_PASSWORD`
   - Valeur : le mot de passe de ton choix
   - Puis **Enregistrer les propriétés du script**

   Le mot de passe reste dans le script, il n'apparaît jamais dans le code du site.

## 3. Publier l'API
1. **Déployer → Nouveau déploiement**, puis ⚙️ **Application Web** :
   - Exécuter en tant que : **Moi**
   - Qui a accès : **Tout le monde**
2. Autorise l'accès (Paramètres avancés → Accéder à … → Autoriser).
3. Copie l'URL qui se termine par `/exec` et colle-la dans `index.html` :
   ```js
   window.API_URL = 'https://script.google.com/macros/s/XXXX/exec';
   ```

## 4. Mettre en ligne
Dans le même dépôt GitHub que la liste d'Elyas, ajoute `index.html` dans un dossier `anarose/`. Sur GitHub, **Add file → Upload files**, puis glisse le dossier `anarose` entier.
Le lien sera `https://<ton-pseudo>.github.io/<ton-depot>/anarose/`.

## Utilisation
- **Ajouter un cadeau** : bouton « ＋ Ajouter un cadeau » en bas à droite. Choisis Ana, Rose ou Les deux, puis renseigne le nom, le lien de la photo (une par ligne), le lien boutique, le commentaire, les cases prioritaire et occasion, et le mot de passe. Le mot de passe est retenu jusqu'à la fermeture de l'onglet.
- **Colonne `pour`** dans le Sheet : `Ana`, `Rose` ou `Les deux` (une case vide compte comme « Les deux »).
- **Filtre Ana** : affiche les cadeaux d'Ana et ceux pour les deux. Même chose pour Rose.
- **Modifier, supprimer, réordonner ou annuler une réservation** : directement dans le Sheet. L'ordre suit la colonne `id`. Pour annuler une réservation, vide `reserve_par` et `reserve_le`.
- Après 10 mots de passe faux, l'ajout est bloqué 10 minutes.
