# Routes Laravel

## Introduction aux Routes

Les routes permettent de définir comment votre application répond aux requêtes HTTP. Toutes les routes Laravel sont définies dans les fichiers de routes situés dans le répertoire `routes/`.

## Fichiers de routes

- **routes/web.php** : Routes pour l'interface web (avec session, cookies, CSRF)
- **routes/api.php** : Routes pour l'API (sans état, avec préfixe `/api`)
- **routes/console.php** : Commandes console personnalisées
- **routes/channels.php** : Canaux de diffusion pour le temps réel

## Routes de base

### Route GET simple

```php
Route::get('/bienvenue', function () {
    return 'Bienvenue sur notre site!';
});
```

### Route avec paramètres

```php
Route::get('/utilisateurs/{id}', function ($id) {
    return 'Utilisateur ' . $id;
});
```

### Paramètres optionnels

```php
Route::get('/utilisateurs/{name?}', function ($name = 'Invité') {
    return 'Utilisateur ' . $name;
});
```

## Contraintes sur les paramètres

```php
// Contrainte par expression régulière
Route::get('/utilisateurs/{id}', function ($id) {
    return 'Utilisateur ' . $id;
})->where('id', '[0-9]+');

// Contraintes multiples
Route::get('/posts/{id}/{slug}', function ($id, $slug) {
    return "Post $id avec slug $slug";
})->where(['id' => '[0-9]+', 'slug' => '[A-Za-z0-9\-]+']);

// Contraintes communes
Route::get('/categorie/{category}', function ($category) {
    return "Catégorie: $category";
})->whereAlpha('category');
```

## Méthodes HTTP

```php
Route::get('/posts', [PostController::class, 'index']);
Route::post('/posts', [PostController::class, 'store']);
Route::put('/posts/{id}', [PostController::class, 'update']);
Route::delete('/posts/{id}', [PostController::class, 'destroy']);

// Plusieurs méthodes
Route::match(['get', 'post'], '/formulaire', [FormulaireController::class, 'gerer']);

// Toutes les méthodes
Route::any('/contenu', [ContenuController::class, 'index']);
```

## Routes vers des contrôleurs

```php
// Format de base
Route::get('/posts', [PostController::class, 'index']);

// Appel d'une méthode d'un contrôleur unique
Route::get('/profile', SingleActionController::class);
```

## Routes nommées

```php
Route::get('/profil/utilisateur', [ProfileController::class, 'show'])
    ->name('profile.show');
```

Utiliser des routes nommées dans votre code:

```php
// Génération d'URL
$url = route('profile.show');

// Redirection
return redirect()->route('profile.show');

// Avec paramètres
Route::get('/utilisateurs/{id}', [UserController::class, 'show'])
    ->name('users.show');

$url = route('users.show', ['id' => 1]);
```

## Groupes de routes

### Préfixe de routes

```php
Route::prefix('admin')->group(function () {
    Route::get('/dashboard', [AdminController::class, 'dashboard']);
    Route::get('/utilisateurs', [AdminController::class, 'users']);
});
// Crée /admin/dashboard et /admin/utilisateurs
```

### Espace de noms de contrôleurs

```php
Route::namespace('App\Http\Controllers\Admin')->group(function () {
    // Contrôleurs dans App\Http\Controllers\Admin
});
```

### Middleware

```php
Route::middleware(['auth'])->group(function () {
    Route::get('/tableau-de-bord', [DashboardController::class, 'index']);
    Route::get('/compte', [AccountController::class, 'index']);
});
```

### Groupe complet

```php
Route::prefix('admin')
    ->middleware(['auth', 'admin'])
    ->name('admin.')
    ->group(function () {
        Route::get('/dashboard', [AdminController::class, 'dashboard'])
            ->name('dashboard'); // Nom complet: admin.dashboard
    });
```

## Routes de ressource

```php
// Crée toutes les routes CRUD pour la ressource posts
Route::resource('posts', PostController::class);

// Routes partielles
Route::resource('comments', CommentController::class)
    ->only(['index', 'show']);

Route::resource('photos', PhotoController::class)
    ->except(['create', 'store', 'update', 'destroy']);

// Routes de ressource imbriquées
Route::resource('posts.comments', PostCommentController::class);
// Crée des routes comme /posts/{post}/comments/{comment}
```

## Injection de dépendances

```php
Route::get('/utilisateurs', function (Request $request) {
    // $request est automatiquement injecté
    return $request->all();
});
```

## Fallback Route

```php
// Route de secours (404 personnalisée)
Route::fallback(function () {
    return view('errors.404');
});
```

## Bonnes pratiques

1. **Organisez vos routes** par fonctionnalités ou domaines métiers
2. **Utilisez des routes nommées** pour ne pas avoir à modifier les URLs dans le code
3. **Préférez les contrôleurs** aux fonctions anonymes pour les routes complexes
4. **Appliquez des contraintes** aux paramètres pour la validation
5. **Utilisez des groupes** pour les routes partageant des attributs communs
6. **Créez des ressources API** séparées pour une meilleure organisation
