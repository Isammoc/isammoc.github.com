---
layout: post
title: "Design pattern : Le singleton"
description: "Le design pattern le plus simple"
comments: true
categories: theorie
tags:
- java
- design pattern
published: true
---

Il y a un an ou deux, j'ai utilisé mon temps libre pour mettre en place une mailing-list décrivant certains points de la programmation orientée objet, et les premiers sujets étaient tout naturellement les design patterns. Je profite donc de l'ouverture de mon blog pour ne pas perdre ces données.

<!--more-->

## Description du problème ##

Nous désirons un type dont on ne peut avoir qu'une seule instance (ou un 
nombre limité d'instances) durant toute l'exécution du programme.
L'intérêt est de créer une instance commune car l'on a aucune utilité à 
venir dupliquer des instances faisant au final un travail commun et 
répétitif. On se situe en fait dans une approche de classe à instance 
unique.

Exemples de cas:

* Gérer les propriétés de l'application dans son ensemble
* Maintenir une connexion à une base de données
* Maintenir un seul et même fichier dans un module de journalisation
* Maintenir un objet gérant des données et valeurs globales tel qu'un cache.

On verra que l'on peut utiliser le Singleton de façon complémentaire 
d'autres pattern, tels que la fabrique abstraite, le monteur, le 
prototype, ou état.


## Description de la solution ##

Deux aspects majeurs du problème sont à prendre en compte.


### Empêcher la création de multiples instances de la classe ###

Le problème est vite réglé : il suffit de déclarer le constructeur comme 
privé. Ainsi il sera impossible de créer une instance de la classe à 
l'extérieur de la classe elle-même. On pourra également déclarer le 
destructeur comme privé pour empêcher une destruction prématurée de 
l'instance unique par mégarde.


### Assurer une instance de la classe ###

Pour cela, cette classe va posséder comme variable membre une référence 
vers une instance d'elle-même. Pour que cette instance soit accessible 
tout au long du programme, et donc pour qu'elle existe de sa création à 
la fin du programme, on va déclarer cet objet comme `static`.

![Diagramme de classe du pattern Singleton] [diaClassSingleton]

### Exemple en java ###

Directement copié collé depuis Wikipédia :

{% codeblock lang:java %}
 public class Singleton {
     private static Singleton INSTANCE = null;
 
     /**
      * La présence d'un constructeur privé supprime
      * le constructeur public par défaut.
      */
     private Singleton() {}
 
     /**
      * Le mot-clé synchronized sur la méthode de création
      * empêche toute instanciation multiple même par
      * différents threads.
      * Retourne l'instance du singleton.
      */
     public synchronized static Singleton getInstance() {
         if (INSTANCE == null) 
             INSTANCE = new Singleton();
         return INSTANCE;
     }
 }
{% endcodeblock %}

## Conséquences ##

Nous avons donc un et un seul objet. Que ce soit pour utiliser moins de 
mémoire, ou pour partager des données d'un bout à l'autre de l'application.

Il faut néanmoins penser au multi-threading, et donc la règle générale 
veut que la méthode statique getInstance ne puisse être accédée par un 
seul thread en même temps (pour assurer l'unicité de l'instance) ainsi 
que ses autres méthodes si nécessaires.


## Références ##

Wikipédia

* <http://fr.wikipedia.org/wiki/Singleton_(patron_de_conception)>
* <http://en.wikipedia.org/wiki/Singleton_pattern>

Java village

* <http://jvillage.wordpress.com/2007/06/19/design-pattern-de-creation-singleton/>

Developpez.com

* <http://smeric.developpez.com/java/uml/singleton/>

Autres

* <http://tfc.duke.free.fr/coding/singleton.html>
* <http://www.journaldunet.com/developpeur/tutoriel/jav/070911-design-pattern-singleton/2.shtml>

[diaClassSingleton]: http://yuml.me/diagram/scruffy/class/[Singleton|-instance|+getInstance():Singleton;],[Singleton]--[note:Ajoutez%20tous%20les%20attributs%20et%20méthodes%20nécessaires{bg:cornsilk}],%20[Singleton]--[note:%20Le%20constructeur%20de%20la%20classe%20doit%20être%20privé{bg:cornsilk}]
