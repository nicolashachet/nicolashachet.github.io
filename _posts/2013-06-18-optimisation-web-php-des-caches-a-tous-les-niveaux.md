---
id: 1789
title: 'Optimisation Web PHP : des caches à tous les niveaux'
date: '2013-06-18T14:26:47+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1789'
permalink: /blog/developpement-php/optimisation-web-php-des-caches-a-tous-les-niveaux/
dsq_thread_id:
    - '1409650482'

image: /wp-content/uploads/2013/06/cache_apc_opcodes.jpg
categories:
    - 'Développement'
tags:
    - 'Architecture Technique'
---

J’ai déjà parlé d’[optimisation de site Web](https://blog.nicolashachet.com/fonctionnement-du-web/optimiser-les-performances-de-son-site-web-google/ "Optimiser les performances de son site Web") et d’[optimisation de code source PHP](https://blog.nicolashachet.com/technologies/php/optimiser-les-performances-de-son-code-php/ "Optimiser les performances de son code PHP"). Sachez qu’il est également possible de mettre en place une **stratégie de caching pour accélérer son site Web**. Voici les niveaux de cache sur lesquels vous pouvez jouer lorsque vous développez ou optimisez une application **PHP**.

Cet article traite des caches suivants :

- <span style="line-height: 13px;">Cache HTTP (navigateur)</span>
- Cache d’opcodes PHP
- Cache applicatif
- Cache MySQL
- Reverse proxy
- CDN : Content Delivery network

[![Image : https://www.technologies-methodes-it.com/dotnet/cache-sur-les-projets-web/](/wp-content/uploads/2013/06/Cache-sur-les-projets-web.png)](/wp-content/uploads/2013/06/Cache-sur-les-projets-web.png)Image : https://www.technologies-methodes-it.com/dotnet/cache-sur-les-projets-web/

Le schéma ci-dessus présente l’ensemble des caches que nous verrons, à l’exception du reverse proxy.

## Cache HTTP (navigateur)

C’est le premier niveau de cache à étudier. Moins votre serveur est sollicité, plus nombreux sont les nouveaux clients à pouvoir être traités par votre serveur. Le **cache navigateur** est donc le meilleur ami des sites Web à fort trafic, sous réserve que vos utilisateurs viennent plusieurs fois…

Le **protocole HTTP/1.1** prévoit un entête définissant la mise en cache : **Cache-Control.** Il permet de spécifier la stratégie de cache à employer : *public, private, no-cache, no-store,* etc.

Un autre entête permet de contrôler la durée de mise en cache : **Expires** (Cache-Control le permet également via l’instruction *max-age*).

[![validite_cache](/wp-content/uploads/2013/06/validite_cache.gif)](/wp-content/uploads/2013/06/validite_cache.gif)Image : https://www.themanualpage.org/http/http_http10.php

Dans ce schéma, on est directement sur le cache client. Nous verrons les autres caches dans le suite de l’article.

## Cache opcodes PHP (APC, Zend Optimizer +)

Dans le cas du **langage PHP**, un cache serveur tel qu’APC permet de mettre en cache les **fichiers PHP pré-compilés**, également appelés **opcodes** ou **bytecodes**. Pour mémoire, PHP est un langage interprété, ce qui signifie que les fichiers sont *parsés*, *pré-compilés* pour être rendus lisibles par un processeur puis *exécutés* par le serveur, ceci à chaque appel des scripts.

Le **cache opcode** consiste à effectuer le parsing et la précompilation une seule fois puis de mettre en cache le résultat **opcodes en mémoire**. Cela évite 2 étapes lourdes liées à l’interprétation des fichiers et placent les fichiers dans une zone beaucoup plus rapide que la lecture sur disque dur.

Le gain en terme de performance est réellement significatif.

Pour mettre en oeuvre un cache serveur, vous pouvez vous tourner vers ces technologies :

- <span style="line-height: 13px;">l’extension [APC pour PHP](https://blog.nicolashachet.com/technologies/php/installer-le-bon-php_apc-dll-sous-windows-7-x64-et-corriger-les-erreurs/ "Installer le bon php_apc.dll sous Windows 7 (x64) et corriger les erreurs") (opcode cache)</span>
- [PHP 5.5](https://php.net/manual/fr/migration55.changes.php) qui intégrera Zend Optimizer + en natif
- [XCache](https://xcache.lighttpd.net/)

[![Fonctionnement du cache opcodes](/wp-content/uploads/2013/06/cache_apc_opcodes.jpg)](/wp-content/uploads/2013/06/cache_apc_opcodes.jpg)Image : https://www.stephane-raymond.com/blog/webperf/caching-avance/

## Cache applicatifs (APC, XCache)

Une autre technique pour optimiser les performances de son application Web est de mettre en place un **cache applicatif**. L’idée est de gérer un cache interne à l’application qui stocke les données ou les blocs de code fréquemment utilisés.

Ce type de cache est fonction du type d’application et du type de données gérées dans celle-ci. Il est en effet relativement simple de mettre en cache des **données référentielles** ou des **objets métiers**, qui ne varient pas ou peu au cours du temps. Il est également facile de stocker en cache des éléments de page HTML "statiques" : menus, entête, pied de page, etc. En revanche, ce fonctionnement nécessite des adaptations au niveau du code et doit donc être pris en compte au plus tôt dans les développements.

Pour mettre en oeuvre un cache applicatif, vous pouvez utiliser ces technologies :

- [<span style="line-height: 13px;">XCache</span>](https://xcache.lighttpd.net/)
- [APC](https://php.net/manual/fr/book.apc.phppKI4OnB4Kq7w&bvm=bv.47883778,d.d2k)
- [Yet Another Cache](https://github.com/laruence/yac)

Je vous invite à consulter cet article sur les[ caches d’opcode et de données en PHP](https://blog.famillecollet.com/post/2013/03/23/PHP-cache-d-opcode-et-de-donnees).

Il est également possible de se tourner vers des **serveurs de cache** :

- [<span style="line-height: 13px;">Redis</span>](https://redis.io/)
- [Memcached](https://memcached.org/)

Pour ces deux derniers, notez qu’on est là sur des systèmes qui peuvent faire bien plus que du simple cache utilisateur.

[![Image : https://www.bliz.fr/blog/2013/02/15/activer-et-configurer-le-blob-cache-pour-sharepoint](/wp-content/uploads/2013/06/fonctionnement_du_cache.jpg)](/wp-content/uploads/2013/06/fonctionnement_du_cache.jpg)Image : https://www.bliz.fr/blog/2013/02/15/activer-et-configurer-le-blob-cache-pour-sharepoint

## Cache MySQL

Les **allers / retours entre serveurs** sont une des problématiques majeures de l’optimisation. Le cache applicatif et la mise en cache des données de requêtes est une solution possible pour éviter de requêter systématiquement la base de données. Avec l’arrivée de PHP 5.4, il est désormais possible de gérer un **cache MySQL en natif**, notamment grâce à l’utilisation du nouveau [driver MySQLnd](https://php.net/manual/fr/mysqlnd.plugin.api.php).

Je vous laisse consulter la documentation officielle de ce nouveau driver MySQL : <https://dev.mysql.com/doc/refman/5.6/en/apis-php-mysqlnd-qc.quickstart.html>

## Reverse proxy (Varnish)

Le **reverse proxy** est un intermédiaire entre le client et le serveur applicatif. Il reçoit les requêtes clients et sert les réponses qu’il a en cache ou qu’il récupère du ou des serveurs applicatifs. Il permet de faire de la **mise en cache partielle** de pages Web, ce qui permet une grande souplesse, notamment lors de l’utilisation sur des sites dynamiques (ex : panier du client).

Cette mise en cache partielle est rendue possible grâce à l’**ESI : Edge Side Include**. Ce mécanisme consiste à définir des zones à mettre à jour sur une page HTML grâce à l’utilisation d’une balise spéciale <esi:include …></esi>. Elle est notamment comprise par des reverse proxy comme **Varnish** par exemple. Voici un schéma permettant de se faire un idée de ce qu’est un reverse proxy.

[![reverse_proxy](/wp-content/uploads/2013/06/reverse_proxy.jpg)](/wp-content/uploads/2013/06/reverse_proxy.jpg)Image : https://zhous.net/groups/basicnetworking/wiki/1f47a/

## Cache de ressources statiques (CDN)

Les **ressources statiques** sont par nature… statiques. Or quel est l’intérêt de servir dynamiquement des ressources qui n’évoluent pas dans le temps ? C’est ainsi qu’est née l’idée des **Content Delivry Network ou CDN**. Ces réseaux sont passés maîtres dans l’art de servir des contenus statiques de manière très rapide.

Toutes les ressources Web sont éligibles à être servies par un CDN mais, pour des raisons de déploiement, l’intérêt est plus grand lorsqu’il s’agit de ressources qui n’évoluent pas : **feuilles de styles CSS, scripts Javascripts et images** en font parties. Ainsi, plutôt, que de charger inutilement son propre serveur Web en servant les CSS, JS et images, il est possible de déléguer leur service à un CDN.

Si le CDN vous parait surdimensionné, il est également possible de désigner un serveur dédié uniquement pour le service de ces ressources statiques.

## Conclusion

Nous avons survolé la multitude de **caches** sur lesquels il est possible de jouer pour **accélérer son site Web** et servir un plus grand nombre d’utilisateurs. Toutes ces techniques peuvent bien sûr être cumulées. Mais il faut bien garder à l’esprit que la **stratégie de caching** employée dépend principalement des moyens mis en oeuvre ainsi que du temps de réponse souhaité. Il ne sert pas forcément à grand chose de répondre en quelques millisecondes dans toutes les situations !

### Cet article n’est qu’une ébauche, pour aller plus loin sur la mise en cache…

Pour en savoir plus, je vous invite à consulter ces articles :

- <span style="line-height: 13px;">Tutoriel de la mise en cache : [https://www.mnot.net/cache_docs/index.fr.html](https://www.mnot.net/cache_docs/index.fr.html)  
    </span>
- RFC 2068 – HTTP/1.1 : <https://tools.ietf.org/html/rfc2616>
- Zend Optimizer + en PHP 5.5 : <https://itnews2day.wordpress.com/2013/03/11/zend-optimizer-is-approved-for-inclusion-in-php-5-5/>
- Varnish et les ESI : <https://naholyr.fr/2011/03/varnish-edge-side-includes-cache-partiel/>
- Caching avancé : <https://www.stephane-raymond.com/blog/webperf/caching-avance/>
- Cache sur les projets Web : <https://www.technologies-methodes-it.com/dotnet/cache-sur-les-projets-web/>
- Proxy et reverse proxy : <https://zhous.net/groups/basicnetworking/wiki/1f47a/>
