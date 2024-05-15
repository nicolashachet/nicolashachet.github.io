---
id: 2128
title: 'Quelle architecture logicielle pour un site Web fort trafic ?'
date: '2014-04-16T10:54:03+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2128'
permalink: /blog/developpement-php/quelle-architecture-logicielle-pour-un-site-web-fort-trafic/
dsq_thread_id:
    - '2615756694'

image: /wp-content/uploads/2014/04/site-web-fort-trafic.jpg
categories:
    - 'Architecture'
tags:
    - 'Architecture Technique'
    - 'Performances Web'
    - PHP
    - Symfony
---

On ne développe pas un **site Web à fort trafic** comme on développe un site institutionnel qui recevra quelques centaines de visites par jour. Quand les performances doivent être optimales, il est nécessaire d’adapter l’**architecture logicielle** du site Web. Quelles sont les technologies à mettre en oeuvre pour servir un maximum de visiteurs en un minimum de temps ?

## Choisir le bon framework

[![symfony2](/wp-content/uploads/2014/04/symfony2-150x150.png)](/wp-content/uploads/2014/04/symfony2.png)Avant toute chose, il vous faudra opter pour un **framework de développement** supportant des techniques d’optimisations avancées :

- précompilation,
- gestion de caches,
- Edge Side Include (ESI)

Ce dernier point est particulièrement important dès lors que vous souhaitez mettre en place une stratégie agressive de caching . En effet, la norme [ESI éditée par Akamai](https://www.akamai.com/html/support/esi.html "ESI by Akamai") permet de mettre en cache des morceaux de page tout en conservant certaines parties dynamiques : nom de l’utilisateur connecté, panier d’achats, news temps réel, etc.

[Symfony 2](https://symfony.com/ "Symfony 2") est particulièrement adapté puisqu’il gère nativement les ESI et intègre un reverse proxy écrit en PHP pour les tester.

## Mettre en place un front solide

[![varnish](/wp-content/uploads/2014/04/varnish.png)](/wp-content/uploads/2014/04/varnish.png)Pour servir un grand nombre de visiteurs, il existe des technologies bien plus performantes que PHP. Vous devrez donc concevoir l’architecture du projet en limitant les appels vers PHP (ou en basculant vers d’autres technologies). Cela passe par la mise en place d’un **front** dédié aux services des pages et un **back** centré sur les aspects métiers.

L’objectif de cette séparation stricte est de réduire au maximum les appels vers les serveurs applicatifs en back tout en servant un maximum de pages en cache via le front.

[Varnish ](https://www.varnish-cache.org/ "Varnish")et [Squid ](https://www.squid-cache.org/ "Squid")sont des reverses proxies à placer en frontal des applications métiers. Ce sont eux qui répondent aux sollicitations :

- soit en servant directement les pages en cache,
- soit en appelant le serveur applicatif ;
- soit un mix des deux lors de l’utilisation d’ESI.

## Une bonne requête est une requête qui ne part pas

[![cache-http](/wp-content/uploads/2014/04/cache-http.png)](/wp-content/uploads/2014/04/cache-http.png)La **mise en cache** des ressources coté utilisateurs est la meilleure des techniques pour augmenter le nombre de visiteurs servis. En effet, la bonne requête est celle qui n’a pas besoin d’être lancée ! L’utilisation des entêtes suivants vous permettra d’éviter les appels inutiles :

- Cache-Control
- Expires
- Last-Modified
- ETag

Là encore, Symfony 2 est adapté puisqu’il gère nativement le cache au plus près de la norme HTTP : durée de vie, expiration, invalidation, etc. Un bundle tel que [LiipCacheControl ](https://github.com/liip/liipcacheControlBundle "LiipCacheControl")vous aidera également dans cette tâche sensible.

## Du cache coté applicatif

[![redis](/wp-content/uploads/2014/04/redis.png)](/wp-content/uploads/2014/04/redis.png)Dans un précédent article, je vous présentais succinctement les [différents types de cache](https://blog.nicolashachet.com/gestion-de-caches/optimisation-web-php-des-caches-a-tous-les-niveaux/ "Optimisation Web PHP : des caches à tous les niveaux") qu’il est possible d’utiliser pour **optimiser une application Web**. L’un des secrets pour accélérer drastiquement une application gérant de nombreuses données métier est d’utiliser un cache **applicatif**. Dans le cadre d’application métier affichant des données dynamiques, plutôt que de calculer la réponse à chaque requête, il est possible de la précalculer régulièrement et de la placer dans des serveurs de cache. C’est cette représentation qui sera utilisée pour l’affichage et qui sera invalidée à intervalle plus ou moins régulier selon la fraîcheur souhaitée des données.

Issu de la mouvance **NoSQL**, [Redis ](https://redis.io/ "Redis")est un serveur clef/valeur évolutif gérant les accès concurrents, les données structurées et de nombreuses fonctionnalités puissantes. Il autorise la montée en charge ainsi que la sauvegarde asynchrone sur disque afin d’optimiser les performances.

## Limiter les requêtes (en nombre et en poids)

[![compress](/wp-content/uploads/2014/04/compress.png)](/wp-content/uploads/2014/04/compress.png)Évidement la **mise en cache coté navigateur** n’apporte un gain qu’à partir de la *seconde* requête effectuée par l’utilisateur. Celui-ci devra toujours récupérer les ressources lors de son *premier* appel. Il est donc nécessaire d’optimiser le nombre et le poids des requêtes en travaillant sur quatre chantiers :

- la minification et l’assemblage des fichiers CSS et Javascript,
- la réduction du nombre d’images via la construction de sprites (images concaténées),
- la taille des fichiers : poids des CSS, Javascript, images, HTML,
- l’utilisation de la compression GZIP pour l’envoi des données.

Des bundles tels que [Assetic](https://symfony.com/doc/current/cookbook/assetic/asset_management.html "Assetic"), [Sprites](https://sprites.readthedocs.org/en/latest/ "Sprites") et [HTMLPurifierBundle ](https://github.com/Exercise/HTMLPurifierBundle "HTMLPurifier")pourront vous être utiles pour gérer ces problématiques.

## Des technologies adaptées

[![website-scalability](/wp-content/uploads/2014/04/website-scalability.png)](/wp-content/uploads/2014/04/website-scalability.png)Quand on aborde les sites à fort trafic, on parle forcément d’architecture évolutive. Une architecture évolutive (scalable) permet avant tout de supporter des évolutions de charge en ajoutant ou retirant des serveurs (front, cache, applicatif, database) **sans changer une ligne de code** hormis la configuration. La contrainte "site Web fort trafic" impose donc d’être prise en compte **dès la phase de conception** du projet afin d’éviter des coûts exorbitants de migration ultérieure voire de réécriture complète.

Ainsi, tout au long de la vie du projet, les technologies devront être minutieusement sélectionnées en ayant à l’esprit cette contrainte de scalabilité.

## Conclusion

J’ai abordé quelques techniques et technologies telles que Symfony, Varnish, Squid, Redis permettant de gérer la montée en charge d’un site Web. L’écosystème Web évolue rapidement, n’hésitez donc pas à suggérer vos outils et technologies en commentaire.
