# Docker - La conteneurisation simplifiée

## Introduction à Docker

Docker est une plateforme open-source qui automatise le déploiement d'applications dans des conteneurs légers et portables. Contrairement aux machines virtuelles traditionnelles, les conteneurs Docker partagent le noyau du système d'exploitation hôte, ce qui les rend plus légers et plus efficaces.

## Pourquoi utiliser Docker ?

- **Isolation** : Chaque conteneur fonctionne de manière isolée
- **Portabilité** : Les applications s'exécutent de la même façon sur tous les environnements
- **Légèreté** : Consomme moins de ressources qu'une machine virtuelle
- **Rapidité** : Démarre en quelques secondes
- **Reproductibilité** : Environnement identique du développement à la production
- **Scalabilité** : Facilite le déploiement horizontal

## Architecture de Docker

- **Docker Engine** : Moteur de conteneurisation
- **Images** : Templates en lecture seule pour créer des conteneurs
- **Conteneurs** : Instances en exécution d'une image
- **Docker Hub** : Dépôt public d'images Docker
- **Dockerfile** : Script de construction d'images
- **Volumes** : Mécanisme de persistance des données

## Installation de Docker

### Linux (Ubuntu/Debian)

```bash
# Installer les prérequis
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# Ajouter la clé GPG officielle de Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Ajouter le dépôt Docker
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Installer Docker CE
sudo apt update
sudo apt install docker-ce

# Démarrer et activer Docker
sudo systemctl start docker
sudo systemctl enable docker

# Ajouter votre utilisateur au groupe docker (évite de taper sudo)
sudo usermod -aG docker $USER
```

Après avoir ajouté votre utilisateur au groupe docker, vous devrez vous déconnecter et reconnecter pour que les changements prennent effet.

## Commandes Docker essentielles

### Gestion des images

```bash
# Lister les images locales
docker images
docker image ls

# Rechercher une image sur Docker Hub
docker search nginx

# Télécharger une image
docker pull nginx:latest

# Construire une image à partir d'un Dockerfile
docker build -t mon-app:v1 .

# Afficher l'historique d'une image
docker history nginx:latest

# Supprimer une image
docker rmi nginx:latest
docker image rm nginx:latest

# Supprimer toutes les images non utilisées
docker image prune
```

### Gestion des conteneurs

```bash
# Lister les conteneurs en cours d'exécution
docker ps

# Lister tous les conteneurs (incluant ceux arrêtés)
docker ps -a

# Créer et démarrer un conteneur
docker run -d --name mon-nginx -p 8080:80 nginx

# Options courantes de docker run :
# -d : Mode détaché (en arrière-plan)
# -p : Publication de ports (hôte:conteneur)
# -v : Montage de volumes (hôte:conteneur)
# --name : Nom personnalisé
# -e : Variables d'environnement
# --network : Réseau à utiliser
# --restart : Politique de redémarrage

# Arrêter un conteneur
docker stop mon-nginx

# Démarrer un conteneur arrêté
docker start mon-nginx

# Redémarrer un conteneur
docker restart mon-nginx

# Supprimer un conteneur
docker rm mon-nginx

# Supprimer un conteneur en cours d'exécution
docker rm -f mon-nginx

# Supprimer tous les conteneurs arrêtés
docker container prune
```

### Interaction avec les conteneurs

```bash
# Exécuter une commande dans un conteneur en cours d'exécution
docker exec -it mon-nginx bash

# Afficher les logs d'un conteneur
docker logs mon-nginx

# Suivre les logs en temps réel
docker logs -f mon-nginx

# Copier des fichiers entre l'hôte et le conteneur
docker cp fichier.txt mon-nginx:/app/
docker cp mon-nginx:/var/log/nginx/access.log ./access.log

# Afficher les statistiques d'utilisation des ressources
docker stats mon-nginx
```

### Gestion des volumes

```bash
# Créer un volume nommé
docker volume create mon-volume

# Lister les volumes
docker volume ls

# Inspecter un volume
docker volume inspect mon-volume

# Utiliser un volume lors du lancement d'un conteneur
docker run -d --name mon-app -v mon-volume:/data nginx

# Monter un dossier local comme volume
docker run -d --name mon-app -v $(pwd):/app nginx

# Supprimer un volume
docker volume rm mon-volume

# Supprimer tous les volumes non utilisés
docker volume prune
```

### Gestion des réseaux

```bash
# Créer un réseau
docker network create mon-reseau

# Lister les réseaux
docker network ls

# Inspecter un réseau
docker network inspect mon-reseau

# Connecter un conteneur à un réseau
docker network connect mon-reseau mon-nginx

# Déconnecter un conteneur d'un réseau
docker network disconnect mon-reseau mon-nginx

# Exécuter un conteneur avec un réseau spécifique
docker run --network=mon-reseau nginx

# Supprimer un réseau
docker network rm mon-reseau

# Supprimer tous les réseaux non utilisés
docker network prune
```

## Exemple de Dockerfile

```dockerfile
# Image de base
FROM node:14-alpine

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers de dépendances
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers
COPY . .

# Variables d'environnement
ENV PORT=3000 NODE_ENV=production

# Exposer le port
EXPOSE 3000

# Commande de démarrage
CMD ["npm", "start"]
```

## Cas d'utilisation typiques

1. **Environnement de développement**

   ```bash
   # Lancer une base de données PostgreSQL
   docker run -d --name postgres -e POSTGRES_PASSWORD=secret -p 5432:5432 postgres:13
   ```

2. **Stack web complète**

   ```bash
   # Créer un réseau pour interconnecter les conteneurs
   docker network create web-app

   # Base de données
   docker run -d --name db --network web-app -v db-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=secret mysql:8

   # Backend
   docker run -d --name api --network web-app -p 8080:8080 -e DB_HOST=db mon-api:latest

   # Frontend
   docker run -d --name frontend --network web-app -p 80:80 mon-frontend:latest
   ```

3. **Conteneur éphémère pour tests**
   ```bash
   # Lancer un conteneur, exécuter une commande puis le supprimer
   docker run --rm -v $(pwd):/app node:14 npm test
   ```

## Bonnes pratiques

1. **Images légères** : Préférez les images Alpine quand possible
2. **Multi-stage builds** : Réduisez la taille des images finales
3. **Sécurité** : Limitez les privilèges, scannez les vulnérabilités
4. **Données persistantes** : Utilisez toujours des volumes pour les données importantes
5. **Logging** : Configurez correctement la gestion des logs
6. **Étiquettes** : Versionnez clairement vos images
