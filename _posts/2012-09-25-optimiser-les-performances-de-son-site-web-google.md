---
id: 1201
title: 'Optimiser les performances de son site Web'
date: '2012-09-25T14:30:53+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1201'
permalink: /blog/developpement-php/optimiser-les-performances-de-son-site-web-google/
image: /wp-content/uploads/2012/09/vitesse_chargement_web-300x97.png
dsq_thread_id:
    - '1285641339'
categories:
    - 'Web'
tags:
    - 'Performances Web'
---

Dans cet article, retrouvez une sélection de techniques permettant d’**optimiser les performances de votre site Web** et ainsi rendre le **Web plus rapide**. Je vous livre ici ce qui me parait le plus pertinent. Vous pouvez [consulter l’article original (en)](https://developers.google.com/speed/articles/).

## Réduire le nombre de requêtes

Quand on fait des **sites Internet optimisés**, l’un des gros problèmes que l’on rencontre est le nombre de requêtes que doit faire le navigateur client pour charger complètement le site. En effet, toutes les requêtes ne sont pas lancées simultanément et le HTML/HTTP n’a pas été pensé pour transférer un nombre très important de ressources (images, javascript, feuille de style, vidéos, etc.). Ainsi, dès lors qu’un site contient de nombreux médias ou de nombreuses ressources, la navigateur doit les charger un à un, ce qui détériore considérablement la vitesse d’affichage.

La solution est simple : pour diminuer le nombre de requêtes, il faut **réduire le nombre de ressources** en les agrégeant. Ainsi, au lieu d’avoir 10 fichiers javascripts, 15 feuilles de styles et 50 images,- donc 75 requêtes au total -, on peut agréger les contenus par type pour ne faire qu’un seul fichier javascript, une seule feuille de style et une seule image ! Gain : 72 requêtes HTTP, le calcul est vite fait…

Ainsi, **un site Web optimisé nécessitera peu de requêtes HTTP** (une bonne limite à ne pas dépasser est 10 requêtes HTTP pour un chargement complet).

[![Faites ce que je dis, pas ce que je fais ! ;)](/wp-content/uploads/2012/09/blog_speed.png "blog_speed")](/wp-content/uploads/2012/09/blog_speed.png)

Faites ce que je dis, pas ce que je fais ! 😉

## Réduire la taille des requêtes

Le second problème des requêtes HTTP est que leur taille en octets est souvent trop importante. Quel intérêt de faire transiter sur le réseau des caractères inutiles à l’affichage sur le navigateur client ?

Il est donc possible de réduire le volume de requêtes en utilisant différentes techniques :

- la minification des JS et des CSS
- la compression des images
- la compression GZIP des requêtes HTTP
- le nettoyage du code source HTML

Ainsi il est possible de supprimer une grande quantité de caractères inutiles tels que les espaces, les sauts de lignes, les balises fermantes, commentaires, etc. Cette réduction du volume des requêtes entraînera une **optimisation des communications réseaux**. Quand il y a moins de données à faire transiter, ça va plus vite : logique…

## Compresser les images

Il est facile de **diminuer la taille des images (en Ko)** en appliquant une simple compression. Sans trop de perte de qualités, vous pourrez parfois diviser la taille de vos images par 10. Vous aurez alors 2 gains : d’une part le transfert réseau ira plus vite ; d’autre part, le navigateur analysera plus rapidement l’image et son affichage sera plus rapide.  
La taille en pixel peut également être réduite si vous n’en avez pas besoin. Il ne sert à rien de laisser une image en 500×600 si, au final, vous la redimensionnez via la balise HTML <img width=50 height=60 /> en 50×60 !

## Utiliser les gestionnaires de caches

Il existe de multiples niveaux de cache :

- cache navigateur
- cache HTTP
- cache du serveurs Web
- cache de la base de données
- reverse proxy

En les conjuguant intelligemment, vous accélérerez la **vitesse de chargement de votre site Web**. Gardez à l’esprit que tous les caches ne sont pas utiles dans toutes les situations. Pas besoin de sortir l’artillerie lourde pour 3 visiteurs simultanés… Tout est une question de besoin et de budget.

[![Cache HTTP](/wp-content/uploads/2012/09/cache_http.png "cache_http")](/wp-content/uploads/2012/09/cache_http.png)  

Crédit image et article intéressant : [OCTO Talks : HTTP Caching avec Nginx / Memcached](https://blog.octo.com/http-caching-avec-nginx-memcached/)

## Inclure les fichiers externes CSS avant les fichiers externes JS

Ça peut paraître étonnant mais l’ordre des requêtes et donc l’ordre dans le code HTML est important dans le chargement d’une page Web. En effet, lors du téléchargement d’un fichier Javascript, le navigateur attend le chargement complet et bloque les requêtes suivantes, ce qu’il ne fait pas dans le cas d’un fichier CSS. Ainsi les fichiers CSS doivent systématiquement être inclus AVANT les fichiers JS.

De manière générale, une des bonnes pratiques est d’**inclure les fichiers Javascript en fin de page**.

A noter qu’il est possible de déférer le chargement des javascripts après le chargement complet de la page Web en utilisant l’attribut **defer** sur la balise **script**. Merci à P2Q pour cette astuce (voir les commentaires) :

{% highlight javascript linenos %}
<script defer="defer" langage="text/javascript" src="js/script.js"></script>
{% endhighlight %}

**Cerise sur le gâteau, cette astuce est compatible tous navigateurs sur HTML4 et HTML5, Internet Explorer y compris !!**

## Conclusion

Ces quelques conseils n’ont pas vocation à être exhaustifs. Il convient à chacun de trouver les parades pour optimiser son site Web selon ses besoins, ses objectifs et son budget. N’hésitez pas à commenter si vous avez d’autres astuces.

Pour des [astuces sur l’optimisation PHP, vous trouverez un article ici](https://blog.nicolashachet.com/2012/09/26/technologies/php/optimiser-les-performances-de-son-code-php/) !
