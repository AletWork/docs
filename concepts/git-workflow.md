# Git Workflow et bonnes pratiques

## Introduction à Git Flow

Git Flow est un modèle de branchement pour Git qui définit une structure stricte de branches pour le développement de projets. Il facilite le développement parallèle, la collaboration et la gestion des versions.

## Branches principales

### `main` (ou `master`)

- Contient le code de production
- Stable et toujours déployable
- Jamais de commit direct (sauf initialisation)
- Chaque commit représente une nouvelle version

### `develop`

- Branche d'intégration principale
- Contient les fonctionnalités terminées en attente de release
- Base pour les branches de fonctionnalités

## Branches de support

### `feature/*`

- Créées à partir de `develop`
- Fusionnées dans `develop`
- Convention de nommage : `feature/nom-de-la-fonctionnalite`
- Une branche par fonctionnalité

```bash
# Créer une branche de fonctionnalité
git checkout develop
git checkout -b feature/nouvelle-fonction

# Une fois terminée, fusionner dans develop
git checkout develop
git merge --no-ff feature/nouvelle-fonction
git push origin develop
git branch -d feature/nouvelle-fonction
```

### `release/*`

- Créées à partir de `develop`
- Fusionnées dans `main` ET `develop`
- Préparation de la version de production
- Corrections de bugs mineures uniquement

```bash
# Créer une branche de release
git checkout develop
git checkout -b release/1.0.0

# Une fois prête, fusionner dans main et develop
git checkout main
git merge --no-ff release/1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"
git push --tags

git checkout develop
git merge --no-ff release/1.0.0
git branch -d release/1.0.0
```

### `hotfix/*`

- Créées à partir de `main`
- Fusionnées dans `main` ET `develop`
- Corrections urgentes en production

```bash
# Créer une branche de hotfix
git checkout main
git checkout -b hotfix/bug-critique

# Une fois corrigé, fusionner dans main et develop
git checkout main
git merge --no-ff hotfix/bug-critique
git tag -a v1.0.1 -m "Version 1.0.1"
git push --tags

git checkout develop
git merge --no-ff hotfix/bug-critique
git branch -d hotfix/bug-critique
```

## Bonnes pratiques Git

### Messages de commit

- Format : `type(scope): message court`
- Types courants : `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
- Exemple : `feat(auth): add social login with Google`
- Message concis en impératif
- Détails supplémentaires dans le corps du message si nécessaire

### Pull Requests

- Description claire
- Lier aux tickets/issues
- Petites PRs pour faciliter la revue
- Inclure des tests
- Demander la revue des personnes appropriées

### Stratégie de fusion

- Merge commit: `git merge --no-ff` pour conserver l'historique des branches
- Rebase: `git rebase` pour un historique linéaire
- Squash: Combiner plusieurs commits en un seul pour une PR

### Résolution de conflits

1. `git pull` pour obtenir les derniers changements
2. Résoudre les conflits dans les fichiers marqués
3. `git add` les fichiers résolus
4. `git commit` pour finaliser la résolution

## Outils recommandés

- **GitKraken** / **SourceTree** : Interfaces graphiques
- **git-flow** : Extension CLI pour faciliter Git Flow
- **husky** : Hooks Git pour validation avant commit/push
- **commitlint** : Validation de la convention de messages de commit
- **GitHub Actions** / **GitLab CI** : Intégration continue

## Anti-patterns à éviter

- Commits directement sur `main`
- Branches de fonctionnalités à durée de vie trop longue
- Messages de commit vagues ou non conventionnels
- Ignorer les revues de code
- Push force sans précaution (`git push --force-with-lease` est préférable)
