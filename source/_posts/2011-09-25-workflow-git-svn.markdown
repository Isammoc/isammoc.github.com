---
layout: post
title: "Workflow git-svn"
description: "Git en tant que client SVN"
comments: true
categories: experience
tags:
- git
- svn
- workflow
published: true
---

Dans mon entreprise actuelle, git n'est pas encore réellement utilisé. Déjà qu'il y a à peine un an, c'est CVS qui primait, il ne faut pas trop demander. Actuellement, donc, notre gestionnaire de sources officiel est SVN. Mais comme le serveur central n'est pas dans l'agence dans laquelle je travaille, cela se révèle pénible à chaque rafraichissement ou à chaque visionnage de l'historique (Environ 10 minutes chrono pour voir l'historique d'un fichier). N'en pouvant plus, et ayant récemment découvert le bonheur d'utilisation de git, je me suis décidé à l'utiliser en tant que client SVN puisque cela est possible grâce à git-svn.

<!--more-->

## Importer la base ##

La première chose à faire est donc de charger la base SVN en local avec la commande :

{% codeblock lang:bash %}
$ git svn clone -s http://repo.svn/repertoirePrincipal mondepot
{% endcodeblock %}

Ce qui va créer un dépot git dans le répertoire local `mondepot`

`-s` permet de dire à git-svn que le dépôt suit les conventions standards pour les répertoires `trunk/tags/branches`.

Pour moi, cela a pris *énormément* de temps, dans les 36 heures. Mais c'est parce que le dépôt SVN est conséquent : 3 ans de développement pour un workspace pesant dans les 2 Gio et il y a toujours le problème du serveur distant et de la faible connexion.

## Travailler ##

A partir du moment où j'ai récupéré la base, les choses se sont tout de suite améliorées. Je pouvais donc avoir les logs, les différentes versions d'un fichier en quelques secondes plutôt qu'en quelques minutes, et cela m'a changé la vie.

J'ai également profité pleinement des branches : ma branche `master` étant reliée à la `trunk` d'SVN, je me mettais sur une autre branche pour travailler tout en synchronisant régulièrement ma branche principale.

Exemple pour ma super fonctionnalité (en partant de `master`):

{% codeblock lang:bash %}
$ git svn rebase
{% endcodeblock %}

Pour me mettre à jour par rapport à SVN.

{% codeblock lang:bash %}
$ git checkout -b super_fonctionnalité
{% endcodeblock %}

Pour créer et travailler dans la nouvelle branche `super_fonctionnalité`.
Et là, je peux modifier des fichiers, commiter, re-modifier des fichiers, recommiter, etc.

{% codeblock lang:bash %}
$ ... (modification de code)
$ git add .
$ git commit
$ ... (autant de fois que nécessaire)
{% endcodeblock %}

Lorsque je sais que d'autres ont fait des choses, je peux me synchroniser :

{% codeblock lang:bash %}
$ git checkout master
$ git svn rebase
$ git checkout super_fonctionnalité
$ git rebase master
{% endcodeblock %}

En détail :

* Je me replace dans la branche `master`
* Je rafraichis le dépôt par rapport à SVN
* Je me remets dans la branche `super_fonctionnalité`
* Je rejoue mes modifications après celle du SVN

Le dernier `rebase` est nécessaire, car git gère très bien les merge, mais SVN beaucoup moins. Du coup, il vaut mieux que l'historique soit plutôt linéaire pour éviter les problèmes lors de la remontée sur le serveur SVN.

A ce moment, je peux continuer à coder ma super fonctionnalité en sachant que j'ai les modifications des collègues (grâce au `rebase`).
Lorsque j'ai fini ma super fonctionnalité, il me reste à l'envoyer sur le serveur SVN :

{% codeblock lang:bash %}
$ git checkout master
$ git merge --ff-only super_fonctionnalité
$ git branch -d super_fonctionnalité
$ git svn rebase && git svn dcommit
{% endcodeblock %}

Ce qui donne en détail :

* Je me replace dans la branche `master`
* Je récupère les modifications de ma super fonctionnalité dans la branche courante
* Je supprime ma branche `super_fonctionnalité`
* Je me remets à jour avec le dépôt SVN et j'envoie sur le serveur SVN mes commits git

Oui, oui, pour chaque commit git, il y aura un commit SVN, d'où l'intérêt de pouvoir faire des squash si nécessaire *AVANT* l'envoi sur le serveur distant.

## Chez le client ##

Là où git prend tout son sens, c'est avec des serveurs multiples. Je vais donc vous expliquer ce que j'ai utilisé lorsque nous sommes allés en intégration chez le client.

Nous devions aller chez le client pour une phase d'intégration (comprendre finir les développements et faire les modifications de dernière minute que le client demande). Mais dans les locaux du client, nous n'avons pas accès à notre serveur SVN, et pour partager nos développements entre les trois collègues, j'ai tout naturellement mis un dépôt git nu (--bare) dans un répertoire partagé et le tour est joué.

Du coup, lorsque nous avons ramené nos machines dans nos locaux, nous avons pu mettre à jour le serveur SVN avec des commits séparés pour chaque développement. Avouez que c'est mieux qu'un gros commit avec toutes les modifications que l'on a faites pendant les deux semaines qu'a duré l'intégration. (Dans mon exemple, c'étaient 80 commits à remonter sur le serveur SVN).

## Conclusion ##

Malgré devoir faire attention à la linéarité de l'historique, j'ai fait ce petit constat :

* moi content, parce que j'utilise git au boulot et que j'ai amené les collègues à l'utiliser également;
* les collègues intéressés car on a pu partager nos développements sans les soucis de merger manuellement des fichiers par clefs USB;
* et la qualité contente, car les commits sont séparés sur le SCM.

Le retour a été plus que satisfaisant sur toute la ligne.

A qui le tour ?
