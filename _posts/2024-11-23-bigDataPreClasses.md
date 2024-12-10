---
layout: post
title: PreClasses
subtitle: Instructions d'exécution sur docker-compose
tags: [Big Data, Docker-compose]
author: Mariem ZAOUALI
---

# Travailler le lab avec docker et docker compose

Pour pouvoir réaliser les labs de big data, vous pouvez toujours vous servir de vos machines sur Azure Lab Services (disponibles du Dimanche après-midi au Jeudi Soir) ou bien travailler sur votre machine en local en se servant d'une image iso Ubtuntu.

# Configurer la machine 
## Installer docker et docker-compose
Je recommande ce tutorial pour installer docker:
```link
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04
```
Et je recommande ce tutorial pour installer docker-compose:
```link
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04
```
## Téléchargement du dossier du lab
Si vous allez travailler sur une machine en local, vous devez télécharger ce fichier compressé:
```link
https://drive.google.com/file/d/1ylYVu1Q0PBY6LxTM7yvH9DHBw1QFnft1/view?usp=sharing
```

# Lancer le network
Placez-vous dans le répertoire du lab où se trouve le fichier **docker-compose.yml**.
Tapez :
```cmd
docker-compose up -d
```
![image](https://github.com/user-attachments/assets/787734b2-a210-4c37-8f74-006937ff937f)

Pour arrêter le réseau des containers lancés, vous devez taper:
```cmd
docker-compose down
```
---
<div class="alert alert-warning">
  <div class="alert-header">
    <i class="fas fa-exclamation-triangle"></i> Avertissement
  </div>
  <div class="alert-body">
    Si vous avez déjà lancé docker-compose durant la séance précédente du tp, une erreur indiquant l'existance d'un certain network qui utilise la même plage d'adresses sera affichée. Pour résoudre ce problème, il faut supprimer tous les containers qui ont une relation avec ce network puis l'effacer lui-même.
  </div>
</div>
---
Voici comment vous devez procéder. Dans un terminal, lancez cette commande pour effacer tous les containers qui sont sur votre machine:
```cmd
docker rm -f $(docker ps -aq)
```
Vérifiez le nom du network que vous voulez supprimer en tapant:
```cmd
docker network ls
```
enfin, lancez par exemple:
```cmd
docker network rm enit_lab3_hive_hadoop_net
```
étant **enit_lab3_hive_hadoop_net** le nom du network à supprimer.
