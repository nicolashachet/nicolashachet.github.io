---
id: 662
title: 'Comment gérer la version d&rsquo;un logiciel ?'
date: '2012-07-22T12:14:31+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=662'
permalink: /blog/gestion-de-projets/comment-gerer-la-version-dun-logiciel/
dsq_thread_id:
    - '1285640211'
image: /wp-content/uploads/2012/07/versionning2-180x100.png
categories:
    - 'Versionning'
---


[![](/wp-content/uploads/2012/07/versionning2.png "versionning")](/wp-content/uploads/2012/07/versionning2.png)Le **versionning** ou la **gestion du numéro de version d’un logiciel ou d’une application** est le fait d’attribuer un code unique à une version d’une application. Ce code permet d’identifier les grandes évolutions ou les correctifs d’un logiciel lors de sa durée de vie.

Il s’agit de méthodes parmi d’autres. Je vous laisse le loisir de vous faire votre propre opinion. Je détaillerai 3 versionning : le versionning simple, le versionning étendu et la gestion du cycle de vie (qui peut être utilisé conjointement).

# Versionning simple : <span style="color: #3366ff;">X</span>.<span style="color: #ff0000;">Y</span>

<span style="color: #3366ff;">X</span>.<span style="color: #ff0000;">Y</span> c’est "la base" : <span style="color: #3366ff;">Version – </span><span style="color: #ff0000;">Révision</span>.

La **<span style="color: #3366ff;">version</span>**, c’est le découpage fonctionnel dans lequel se trouve un logiciel à un instant T. Ainsi il peut être prévu de découper une application de blogging comme ceci :

> <address>Version 1 :</address>gestion des utilisateurs  
> gestion des articles
> 
> *Version 2 :*
> 
> gestion des commentaires  
> réécriture de la gestion des utilisateurs  
> gestion des thèmes

La **<span style="color: #ff0000;">révision</span>** c’est l’état d’un lot fonctionnel.

La première ***release* officielle** sera donc identifiée par le numéro de **version 1.0** (version 1 révision zéro). En cas de correctifs, ce même lot d’évolutions sortira sous le numéro de version 1.1 (version 1 révision 1). Cela indique que les fonctionnalités sont identiques (ni ajout ni suppression de fonctionnalités) mais que des corrections ou améliorations y ont été apportées. Cela continue jusqu’à ce qu’il n’y ait plus de bugs…

La seconde ***release* officielle** sortira sous le numéro 2.0 (même si la version 1 est en révision 1.4).

Ce processus se poursuit jusqu’à ce que le logiciel ait atteint les fonctionnalités souhaitées. Ce type de versionning peut être utilisé pour n’importe projet, de n’importe quel taille. Pour des projets aux nombreuses fonctionnalités, il peut cependant être utile d’utiliser un versionning étendu.

# Versionning étendu : <span style="color: #3366ff;">X</span>.<span style="color: #339966;">Y</span>.<span style="color: #ff0000;">Z</span>

Le versionning étendu est, comme son nom l’indique, une extension du versionning simple. Le concept est strictement identique, au delta près que l’on différencie les lots d’évolutions en leur ajoutant une **criticité**.

<span style="color: #3366ff;">X</span>.<span style="color: #339966;">Y</span>.<span style="color: #ff0000;">Z</span> : <span style="color: #3366ff;">Version majeure</span> – <span style="color: #339966;">Version mineure</span> – <span style="color: #ff0000;">Révision</span>.

Lorsqu’on développe des logiciels aux nombreuses fonctionnalités, il est nécessaire de les hiérarchiser et de les trier. On parle alors de version majeure et de version mineure. Ce découpage est à l’appréciation du chef de projet fonctionnel qui est capable d’identifier les différences hiérarchiques entre les fonctionnalités.

Dans notre exemple d’application de blogging, ça pourrait donner ça :

> <address>Version 1.0 :</address>gestion des utilisateurs  
> gestion des articles
> 
> *Version 1.1 :*
> 
> gestion des commentaires  
> gestion des thèmes
> 
> *Version 2.0 :*
> 
> gestion des pages  
> gestion des widgets  
> gestion des extensions

Le processus d’affectation de la révision est alors identique à la forme simple.

# Cycle de vie d’une application

Une application ne sort pas forcément directement en version officielle **finale ou stable**. Il arrive que l’application soit proposée à un nombre restreint d’utilisateurs ou qu’elle soit disponible pour tous sans garantie de fonctionnement. Il est ainsi possible d’ajouter à son numéro de version un identifiant qui indique l’état d’avancement du cycle de développement. On suffixe généralement son numéro de version avec un indicateur dont voici une liste :

<span style="color: #3366ff;">X</span>.<span style="color: #ff0000;">Y</span>–<span style="color: #ff9900;">V <span style="color: #000000;">: <span style="color: #3366ff;">Version</span> – <span style="color: #ff0000;">Révision </span>– <span style="color: #ff9900;">Etat</span></span></span>

| Etat | Exemple | Description |
|---|---|---|
| dev | 1.5.1-dev | Version en cours de développement. Généralement utilisée en interne. |
| alpha | 1.5.1-alpha | Version en cours de développement. Les fonctionnalités ne sont pas toutes développées et peuvent contenir des bugs. Généralement utilisée comme POC (Proof Of Concept) afin de valider un fonctionnement général. |
| beta | 1.5.1-beta | Version en cours de développement. Les fonctionnalités sont presque toutes développées et peuvent contenir des bugs. Très utilisée pour faire une première passe de test en conditions réelles, notamment dans le cadre de *beta private* (nombre d’utilisateurs restreints). |
| release candidate | 1.5.1-rc1 | Version terminée. Les fonctionnalités sont toutes développées mais peuvent contenir des bugs que la RC a pour but de corriger. Il y a souvent un versionning des RC (rc1, rc2, rc3, etc.). |
| stable   final | 1.5.1-stable   1.5.1 | Version terminée et validée. Les fonctionnalités sont toutes développées et considérées comme stables (utilisables en production). |

Il existe d’autres nomenclatures et d’autres gestion de versions, n’hésitez pas à les indiquer en commentaire !
