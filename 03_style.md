# III - Styles

Avec React Native, vous stylisez votre application à l'aide de JavaScript. Tous les composants principaux acceptent une props nommée style.
Les noms et valeurs de style correspondent généralement à la manière dont le CSS fonctionne sur le web, à l'exception des noms qui sont écrits en camel case, par exemple _backgroundColor_ plutôt que _background-color_.


## 1. Utilisation de la props style
La props style peut être un simple objet JavaScript.
```js
<SafeAreaView style={{ flex: 1, justifyContent: "center" }}>
```

## 2. StyleSheet.create
Au fur et à mesure qu'un composant gagne en complexité, il est souvent plus clair d'utiliser StyleSheet.create pour définir plusieurs styles en un seul endroit.

**Voici un exemple :**
```js
  import React from 'react';
  import {StyleSheet, Text, View} from 'react-native';

  const App = () => (
    <View style={styles.container}>
      <Text style={styles.title}>React Native</Text>
    </View>
  );
  const styles = StyleSheet.create({
      container: {
          flex: 1,
          padding: 16,
          backgroundColor: 'white',
      },
      title: {
          fontSize: 24,
          fontWeight: 'bold',
      },
      });
      export default App;
```

#### Exercice 1 : Mise en forme de base
**Objectif :**
Créez un écran avec un titre "React Native Styles" centré à l'écran avec une taille de police de 24 et une couleur de texte bleue.
**Conseil :**
Utilisez les propriétés fontSize et color dans votre objet de style.

#### Solution :
**components/Square.js**
```js
import React from "react";
import { View, StyleSheet } from "react-native";

const Square = ({ color }) => {
  return (
    <View
      style={[styles.square, { backgroundColor: color || "black" }]}
    />
  );
};

const styles = StyleSheet.create({
  square: {
    width: 50,
    height: 50,
    margin: 10,
  },
});

export default Square;
```

**App.js**
```js
import { StatusBar } from "expo-status-bar";
import { StyleSheet, Text, View } from "react-native";
import Constants from 'expo-constants';


import Square from "./components/Square";

export default function App() {
  return (
    <View style={styles.container}>
      <View style={styles.row}>
        <Square color="red" />
        <Square color="green" />
        <Square color="blue" />
      </View>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
    marginTop: Constants.statusBarHeight
  },
  row: {
    flexDirection: "row",
  },
});
```

---

## 2. Exercice style : Positionnement
**Objectif :**
Positionnez un carré  au coin supérieur droit de l'écran.

**Conseil :**
Utilisez les propriétés position, top, et right.

#### Solution:
**App.js**
```js
import { StatusBar } from "expo-status-bar";
import { StyleSheet, Text, View } from "react-native";
import Constants from 'expo-constants';


import Square from "./components/Square";

export default function App() {
  return (
    <View style={styles.container}>
      <Square color="violet" position={styles.topRightPosition} />
      <View style={styles.row}>
        <Square color="red" />
        <Square color="green" />
        <Square color="blue" />
      </View>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
    marginTop: Constants.statusBarHeight
  },
  row: {
    flexDirection: "row",
  },
  topRightPosition: {
    position: "absolute",
    top: Constants.statusBarHeight,
    right: 0,
  },
});
```

**Square.js**
```js
import React from "react";
import { View, StyleSheet } from "react-native";

const Square = ({ color, position }) => {
  return (
    <View
      style={[styles.square, position, { backgroundColor: color || "black" }]}
    />
  );
};

const styles = StyleSheet.create({
  square: {
    width: 50,
    height: 50,
    margin: 10,
  },
});

export default Square;
```

!!! SUCCESS Lorsque vous utilisez position: "absolute" avec top: 0 et right: 0, le composant sera positionné en haut à droite de son conteneur parent. Si ce conteneur parent est le conteneur principal de l'application, le composant sera positionné en haut à droite de l'écran, ce qui peut le faire chevaucher la barre d'état sur certains appareils, en particulier sur iOS.
    Pour éviter cela, vous pouvez ajouter un espace en haut pour tenir compte de la barre d'état. **Expo** fournit un module appelé **Constants** qui a une propriété **statusBarHeight** qui vous donne la hauteur de la barre d'état.
    ```js
    import Constants from 'expo-constants';
    top: Constants.statusBarHeight,
    ```

#### Exercice style 3 : Bordures et arrondis
**Objectif :**
Dans un composant, créez un rectangle avec des bordures arrondies, une bordure épaisse et une couleur de fond.
**Conseil :**
Utilisez les propriétés `borderRadius`, `borderWidth`, et `borderColor`.

#### Solution: 
```js 
import React from 'react';
import { View } from 'react-native';

const Rectangle = () => {
    return (
        <View
            style={{
                width: 200,
                height: 100,
                backgroundColor: 'lightblue',
                borderRadius: 20,
                borderWidth: 5,
                borderColor: 'darkblue',
            }}
        />
    );
};

export default Rectangle;
```

---

### Exercice style 4: Opacité et superposition

**Objectif :**
Un composant Affiche deux carrés de couleur differente superposés, où le carré supérieur a une opacité de 0,5.

**Conseil :**
Utilisez la propriété opacity et jouez avec zIndex si nécessaire.

#### Solution
```js
import React from "react";
import { View, StyleSheet } from "react-native";

const SuperposedSquares = () => {
  return (
    <View style={styles.container}>
      <View style={styles.lowerSquare} />
      <View style={styles.upperSquare} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    alignItems: "center",
    justifyContent: "center",
    flex: 1,
  },
  lowerSquare: {
    width: 100,
    height: 100,
    backgroundColor: "blue",
    position: "absolute",
     left: 9,
        top: 35,
  },
  upperSquare: {
    width: 100,
    height: 100,
    left: 5,
    top: 5,
    backgroundColor: "red",
    opacity: 0.5,
    position: "absolute",
    zIndex: 1,
  },
});

export default SuperposedSquares;
```