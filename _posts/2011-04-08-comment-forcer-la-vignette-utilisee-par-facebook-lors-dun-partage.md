---
id: 81
title: 'Comment forcer la vignette utilisée par Facebook lors d&rsquo;un partage ?'
date: '2011-04-08T14:45:27+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=81'
permalink: /blog/developpement-php/comment-forcer-la-vignette-utilisee-par-facebook-lors-dun-partage/
dsq_thread_id:
    - '1285615568'
categories:
    - 'Social'
tags:
    - 'Réseaux sociaux'
---

La **vignette affichée par Facebook** lors du partage d’un lien est ce qui attire l’oeil de ses amis et connaissances. On peut raisonnablement supposer que Facebook analyse le code source de la page partagée et qu’il propose les images qu’il rencontre sur celle-ci à l’utilisateur qui choisira la vignette. Voici l’astuce permettant de forcer cette vignette, !

**Modifier l’entête de sa page (balise HEAD)**

Pour forcer Facebook à utiliser la vignette de son choix, il suffit d’inclure ce code dans l’entête de son site (entre la balises HEAD) :

```html
<html>  
<head>  
// …

<link href="https://www.votresiteweb.com/lavignettefacebook.png" rel="image_src" />

// …  
</head>  
<body>  
</body>  
</html>  
```

Tout est dans le **rel="image_src"** ! 😉

A noter que Facebook recommande que votre image fasse **200px de largeur**. Si la taille de votre image est trop petite, Facebook l’ignorera. Je vous conseille d’opter pour une image d’au moins 180 pixels de largeur.

Un article intéressant sur le sujet : [5 astuces pour optimiser votre page Facebook](https://fr.mashable.com/2009/04/09/5-astuces-pour-optimiser-votre-page-facebook/)
