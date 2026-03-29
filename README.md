# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)

---

## Fonctionnalités personnalisées du projet

Le cœur du projet est un gestionnaire de **tâches** avec des **catégories dynamiques** (appelées "lists"). Voici ce qui a été ajouté et comment l'ensemble fonctionne :

1. **État des catégories**
   - `App.js` contient désormais :
     ```js
     const [categories, setCategories] = useState(["Personnel", "Work"]);
     ```
   - Cet état est transmis en props à `AddTask` et `NavComponant` pour que les deux composants utilisent la même liste de catégories.

2. **Ajout de tâches** (`src/task/modifiertasks/addtask.js`)
   - Le formulaire propose un `NavDropdown` rempli par la prop `categories`.
   - Lorsque l'utilisateur choisit "Add new list", un `prompt` lui demande le nom, puis on ajoute la nouvelle catégorie via `setCategories`.
   - Au moment de l'ajout, chaque tâche contient un champ `category` qui correspond à ce que l'utilisateur a sélectionné.

3. **Navigation dynamique** (`src/nav/nav.js`)
   - Le menu calcule `countsByCategory` en parcourant les tâches :
     ```js
     const countsByCategory = categories.reduce((acc, cat) => {
       acc[cat] = taskList.filter((t) => t.category === cat).length;
       return acc;
     }, {});
     ```
   - Chaque catégorie est affichée avec son badge de compteur. Le lien "Add New List" déclenche le même `prompt` que dans le formulaire pour créer une catégorie.

4. **Flux de travail pour l'utilisateur**
   - Choisir ou créer une catégorie dans `AddTask` avant de soumettre.
   - La tâche apparaît instantanément dans la liste `Modifiers`/`List` et renverra un décompte dans la nav.
   - Ajouter une liste via le menu ou le formulaire met à jour l'autre composant automatiquement, car ils partagent le même état.

5. **Étapes pour le développeur**
   - `App.js` : maintenir `taskList` et `categories` + passer les props nécessaires.
   - `AddTask.js` : consommer `categories` et `setCategories`, gérer la sélection, et générer l'objet `newTask`.
   - `nav/nav.js` : consommer les mêmes props, calculer les totaux et permettre l'ajout.
   - `modifiertasks/list.js` et `modifiertasks/modifee.js` restent inchangés mais peuvent être étendus pour filtrer par catégorie.

En suivant ce modèle, tu peux étendre l'application : ajouter des filtres par catégorie dans la liste, stocker les données dans `localStorage`, connecter à un backend, etc.

Bonne exploration ! N'hésite pas à lire chaque composant pour comprendre le fonctionnement et à modifier petit à petit.
# tst
