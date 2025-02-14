# V - Composants part_2

## 1. Input :
Pour créer un composant qui permet à l'utilisateur d'entrer du texte, vous pouvez utiliser le composant `TextInput` 

#### Exercice 1 - Input :
Créez un composant qui permet à l'utilisateur d'entrer du texte. Le texte saisi doit s'afficher sous le champs input

#### Solution :

``` js
import React, { useState } from "react";
import { TextInput, View, Text, StyleSheet } from "react-native";

const AffichageSaisie = () => {
  const [texte, setTexte] = useState("");

  const gererChangementTexte = (nouveauTexte) => {
    console.log(nouveauTexte);
    setTexte(nouveauTexte);
  };

  return (
    <View style={styles.conteneur}>
      <Text style={styles.etiquette}>Saisissez votre texte :</Text>
      <TextInput
        style={styles.champSaisie}
        onChangeText={gererChangementTexte}
        value={texte}
      />
      <Text style={styles.texteAffiche}>Vous avez saisi :
      </Text>
      <Text style={styles.texteAffiche}>
        {texte}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  conteneur: {
    padding: 20,
  },
  etiquette: {
    marginBottom: 10,
  },
  champSaisie: {
    height: 40,
    borderColor: "gray",
    borderWidth: 1,
    marginBottom: 10,
    paddingHorizontal: 10,
  },
  texteAffiche: {
    marginTop: 20,
    fontSize: 30
  },
});

export default AffichageSaisie;
```

---


## 2. FlatList
Le composant `FlatList` est un composant de liste performant qui permet d'afficher des données dans une liste. 
Il est entièrement compatible avec les plates-formes iOS et Android et prend en charge de nombreuses fonctionnalités utiles, telles que la pagination, le chargement de défilement, le rafraîchissement de tirer pour actualiser, et bien plus encore.
Pour utiliser le composant `FlatList`, vous devez fournir un tableau de données et une fonction de rendu qui définit comment chaque élément de la liste doit être affiché. Vous pouvez également fournir des options de configuration pour personnaliser l'apparence et le comportement de la liste.
Voici les étapes de base pour utiliser le composant `FlatList` :

Importez le composant `FlatList` depuis la bibliothèque React Native.

```js
import { View, Text, FlatList } from 'react-native';

const names = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Jane' },
  { id: 3, name: 'Bob' },
  { id: 4, name: 'Alice' },
];


const renderItem = ({ item }) => (
  <Text>{item.name}</Text>
);

const FlatListExample = () => {
  return (
    <View>
      <FlatList
        data={names}
        renderItem={renderItem}
        keyExtractor={(item) => item.id.toString()}
      />
    </View>
  );
};

export default FlatListExample;
```

- Dans cet exemple, nous créons un tableau de données names qui contient une liste de noms. 
- Nous créons ensuite une fonction de rendu `renderItem` qui définit comment chaque élément de la liste doit être affiché. 
- Nous utilisons le composant `FlatList` pour afficher la liste en fournissant le tableau de données et la fonction de rendu en tant que props. Nous utilisons également la méthode `keyExtractor` pour spécifier une clé unique pour chaque élément de la liste.

!!! CHECK Les avantages de l'utilisation du composant FlatList sont qu'il est performant, facile à utiliser et prend en charge de nombreuses fonctionnalités utiles pour l'affichage de listes de données.

#### Exercice 1 - Flatlist : 
Créez une liste simple avec `FlatList` qui affiche une liste de noms. 
Chaque nom doit être cliquable et doit afficher une alerte avec le nom sélectionné.

#### Solution :
```js
import React from "react";
import {
  View,
  Text,
  FlatList,
  TouchableOpacity,
  Alert,
  StyleSheet,
} from "react-native";

// Liste des noms à afficher
const noms = [
  { id: 1, nom: "John" },
  { id: 2, nom: "Jane" },
  { id: 3, nom: "Bob" },
  { id: 4, nom: "Alice" },
];

// Fonction pour afficher chaque élément de la liste
const afficherElement = ({ item }) => (
  // Lorsqu'on appuie sur un nom, une alerte s'affiche avec le nom sélectionné
  <TouchableOpacity
    style={styles.item}
    onPress={() => Alert.alert("Nom sélectionné:", item.nom)}
  >
    <Text style={styles.text}>{item.nom}</Text>
  </TouchableOpacity>
);

const ListeSimple = () => {
  return (
    <View style={styles.container}>
      <FlatList
        data={noms} // Données à afficher
        renderItem={afficherElement} // Comment chaque élément doit être affiché
        keyExtractor={(item) => item.id} // Comment chaque élément est identifié de manière unique
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#f5f5f5",
    padding: 10,
  },
  item: {
    backgroundColor: "#fff",
    padding: 15,
    marginBottom: 10,
    borderRadius: 5,
    shadowColor: "#000",
    shadowOffset: { width: 0, height: 1 },
    shadowOpacity: 0.3,
    shadowRadius: 2,
    elevation: 3,
  },
  text: {
    fontSize: 18,
  },
});

export default ListeSimple;
```

---

!!! ATTENTION Vous n'avez pas besoin d'utiliser .map() dans ce cas. 
    Lorsque vous utilisez `FlatList` dans React Native, **il s'occupe de la boucle interne pour vous.** 
    Vous fournissez simplement les données via la prop data et indiquez comment chaque élément doit être rendu via la prop `renderItem`.

Dans l'exemple, `FlatList` prend le tableau noms et appelle la fonction afficherElement pour chaque élément du tableau. 
C'est similaire à ce que `.map()` ferait, mais `FlatList` est optimisé pour les grandes listes et offre des fonctionnalités supplémentaires comme le défilement et la réutilisation des éléments pour de meilleures performances.

Si vous n'utilisiez pas `FlatList`, vous pourriez utiliser `.map()` pour rendre chaque élément de la liste, mais dans le contexte de React Native, il est généralement recommandé d'utiliser `FlatList` pour les listes, car il est **optimisé** pour les performances sur les appareils mobiles.


#### Exercice 2 - Header :
Dans "components", créez un dossier "Header" contenant un fichier "index.js". 
Dans ce fichier, concevez un composant "Header" qui affiche la date actuelle.

#### Solution :
```js 
import React from "react";
import { View, Text, StyleSheet } from "react-native";
const Header = () => {
  const dateActuelle = new Date(Date.now());

  const jours = [
    "Dimanche",
    "Lundi",
    "Mardi",
    "Mercredi",
    "Jeudi",
    "Vendredi",
    "Samedi",
  ];
  const mois = [
    "Janvier",
    "Février",
    "Mars",
    "Avril",
    "Mai",
    "Juin",
    "Juillet",
    "Août",
    "Septembre",
    "Octobre",
    "Novembre",
    "Décembre",
  ];

  const nomDuJour = jours[dateActuelle.getDay()];
  const nomDuMois = mois[dateActuelle.getMonth()];

  const numeroDuJour = dateActuelle.getDate();
  const annee = dateActuelle.getFullYear();

  return (
    <View style={styles.conteneurHeader}>
      <Text style={styles.texteHeader}>
        {nomDuJour} {numeroDuJour} {nomDuMois} {annee}
      </Text>
    </View>
  );
};

const styles = StyleSheet.create({
  conteneurHeader: {
    backgroundColor: "#2b372c",
    padding: 15,
    alignItems: "center",
  },
  texteHeader: {
    color: "white",
    fontSize: 22,
  },
});

export default Header;
```