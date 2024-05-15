---
id: 60
title: 'La structure conditionnelle IF en PHP (simple, étendue, ternaire)'
date: '2011-04-08T08:45:55+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=60'
permalink: /blog/developpement-php/la-structure-conditionnelle-if-en-php-simple-etendue-courte/
dsq_thread_id:
    - '1285615536'

categories:
    - 'PHP'
tags:
    - PHP
---

Commençons light pour ce premier post qui a pour but de lister les **différentes formes de test en PHP (if)** : la forme simple, la forme étendue et l’écriture courte dite ternaire.  
Dans une application MVC, il arrive d’utiliser les différentes formes de IF afin d’accroître la lisibilité du code source en fonction de la couche sur laquelle on travaille.  
   
Voici une liste des différentes formes de IF en PHP.

## Le test simple

C’est le bon vieux IF que tout le monde connait : on peut en user et en abuser. Dans la majorité des cas, il suffit amplement. C’est par ailleurs la forme la plus optimisée. ```

```php
<?php if ($monTest) { echo 'Mon test est VRAI'; } else { echo 'Mon test est FAUX'; } ?>
```

## Variante

Lorsqu’une seule instruction doit être exécutée après le test, on peut omettre les accolades. Ce qui donne :   
```php
<?php if ($monTest) echo 'Mon test est VRAI'; else echo 'Mon test est FAUX'; ?>
```

  
Attention à l’utiliser avec parcimonie car la lecture du code est plus difficile sous cette forme. Je le déconseille absolument. ## La forme étendue

Il arrive régulièrement d’utiliser ce IF, notamment dans les scripts de Vues (mêlant PHP et HTML). C’est très pratique pour ne pas mettre des ECHO partout.

```php
<?php if ($monTest) : ?> Mon test est VRAI <?php else : ?> Mon test est faux <?php endif; ?> 
```

## La forme ternaire(courte)

Souvent utilisée, parfois à tort, c’est la réduction du IF à l’extrême. Même si son utilisation peut être discutée, elle reste pratique pour ne pas surcharger le code PHP.

```php
 <?php echo 'Mon test est ' . ($monTest) ? 'VRAI' : 'FAUX'; ?&gt,
```

A noter que cette forme ternaire n’est absolument pas optimisée. Plus d’infos sur le blog de [Fabien Potencier (SF)](https://fabien.potencier.org/article/48/the-php-ternary-operator-fast-or-not).
