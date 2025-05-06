# Git - Le système de contrôle de version

## Introduction à Git

Git est un système de contrôle de version distribué conçu pour suivre les modifications du code source pendant le développement logiciel. Il permet à plusieurs développeurs de travailler ensemble sur un même projet sans conflit. Créé par Linus Torvalds en 2005 pour le développement du noyau Linux, Git est aujourd'hui l'outil standard de gestion de versions.

## Pourquoi utiliser Git ?

- **Historique complet** : Conserve l'historique détaillé de toutes les modifications
- **Système distribué** : Chaque développeur dispose d'une copie complète du dépôt
- **Branches** : Facilite le développement parallèle de fonctionnalités
- **Fusion intelligente** : Résolution automatique de la plupart des conflits
- **Rapidité** : Opérations locales très performantes

## Configuration initiale

```bash
# Configurer votre identité
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@exemple.com"

# Configurer l'éditeur par défaut
git config --global core.editor "code --wait"  # Pour VS Code

# Vérifier votre configuration
git config --list
```

## Commandes Git essentielles

### Démarrer et cloner des projets

```bash
# Initialiser un nouveau dépôt Git
git init

# Cloner un dépôt existant
git clone https://github.com/utilisateur/depot.git

# Cloner une branche spécifique
git clone -b ma-branche https://github.com/utilisateur/depot.git
```

### Gérer les changements

```bash
# Vérifier l'état des fichiers
git status

# Ajouter des fichiers à l'index (staging)
git add fichier.txt       # Un fichier spécifique
git add dossier/          # Tous les fichiers d'un dossier
git add .                 # Tous les fichiers modifiés

# Créer un commit (valider les changements)
git commit -m "Description du changement"

# Ajouter et commiter en une seule étape
git commit -am "Description du changement"
```

### Synchroniser avec le dépôt distant

```bash
# Récupérer les modifications du dépôt distant sans fusion
git fetch origin

# Récupérer ET fusionner les modifications
git pull origin main

# Envoyer vos commits vers le dépôt distant
git push origin main

# Configurer le suivi de branche
git branch --set-upstream-to=origin/main main
```

### Travailler avec les branches

```bash
# Lister les branches
git branch                # Branches locales
git branch -r             # Branches distantes
git branch -a             # Toutes les branches

# Créer une nouvelle branche
git branch nouvelle-branche

# Changer de branche
git checkout nouvelle-branche
git switch nouvelle-branche    # Git récent

# Créer et changer en une commande
git checkout -b nouvelle-branche
git switch -c nouvelle-branche  # Git récent

# Fusionner une branche dans la branche courante
git merge autre-branche

# Supprimer une branche
git branch -d branche-terminee  # Supprime si fusionnée
git branch -D branche-a-supprimer  # Force la suppression
```

### Examiner l'historique

```bash
# Afficher l'historique des commits
git log
git log --oneline         # Format compact
git log --graph --oneline # Avec graphe
git log -p                # Avec détail des modifications

# Voir les modifications sur un fichier
git blame fichier.txt     # Qui a modifié quoi et quand
```

### Annuler des changements

```bash
# Annuler les modifications non indexées
git restore fichier.txt
git checkout -- fichier.txt  # Ancienne syntaxe

# Désindexer un fichier (retirer du staging)
git restore --staged fichier.txt
git reset HEAD fichier.txt   # Ancienne syntaxe

# Modifier le dernier commit
git commit --amend -m "Nouveau message"

# Revenir à un commit spécifique
git reset --soft HEAD~1   # Conserve les modifications en staging
git reset --mixed HEAD~1  # Désindexe les modifications (défaut)
git reset --hard HEAD~1   # Supprime toutes les modifications
```

### Gérer les conflits

```bash
# Après un conflit lors d'un merge ou pull
# 1. Éditer les fichiers pour résoudre les conflits
# 2. Marquer comme résolus
git add fichier-avec-conflit.txt
# 3. Finaliser le merge
git commit
```

### Stash (remiser) des modifications

```bash
# Remiser les modifications non commitées
git stash

# Lister les stash
git stash list

# Appliquer le dernier stash
git stash apply

# Appliquer un stash spécifique
git stash apply stash@{2}

# Appliquer et supprimer le dernier stash
git stash pop

# Supprimer un stash
git stash drop stash@{0}

# Créer une branche à partir d'un stash
git stash branch nouvelle-branche
```

## Workflow Git typique

```bash
# 1. Mettre à jour votre copie locale
git pull origin main

# 2. Créer une branche pour votre fonctionnalité
git checkout -b feature/nouvelle-fonctionnalite

# 3. Faire des modifications et commiter
git add .
git commit -m "Ajoute la nouvelle fonctionnalité"

# 4. Mettre à jour avec la branche principale
git fetch origin
git rebase origin/main

# 5. Pousser votre branche
git push origin feature/nouvelle-fonctionnalite

# 6. Créer une Pull Request (via l'interface GitHub/GitLab)

# 7. Une fois la PR fusionnée, retourner sur main et mettre à jour
git checkout main
git pull origin main

# 8. Supprimer la branche de fonctionnalité
git branch -d feature/nouvelle-fonctionnalite
```

## Astuces avancées

- **Alias** : Créez des raccourcis pour les commandes fréquentes

  ```bash
  git config --global alias.co checkout
  git config --global alias.br branch
  git config --global alias.st status
  ```

- **Ignorer des fichiers** : Créez un fichier `.gitignore` à la racine de votre projet

- **Git hooks** : Automatisez des actions avec des scripts dans `.git/hooks/`

- **Interactive rebase** : Réorganisez, modifiez, écrasez des commits
  ```bash
  git rebase -i HEAD~3  # Pour les 3 derniers commits
  ```
