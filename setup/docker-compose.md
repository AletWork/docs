# Docker Compose - Orchestration multi-conteneurs

## Introduction à Docker Compose

Docker Compose est un outil qui permet de définir et d'exécuter des applications Docker multi-conteneurs. Avec un simple fichier YAML, vous pouvez configurer tous les services de votre application, puis démarrer l'ensemble de votre stack d'un seul coup de commande.

## Pourquoi utiliser Docker Compose ?

- **Simplicité** : Décrivez toute votre stack dans un seul fichier
- **Reproductibilité** : Garantit que chaque environnement est identique
- **Organisation** : Gère facilement les dépendances entre services
- **Développement simplifié** : Facilite la configuration des environnements de développement
- **Contrôle de versions** : Le fichier docker-compose.yml peut être versionné avec votre code
- **Gestion du cycle de vie** : Démarrer, arrêter et reconstruire tous les services en une commande

## Installation de Docker Compose

Docker Compose est généralement installé avec Docker Desktop sur Windows et macOS. Sur Linux :

```bash
# Télécharger la version stable
sudo curl -L "https://github.com/docker/compose/releases/download/v2.17.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# Rendre le binaire exécutable
sudo chmod +x /usr/local/bin/docker-compose

# Vérifier l'installation
docker-compose --version
```

Pour les versions plus récentes de Docker, vous pouvez utiliser le plugin intégré :

```bash
docker compose version
```

## Structure d'un fichier docker-compose.yml

```yaml
version: "3.8"

services:
  webapp:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./site:/usr/share/nginx/html
    depends_on:
      - api
    restart: always

  api:
    build: ./api
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DB_HOST=db
    depends_on:
      - db

  db:
    image: postgres:13
    volumes:
      - postgres-data:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=secret
      - POSTGRES_USER=myuser
      - POSTGRES_DB=mydb

volumes:
  postgres-data:

networks:
  default:
    name: my-network
```

## Commandes Docker Compose essentielles

### Gestion des services

```bash
# Démarrer tous les services définis dans docker-compose.yml
docker-compose up

# Démarrer en mode détaché (background)
docker-compose up -d

# Démarrer des services spécifiques
docker-compose up -d webapp api

# Arrêter les services
docker-compose stop

# Arrêter et supprimer les conteneurs
docker-compose down

# Arrêter et supprimer les conteneurs, volumes et images créés
docker-compose down --volumes --rmi all

# Redémarrer les services
docker-compose restart

# Recréer les conteneurs (utile après modification de docker-compose.yml)
docker-compose up -d --force-recreate

# Mettre à l'échelle un service (créer plusieurs instances)
docker-compose up -d --scale api=3
```

### Suivi et inspection

```bash
# Voir l'état des services
docker-compose ps

# Afficher les logs de tous les services
docker-compose logs

# Afficher les logs d'un service spécifique
docker-compose logs api

# Suivre les logs en temps réel
docker-compose logs -f

# Exécuter une commande dans un service
docker-compose exec api npm test

# Afficher les processus en cours dans un service
docker-compose top
```

### Construction et gestion des images

```bash
# Construire ou reconstruire les services
docker-compose build

# Construire sans cache
docker-compose build --no-cache

# Construire un service spécifique
docker-compose build api

# Tirer (pull) les dernières images
docker-compose pull

# Pousser des images vers le registre
docker-compose push
```

### Configuration et validation

```bash
# Valider le fichier docker-compose.yml
docker-compose config

# Afficher les variables d'environnement
docker-compose config --services

# Générer un fichier docker-compose.yml à partir d'un conteneur existant
docker-compose convert
```

## Concepts clés de Docker Compose

### Services

Définissent les conteneurs à exécuter et leur configuration :

```yaml
services:
  app:
    image: node:14-alpine
    command: npm start
    ports:
      - "3000:3000"
```

### Volumes

Permettent la persistance des données entre les redémarrages :

```yaml
services:
  db:
    volumes:
      - db-data:/var/lib/mysql
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql

volumes:
  db-data:
```

### Networks

Permettent aux conteneurs de communiquer entre eux :

```yaml
services:
  frontend:
    networks:
      - frontend-network

  backend:
    networks:
      - frontend-network
      - backend-network

networks:
  frontend-network:
  backend-network:
```

### Variables d'environnement

Plusieurs façons de définir des variables d'environnement :

```yaml
services:
  api:
    # Directement dans le fichier
    environment:
      - DEBUG=true
      - API_KEY=secret

    # Depuis un fichier
    env_file:
      - .env.api

    # Depuis les variables d'environnement de l'hôte
    environment:
      - HOST_VAR=${HOST_VARIABLE}
```

## Cas d'utilisation courants

### Stack de développement web

```yaml
version: "3.8"

services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    volumes:
      - ./frontend:/app
      - /app/node_modules
    command: npm start
    environment:
      - REACT_APP_API_URL=http://localhost:4000

  backend:
    build: ./backend
    ports:
      - "4000:4000"
    volumes:
      - ./backend:/app
      - /app/node_modules
    command: npm run dev
    environment:
      - DB_HOST=db
      - DB_USER=postgres
      - DB_PASS=secret
    depends_on:
      - db

  db:
    image: postgres:13
    ports:
      - "5432:5432"
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=secret
      - POSTGRES_DB=myapp
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

### Stack WordPress

```yaml
version: "3.8"

services:
  wordpress:
    image: wordpress:latest
    ports:
      - "8080:80"
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
    volumes:
      - wordpress_data:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:5.7
    environment:
      - MYSQL_ROOT_PASSWORD=rootpass
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    volumes:
      - db_data:/var/lib/mysql

volumes:
  wordpress_data:
  db_data:
```

## Bonnes pratiques

1. **Versionnez votre docker-compose.yml** avec le code source
2. **Utilisez des fichiers .env** pour les configurations spécifiques à l'environnement
3. **Créez des builds multi-étapes** pour réduire la taille des images
4. **Spécifiez des versions précises** d'images plutôt que `latest`
5. **Utilisez des healthchecks** pour vérifier l'état des services
6. **Nommez vos volumes** pour faciliter leur identification
7. **Configurez des redémarrages automatiques** avec `restart: always` ou `restart: unless-stopped`

## Méthodes de déploiement

### Développement local

```bash
docker-compose up
```

### Production avec fichier alternatif

```bash
# Utiliser un fichier spécifique pour la production
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

### Déploiement avec Docker Swarm

```bash
# Initialiser Docker Swarm
docker swarm init

# Déployer la stack
docker stack deploy -c docker-compose.yml my-stack
```

## Limitations de Docker Compose

- Non conçu pour l'orchestration à grande échelle (utilisez Kubernetes pour cela)
- Options limitées pour l'équilibrage de charge et le scaling automatique
- Fonctionnalités de haute disponibilité limitées

Pour des déploiements de production plus robustes, envisagez Docker Swarm, Kubernetes ou des services gérés comme AWS ECS/EKS.
