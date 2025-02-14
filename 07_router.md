00-cour.js

# VII - Expo Router
## 1. Intro :
 Expo Router est une bibliothèque qui permet d'utiliser un système de navigation basé sur les fichiers dans une application React Native.

 📌 Chaque fichier dans le dossier app/ devient une route automatiquement.

 - Plus simple que react-navigation (pas besoin d'utiliser Stack.Navigator manuellement).
 - Compatible avec iOS et Android.

## 2. Installation et Création du Projet :
 Dans les versions récentes, Expo Router est inclus par défaut lors de la création d'un nouveau projet avec Expo. 
 Pour créer un projet déjà configuré avec Expo Router, exécutez :
 ```bash
 npx create-expo-app my-router-app
 cd my-router-app
 ```

 Vérifiez ensuite dans le fichier `package.json` que la configuration suivante est présente :
```json
 {
   "main": "expo-router/entry"
 }
 ```

 Cela permet à Expo Router d’être le point d’entrée principal.
 Structure d'un projet avec Expo Router :

```
my-router-app/
 ├── app/              // 📌 Tous les fichiers ici deviennent des routes
 │   ├── index.js      // Page d'accueil `/`
 │   ├── about.js      // Page "À propos" `/about`
 │   ├── profile/
 │   │   ├── index.js  // Page de profil `/profile`
 │   │   ├── [id].js   // Page dynamique `/profile/:id`
 │   ├── _layout.js    // Mise en page globale (barre de navigation commune)
 ├── components/       // 📌 Composants réutilisables (ne pas placer ici des fichiers route)
 │   ├── Header.js
 │   ├── Button.js
 ├── package.json
 ├── app.json
```

## 3. Page :
Par convention, les fichiers qui représentent des routes dans le dossier `app/` sont généralement nommés en minuscules. 
Cela permet de :
- Aligner le nom de la route avec l'URL (les URLs étant habituellement en minuscules).
- Éviter des incohérences entre le nom du fichier et la manière dont Expo Router génère les routes.
 
 
#### Exercice 1 : Créer la page d'accueil
**Objectif :**
Créer une page d'accueil accessible à l'URL /.

**Instruction :**
* Crée le fichier app/index.jsx avec le contenu suivant :
```js
import { Text, View } from 'react-native';

export default function HomePage() {
  return (
    <View style={{ padding: 20 }}>
      <Text style={{ fontSize: 18 }}>Bienvenue sur l'Accueil !</Text>
    </View>
  );
}
```

* Créer une page "À propos" accessible à l'URL `/about`.
```js
 import { Text, View } from 'react-native';

export default function AboutPage() {
  return (
    <View style={{ padding: 20 }}>
      <Text style={{ fontSize: 18 }}>À propos de cette app</Text>
    </View>
  );
}
```
---

## 4. Link :
`Link` est un composant fourni par **Expo Router** utilisé pour effectuer la navigation entre les pages de l'application. 
Il remplace l'usage de `navigation.navigate()` pour effectuer des transitions transversales entre les routes définies dans le dossier `app/`. 
Pour l'utiliser, il suffit de fournir une URL cible via la propriété `href` du composant `<Link href="/path">`. 

ajouter un link vers about dans index  .
```js
import { Text, View } from 'react-native';
import { Link } from 'expo-router';

export default function HomePage() {
  return (
    <View style={{ padding: 20 }}>
      <Text style={{ fontSize: 18 }}>Bienvenue sur l'Accueil !</Text>
      <Link href="/about" style={{ marginTop: 20, color: 'blue' }}>
        Aller à la page À propos
      </Link>
    </View>
  );
}
```

## 5. Layout
#### Ajout de la Navigation
**Mise en page globale (app/_layout.js)**
Le fichier `_layout.js` (situé dans le dossier `app/`) est utilisé pour définir une mise en page globale qui sera partagée par toutes les pages (routes) de l'application.

**Navigation Commune :**
Il permet de définir des éléments communs à toutes les pages, par exemple une barre de navigation (ou header, footer, etc.) qui restera inchangée lors de la navigation entre les routes.

**Enveloppement Automatique :**
Expo Router détecte automatiquement la présence de ce fichier et enveloppe 
toutes les pages (ou routes) définies dans app/ avec ce layout.
Cela garantit une cohérence visuelle et fonctionnelle 
sans avoir à dupliquer le code dans chaque page.

Vous pouvez y importer et utiliser un composant de navigation (comme `Stack` ou `Tabs`) pour définir le comportement de la navigation entre vos écrans.

#### Exercice 3 : Créer un layout global
**Objectif :**
Définir une navigation globale avec un layout commun à toutes les pages.

**Instruction :**
Créer le fichier `app/_layout.js` :

```js
import { Stack } from "expo-router";
import { View, Text } from "react-native";

// Ce composant définit le layout global de l'application.
// Il inclut un header commun et une navigation par pile (Stack) pour gérer les différentes routes.
export default function Layout() {
  return (
    // Le conteneur principal qui englobe l'ensemble du layout.
    <View style={{ flex: 1 }}>
       
      <View style={{ padding: 16, backgroundColor: "#f0f0f0" }}>
        <Text style={{ fontSize: 20, fontWeight: "bold" }}>
          Mon Application
        </Text>
      </View>
      
      <Stack>
        <Stack.Screen name="index" options={{ title: "Accueil" }} />
        <Stack.Screen name="about" options={{ title: "À propos" }} />      </Stack>      
    </View>
  );
}
```
---
!!! INFO Toutes les pages définies dans le dossier app/ bénéficieront de ce layout 

## 6. Dynamique :

Les routes dynamiques permettent de créer des pages dont le contenu dépend de paramètres variables dans l'URL.
Nommez le fichier avec des crochets, par exemple `[id].js`, dans le dossier app/.
Expo Router interprétera ce fichier comme une route dynamique et extraira la valeur du paramètre depuis l'URL.

Vous pouvez accéder à cette valeur dans votre composant grâce au hook `useLocalSearchParams()`.

Le hook `useLocalSearchParams()` d'Expo Router permet d'accéder facilement aux paramètres dynamiques de l'URL dans vos composants. 

Par exemple, dans un fichier nommé `[id].js`, vous pouvez récupérer l'ID en écrivant `const { id } = useLocalSearchParams()`. 

!!! INFO Cela simplifie grandement la création de routes dynamiques en évitant de parser manuellement l'URL. Cette approche permet de générer des pages personnalisées, par exemple pour afficher des profils ou des articles en fonction de l'ID passé dans l'URL.