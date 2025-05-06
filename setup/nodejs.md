# Node.js - Environnement d'exécution JavaScript côté serveur

## Introduction à Node.js

Node.js est un environnement d'exécution JavaScript open-source, multi-plateforme, qui permet d'exécuter du code JavaScript côté serveur. Construit sur le moteur JavaScript V8 de Chrome, Node.js utilise une architecture orientée événements, non-bloquante et asynchrone qui le rend léger et efficace, parfait pour des applications temps réel gourmandes en données.

## Pourquoi utiliser Node.js ?

- **JavaScript partout** : Même langage côté client et serveur
- **Performances** : Exécution rapide grâce au moteur V8 et au modèle non-bloquant
- **Scalabilité** : Excellente gestion des connexions simultanées
- **Écosystème riche** : NPM (Node Package Manager) offre plus d'un million de packages
- **Communauté active** : Support et documentation abondants
- **Polyvalence** : API REST, applications web, microservices, outils CLI, IoT...

## Installation de Node.js

### Sur Linux (Ubuntu/Debian)

```bash
# Via apt
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Vérifier l'installation
node -v
npm -v
```

### Via NVM (Node Version Manager) - Recommandé

```bash
# Installer NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash

# Charger NVM dans le terminal actuel
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

# Installer la dernière version LTS de Node.js
nvm install --lts

# Utiliser une version spécifique
nvm use 16.20.0

# Définir une version par défaut
nvm alias default 18.16.0
```

## Commandes Node.js essentielles

### Exécution de code JavaScript

```bash
# Exécuter un fichier JavaScript
node app.js

# Mode REPL (Read-Eval-Print Loop) - Console interactive
node

# Évaluer une expression JavaScript
node -e "console.log('Hello World')"

# Vérifier la syntaxe sans exécuter
node --check app.js
```

### Debugging

```bash
# Déboguer avec l'inspecteur
node --inspect app.js

# Attendre la connexion du débogueur avant de démarrer
node --inspect-brk app.js

# Exécuter en mode strict
node --use-strict app.js
```

## Gestion des packages avec NPM

### Initialisation et configuration

```bash
# Initialiser un nouveau projet (crée package.json)
npm init

# Initialiser avec valeurs par défaut
npm init -y

# Définir des configurations
npm config set init-author-name "Votre Nom"
npm config set init-license "MIT"
```

### Installation de packages

```bash
# Installer un package (ajouté aux dépendances)
npm install express

# Installer une version spécifique
npm install express@4.18.2

# Installer en tant que dépendance de développement
npm install jest --save-dev

# Installer globalement (accessible partout)
npm install -g nodemon

# Installer toutes les dépendances du package.json
npm install
```

### Gestion des dépendances

```bash
# Mettre à jour les packages
npm update

# Voir les packages obsolètes
npm outdated

# Désinstaller un package
npm uninstall express

# Lister les packages installés
npm list

# Lister seulement les packages de premier niveau
npm list --depth=0
```

### Scripts NPM

```bash
# Exécuter un script défini dans package.json
npm run start

# Exécuter le script "test"
npm test

# Exécuter le script "dev"
npm run dev
```

### Publication et gestion de packages

```bash
# Se connecter à npm
npm login

# Publier un package
npm publish

# Dépublier un package
npm unpublish <package-name> --force
```

## Alternatives à NPM

### Yarn

```bash
# Installer Yarn
npm install -g yarn

# Installer les dépendances
yarn

# Ajouter un package
yarn add express

# Ajouter une dépendance de développement
yarn add --dev jest

# Exécuter un script
yarn run start
```

### PNPM

```bash
# Installer pnpm
npm install -g pnpm

# Installer les dépendances
pnpm install

# Ajouter un package
pnpm add express

# Ajouter une dépendance de développement
pnpm add -D jest
```

## Structure d'un projet Node.js typique

```
projet/
├── node_modules/       # Dépendances installées
├── src/                # Code source
│   ├── controllers/    # Contrôleurs
│   ├── models/         # Modèles
│   ├── routes/         # Routes
│   └── index.js        # Point d'entrée
├── tests/              # Tests
├── .env                # Variables d'environnement
├── .gitignore          # Fichiers ignorés par Git
├── package.json        # Métadonnées et dépendances
└── README.md           # Documentation
```

## Exemple de code basique

### Serveur HTTP simple

```javascript
// app.js
const http = require("http");

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader("Content-Type", "text/plain");
  res.end("Hello World\n");
});

server.listen(3000, () => {
  console.log("Serveur démarré sur http://localhost:3000/");
});
```

### Serveur Express

```javascript
// app.js
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Serveur démarré sur http://localhost:${port}/`);
});
```

## Outils de développement populaires

### Nodemon

Redémarre automatiquement l'application lorsque des fichiers sont modifiés.

```bash
# Installation
npm install -g nodemon

# Exécution
nodemon app.js
```

### PM2

Gestionnaire de processus pour les applications Node.js en production.

```bash
# Installation
npm install -g pm2

# Démarrer une application
pm2 start app.js

# Lister les applications
pm2 list

# Monitorer les applications
pm2 monit

# Redémarrer une application
pm2 restart app

# Arrêter une application
pm2 stop app

# Configurer le démarrage automatique
pm2 startup
```

### TypeScript avec Node.js

```bash
# Installer TypeScript
npm install -g typescript
npm install --save-dev typescript @types/node

# Initialiser tsconfig.json
npx tsc --init

# Compiler
npx tsc

# Exécuter avec ts-node
npm install -g ts-node
ts-node src/index.ts
```

## Meilleures pratiques Node.js

1. **Utiliser des gestionnaires de versions** comme NVM pour gérer plusieurs versions
2. **Structurer le code** en modules réutilisables
3. **Gérer les erreurs** correctement avec try/catch et promesses
4. **Utiliser les promesses ou async/await** plutôt que les callbacks
5. **Valider les entrées utilisateur** pour la sécurité
6. **Implémenter la journalisation** avec des outils comme Winston ou Pino
7. **Utiliser des variables d'environnement** pour la configuration
8. **Écrire des tests unitaires** avec Jest, Mocha ou autre
9. **Mettre en cache** les données fréquemment utilisées
10. **Utiliser les clusters** pour maximiser les performances multi-cœurs
