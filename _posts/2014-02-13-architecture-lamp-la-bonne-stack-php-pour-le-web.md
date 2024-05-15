---
id: 2041
title: 'Architecture LAMP : la bonne stack PHP pour le Web ?'
date: '2014-02-13T11:42:54+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2041'
permalink: /blog/developpement-php/architecture-lamp-la-bonne-stack-php-pour-le-web/
dsq_thread_id:
    - '2260520307'

image: /wp-content/uploads/2014/02/lamp-linux_apache_mysql_php.jpg
categories:
    - 'LAMP'
tags:
    - 'Performances Web'
    - PHP
---

Il y a quelques années l’**architecture Web LAMP** était à la mode dans le monde opensource. De nos jours, la question se pose et le choix de cette **stack PHP opensource** nécessite une solide justification. Rapide tour d’horizon des alternatives.

## LAMP

"LAMP" est un acronyme désignant les technologies Linux, Apache, MySQL et PHP. Dans ces technologies on retrouve tout ce qui permet de bâtir une application Web :

- un **système** : Linux ;
- un **serveur Web** traitant les requêtes HTTP : Apache ;
- un serveur de **base de données** : MySQL ;
- un **langage** de programmation : PHP.

Bref, avec LAMP, on est équipé pour faire des sites Web, des applications métiers, des webservices. Seulement, il y a plusieurs années sont arrivées des alternatives intéressantes et plus performantes (ou pas).

## Nginx plutôt que Apache

Il existe de nombreux benchmarks de comparaison entre **Nginx** et **Apache** sur le Web ([par là](https://blog.f3re.com/comparatif-nginx-vs-apache/) ou [par ici](https://wiki.dreamhost.com/Web_Server_Performance_Comparison)) et je ne vais pas en remettre une couche, mais sachez que les performances de Nginx sont bien meilleures.

L’utilité d’avoir un serveur Web performant est qu’il est capable de traiter plus de requêtes simultanément. Ça s’accompagne généralement d’une plus grande réactivité en termes de temps de réponse. Concrètement une requête qui mettrait 100 ms de traitement sous Apache, en mettrait 40 ms par Nginx (données d’exemple).

Sachez que [Nginx ](https://nginx.org/)n’est pas la seule **alternative à Apache**. Vous pourriez préférer LightHTTPD, [Hiawatha ](https://www.hiawatha-webserver.org/)ou [Cherokee](https://cherokee-project.com/). Il existe également des comparatifs : [là](https://centminmod.com/benchmarks_nginx_openlitespeed_cherokee.html), [là](https://www.rootusers.com/web-server-performance-benchmark/) et [là](https://www.wjunction.com/64-webmaster-resources/81962-apache-vs-nginx-vs-lighttpd-cherokee.html).

## MySQL 5.6 plutôt que MySQL 5.5 ou MariaDB

Coté **base de données** : le constat est différent. S’il s’avère que des moteurs SGBD tels que MariaDB sont plus performants que des versions vieillissantes de MySQL, la nouvelle version de MySQL 5.6 optimise drastiquement les performances (voir un bench [par ici](https://dimitrik.free.fr/blog/archives/2013/02/mysql-performance-mysql-56-vs-mysql-55-vs-mariadb-55.html)). La guerre est ouverte comme en témoigne [ce benchmark ](https://blog.mariadb.org/mariadb-5-3-optimizer-benchmark/)issu du blog **MariaDB** qui semble indiquer que **MySQL 5.6** ne répond pas forcément de manière optimisée à toutes les requêtes.

Bref, au niveau SGBD les choses ne sont pas tranchées et seuls des tests poussés sur ces technologies permettront de vous faire une idée.

## PHP plutôt que PHP ?

Des alternatives comme [Python ](https://www.python.org/)ou [Ruby On Rails](https://rubyonrails.org/) sont actuellement crédibles. Mais la puissance de PHP réside dans 4 choses :

- sa simplicité d’apprentissage et d’utilisation ;
- ses bibliothèques natives qui intègrent tout ce dont on a besoin dans un seul package ;
- sa large communauté;
- ses composants tiers issus de la communauté.

Que vous [choisissiez des frameworks](https://www.nicolashachet.com/blog/technologies/php/pourquoi-utiliser-un-framework-php/ "Pourquoi utiliser un framework PHP ?") comme **Symfony, CakePHP, Zend** ou autre, PHP reste la référence du **développement Web**. Ce discours prêche évidement pour ma paroisse mais je crois réellement que PHP est le parfait allié de vos [projets Web pour 2014](https://www.nicolashachet.com/blog/technologies/php/quel-framework-php-pour-2014/ "Quel framework PHP pour 2014 ?").

## La stack PHP 2014

En conclusion, je vous livre sans surprise ma stack PHP favorite pour 2014 :

- Nginx 1.4.5 (dispo depuis 2 jours) ;
- MySQL 5.6
- PHP 5.5
