---
layout: post
title: "London Epidemic - introduction"
date: 2012-03-27 21:31
comments: true
categories: projet
---

Suite à ma visite sur le site [1 Month Game](http://www.1monthgame.com/blog/), je me suis dit que j'allais faire des articles pour faire vivre mon petit blog à l'abandon et pour me motiver à avancer dans la création d'un jeu.

<!--more-->

## But du jeu ##

Le sujet de ce jeu est d'incarner une maladie et d'envahir Londres. A la base, c'est un jeu qui se joue sur table avec des vrais gens autour de la vraie table.

On contamine un quartier, des malades apparaissent qui vont aller contaminer un autre quartier, afin de contaminer le plus de quartiers possible avant les autres joueurs.

On peut trouver les règles originales à cet endroit : <http://globalgamejam.org/2011/london-epidemic>.  Le site est en anglais, mais les règles en français sont également fournies.

## Mon but ##

Mon but est d'en faire une version par navigateur en temps réel (ou au moins semi-réel) et de réussir à finir ce projet.
J'ai beau avoir commencer des dizaines de projets personnels, je n'en ai pas amené un réellement jusqu'au bout.

C'est décidé, celui-là sera le bon.

## Comment ? ##

 * [Grails](http://grails.org) Parce que je suis feignant et que même si je veux le finir, je veux d'abord qu'il soit fonctionnel rapidement, j'ai choisi ce framework : il a l'avantage indéniable que je sais un minimum l'utiliser, et qu'il est parfait pour faire rapidement une application web.
 * [jQuery](http://www.jquery.com) car je ne connais pas grand chose à javascript, et ce framework me parait le plus abordable et suffisament connu pour trouver de l'aide si besoin (et il y a plein de plugins).
 * [SVG](http://www.w3.org/Graphics/SVG/) qui me parait le format d'image manipulable par excellence; puisqu'en XML, il fait partie du DOM et est donc accessible à jQuery. De plus, c'est un format vectoriel, donc adaptable aussi bien sur grand écran que sur téléphone portable.

## État actuel ##

Pour l'heure, une série de fonctionnalités est déjà en place, mais aucune n'est réellement finalisée. (Je rappelle que mon premier but est que ce soit fonctionnel !)

Voici les fonctionnalités en questions : 

 * Inscription
 * Connexion
 * Déconnexion
 * Ajout d'une nouvelle partie
 * Liste des parties en attente de joueurs
 * Vue de la liste des joueurs en attente pour cette partie
 * Choix de la maladie à incarner
 * Affichage de la carte avec les marqueurs à l'emplacement des foyers des maladies.

La prochaine étape : lister l'ordre de jeu des joueurs et de permettre au premier joueur de choisir une action.
