---
layout: post
title: TP1 Prise en main de la plateforme Camuda
subtitle: Premier TP
tags: [BPMN, Workflow, BPM, Microservices, Java, Software Engineering]
author: Mariem ZAOUALI
---

# TP1 : Prise en main de la plateforme Camuda
> 📔 Objectif
>Ce TP vous fournira une brève introduction aux processus de modélisation à l'aide de Camunda. Vous configurerez un >processus simple de demande d’assurance automobile afin de comprendre les principales fonctionnalités disponibles dans >le modélisateur.

## Besoin fonctionnel
La compagnie d'assurance «Sou9Metmen» (où bien "driveConfident") souhaite introduire l'automatisation des processus dans toute son organisation. Le premier processus qu’ils aimeraient automatiser est le processus de demande d’assurance automobile. 
Un analyste commercial de «Sou9Metmen» qui connaît déjà BPMN, s'est porté volontaire pour rechercher les capacités de modélisation de processus de Camunda en utilisant une version simplifiée du processus de demande d'assurance automobile.
<p align="center">
  <img src="https://github.com/user-attachments/assets/21b8a821-a3ec-4d68-af6c-83c7e160c96f" alt="logo de l'entreprise"/>
</p>

## Product Backlog 
### User stories
L'entreprise suivra la méthodologie de gestion de projet "Scrum" pour la mise en place de l'automatisation de ce processus métier. Ainsi, l'analyste commercial a défini un ensemble de tâches sous forme de user stories:
-  En tant qu'analyste commercial à «Sou9Metmen», je souhaite modéliser une version simplifiée du processus de demande d'assurance automobile afin de comprendre les capacités de modélisation de processus de Camunda.
-  En tant qu'analyste commercial à «Sou9Metmen», je souhaite ajouter des commentaires et des annotations supplémentaires à un processus pour que je comprenne comment collaborer avec d'autres Business Analysts.
-   En tant qu'analyste commercial à «Sou9Metmen», je souhaite marquer les versions importantes de mon processus pour que les autres Business Analysts puissent voir l'historique du processus.
-   En tant qu'analyste commercial à «Sou9Metmen», je souhaite valider un processus que j'ai modélisé pour que j'aie la certitude qu'il est correct avant de le partager avec des collègues.

### Critères d'acceptation
Nous adopterons une approche Minimum Viable Product (MVP) pour modéliser un processus utilisant Camunda qui répond à ces exigences User stories, comme indiqué dans la Figure 1.
<figure>
<p align="center">
  <img src="https://github.com/user-attachments/assets/7813a522-f674-4e8e-8883-603fb5d0d26c" />
  <figcaption>Figure 1 : MVP est le produit qui peut attirer des consommateurs mêmes dans ses plus premières étapes de réalisation</figcaption>
</p>
</figure>

Les critères d’acceptation initiaux sur lesquels nous travaillerons sont :
-  Le Business Analyst de «Sou9Metmen»  est capable de modéliser un processus en utilisant BPMN.
-  Le Business Analyst de «Sou9Metmen» est en mesure d'ajouter des commentaires à un processus pour une révision ultérieure.
-  Le Business Analyst de «Sou9Metmen» est capable de baliser les versions importantes dans le développement d'un processus.
-   Le Business Analyst de «Sou9Metmen» est capable de valider que le processus modélisé est correct.


