---
id: 2656
title: 'Mobile : Application Native vs Responsive Design ?'
date: '2016-07-22T15:04:39+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2656'
permalink: /blog/developpement-php/mobile-application-native-vs-responsive-design/
dsq_thread_id:
    - '5005713161'
image: /wp-content/uploads/2016/07/app-native-vs-mobile-responsive-design-700x356.png
categories:
    - 'Responsive'
tags:
    - Android
    - 'Responsive Design'
---

Quand on développe un projet Web (application, site Web, …), on se retrouve systématiquement confronté à la problématique d’accès via périphérique mobile (smartphones et tablettes). Une question revient toujours : **on fait une application mobile ou un design responsive** ? Les deux ont des avantages et des inconvénients. On revient sur ce que c’est, et on vous dit ce qu’il faut faire.

## Application Native

Une application native est concue, développée, compilée pour un OS mobile : **iOS ou Android** pour faire court. Ce type d’application est développé spécifiquement pour le périphérique mobile sur lequel il s’exécute, avec tous les avantages qu’on connait quand une application est dédiée :

- accès à toutes les fonctionnalités du téléphone (GPS, accéléromètre, GPU, …),
- performances aux plus proches du périphérique (pour la gestion de la 3D par exemple),
- diffusion via les canaux Apple Store et Google Play,
- etc.

Concrètement le développement spécifique mobile offre une grande liberté sur les fonctionnalités proposées. Le revers de la médaille est un coût qui explose puisque vous devrez développer et maintenir non pas *un* projet, mais *trois* : le site Web, l’application mobile iOS et l’application Android. Il existe cependant des solutions pour réaliser des applications cross-plateformes sur un code unique (Apache Cordova par exemple) mais les inconvénients sont réels, j’y reviendrai peut être dans un autre article.

## Responsive Design

L’autre solution est de rester sur un unique projet Web avec un design et des fonctionnalités qui s’adaptent aux périphériques qui le consultent. C’est le principe du design adaptatif, ou Responsive Design. Initialement, le Responsive Design se limitait au code CSS, c’est à dire à la **présentation** des éléments. Depuis quelques temps, il est également possible de modifier le **comportement** de votre site Web selon le type et la résolution du périphérique via des librairies Javascript.

[→ En savoir plus sur les frameworks CSS compatible responsive design.](https://www.nicolashachet.com/blog/ergonomie-design/les-frameworks-css-responsive-design/)

Ce fonctionnement a le gros avantage d’être moins coûteux par rapport à des applications natives. Attention cependant, car selon votre projet vous pourrez être limité en fonctionnalités et en performances sur ce qu’il est possible de faire ou non. Concrètement, oubliez la 3D et les interfaces trop riches. L’autre inconvénient est lié aux performances réseaux qui peuvent être aléatoires et changeantes sur périphérique mobile : imaginez le chargement d’un site Web de plusieurs mégas sur une connexion 2G…

## Alors, application iOS/Android ou projet responsive ?

De mon point de vue, il est évident que **votre projet Web doit être responsive design**, que vous ayez des applications iOS/Android dédiées ou non. Ne vous privez pas d’un grand nombre de visiteurs accédant à vos contenus et services via les périphériques mobiles. Cette tendance ne fait que s’accentuer au fil du temps : ne pas prévoir ce type d’accès sur vos nouveaux projets Web est clairement hors sujet. D’autant plus que les technologies facilant la gestion du responsive existent et fonctionnent très bien.

[→ Pourquoi le responsive design devrait être votre priorité ?](https://www.nicolashachet.com/blog/ergonomie-design/projet-web-pourquoi-le-responsive-design-devrait-etre-votre-priorite/)

Concernant les applications natives, le choix est plus complexe. En effet, il est nécessaire de peser le pour et le contre, notamment sur les **coûts de conception, de développement et de maintenance.** Il s’agit de projets séparés, dédiés et devant être considéré comme tels, et non comme une simple déclinaison du site principal. Dès lors que vous aurez besoin de performances et de design, optez pour une application dédiée, par exemple pour les jeux ou pour des applications utilisant des composants du périphérique mobile.
