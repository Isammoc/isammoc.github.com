---
layout: post
title: "Document de conception de jeu [Traduction]"
date: 2012-05-17 17:29
comments: true
categories: projet
---

Comme je l'ai dit dans mon dernier article, je vous présente ma traduction du document de conception d'un jeu vidéo selon Tom Sloper's

<!--more-->

|  Tom Sloper http://www.gamedev.net/page/resources/_/creative/game-design/tom-slopers-format-for-game-design-specifi-r243 Format for Game Design Specifications

<h2>Titre du jeu</h2>

Les objectifs principaux d'une conception de jeu sont de (1) suciter l'intérêt et (2) d'informer le lecteur. Le premier paragraphe doit intéresser le lecteur et faire en sorte que le lecteur veuille lire le document complet. Lorsqu'il a fini de lire le document de conception complet, si le lecteur n'a pas une compréhension claire de ce que vous voulez que le jeu devienne, vous avez échoué à communique votre vision du jeu.

<h3>I. Informations générales</h3>

<ul>
<li>Décrivez brièvement le jeu. Le premier paragraphe doit conserver l'intérêt du lecteur en créant une image mentale de l'intérêt du jeu.</li>
<li>Survol un peu plus détaillé. A travers des illustrations et des schémas, guidez le lecteur à travers les points principaux du gameplay, en vous concentrant sur les points importants qui ont besoin d'être communiqués. Dans le cas d'un jeu "Shangai", les aspects importants peuvent être les différents modes de jeu et les nouvelles fonctionnalités de ce jeu. Après que le lecteur ait parcouru les 2-3 premières pages, il devrait avoir une idée claire de ce à quoi le jeu ressemble, quelle est le point de vue et à quel point il serait amusant de jouer à ce jeu.</li>
</ul>

<h3>II. Description détaillée</h3>

<ul>
<dl>
<dt>Concept de base</dt><dd>Quel est le grand concept du jeu ?</dd>
<dt>Contexte (Background)</dt><dd>Si possible, racontez l'histoire du monde qui conduit au début du jeu et racontez les dénouements durant le jeu, s'il y en a (dans le cas d'un jeu de réflexion comme Shangai, par exemple, cela ne sera probablement pas nécessaire; mais cela le sera probablement dans un jeu comme Alien vs Predator) Quel est le ton ? Quelle est la base narrative ? Quelle est le coeur de l'histoire ? Est-ce une histoire linéaire ?</dd>
<dt>Objectif</dt><dd>Décrivez l'objectif du jeu. Si l'objectif est simplement "Avoir le plus de points possible" alors faites le savoir. Mais si l'objectif est "sauver la princesse", c'est une autre histoire. Dans chaque cas, donnez autant de détails que possible pour aider le lecteur à avoir les bases pour comprendre le reste du document de conception pendant qu'il le lit. Quel est le but des joueurs et pourquoi veulent-ils l'accomplir ?</dd>
<dt>Gameplay</dt><dd>Décrivez la manière dont le jeu fonctionne, du début à la fin. Après le démarrage de la console (où le lancement du jeu sous PCà, y a-t-il un écran de titre ? à quoi ressemble-t-il ? Est-ce qu'il y a un écran de paramétrage ? Quels sont les choix ? Y a-t-il une séquence d'introduction ? Peut-on la passer et comment ?... Puis, lorsque le jeu commence, nous voyons notre héros apparaître dans un lieu. Décrivez le lieu et ce qui arrive ensuite. Si rien n'arrive avant l'action de l'utilisateur, décrivez les options disponibles et ce qui arrive en résultat de chaque action. Gardez en tête que la plupart des jeux sont, jusqu'à un certain point, controllés par l'utilisateur. Le héros ne fait rien automatiquement; l'utilisateur, lorsqu'il joue au mieux, doit faire faire au héros telle ou telle action, qui ferait faire à l'ennemi controllé par ordinateur telle réponse, et les options de l'utilisateur serait alors de faire X ou Y... Décrivez l'IA des opposants, s'il y en a. C'est quelque fois utile d'écrire une solution complète (walkthrough) du jeu pour améliorer encore plus la capacité du lecteur à visualiser le jeu. Quelle est l'interface prévue ? Quelle est la perspective prévue (1ère personne ou 3e personne) ? Quelle est la structure interactive de base ? (ie Chapitre ou Section/Sous-section, découpage par niveaux, etc.) Quel est le coeur du gameplay ? (ie la vitesse, les actions, le stule, le temps réel, le tour par tour, etc.) ? Comment fonctionne le mode multi-joueur ? Quelle est la difficulté du jeu ? Combien de temps cela prendra à un joueur moyen pour le finir ?</dd>
</dl>

<h3>III. Autres aspects de la conception produit</h3>

<dl>
<dt>Personnages</dt><dd>Lister et décrivez les personnages du jeu, s'il y en a. Parlez de leur personnalités et de leur compétences, et de la façon dont ils agissent en jeu. Le(s)quel(s) le joueur joue-t-il ? Solo / multi-joueur ? Y a-t-il d'autres personnages clés ?</dd>
<dt>Licence d'exploitation</dt><dd>Si les personnages sont basés sur une licence (comme dans Alien vs Predator), fournissez les indices d'utilisation des possibilités de la licence. Comment le jeu s'insérera-t-il dans le monde de la licence ?</dd>
<dt>Monde</dt><dd>Décrivez le(s) lieu(x) dans le(s)quel(s) l'action se joue, si applicable. Dans le cas d'un jeu d'aventure (comme Leather Goddesses of Phobos 2), le document de conception doit probablement être organisé par lieu, montrant tous les personnages et tous les objets du lieu, et indiquer quels évènements s'y passe. Si les lieux peuvent être visités dans différents ordres, listez les soit dans l'ordre optimum, soit dans l'ordre d'accès le plus simple à visiter.</dd>
<dt>Commandes</dt><dd>Décrivez l'interface utilisateur. Comment le joueur fait-il en sorte que toutes les actions du jeu arrivent ? Dans le cas d'un jeu console, décrivez l'utilisation des boutons de la manette. Dans le cas d'un jeu sur ordinateur, décrivez quels périphériques le jeu supporte et comment ils sont utilisés pour accomplir toutes les actions du jeu. Décrivez l'afficage à l'écran (s'il y a un score et une jauge de vie... s'il y a une icône d'inventaire ou les choix dans les boites de dialogue) et ce que font les éléments. Décrivez tous les menus en détail et mettez en avant leur arborescence. Les messages tectuels à l'écran font également partie de l'interface; si vous ne pouvez décrire tous les textes dans ce document, décrivez au moins à quoi ils ressembleront dans les grandes lignes.</dd>
<dt>Graphismes</dt><dd>Décrivez le style graphique général. Dans le cas d'un jeu avec plusieurs modes graphiques, dites celui qui va être tuilisé. S'il existe d'autres jeux ou produits auxquels le lecteur peut se référer pour une impression du style graphique, c'est une bonne idée de les mentionner. C'est encore mieux d'inclure des croquis de certaines scènes pour aider le lecteur à visualiser le jeu. Montrez une scène typique et donnez des indications sur ce que cela représente. Les croquis devraient inclure une représentation de ce à quoi les personnages (s'il y en a) ressembleront. Montrez ce à quoi ressemblera l'interface graphique et légendez vos croquis pour que le lecteur sache quoi est quoi. La liste des graphismes détaillés sera dans un document séparé (pas une partie de ce document).</dd>
<dt>Sons et musique</dt><dd>Décivez au moins de manière générale l'utilisation des effets sonores dans le jeu. Chaque action du jeu devrait être accompagné d'un son, et les sons devraient être priorisés afin que les sons de moindre importance n'étouffent pas les sons importants. Décrivez comment les sons vont être créés. Si des effets ou des voix générés vont être utilisés dans le jeu, parlez en en détail. Décrivez le style général de musique, avec quelques références à des musiques bien connues du lecteur. Dites comment la musique sera utilisée dans le jeu. Les listes détailles de sons et musiques ne doivent pas apparaître dans ce document.</dd>
</dl>

# Sources
 * [Article original](http://www.gamedev.net/page/resources/_/creative/game-design/tom-slopers-format-for-game-design-specifi-r243)
