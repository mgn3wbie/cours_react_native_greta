# VI - Formulaire

## 0. Introduction
Nous allons explorer comment créer un formulaire simple avec React Native. 
Ce formulaire contiendra un champ de texte et un bouton de soumission. 
Lorsque l'utilisateur soumet le formulaire, une alerte s'affichera avec le texte saisi.

## 1. Comprendre les composants de base
- `TextInput` : C'est le composant de React Native qui permet à l'utilisateur de saisir du texte. Il a plusieurs propriétés, dont `onChangeText` pour gérer le changement de texte et value pour afficher la valeur actuelle.
<br>
- `TouchableOpacity` : C'est un conteneur qui rend ses enfants "touchables" et exécute une fonction lorsqu'il est pressé. Il est souvent utilisé pour créer des boutons.
<br>
- `Alert` : C'est un composant qui affiche des alertes sous forme de boîtes de dialogue modales.

#### Solution : 
```js
import React, { useState } from "react";
import {
  View,
  Text,
  TextInput,
  StyleSheet,
  TouchableOpacity,
  Alert,
} from "react-native";

const SimpleForm = () => {
  const [text, setText] = useState("");

  const handleSubmit = () => {
    Alert.alert("Text entered:", text);
  };

  return (
    <View style={styles.container}>
      <TextInput
        style={styles.input}
        onChangeText={setText}
        value={text}
        placeholder="Enter text here"
      />
      <TouchableOpacity style={styles.button} onPress={handleSubmit}>
        <Text style={styles.buttonText}>Submit</Text>
      </TouchableOpacity>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
  },
  input: {
    borderWidth: 1,
    borderColor: "gray",
    padding: 10,
    width: "80%",
    marginBottom: 20,
  },
  button: {
    backgroundColor: "lightblue",
    padding: 10,
    borderRadius: 5,
  },
  buttonText: {
    color: "white",
    fontWeight: "bold",
  },
});

export default SimpleForm;
```
