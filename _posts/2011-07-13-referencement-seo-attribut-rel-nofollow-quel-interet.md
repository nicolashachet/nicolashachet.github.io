---
id: 188
title: 'Référencement SEO : attribut rel=nofollow, quel intérêt ?'
date: '2011-07-13T10:46:09+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=188'
permalink: /blog/seo/referencement-seo-attribut-rel-nofollow-quel-interet/
categories:
    - SEO
tags:
    - Google
---

## Qu’est-ce que le nofollow ?

Initialement, la valeur **nofollow** est placée sur une balise **meta** via l’attribut **content**. Cette directive s’applique à l’ensemble de la page puisqu’elle est placée dans l’entête **head** du fichier HTML. Elle permet d’indiquer aux moteurs de recherche de ne suivre aucun lien externe présent sur la page. Ainsi, le pagerank des sites cibles n’est pas majoré par le lien placé sur le site source.

```html
<meta name="robots" content="nofollow" />  
```

## Intérêt du rel=nofollow

Par extension, et dans l’optique de lutter contre le spam avec plus de discernement, certains moteurs de recherche comme Google et Bing ont décidé d’interpréter également la valeur **nofollow** placée sur l’attribut **rel** de la balise **a**. Il est ainsi possible de décider quels liens profiteront de la notoriété du site pour leur positionnement et quels liens seront considérés comme "sans intérêt".

[html]  
<a href="https://www.google.fr" rel="nofollow">Un moteur de recherche</a>  
[/html]

Dans l’exemple suivant, Google ne profitera pas de mon positionnement… 😀
