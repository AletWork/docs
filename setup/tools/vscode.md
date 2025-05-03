# Visual Studio Code

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

## Extensions essentielles

- **Prettier** : Formatteur de code automatique
- **ESLint** : Linter pour JavaScript
- **PHP Intelephense** : Support avancé pour PHP
- **Laravel Blade Snippets** : Snippets pour Laravel Blade
- **Remote - WSL** : Développement dans WSL
- **Docker** : Gestion de conteneurs Docker

## Raccourcis clavier utiles

| Action                       | Windows            | Mac               |
| ---------------------------- | ------------------ | ----------------- |
| Palette de commandes         | `Ctrl+Shift+P`     | `Cmd+Shift+P`     |
| Rechercher dans les fichiers | `Ctrl+Shift+F`     | `Cmd+Shift+F`     |
| Ouvrir un fichier            | `Ctrl+P`           | `Cmd+P`           |
| Commenter/décommenter        | `Ctrl+/`           | `Cmd+/`           |
| Multi-sélection              | `Ctrl+D` (répéter) | `Cmd+D` (répéter) |
| Terminal intégré             | `` Ctrl+`  ``      | `` Cmd+`  ``      |

## Configuration recommandée

Voici quelques paramètres recommandés à ajouter à votre `settings.json` :

```json
{
  "editor.formatOnSave": true,
  "editor.tabSize": 2,
  "editor.renderWhitespace": "boundary",
  "editor.wordWrap": "on",
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  "terminal.integrated.defaultProfile.windows": "Git Bash"
}
```

## Déboguer avec VS Code

1. Ouvrir la vue débogage (`Ctrl+Shift+D`)
2. Créer un fichier de configuration de lancement (`.vscode/launch.json`)
3. Configurer selon le langage utilisé
4. Lancer le débogage avec `F5`

## Intégration Git

- Visualisation des modifications dans l'éditeur
- Gestion des branches avec la barre de statut
- Résolution de conflits intégrée
- Historique des commits
