# README.md



### Sommaire
1. [Description du projet](#1-description-du-projet)
2. [Intro](#2-intro)
3. [Choix techniques](#3-choix-techniques)
- 3.1 [Machines Virtuelles](#31-machines-virtuelles)
- 3.2 [Outils utilisés](#32-outils-utilisés)
4. [Difficultés rencontrées](#4-difficultés-rencontrées)
5. [Solutions trouvées](#5-solutions-trouvées)
6. [Améliorations possibles](#6-améliorations-possibles)

## 1. Description du projet

Cet outil d'administration centralisée permet de gérer des utilisateurs et des machines Linux à distance via un Script Bash.

Il est capable de :
- Gérer des utilisateurs à distance 
- Administrer des postes clients
- Interroger le status d'une machine
- Automatiser des opérations ciblées
---

## 2. Intro

Ce projet consiste à mettre en place une infrastructure virtuelle client/serveur Linux et déveloper un script d'administration centralisée en Bash.
Les machines sont sur le meme réseau.

---

## 3. Choix techniques

### 3.1 Machines Virtuelles

2 VM sont hébergées sur **VirtualBox** en réseau interne (`intnet`).

| Nom | Role | OS | IP | Compte | Mot de passe |
|-----|------|----|----|--------|--------------|
| SRVLX01 | Serveur Principal | Debian | 172.16.50.10 | root/wilder | Azerty1* |
| CLILIN01 | Client | Ubuntu | 172.16.50.30 | wilder | Azerty1* |

### 3.2 Outils utilisés

| Outil | Usage |
|-------|-------|
| VirtualBox | Virtualisation des machines |
| Github | Gestion de versions et dépot |
| OpenSSH Server | Communication entre les machines |
| Nano | Editer fichiers avec Terminal |
| Bash | Language du script d'admisnistration |

---

## 4. Difficultés rencontrées 

 ### Sprint 1 
 - Configuration du réseau interne entre les VMs — les machines ne se voyaient pas au départ
 - Configuration de l'IP fixe sur Ubuntu via Netplan

## Sprint 2 
- **Ordre des fonctions** - Bash une fonction doit etre définie avant d'etre apppelé. Les menus étaient placés avant les focntions ce qui causait des erreurs
- **Variables mal écrites** - le `$` manquait devant `CIBLE_IP` dans certaines fonctions SSH ce qui empechait de joindre la machine
- **Tabulations invisibles** - des caractères `^I` s'étaient glissés dans le script et causaient des erreurs de syntaxe
- **Droit sudo** - les commandes `shutdown`, `reboot`, `useradd` et `deluser` nécessitaient une configuration spéciale pour fonctionner sans mot de passe via SSH
- **Création d'utilisateurs** - `adduser` ne fonctionnait pas via SSH car il attend une interaction utilisateur

  ---

## 5. Solutions trouvées

 ### Sprint 1 
 - Passage en mode **Réseau interne** (`intnet`) dans VirtualBox pour que les VMs se voient entre elles
 - Configuration de l'IP fixe via le fichier `/etc/netplan/00-installer-config.yaml` sur Ubuntu

### Sprint 2
- Réorganisations du script - toutes les fonctions définies **en haut**, code principal **en bas**
-  Correction de toutes les variables avec `$CIBLE_IP` et `$CIBLE_USER`
- Suppression des tabulations invisibles avec la commande `sed -i 's/\t//g'`
- Ajout des commandes dans le fichier **sudoers** de CLILIN01 via `visudo` pour autoriser `wilder` sans mot de passe
- Remplacement de `adduser` par `useradd -m -s /bin/bash` combiné avec `chpasswd` pour créer les utilisateurs sans interaction

  ## 6. Améliorations possibles
  - Ajouter la gestion de **plusieurs machines cibles** en même temps
- Ajouter un **système de logs** pour tracer toutes les actions effectuées
- Ajouter une **vérification** que l'utilisateur existe avant de le supprimer
- Améliorer la **gestion des erreurs** avec des messages plus explicites
- Ajouter la possibilité de **choisir le mot de passe** lors de la création d'un utilisateur
  
