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
   - 5.2 [Copier clé vers CLILI01](#52-copier-clé-vers-clili01)
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

## 3.2 Configurer l'IP fixe

Sur Ubuntu, la configuration de l'IP fixe peut se faire via l'interface graphique.

Aller dans **Paramètres**, **Réseau** cliquer sur la roue cranté de la carte réseau.

Dans l'onglet **IPv4** :
- Passer le mode de **Automatique (DHCP)** à **Manuel**
- Renseigner les champs suivants
- 
<img width="852" height="608" alt="config reseau perm" src="https://github.com/user-attachments/assets/7a787f9c-cc65-4c73-afdb-610c5205185d" />


| Champ | Valeur |
|---|---|  
| Adresse | 172.16.50.30 |
| Masque de sous-réseau | 255.255.255.0 |
| DNS | 8.8.8.8 |


Cliquer sur **Appliquer**, puis désactiver et réactiver la connexion réseau pour que les changements prennent effet.

IP fixe Ubuntu 172.16.50.30

> La commande `ip a` doit afficher l'adresse **172.16.50.30**.

<img width="1150" height="498" alt="ip a Verif" src="https://github.com/user-attachments/assets/3e08f1aa-76b8-42cb-8bfc-d4dca54594dc" />

### 3.3 Installer OpenSSH
```
sudo apt update && sudo apt install openssh-server -y
```
<img width="738" height="152" alt="sudo apt ubuntu" src="https://github.com/user-attachments/assets/9fe1b3dd-9979-4b49-9967-ae09f937bfd9" />


 activer le service SSH :

<img width="1122" height="539" alt="systemctl status" src="https://github.com/user-attachments/assets/ef35ac6b-304b-4db9-a70e-d578188fb8b9" />

 ```
 sudo systemctl start ssh
 sudo systemctl enable ssh
 sudo systemctl status ssh
 ```
 > Le statut doit indiquer **active (running)** en vert.

 ### 3.4 Configuration du pare-feu

 ```
 sudo ufw allow
 sudo ufw enable
 sudo ufw status
 ```
 > Résultat attendu : `22/tcp ALLOW`
 
 ---

 ## 4. Vérification de la connexion réseau

Depuis **SRVLX01**, vérifier que la communication avec CLILIN01 fonctionne :
```
ping 172.16.50.30
```
<img width="542" height="371" alt="ping" src="https://github.com/user-attachments/assets/74c60193-5034-44ae-b40f-82cbaf495834" />

> Résultat attendu **0% packet loss** - les machines se voient correctement sur le réseau.

---

## 5. Connexion SSH sans mot de passe

> Une clé SSH fonctionne comme un tunnel sécurisé entre deux ordinateurs elle permet de se connecter sans mot de passe.

## 5.1 Générer une clé SSH

Depuis **SRVLX01** :

ssh-keygen -t ed22519 -C "root@172.16.50.10"

<img width="593" height="358" alt="clé SSH debian" src="https://github.com/user-attachments/assets/2e3a4fc5-2b4b-4093-a1bd-07b00f764c88" />

 > Appuyez **Entrée** pour valider par défaut.

 ### 5.2 Copier clé vers CLILI01

ssh-copy-id `wilder@172.16.50.30`
ou
ssh-copy-id -i ~/.ssh/id_ed22519.pub `wilder@172.16.50.30`

<img width="933" height="270" alt="ssh-copy-id" src="https://github.com/user-attachments/assets/62295ea9-8e6a-433e-baa3-09de9e90ed8e" />

>  Le mot de passe de passe de `wilder` sera demandé une dernière fois : `Azerty1*`

### 5.3 Tester la connexion 

`ssh wilder@172.16.50.30`

<img width="722" height="245" alt="connexion établi" src="https://github.com/user-attachments/assets/3ae3cacb-181e-49d9-81fb-48e14d7c55fe" />

> connexion sans demander de **mot de passe**
