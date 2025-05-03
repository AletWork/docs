# Documentation PHP

## Introduction

PHP (PHP: Hypertext Preprocessor) est un langage de script orienté serveur particulièrement adapté au développement web. Il est utilisé par des millions de sites et d'applications web à travers le monde.

## Structure de la documentation PHP

Cette documentation PHP couvre les aspects suivants :

- [Bases du PHP](bases.md) - Syntaxe fondamentale, types de données, variables, constantes
- [Fonctions en PHP](fonctions.md) - Création et utilisation de fonctions
- [Laravel](laravel/index.md) - Framework PHP moderne

## Environnement de développement

Pour développer efficacement en PHP, vous aurez besoin :

1. **Serveur web avec PHP** : Apache, Nginx ou le serveur de développement intégré de PHP
2. **Base de données** : MySQL, PostgreSQL ou SQLite
3. **Gestionnaire de dépendances** : Composer
4. **IDE ou éditeur de code** : PHPStorm, VS Code avec extensions PHP
5. **Outils de débogage** : Xdebug

## Versions de PHP

| Version | Date de sortie | Fin du support | Fin du support sécurité |
| ------- | -------------- | -------------- | ----------------------- |
| PHP 8.3 | Nov 2023       | Nov 2025       | Nov 2026                |
| PHP 8.2 | Déc 2022       | Déc 2024       | Déc 2025                |
| PHP 8.1 | Nov 2021       | Nov 2023       | Nov 2024                |
| PHP 8.0 | Nov 2020       | Nov 2022       | Nov 2023                |
| PHP 7.4 | Nov 2019       | Nov 2021       | Nov 2022                |

Il est recommandé d'utiliser PHP 8.1 ou supérieur pour les nouveaux projets.

## Bonnes pratiques

- Suivre les [PHP Standard Recommendations (PSR)](https://www.php-fig.org/psr/)
- Utiliser Composer pour gérer les dépendances
- Structurer son code de façon orientée objet
- Isoler la logique métier de la logique de présentation
- Écrire des tests unitaires
- Utiliser des outils d'analyse statique comme PHPStan ou Psalm

## Ressources utiles

- [Documentation officielle PHP](https://www.php.net/manual/fr/)
- [PHP: The Right Way](https://phptherightway.com/)
- [Packagist](https://packagist.org/) - Dépôt de packages pour Composer
