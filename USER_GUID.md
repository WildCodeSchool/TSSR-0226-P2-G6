# USER_GUID.md

## Sommaire

1. [Prérequis](#1-prérequis)
2. [Lancement du script](#2-lancement-du-script)
3. [Saisir la machine cible](#3-saisir-la-machine-cible)
4. [Menu principal](#4-menu-principal)
5. [Gérer la machine](#5-gérer-la-machine)
6. [Gérer les utilisateurs](#6-gérer-les-utilisateurs)
7. [Quitter le script](#7-quitter-le-script)

---

## 1. Prérequis 

Avant de lancer le script, vérifier :

| Prérequis | Commande de vérif |
|-----------|-------------------|
| CLILIN01 doit etre allumée | `ping 172.16.50.30` |
| SSH est actif sur CLILIN01 | `sudo systemctl status ssh` |
| La clé SSH est configuré | `ssh wilder@172.16.50.30` |

> Si la clé SSH n'est pas confu=iguée, regarder a l'**INSTALL.md**.

> Si l'arrêt ou le redémarrage demande un mot de passe, exécuter sur **CLILIN01** :
`sudo visudo`
<img width="790" height="116" alt="wilder sudo vusio" src="https://github.com/user-attachments/assets/60ed7100-3db4-490d-a1bd-f5d192c985e2" />

> Ajouter la ligne suivante à la fin du fichier :
<img width="804" height="586" alt="config wilder sans mdp" src="https://github.com/user-attachments/assets/ab0c760d-c4be-4ecb-ace2-709782ce0ae6" />

> wilder ALL=(ALL) NOPASSWD: /sbin/shutdown, /sbin/reboot
---

## 2. Lancement du script 

Se connecter sur **SRVLX01** puis taper :

```
cd TSSR-O226-P2-G6/
./script.sh
```

---

## 3. Saisir la machine cible

Au lancement, le script demande l'IP ou le nom de la machine à administrer :

<img width="587" height="149" alt="SRVLX01 OUTIL" src="https://github.com/user-attachments/assets/07f653ea-cd92-4789-9098-9f614f11376b" />

Si la machine est joignable :


<img width="572" height="190" alt="Connexion etablie" src="https://github.com/user-attachments/assets/b138d3e7-fcbe-459d-a819-524dc3937842" />
 
 Connexion établie !
 
 > La machine cible disponible est **CLILIN01** à l'adresse `172.16.50.30`

 ---

 ## 4. Menu principal 

<img width="667" height="181" alt="Menu principale" src="https://github.com/user-attachments/assets/66a45c3a-400c-4443-95f2-0f45cee3ace2" />

 ```
 1. Gerer la machine 
 2. Gerer les utilisateurs
 3. Quitter

 Votre choix :
 ```

 > Taper le **numéro** du choix souhaité puis appuyer sur **Entrée**.

 ---

 ## 5. Gérer la machine 

 Deouis le menu principal, choisir `1`. Le sous-menu affiche :

<img width="748" height="273" alt="Menu principale choix 1" src="https://github.com/user-attachments/assets/8aec17d5-44ee-4771-a39b-d9e44f676434" />

---

| Option | Action | Résultat |
|--------|--------|----------|
| 1 | Arreter la machine | CLILIN01 s'éteint |
| 2 | Redémarrer la machine | CLILIN01 redémarre |
| 3 | Voir la version de l'OS | Affiche le nom et la version du système |
| 4 | Voir l'adresse IP | Afffiche l'IP de CLILIN01 |
| 5 | Retour | Retour au menu principal |

## 6. Gérer les utilisateurs
| Option | Action | Résultat |
|--------|--------|----------|
| 1 | Creer un utilisateur | utilisateur crée |
| 2 | Supprimer un utilisateur | utilisateur supprimé |
| 3 | Modifier le mot de passe | mdp modifié |
| 4 | Voir la dernier connexion | Affiche dernière connexion |
| 5 | Voir le dernier mot de passe | Affiche le dernier mdp |
| 6 | Retour au menu principal | Votre choix : |

<img width="329" height="158" alt="gestion user" src="https://github.com/user-attachments/assets/e42a6604-7c1f-435b-a06f-b2a595936e30" />
