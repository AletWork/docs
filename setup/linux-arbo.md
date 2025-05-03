# Comprendre l'arborescence Linux

## Structure principale du système de fichiers Linux

Linux organise ses fichiers selon un système hiérarchique standardisé. Voici les répertoires principaux et leur rôle :

### `/` (root)

Le point de départ de toute l'arborescence du système de fichiers.

### `/bin`

Contient les binaires essentiels du système, accessibles à tous les utilisateurs.

### `/boot`

Contient les fichiers nécessaires au démarrage du système (noyau, initramfs, bootloader).

### `/dev`

Contient les fichiers spéciaux représentant les périphériques matériels.

### `/etc`

Contient les fichiers de configuration système.

### `/home`

Contient les répertoires personnels des utilisateurs.

### `/lib`

Contient les bibliothèques partagées essentielles au système.

### `/media` et `/mnt`

Points de montage pour les périphériques amovibles et les montages temporaires.

### `/opt`

Emplacement pour l'installation de logiciels optionnels.

### `/proc`

Système de fichiers virtuel qui fournit des informations sur les processus en cours.

### `/root`

Répertoire personnel de l'utilisateur root.

### `/sbin`

Contient les binaires système critiques, généralement exécutés par l'administrateur.

### `/tmp`

Répertoire pour les fichiers temporaires.

### `/usr`

Contient la majorité des programmes et utilitaires destinés aux utilisateurs.

### `/var`

Contient les données variables comme les logs, les bases de données, les sites web, etc.

## Navigation dans le système de fichiers

```bash
# Afficher le répertoire courant
pwd

# Lister les fichiers et dossiers
ls -la

# Changer de répertoire
cd /chemin/vers/dossier

# Afficher le contenu d'un fichier
cat /chemin/vers/fichier
```

## Permissions des fichiers

Linux utilise un système de permissions basé sur trois niveaux : propriétaire, groupe et autres.

```bash
# Afficher les permissions d'un fichier
ls -l fichier.txt

# Modifier les permissions
chmod 755 fichier.txt  # rwx pour propriétaire, r-x pour groupe et autres
```
