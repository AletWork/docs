# Laravel

## Introduction

Laravel est un framework PHP open-source élégant et expressif, conçu pour faciliter et accélérer le développement d'applications web. Il suit le pattern architectural MVC (Modèle-Vue-Contrôleur) et propose une syntaxe expressive et fluide.

## Philosophie

Laravel a été créé avec l'idée que le développement doit être une expérience agréable et créative. Il vise à rendre le processus de développement satisfaisant tout en maintenant la flexibilité nécessaire pour les grandes applications complexes.

## Structure de la documentation Laravel

Cette documentation Laravel couvre les aspects suivants :

- [Routes](routes.md) - Configuration et gestion des routes
- [Controllers](controllers.md) - Structure et bonnes pratiques
- [Exemples](exemples.md) - Cas pratiques d'utilisation

## Installation et configuration

### Prérequis

- PHP >= 8.1
- Composer
- Extensions PHP : OpenSSL, PDO, Mbstring, Tokenizer, XML

### Installation via Composer

```bash
composer create-project laravel/laravel mon-projet
cd mon-projet
php artisan serve
```

## Architecture de l'application

Laravel suit une architecture MVC bien organisée :

```
app/
├── Console/          # Commandes Artisan personnalisées
├── Exceptions/       # Gestionnaires d'exceptions
├── Http/
│   ├── Controllers/  # Contrôleurs
│   ├── Middleware/   # Middleware
│   └── Requests/     # Form requests
├── Models/           # Modèles Eloquent
├── Providers/        # Service providers
└── Services/         # Services métier

bootstrap/           # Bootstrap de l'application
config/              # Fichiers de configuration
database/
├── factories/        # Factories pour les tests
├── migrations/       # Migrations de base de données
└── seeders/          # Seeders de base de données

public/              # Point d'entrée public
resources/
├── css/             # Fichiers CSS
├── js/              # Fichiers JavaScript
└── views/           # Templates Blade

routes/
├── api.php          # Routes API
├── channels.php     # Canaux de broadcast
├── console.php      # Commandes console
└── web.php          # Routes web

storage/             # Fichiers générés
tests/               # Tests unitaires et fonctionnels
```

## Concepts clés

- **Artisan** : Interface en ligne de commande de Laravel
- **Eloquent ORM** : ORM expressif pour interagir avec la base de données
- **Blade** : Moteur de templates puissant et intuitif
- **Middleware** : Filtres des requêtes HTTP
- **Service Container** : Conteneur d'injection de dépendances
- **Service Providers** : Point central de bootstrap de l'application
- **Migrations** : Contrôle de version pour la base de données
- **Seeding** : Remplissage de la base de données avec des données de test

## Ressources utiles

- [Documentation officielle](https://laravel.com/docs)
- [Laracasts](https://laracasts.com) - Tutoriels vidéo
- [Laravel News](https://laravel-news.com) - Actualités sur Laravel
- [Laravel Forge](https://forge.laravel.com) - Déploiement simplifié
