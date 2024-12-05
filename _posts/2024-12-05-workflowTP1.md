---
layout: post
title: TP1 Prise en main de la plateforme Camuda
subtitle: Premier TP
tags: [BPMN, Workflow, BPM, Microservices, Java, Software Engineering]
author: Mariem ZAOUALI
---

# TP1 : Prise en main de la plateforme Camuda
> 📔 Objectif
> 
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
## Création du compte
Accédez à Camunda SaaS sur : https://accounts.cloud.camunda.io/signup
![image](https://github.com/user-attachments/assets/dbb61109-aa91-48f9-9dab-7066ec78ed22)

Vous pouvez soit remplir le formulaire et le soumettre, soit vous connecter en utilisant votre compte Google ou GitHub existant.

-   Si vous avez créé un compte en remplissant le formulaire, vous receverez un email de confirmation. Cliquez sur le lien inclus dans le message reçu pour vérifier votre adresse e-mail et définir un mot de passe.
-   Si vous avez créé un compte en utilisant Google ou GitHub, vous serez automatiquement redirigé vers le console Camunda
-   Si vous remplissez le formulaire, vous receverez un e-mail de confirmation. Cliquez sur le lien pour vérifier votre adresse e-mail et définir votre mot de passe.


![image](https://github.com/user-attachments/assets/98825d31-5c3a-4bc4-94e0-c75cd19902ab)

Après la connexion, vous verrez la page de présentation de le console Camunda. Celui-ci donne accès à la gestion des clusters, diagrammes et formulaires que vous déployerez sur Camunda.

![image](https://github.com/user-attachments/assets/413ea0dc-05c0-4203-81aa-7c1401554af5)

## Création du projet
Créez un nouveau projet en suivant les étapes ci-dessous :
Cliquez sur Ignorer le didacticiel. Concevoir un processus dans le lien Modeler depuis le panneau de la console

![image](https://github.com/user-attachments/assets/ecfe78a5-451f-438b-a337-09d1b4f836eb)
Depuis le centre de l'écran, cliquez sur le bouton Créer un nouveau projet pour créer un nouveau projet.

![image](https://github.com/user-attachments/assets/676f2a5d-dd31-4d1f-b07c-0fb2ab04db19)
Une zone de texte apparaîtra dans la barre de menu dans laquelle vous devrez saisir un nom de projet. Pour ce cours, nous utiliserons "Sou9Metmen".
![image](https://github.com/user-attachments/assets/641de074-bccd-4637-92c2-66b631d2fe6b)

### Créer un processus métier
Depuis le projet Sou9Metmen dans le Modeler, cliquez sur le bouton Nouveau puis sur Diagramme BPMN dans le menu qui apparaît. Le modèle à réaliser est inspiré du papier de recherche *Towards integrating BPMN 2.0 with CMMN and DMN standards for flexible business process modeling*.

![image](https://github.com/user-attachments/assets/04b34b6c-dda8-44b6-9f92-7ccd2fb75f4d)

![image](https://github.com/user-attachments/assets/ac9a6bba-a288-4f32-90a9-6f01b00c1947)

### Ajout des évènements
Dans la mesure du possible, nommez un événement en utilisant un objet et un verbe reflétant un état. Essayez toujours de décrire dans quel état se trouve un objet lorsque le processus est sur le point de quitter l’événement.
Commencez par créer les évènements de notre processus. Les cercles en gras sont les évènements de fin alors que les cercles fins sont les évènements de début.

> ⚠️ *Notez bien*:
>  Ajoutez aussi deux évènements de fin : Email envoyé, Rappel envoyé.

![image](https://github.com/user-attachments/assets/6fbf13b3-fae1-4ce0-a342-acf430bd8805)

### Ajout des tâches
Nous allons créer plusieurs tâches pour modéliser notre processus de demande d'assurance automobile. Nous utiliserons les tâches de règles métier, les tâches de service, les tâches utilisateur et les tâches d'envoi. Les figures montrent les étapes d’ajout d’une tâche. Vous suivrez la même démarche pour créer toutes les tâches demandées dans la dernière figure de cette section.
![image](https://github.com/user-attachments/assets/e28e7aa7-23a1-4aa4-aaa6-636efeaab4e7)

![image](https://github.com/user-attachments/assets/085a3ddb-cd57-44de-9b98-677411d23ac6)

![image](https://github.com/user-attachments/assets/e0d13785-c6a2-4851-8b45-47f807869c9d)

Votre diagramme devrait ressembler à celui ci-dessous lorsque vous avez terminé.

![image](https://github.com/user-attachments/assets/098e8c4f-f978-47d8-b93e-45d82137d61c)

 #### Boundary event

Nous allons maintenant ajouter un événement de limite de minuterie pour gérer un retard dans la tâche "Accélérer la vérification de la demande". Cliquez sur la limite inférieure à droite de la tâche "Accélérer la vérification de la demande" et choisir l’évenement "timer boundary event". Nommez-le 2 jours.

### Ajouter une passerelle exclusive
Nous devons maintenant connecter les éléments qui ont été ajoutés au processus afin qu'ils puissent être exécutés.

![image](https://github.com/user-attachments/assets/c4877878-96e7-45dc-ba74-e340af20ddbe)

![image](https://github.com/user-attachments/assets/5bbf1138-d411-4a5a-a709-d8f33d53621e)

Votre diagramme devrait ressembler à celui ci-dessous lorsque vous avez terminé.
![image](https://github.com/user-attachments/assets/73a225e2-306d-47de-8702-e1447076545a)


### Ajouter annotation
Créez une nouvelle annotation en suivant les étapes ci-dessous :

![image](https://github.com/user-attachments/assets/80f2c296-67c6-4092-b6d7-fab875e2cb5d)
![image](https://github.com/user-attachments/assets/349e2e51-8262-4448-a745-cd3c74615902)

### Ajouter un commentaire
Créez un nouveau commentaire en suivant les étapes ci-dessous :

> ⚠️ *Notez bien*:
> Les commentaires ne font PAS partie de la spécification BPMN. Les commentaires sont une fonctionnalité de Camunda
> et ne font donc pas partie de la définition du processus ; les commentaires ne seront pas inclus si vous
> téléchargez le processus sous forme de fichier XML BPMN 2.0.

![image](https://github.com/user-attachments/assets/21201e86-1d25-40a1-9f32-dff2a1e0dbf9)

### Ajouter milestones
Créez un nouveau jalon (milestone) en suivant les étapes ci-dessous :
![image](https://github.com/user-attachments/assets/ce4825ee-caaa-47e4-a04d-6df7c9c94e25)
![image](https://github.com/user-attachments/assets/6330da34-480d-477d-9fb6-5aeccf3c326e)
![image](https://github.com/user-attachments/assets/0c08c72f-2346-42a0-b078-656318c5fdc6)
![image](https://github.com/user-attachments/assets/5dedf868-a7cc-483f-a997-500a8762b663)
![image](https://github.com/user-attachments/assets/09d35641-ffa7-4d9f-b62c-11a317c0b6f4)
Nous allons maintenant comparer la version actuelle de la définition du processus avec le jalon précédemment enregistré.
![image](https://github.com/user-attachments/assets/bc8e02a9-c99e-40d8-afa9-ecb51dcb5b99)
Vous pouvez restaurer la version qui vous convient comme suit.
![image](https://github.com/user-attachments/assets/91b0d900-437b-4489-b9ff-67290d7d5e5f)

### Simuler le processus
Assurez-vous que vous êtes dans l'onglet Conception dans le coin supérieur gauche de l'écran.
Vous pouvez valider votre processus en suivant les étapes ci-dessous :
-  Cliquez sur le bouton **Token Simulator** dans le coin supérieur droit de l'écran.
-  Cliquez sur le bouton **Jouer** qui est maintenant apparu sur l'événement de démarrage pour simuler une nouvelle instance de processus par rapport au processus modélisé.
-  Le simulateur de jetons démarrera une instance de processus qui suivra l'itinéraire par défaut tout au long du processus ; cela se terminera lorsque la demande sera approuvée.
- 
Vous pouvez changer le flux pour tester une autre branche du processus

![image](https://github.com/user-attachments/assets/111cdfbd-0978-40c9-9762-2e906c11a566)














