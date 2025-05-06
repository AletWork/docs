# Visual Studio Code - Ma Configuration Personnalisée

## Installation

### Windows

1. Téléchargez l'installateur depuis le [site officiel](https://code.visualstudio.com/)
2. Exécutez l'installateur et suivez les instructions

### Linux

```bash
# Via Snap
sudo snap install code --classic

# Via apt (Debian/Ubuntu)
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update
sudo apt install code
```

## Mes Extensions Quotidiennes

### Productivité générale

- **GitHub Copilot** : Assistant de code IA pour suggestions intelligentes
- **GitLens** : Supercharge les fonctionnalités Git dans VS Code
- **Project Manager** : Gestion facile de projets multiples
- **Error Lens** : Affiche les erreurs et avertissements directement dans l'éditeur

### Pour le développement Web

- **ESLint** : Analyse statique du code JavaScript
- **Prettier** : Formatteur de code automatique
- **Live Server** : Lancement d'un serveur local avec reload automatique
- **Auto Rename Tag** : Renommage automatique des balises HTML/XML

### Pour PHP

- **PHP Intelephense** : Support avancé pour PHP avec autocomplétion
- **Laravel Blade Snippets** : Snippets et colorisation pour Laravel Blade
- **PHP Debug** : Support de débogage XDebug

### Pour JavaScript/TypeScript

- **JavaScript (ES6) Code Snippets** : Snippets pour le JS moderne
- **Import Cost** : Affiche la taille des packages importés
- **Quokka.js** : Évaluation de code JS/TS en temps réel

### Personnalisation

- **Material Icon Theme** : Icônes modernes pour l'explorateur de fichiers
- **One Dark Pro** : Thème sombre élégant (mon préféré)

## Raccourcis Clavier Essentiels

| Action                              | Raccourci Windows        | Raccourci Mac           |
| ----------------------------------- | ------------------------ | ----------------------- |
| **Navigation & Recherche**          |                          |                         |
| Palette de commandes                | `Ctrl+Shift+P`           | `Cmd+Shift+P`           |
| Recherche dans les fichiers         | `Ctrl+Shift+F`           | `Cmd+Shift+F`           |
| Recherche dans le fichier           | `Ctrl+F`                 | `Cmd+F`                 |
| Ouvrir un fichier rapidement        | `Ctrl+P`                 | `Cmd+P`                 |
| Navigation entre onglets            | `Ctrl+Tab`               | `Cmd+Tab`               |
| Aller à la ligne                    | `Ctrl+G`                 | `Cmd+G`                 |
| **Édition**                         |                          |                         |
| Multi-curseurs                      | `Alt+Clic`               | `Option+Clic`           |
| Sélection multiple                  | `Ctrl+D` (répéter)       | `Cmd+D` (répéter)       |
| Sélectionner toutes les occurrences | `Ctrl+Shift+L`           | `Cmd+Shift+L`           |
| Commenter/décommenter               | `Ctrl+/`                 | `Cmd+/`                 |
| Indentation automatique             | `Shift+Alt+F`            | `Shift+Option+F`        |
| Déplacer une ligne                  | `Alt+↑/↓`                | `Option+↑/↓`            |
| Dupliquer une ligne                 | `Shift+Alt+↓`            | `Shift+Option+↓`        |
| **Terminal & Débogage**             |                          |                         |
| Ouvrir terminal                     | `` Ctrl+`  ``            | `` Cmd+`  ``            |
| Démarrer débogage                   | `F5`                     | `F5`                    |
| Point d'arrêt                       | `F9`                     | `F9`                    |
| **Fonctionnalités Git**             |                          |                         |
| Voir les changements                | `Ctrl+Shift+G`           | `Cmd+Shift+G`           |
| Stage des changements               | `Ctrl+Enter` (dans diff) | `Cmd+Enter` (dans diff) |

## Ma Configuration settings.json

Le fichier `settings.json` permet de personnaliser complètement votre environnement VSCode. Pour y accéder, utilisez `Ctrl+Shift+P` puis tapez "settings json".

Voici comment personnaliser votre configuration:

```json
{
  // Apparence
  "workbench.colorTheme": "One Dark Pro",
  "workbench.iconTheme": "material-icon-theme",
  "editor.fontFamily": "'Fira Code', monospace",
  "editor.fontLigatures": true,
  "editor.fontSize": 14,

  // Comportement de l'éditeur
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true,
  "editor.tabSize": 2,
  "editor.wordWrap": "on",
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": true,
  "editor.suggestSelection": "first",
  "editor.cursorBlinking": "smooth",
  "editor.cursorSmoothCaretAnimation": "on",
  "editor.linkedEditing": true,
  "editor.snippetSuggestions": "top",

  // Terminal
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  "terminal.integrated.defaultProfile.linux": "bash",
  "terminal.integrated.fontFamily": "MesloLGS NF",

  // Files
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true,
  "files.trimFinalNewlines": true,
  "files.eol": "\n",

  // Git
  "git.enableSmartCommit": true,
  "git.confirmSync": false,
  "gitlens.codeLens.enabled": true,

  // Formatters
  "prettier.singleQuote": true,
  "prettier.printWidth": 100,
  "prettier.trailingComma": "es5",

  // Langages spécifiques
  "php.suggest.basic": false, // Désactivé car Intelephense gère ça
  "[php]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "bmewburn.vscode-intelephense-client"
  },
  "[javascript]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

## Augmenter votre productivité

1. **Utiliser les espaces de travail (workspaces)**

   - Enregistrez vos projets comme workspace pour conserver leur configuration spécifique
   - `File > Save Workspace As...`

2. **Personnaliser les snippets**

   - Créez vos propres snippets pour le code que vous tapez souvent
   - `File > Preferences > Configure User Snippets`

3. **Utiliser le mode Zen**

   - Mode plein écran sans distractions: `Ctrl+K Z` (Windows) / `Cmd+K Z` (Mac)

4. **Exploiter les tâches (Tasks)**

   - Automatisez des processus répétitifs avec des tasks personnalisées
   - Créez un fichier `.vscode/tasks.json`

5. **Synchroniser vos paramètres**
   - Utilisez "Settings Sync" pour maintenir votre configuration entre différentes machines
   - Connectez-vous avec votre compte GitHub pour synchroniser automatiquement
