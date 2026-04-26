# README.md



### Sommaire
1. [Description du projet](#1-description-du-projet)
2. [Intro](#2-intro)
3. [Choix techniques](#3-choix-techniques)
- 3.1 [Machines Virtuelles](#31-machines-virtuelles)
- 3.2 [Outils utilisés](#32-outils-utilisés)
4. [Difficultés rencontrées](#4-difficultés-rencontrées)

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
