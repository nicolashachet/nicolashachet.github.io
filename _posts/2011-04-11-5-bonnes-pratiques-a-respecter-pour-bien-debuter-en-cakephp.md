---
id: 89
title: '5 bonnes pratiques à respecter pour bien débuter en CakePHP'
date: '2011-04-11T20:20:15+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=89'
permalink: /blog/developpement-php/5-bonnes-pratiques-a-respecter-pour-bien-debuter-en-cakephp/
categories:
    - 'PHP'
tags:
    - CakePHP
    - PHP
---

CakePHP est un framework PHP simple à utiliser et très puissant. Sa souplesse et sa facilité de mise en oeuvre en font un outil parfait pour débuter. Il est cependant nécessaire de respecter un certain nombre de bonnes pratiques afin de conserver toute la puissance et la flexibilité du framework.[![Logo CakePHP](/wp-content/uploads/2011/04/cake-logo.png "cakephp logo")](/wp-content/uploads/2011/04/cake-logo.png)

**1. Utiliser les conventions de CakePHP**

"Convention over configuration" (des conventions plutôt que de la configuration), telle est la devise de CakePHP. Il est nécessaire de prendre ce paradigme au pied de la lettre car l’utilisation de ces conventions simplifie énormément le développement. Elles sont détaillées sur le site de Cake et sur tout un tas de blogs dispos sur le Web.

**2. Respecter le MVC**

Ça peut paraître banal de dire ça, mais l’utilisation du MVC (Modèle, Vue, Contrôleur) est indispensable.

La couche Modèle est réservée à tout ce qui touche à la récupération des données. En gros : **pas de find() dans les contrôleurs !** Mieux vaut faire une fonction de récupération dans le modèle.  
La couche Contrôleur doit contenir la logique applicative (enregistrements, traitements, règles de gestion, etc.).  
La couche Vue est réservée à tout ce qui sera envoyé coté client (formulaires HTML, tableaux, etc.).

**3. Bannir les associations à la volée (belongsTo, hasMany, etc.)**

Sur de petites applications, ça peut paraître pratique. Dès que la base de données commencent à prendre du poids, l’utilisation de ces associations est catastrophique. Par expérience, mieux vaut définir les jointures à la main en utilisant les clefs "joins" des tableaux d’options.

**4. Utiliser les helpers du coeur CakePHP**

Que ce soit les helpers Html, Form, Javascript, leur utilisation facilite le développement et garantit un code propre et bien formé. Il est nécessaire d’utiliser ces helpers dès ses débuts en CakePHP. Après un court temps d’adaptation, ils vous permettront de gagner un temps précieux.

**5. Réfléchissez à l’architecture de votre application**

Il existe de multiples moyens d’étendre les fonctionnalités de CakePHP : helpeurs, composants, comportements, plugins. Chaque composant logiciel a sa place et peut être utile à un moment ou à un autre. N’hésitez pas à abuser de ces composants et à fabriquer des briques réutilisables dans vos projets.

Il est parfois nécessaire de prendre son temps pour réfléchir à l’architecture de son application. Gardez à l’esprit que ce n’est jamais du temps perdu !
