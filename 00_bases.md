# _ - Bases
## 1. React Native avec Expo
React Native est un framework permettant de développer des applications mobiles multiplateformes (iOS et Android) en utilisant JavaScript et React. Expo est un ensemble d'outils qui simplifie le développement avec React Native.

## 2. Introduction à Expo
Expo est une plateforme qui facilite la création, le test et le déploiement d'applications React Native sans nécessiter de configuration complexe pour les environnements natifs iOS et Android

!!! HINT https://expo.dev/go


## 3. Installation et configuration
- Installez Node.js sur votre machine
- [Installez android studio](https://docs.expo.dev/get-started/set-up-your-environment/?platform=android&device=simulated)  

Lorsque vous démarrez avec Expo, le processus de création et d'exécution d'un nouveau projet Expo se déroule en trois étapes principales : 
   - Initialiser un nouveau projet, 
   - démarrer le serveur de développement avec Expo CLI, 
   - et enfin, ouvrir l'application sur votre appareil avec Expo Go pour voir vos modifications en temps réel.


Pour initialiser un nouveau projet, vous pouvez utiliser la commande 
```npx create-expo-app``` suivie du nom de votre projet. 

Par exemple, pour créer un projet nommé "my-app", vous pouvez exécuter la commande suivante :
```sh
 npx create-expo-app@latest my-app --template blank
 cd my-app
 npx expo start
 ```

 Une fois le serveur démarré, vous verrez un QR code dans votre terminal. Vous pouvez le scanner avec l'application Expo Go sur votre smartphone pour voir votre application en direct

-> [Snack Expo](https://snack.expo.dev/?platform=android)

## 4. Structure de fichiers:
    myApp/
    │── assets/  
    │── node_modules/  
    │── .gitignore  
    │── App.js  
    │── app.json  
    │── babel.config.js  
    │── package.json  
    │── package-lock.json (ou yarn.lock)  
    │── metro.config.js (parfois présent)  
    │── tsconfig.json (si TypeScript est utilisé)

**assets/**
    Contient les fichiers statiques de l'application comme :
    icônes (icon.png pour l'icône de l'app)
    splash screen (splash.png pour l’écran de démarrage)
    autres images (favicon.png, etc.)
    sons, vidéos, fonts.

**node_modules/**
    Dossier où sont stockées toutes les dépendances npm.
    Créé automatiquement après npm install ou yarn install.

**.gitignore**
    Fichier indiquant à Git quels fichiers et dossiers ne doivent pas être suivis (ex : node_modules/, .expo/, .env).

**App.js**
    Fichier principal de l'application.
    C'est ici que démarre l'application Expo.

**app.json**
    Fichier de configuration de l'application .
    Définit des paramètres comme :
        Nom de l’app
        Icônes et splash screen
        Orientation de l’écran
        Permissions

**package.json**
    Fichier listant les dépendances et les scripts npm.

**package-lock.json** ou **yarn.lock**
    Gère les versions précises des dépendances installées.