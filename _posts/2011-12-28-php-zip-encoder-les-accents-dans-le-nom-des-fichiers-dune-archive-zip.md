---
id: 441
title: 'PHP / Zip : encoder les accents dans le nom des fichiers d&rsquo;une archive ZIP'
date: '2011-12-28T16:44:41+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=441'
permalink: /blog/developpement-php/php-zip-encoder-les-accents-dans-le-nom-des-fichiers-dune-archive-zip/
dsq_thread_id:
    - '1286601294'
image: /wp-content/uploads/2011/12/zip_file.jpg
categories:
    - 'PHP'
tags:
    - PHP
---

Les archives ZIP permettent d’archiver et de compresser des fichiers (Wikipédia vous expliquera le [principe des archives ZIP](https://fr.wikipedia.org/wiki/ZIP_(format_de_fichier)) mieux que moi). Il est possible de générer des archives ZIP en PHP via des librairies que vous trouverez aisément sur le net. Il est néanmoins possible qu’un problème d’encodage du nom des fichiers survienne lors de la génération. En effet, le nom des fichiers nécessite un **encodage en IBM850**. Ainsi vous devrez convertir vos chaines dans ce format, vos accents seront alors correctement affichés.

Exemple ci-dessous avec une **conversion de UTF-8 vers IBM850**.  
```php  
$name = iconv(‘UTF-8’, ‘IBM850’, $name);  
```
