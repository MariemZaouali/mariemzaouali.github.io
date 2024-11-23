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

![image](https://github.com/user-attachments/assets/c6e93314-df30-43c2-8663-088195335d8e)
Pour arrêter le réseau des containers lancés, vous devez taper:
```cmd
docker-compose down
```
