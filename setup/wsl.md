# Installation et usage de WSL

## Introduction à WSL

WSL (Windows Subsystem for Linux) permet d'exécuter un environnement Linux directement sous Windows, sans la surcharge d'une machine virtuelle traditionnelle.

## Installation

1. Ouvrir PowerShell en tant qu'administrateur
2. Exécuter la commande : `wsl --install`
3. Redémarrer l'ordinateur
4. Une fois redémarré, terminer la configuration de votre distribution Linux

## Usage courant

### Accéder à vos fichiers Windows depuis WSL

Les lecteurs Windows sont montés sous `/mnt/` :
```bash
# Accéder au lecteur C:
cd /mnt/c
```

### Accéder aux fichiers WSL depuis Windows

Via l'explorateur Windows avec le chemin : `\\wsl.localhost\<NomDeLaDistribution>\`
Exemple : \\wsl.localhost\Ubuntu

## Bonnes pratiques

- Stocker vos projets de développement dans le système de fichiers Linux pour de meilleures performances
- Utiliser Visual Studio Code avec l'extension "Remote - WSL" pour une intégration optimale

## Dépannage

### Problèmes courants et solutions

- Si WSL ne démarre pas, vérifiez que la virtualisation est activée dans le BIOS
- Pour redémarrer WSL : `wsl --shutdown` puis relancer votre terminal WSL