# IV - Pressable
Le composant `Pressable` est un élément enveloppant de base qui peut détecter diverses étapes des interactions de pression sur n'importe lequel de ses enfants définis. Voici une explication détaillée de son fonctionnement et de ses propriétés :

## 1. Fonctionnement de Pressable :
Lorsqu'un élément est enveloppé par `Pressable`, la méthode onPressIn est appelée lorsqu'une pression est activée.
**onPressOut** est appelé lorsque le geste de pression est désactivé.
Après avoir pressé **onPressIn**, l'une des deux choses suivantes se produira :
La personne retirera son doigt, déclenchant **onPressOut**.
Si la personne laisse son doigt plus de 500 millisecondes avant de le retirer, **onLongPress** est déclenché. (**onPressOut** sera toujours déclenché lorsqu'ils retireront leur doigt.)


#### Exercice 1 - Styles conditionnels :
**Objectif :**
Dans un component, affichez un texte qui change de couleur quand on appuie dessus 
**Conseil :**
Utilisez le useState pour gérer l'état et appliquez des styles conditionnels en fonction de cet état.

#### Solution : 
```js
import React, { useState } from "react";
import { View, Text, StyleSheet, Pressable } from "react-native";

const ColorChangingText = () => {
  const [isActive, setIsActive] = useState(false);

  return (
    <View style={styles.container}>
      <Pressable onPress={() => setIsActive(!isActive)}>
        <Text
          style={[
            styles.text,
            isActive ? styles.activeText : styles.inactiveText,
          ]}
        >
          {isActive ? "Actif" : "Inactif"}
        </Text>
        <Text>Changer l'état</Text>
      </Pressable>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    fontSize: 20,
    marginBottom: 10,
  },
  activeText: {
    color: "green",
  },
  inactiveText: {
    color: "red",
  },
});

export default ColorChangingText;
```
