---
layout: post
title: "Workflow git svn et git bundle"
date: 2012-04-12 23:00
comments: true
categories: experience
tags:
- git
- svn
- bundle
- workflow
published: true
---

Il y a quelques temps, j'expliquais mon [workflow git-svn](http://blog.isammoc.net/blog/2011/09/25/workflow-git-svn/). J'avais donc mes petites habitudes, tout allait bien. Un jour, le chef vient voir notre petite équipe et désigne deux de mes collègues pour aller chez le client. Le problème survient lorsque l'on connait les restrictions : pas de connexion direct, seul les mails passent et il va falloir faire des modifications en live (ie. chez le client) et bien sûr, on doit rester synchronisé. Heureusement, git est venu à notre secours.

<!--more-->
## Préparation ##

Avant que mes deux collègues ne partent, je leur ai fait un petit topo de ce que je vous présente dans cet article. 

Du côté de leur machine, nous avons cloné mon dépôt git :

```bash
$ git clone git://machine/chemin/de/mon/depot
```

Sur ma machine, j'ai juste taggué la version actuelle de master :

```bash
$ git tag client
```

Et ils étaient parés à affronter le client en toute sérénité.

## Chez le client ##

Lorsque mes collègues avaient des choses à faire... ils les faisaient.
Les seules règles : 

 * faire tout travail dans une branche tiré de master
 * ne jamais merger avec master

```bash
$ git checkout -b fix1 master
hack hack hack
$ git add .
$ git commit
```

Ils pouvaient donc faire plusieurs tâches différentes (dans des branches différentes), et lorsqu'ils avaient fini, ils devaient m'envoyer un bundle regroupant leurs branches locales.

```bash
$ git bundle create projet-date.bundle ^master fix1 fix2 ...
```

Cela crée un fichier `projet-date.bundle` qui contient uniquement les différences entre leur branches et `master` et non l'historique depuis le début du projet, ni les fichiers complets ; uniquement le patch, ce qui allège considérablement la taille du fichier.
Le fichier m'était ensuite transmis par mail. Je leur envoyais en retour un autre bundle contenant les modifications du reste de l'équipe (restant dans nos locaux) ainsi que leur modifications mergées dans master qu'ils intégraient avec :

```bash
$ git fetch projet-date.bundle
```

Ils pouvaient alors supprimer leurs branches s'ils le désiraient.

## Dans nos locaux ##

De mon côté, je continuais à travailler normalement (comprendre avec le [workflow git-svn](http://blog.isammoc.net/blog/2011/09/25/workflow-git-svn/) ) et lorsque je recevais leur bundle :


```bash
$ git bundle verify projet-date.bundle
```

Cela permet de lister les branches contenues dans le bundle et de vérifier qu'il ne manque pas de données pour pouvoir récupérer les commits. Une fois rassuré, je pouvais rapatrier les branches une à une avec :

```bash
$ git fetch projet-date.bundle fix1:monfix1
```

Sachant que SVN gère mal les historiques complexes, je rebasais cette nouvelle branche puis envoyais le résultat sur le serveur central.

```bash
$ git checkout monfix1
$ git rebase master
$ git checkout master
$ git merge monfix1 --ff-only
$ git svn rebase
$ git svn dcommit
```

Et de même pour toutes les branches fournies dans le bundle.

Une fois le serveur à jour avec les dernières modifications, j'empaquetais le dernier état de `master` dans un bundle :
 
```bash
$ git bundle create projet-date.bundle ^client master
$ git tag -f client
```

Le fichier créé comporte donc les différences entre le tag `client` et le `master` actuel. Le tag `client` est réactualisé de force pour la prochaine itération.

Je leur transmettais le nouveau bundle par mail pour qu'ils puissent tester (et corriger si besoin) directement avec l'environnement du client.

## Conclusion ##

Malgré la contrainte de devoir utiliser SVN comme serveur central de référence et la difficulté de ne pouvoir se contacter que par mails,
nous nous en sommes sortis grâce à git qui nous a évité les conflits par patches ou les diff à rallonge.
Ce ne fut pas forcément très simple, mais avec les quelques commandes présentées ci-dessus, nous avons pu continuer à travailler le plus proprement possible malgré les conditions.
