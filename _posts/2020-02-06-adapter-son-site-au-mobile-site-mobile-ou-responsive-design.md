---
id: 3620
title: 'Adapter son site au mobile : site mobile ou responsive design ?'
date: '2020-02-06T17:40:28+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=3620'
permalink: /blog/developpement-php/adapter-son-site-au-mobile-site-mobile-ou-responsive-design/
dsq_thread_id:
    - '7856747163'
image: /wp-content/uploads/2020/02/design-responsive-vs-site-mobile-dedie-700x525.png
categories:
    - 'Web'
tags:
    - 'Responsive Design'
---

À ce jour, on compte trois technologies différentes pour **consulter un site web sur son smartphone** : l’application mobile, le site web version mobile et le site web responsive design. Ces deux dernières semblent identiques et pourtant chacune des deux proposent des avantages et des inconvénients. Analysons ce qui **différencie un site mobile dédié d’un site Web responsive**.

## Différenciation entre un site version mobile et un site responsive design 

### Le site version mobile 

Une entreprise décide de créer son site web, jusque là rien d’anormal. Sauf qu’elle décide d’en créer un second, **spécialement dédié aux internautes sur smartphone**. C’est le site web qui détecte son support de lecture, mobile ou ordinateur, et envoie la bonne version sur la plateforme. Par conséquent, il faut réaliser un second site internet, pensé et optimisé pour les appareils de types tablettes et smartphones.

La mise en place se fait généralement via un **sous domaine** hébergeant le site mobile dédié :

- www.monsiteweb.com : le site Web principal
- m.monsiteweb.com : le site dédié aux mobiles

### Le site responsive design 

À l’inverse, un **site responsive design** est un unique site web qui adapte automatique son aperçu selon la taille du terminal de lecture.

Il est hébergé sur un domaine unique :

- www.monsiteweb.com

## Leurs avantages 

### Le site version mobile 

Différents aspects sont très intéressants à développer sur un site version mobile ; notamment l’ergonomie du site. Puisqu’il est spécialement conçu pour un terminal avec un petit écran, son design et ses contenus s’adaptent parfaitement à lui. Par exemple, sur un site commerce, le tunnel d’achat peut être simplifié au maximum sur mobile. De plus, des outils supplémentaires peuvent y être ajoutés comme une géolocalisation ou une interaction avec des applications installées sur le mobile. Enfin, un site version mobile permet de garantir une expérience utilisateur optimale en fonction des technologies utilisées, en faisant appel à un [développeur react](https://thetribe.io/metier-react.html) par exemple.

### Le site responsive design 

L’atout principal du site avec un responsive design est la maîtrise parfaite des coûts avec une unique programmation et sa compatibilité avec tous les supports (ordinateurs, smartphones, tablettes). La maintenance étant faite sur point d’entrée unique, le gain de temps et d’argent est important. Autre point, un site responsive design est globalement meilleur en [référencement naturel](https://www.abondance.com/20191213-41552-infographie-le-seo-de-qualite-en-2020.html) puisque tous les liens entrants pointent sur le même domaine. Le SEO n’est donc pas dilué entre deux sous-domaines. Les moteurs de recherche peuvent alors mieux référencer le site internet.

## Leurs inconvénients 

### Le site version mobile 

Vous l’aurez sûrement compris, l’inconvénient majeur d’un site version mobile est l’hébergement sur deux sous-domaines séparés : l’un pour la version ordinateur, l’autre pour les smartphones et tablettes, ce qui implique deux applications distinctes. Si les sites sont hébergéq sur deux sous-domaines , le référencement sera moins bons puisque les liens entrants pointeront sur les deux sous-domaines (il est néanmoins possible de jouer avec les balises href *Canonical* pour palier à ceci).

Par ailleurs, cela représente un coût supplémentaire au niveau du développement et de la maintenance. Le fait d’utiliser une architecture Front / Back peut réduire les coûts de maintenance tout en complexifiant le projet :

- un back-office pour éditer les contenus et exposer une API ;
- deux front-offices utilisant l’API pour récupérer les contenus et les afficher selon les logiques métiers spécifiques.

### Le site responsive design 

Quant au responsive design, il présente lui aussi des aspects négatifs. Il est fortement conseillé de choisir cette solution en amont du projet car l’ajout à posteriori peut s’avérer complexe et coûteux selon les technologies retenues.

Enfin, le choix du responsive design est un choix pratique mais qui nécessite de bien penser l’UX/UI (expérience utilisateur) dès la phase de conception pour éviter d’avoir un site uniquement adapté sur ordinateur et pas sur mobile, ou inversement.

## Pour récapituler

|  | **Site version mobile** | **Site responsive design** |
|---|---|---|
| **Avantages** | – Parfaitement adapté aux petits écrans   – UX optimal car possibilité de différencier les contenus et les logiques métiers | – Coûts encadrés   – Compatibilité maximale    – Meilleur référencement (SEO) |
| **Inconvénients** | – Surcoût en développement et maintenance    – Plutôt négatif pour le SEO car hébergement sur 2 sous-domaines | – A prendre en compte dès le début du projet   – UX moins flexible |
