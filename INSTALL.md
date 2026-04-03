## Sommaire

1. [Prérequis techniques](#1-prérequis-techniques)
2. [Installation sur le serveur Debian SRVLX01](#2-installation-sur-le-serveur-debian-srvlx01)
   - 2.1 [Mise à jour du système](#21-mise-à-jour-du-système)
   - 2.2 [Changer le nom de la machine](#22-changer-le-nom-de-la-machine)
   - 2.3 [Configurer l'IP fixe](#23-configurer-lip-fixe)
   - 2.4 [Installer OpenSSH serveur](#24-installer-openssh-serveur)
   - 2.5 [Vérification du service](#25-vérification-du-service)
3. [Installation sur le client Ubuntu CLILIN01](#3-installation-sur-le-client-ubuntu-clilin01)
   - 3.1 [Changer le nom de la machine](#31-changer-le-nom-de-la-machine)
   - 3.2 [Configurer l'IP fixe](#32-configurer-lip-fixe)
   - 3.3 [Installer OpenSSH](#33-installer-openssh)
   - 3.4 [Configuration du pare-feu](#34-configuration-du-pare-feu)
4. [Vérification de la connexion réseau](#4-vérification-de-la-connexion-réseau)
5. [Connexion SSH sans mot de passe](#5-connexion-ssh-sans-mot-de-passe)
   - 5.1 [Générer une clé SSH](#51-générer-une-clé-ssh)
   - 5.2 [Copier la clé sur les machines cibles](#52-copier-la-clé-sur-les-machines-cibles)
   - 5.3 [Tester la connexion](#53-tester-la-connexion)

---

## 1. Prérequis techniques

### Matériel recommandé

- Toutes les VMs en mode **Réseau interne** (`intnet`) dans VirtualBox

### Machines du projet

| Machine | OS | IP | Accès requis |
|---|---|---|---|
| SRVLX01 | Debian | 172.16.50.10 | root ou sudo |
| CLILIN01 | Ubuntu 24 LTS | 172.16.50.30 | sudo |


---

## 2. Installation sur le serveur Debian SRVLX01

### 2.1 Mise à jour du système

Se connecter avec `wilder` ou `root`, puis mettre à jour :
```
sudo apt update && sudo apt upgrade -y
```
<img width="756" height="192" alt="sudo apt updat-1$-1" src="https://github.com/user-attachments/assets/622e1c37-7dbe-498b-8341-57f1786d44c8" />

### 2.2 Changer le nom de la machine
```
sudo hostnamectl set-hostname SRVLX01
```
<img width="560" height="344" alt="hostnamectl Vérifier si ça fonctionne-1" src="https://github.com/user-attachments/assets/66ee156d-25e6-4ae7-85ba-a406a48f3142" />

Vérifier que le changement est bien pris en compte :
```
hostnamectl
```
Redémarrer pour appliquer le changement :
```
sudo reboot
```

### 2.3 Configurer l'IP fixe

Identifier le nom de la carte réseau et vérifiez :
```
ip a
```
Modifier le fichier de configuration réseau :
```
sudo nano /etc/network/interfaces
```
<img width="786" height="416" alt="systemctl restart networking Enregistre fichier réseau et redémarrer" src="https://github.com/user-attachments/assets/6af9dfe9-ef22-402b-9499-f1f56ad274da" />

Redémarrer le service réseau :
```
sudo systemctl restart networking
```

IP fixe Debian 172.16.50.10

> La commande `ip a` doit afficher l'adresse **172.16.50.10**.

<img width="870" height="396" alt="ip a vérif la configuration" src="https://github.com/user-attachments/assets/612dace3-269c-4245-b489-9e16e98c6f29" />

### 2.4 Installer OpenSSH serveur
```
sudo apt install openssh-server -y
```
<img width="940" height="451" alt="open ssh" src="https://github.com/user-attachments/assets/af9f4bd2-fbd8-40f8-a472-030debe077b1" />

### 2.5 Vérification du service
```
sudo systemctl status ssh
```

<img width="716" height="302" alt="verif ssh" src="https://github.com/user-attachments/assets/357e1346-4c4c-46a9-82ef-376ecf21204f" />

> Le statut doit indiquer **active (running)** en vert.

---

## 3. Installation sur le client Ubuntu CLILIN01

### 3.1 Changer le nom de la machine
```
sudo hostnamectl set-hostname CLILIN01
```
<img width="629" height="133" alt="sudo hostnamectl set-hostname" src="https://github.com/user-attachments/assets/5616eab7-3596-42c8-9d32-4f4537a8644d" />
