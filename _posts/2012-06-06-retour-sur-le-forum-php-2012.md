---
id: 1000
title: 'Retour sur le Forum PHP 2012'
date: '2012-06-06T22:38:54+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1000'
permalink: /blog/actualites/retour-sur-le-forum-php-2012/
dsq_thread_id:
    - '1297780528'
image: /wp-content/uploads/2012/06/php_elephant-120x120.jpg
categories:
    - PHP
tags:
    - PHP
---

[![](/wp-content/uploads/2012/06/ciup-300x225.jpg "ciup")](/wp-content/uploads/2012/06/ciup.jpg)La Cité Internationale Universitaire de Paris

Organisé par l’AFUP, le <a rel="noopener noreferrer" target="_blank">Forum PHP 2012</a> s’est tenu les 5 et 6 juin 2012 à la Cité  
Internationale Universitaire de Paris ([CIUP](https://www.ciup.fr/)). J’étais présent le 5 avec **GFI Informatique**.

Voici les conférences auxquelles j’ai assisté :

- [PHP in 2012](#php-en-2012) – Espace Adenauer
- [Annotating with Annotations](#annotations) – Espace Adenauer
- [Anatomie du test](#testing) – Salon Honorat
- [Monitoring applicatif : Pourquoi et comment ?](#monitoring) – Salon Honorat
- [Haute disponibilité au service du public](#service-public) – Salon Honorat
- [Magic Behind The Numbers – Software Metrics In Practice](#software-metrics) – Espace Adenauer
- [Modélisation des menaces d’une application web : étude de cas](#modelisation-des-menaces) – Espace Adenauer
- [Fonctions avancés du driver MySQL natif pour PHP](#mysqlnd) – Espace Adenauer

Je consacrerai un article à chaque conférence afin d’avoir une vision précise de chaque sujet. Pour l’heure, retour rapide sur cette journée riche !

[![](/wp-content/uploads/2012/06/php_elephant-300x225.jpg "php_elephant")](/wp-content/uploads/2012/06/php_elephant.jpg)L'éléphant PHP était bien présent !

<a name="php-en-2012"></a>

## PHP en 2012

Ce fut light car je n’ai pu assister qu’à la fin de la conférence. Dommage, c’était **Rasmus Lerdorf** aux commandes, créateur du langage PHP ! Un gros poisson pour l’ouverture du forum et un bon coup de com’ pour l’AFUP. Il a pris soin de faire un retour sur la sortie de PHP 5.4 et un état global du langage en 2012.

La présentation : <https://talks.php.net/show/afup12>

<a name="annotations"></a>

## Annotating with Annotations

Animée par **Rafael Dohms**, cette conférence a permis de faire l’éloge des annotations dans les développements PHP. Même si je ne reste pas convaincu par l’utilisation systématique des annotations, les applications sont nombreuses et parfois très intéressantes (notamment pour la gestion du routing en Symfony 2 par exemple). Nous y reviendrons dans l’article qui fera suite.

La présentation : <https://www.slideshare.net/rdohms/annotating-with-annotations-forumphp-2012>

<a name="testing"></a>

## Anatomie du test

Présentation assez générale des différents tests, cette conférence était animée par **Frédéric Hardy** et **Ivan Enderlin** ([HOA project](https://hoa-project.net/)). TDD (Test Driven Development), *tests* unitaires, d’intégrations ou fonctionnels, l’objectif était de passer en revu la démarche et non de rentrer dans le vif du sujet. Une conférence plutôt plaisante où quelques outils auront quand même été cités : *ATOM, PHPUnit, SempleTest, HOA*, notamment.

<a name="monitoring"></a>

## Monitoring applicatif : Pourquoi et comment ?

Cette conférence proposait un **retour d’expérience** sur le monitoring applicatif des sites gérés par M6Web : *clubic, turbo, deco, Jeuxvideo*, etc. Animée par **Dits Kenny**, responsable Etude et développements chez M6Web, la conférence a principalement tourné autours des solutions mises en oeuvre pour monitorer l’ensemble des serveurs et applications : **Node.js, StatsD et graphite**. Un recul très intéressant notamment sur l’utilisation des rapports proposés par **Graphite**.

La présentation sera disponible dans quelques jours ([info Twitter](https://twitter.com/kenny_dee/status/209987392734625795)).  
En attendant, une autre pres (voir 32, 33, 34 pour statsd + graphite) : <https://www.slideshare.net/kennydee/performances-php-chez-m6web>

<a name="service-public"></a>

## Haute disponibilité au service du public

**Retour d’expérience** présenté par **Christophe Villeneuve** et **Stephane Baixas**, ce fut l’occasion de revenir sur la mise en place de l’*autolib’* et notamment l’outil central de supervision du système. Une bonne explication des problématiques et enjeux du projet et un retour intéressant sur le planning et les contraintes projets.

<a name="software-metrics"></a>

## Magic Behind The Numbers – Software Metrics In Practice

**Sebastian Marek** nous présentait la signification des différentes métriques et outils de test. L’occasion de revenir sur des notions et outils parfois obscures : complexité cyclomatic, nPath, Sonar, PHPMD, etc. Une conférence très intéressante, parfois complexe.

Les slides : <https://www.slideshare.net/proofek/magic-behind-the-numbers-software-metrics-in-practice>

<a name="modelisation-des-menaces"></a>

## Modélisation des menaces d’une application web : étude de cas

Présentation très intéressante sur la modélisation des menaces, l’objectif était d’identifier la démarche mise en oeuvre pour identifier les menaces, les risques et les contre mesures à mettre en place. La conférence état animée par **Antonio Fontes**, expert en sécurité. Dommage que la présentation ait été écourtée faute de temps !

Les slides : <https://www.slideshare.net/starbuck3000/modliser-les-menaces-dune-application-web>

<a name="mysqlnd"></a>

## Fonctions avancés du driver MySQL natif pour PHP

Animée par **Serge Frezefond**, cette conférence a permis de découvrir (ou re découvrir) les bénéfices apportés par le passage au driver MySQLnd (natif en PHP 5.4). L’occasion de constater qu’il devient urgent d’y passer !

En bref, pour son grand retour, l’AFUP a frappé fort et bien. De bonnes conférences et une organisation au top ont fait du Forum PHP 2012 une vraie réussite.
