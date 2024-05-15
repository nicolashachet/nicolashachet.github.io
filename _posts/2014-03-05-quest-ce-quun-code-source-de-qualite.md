---
id: 1903
title: 'Qu&rsquo;est-ce qu&rsquo;un code source de qualité ?'
date: '2014-03-05T11:49:57+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1903'
permalink: /blog/developpement-php/quest-ce-quun-code-source-de-qualite/
dsq_thread_id:
    - '2363927034'

image: /wp-content/uploads/2014/03/code_source.jpg
categories:
    - 'Développement'
---

Le **code source** est l’ADN d’une application. Quand on regarde sous le capot d’un site Web ou d’un logiciel, on peut trouver tout et n’importe quoi. Parfois c’est la jungle et parfois tout est délicatement bien rangé. Qu’est-ce qui fait un **code source de qualité** ? 6 éléments de réponse.

## 1. Une architecture claire

Avant même de regarder le code source, l’**architecture technique des fichiers et des répertoires** indiquent si le code est qualitatif. Un bon découpage, par exemple MVC, permet de se retrouver facilement dans les fichiers et de séparer les logiques applicatives : récupération des données, contrôles, règles de gestion, présentation des données.

Au niveau **métier**, le découpage d’un projet est tout aussi important. Ainsi, il est très souvent utile d’utiliser la notion de **module, de plugin ou de bundle** (selon le [framework](https://blog.nicolashachet.com/technologies/php/pourquoi-utiliser-un-framework-php/ "Pourquoi utiliser un framework PHP ?")) afin de de regrouper des notions fonctionnelles proches.

## 2. Un code source documenté

Les[ commentaires phpDoc et en ligne](https://blog.nicolashachet.com/technologies/php/les-commentaires-dans-les-codes-sources-php/ "Les commentaires dans les codes sources PHP") jouent un rôle central dans la qualité d’un code source. Les commentaires sont l’un des indicateurs que je vérifie en premier pour avoir un aperçu de la qualité globale. La devise quand on commente : **ni trop, ni trop peu**. S’il y en a trop, le code sera noyé sous les informations inutiles ; s’il y en a trop peu, on ne comprend pas quel rôle il joue dans l’application et sa logique.

Certains affirment qu’un code clair ne nécessite pas de commentaire car il est lisible en l’état. Pour moi, <span style="text-decoration: underline;">c’est une erreur.</span> En effet, il est lisible au moment de l’écriture. Mais même un code simple peut devenir obscur dès lors qu’il est modifié, refactoré ou utilisé à des fins qui n’étaient pas forcément prévues au départ. Mon conseil est donc de commenter intelligemment et suffisamment pour pouvoir revenir dessus par la suite sans être obligé de relire entièrement le code source.

## 3. Des fonctions mutualisées

Un code source de qualité, c’est un code qui n’est pas dupliqué. La **factorisation du code** doit être à l’esprit des développeurs tout au long du processus de développement. Le code étant un bien commun à toute l’équipe, les conflits arrivent forcément et doivent être résolus au plus vite en réunissant 3 choses :

- une mise en place du projet avec une cartographie des composants ;
- une bonne communication entre les membres de l’équipe de développement ;
- des revues de code régulières.

<span style="line-height: 1.5em;">Pour éviter cette duplication, il n’y a pas de recette miracle : il faut **refactorer**. On peut penser une architecture très simple et claire au départ, mais un projet informatique n’étant pas figé, le besoin évoluera probablement et le code qui va avec également. </span>

## 4. Un code source compréhensible par tous

Le compréhension d’un code revêt 2 facettes : la lisibilité du code source et son découpage clair. Un code source est avant tout un texte que l’on peut aisément lire et aisément comprendre. La documentation joue un rôle important *mais pas uniquement*. Le **formatage du code source** est également un élément à prendre en compte. Il est plus simple d’appréhender un code correctement aéré, plutôt qu’un ramassis de lignes.

Pour cela, il existe les [recommandations PSR](https://blog.nicolashachet.com/technologies/php/quest-ce-que-les-recommandations-psr/ "Qu’est-ce que les recommandations PSR en PHP ?") éditées par le [FIG](https://blog.nicolashachet.com/technologies/php/quest-ce-que-le-php-framework-interoperability-group-fig/ "Qu’est-ce que le PHP Framework Interoperability Group (FIG) ?") que je vous invite à consulter pour en savoir plus.

## 5. Un code qui ne réinvente pas la roue

A quoi ça sert de développeur et re-développer systématiquement les mêmes fonctionnalités ? Routing, gestion des utilisateurs, récupération des données, il existe de nombreuses librairies qui font le job à votre place. Il suffit de vous brancher dessus. A mon sens, un code de qualité passe donc par l’[utilisation d’un framework](https://blog.nicolashachet.com/technologies/php/quel-framework-php-pour-2014/ "Quel framework PHP pour 2014 ?") ou, à minima, d’une [architecture standard type MVC](https://blog.nicolashachet.com/technologies/php/mvc-la-couche-metier-en-php/ "MVC : la couche métier en PHP") avec des composants tiers.

A noter que l’utilisation de composants tiers est à double tranchant… Autant une librairie éprouvée et maintenue rend bien des services, autant il ne faut pas s’enfermer dans une librairie qui ne fourni aucune assurance sur ses fonctionnalités, son ouverture aux extensions, sa maintenance… Dans ce cas, si une librairie vous est réellement utile, la bonne pratique est de privilégier le **fork**.

## 6. Un code source testé unitairement

Enfin, le dernier indicateur d’une code source de qualité est la couverture en [tests unitaires automatisés](https://blog.nicolashachet.com/methodes/a-propos-des-tests-unitaires-automatises/ "A propos des tests unitaires automatisés"). Bien qu’ils ne garantissent pas un code sans bug ni un code répondant aux besoins, les **TUA** permettent d’apporter un premier niveau de contrôle. Quand vous choisissez une librairie, préférez toujours une librairie contenant des tests unitaires. Quand vous développez, préférez toujours l’ajout de tests unitaires.

Voici donc 6 critères qui permettant d’appréhender la **qualité d’un code source PHP** (ou non). Si vous avez d’autres critères ou si vous souhaitez réagir, les commentaires sont ouverts !
