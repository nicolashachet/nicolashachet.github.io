---
id: 374
title: 'CakePHP 2.0 : liste des évolutions du framework'
date: '2011-11-27T16:22:23+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=374'
permalink: /blog/developpement-php/cakephp-2-0-liste-des-evolutions-du-framework/
dsq_thread_id:
    - '1285641159'
image: /wp-content/uploads/2011/11/cake-logo1.png
categories:
    - 'PHP'
tags:
    - CakePHP
    - PHP
---



[![](/wp-content/uploads/2011/11/cake-logo-150x150.png "cake-logo")](/wp-content/uploads/2011/11/cake-logo.png)CakePHP 2.0.0 est sorti le 16 octobre 2011. Avec cette première version stable de la branche 2.0, le framework apporte un lot considérable de changements et d’améliorations, parfois structurantes pour vos projets. Je liste ici **les principales évolutions structurantes du framework CakePHP v2**.

## Abandon du support de PHP 4 ; PHP 5.2.6 obligatoire

Ce n’est pas une mauvaise nouvelle : la rétro-compatibilité PHP4 est abandonnée. **CakePHP s’appuie désormais sur PHP 5.2.6 ou supérieur**. Le choix de ne pas s’appuyer sur PHP 5.3 (comme Symfony) est justifié par le fait que la communauté est actuellement plus active sur PHP 5.2. Le code prend cependant en compte une future évolution vers PHP 5.3 (notamment l’utilisation des namespaces). Un pari de l’équipe de développement qui ne souhaite pas aller plus vite que la musique en passant directement de PHP 4 à PHP 5.3.

Note : une excellente nouvelle pour les avant-gardistes qui sont déjà en PHP 5.4, **la version 2.0.3 de CakePHP est compatible avec PHP 5.4-rc1** ([en savoir +](https://bakery.cakephp.org/articles/lorenzo/2011/11/14/cakephp_2_0_3_out_of_the_oven)).

## Renommage des fichiers et répertoires

Afin de préparer CakePHP à une migration vers PHP 5.3 et notamment à l’utilisation des namespaces, les règles de nommage des fichiers et répertoires ont été revues. Ainsi,  
les noms de fichiers comme les noms de classes s’écrivent désormais en [notation CamelCase](https://fr.wikipedia.org/wiki/CamelCase). De même pour les répertoires, à l’exception des répertoires "tmp" et "webroot". Finis, donc, les underscores dans les noms de fichiers : *my_controller.php devient MyController.php*.

Seconde évolution : les types de composants (Component, Helper, Behavior, etc.) sont affichés dans le nom du fichier. Ainsi *session.php (Component) devient SessionComponent.php*. Ceci améliore la clarté du code et on s’y retrouve mieux dans l’arborescence.

## Suppression des alias de fonctions

Les fonctions "aliases" getMicrotime(), e(), r(), a(), aa(), up(), low(), params(), ife(), uses(), ont été supprimées au profit de leur équivalent en PHP. A bannir de vos projets donc.  
Dans le même esprit, la fonction de traduction __() n’effectue plus directement le echo, il faut forcer l’affichage via un *echo __(‘string’);*

## Ajout des classes CakeRequest et CakeResponse

La classe CakeRequest remplace une partie des traitements de routage et des fonctions liées aux paramètres de requête. Il n’est désormais plus possible d’accéder aux paramètres de requête via $this->params. Vous trouverez plus d’infos sur cette nouvelle classe sur le blog Mark Story : <https://mark-story.com/posts/view/the-cakerequest-object-in-cakephp-2-0> et sur [l’API de la classe CakeRequest](https://api20.cakephp.org/class/cake-request).

La classe CakeResponse, quant à elle, s’occupe de la réponse envoyée par le contrôleur. Plus d’infos sur le blog Mark Story : <https://mark-story.com/posts/view/cakeresponse-in-cakephp-2-0> et sur [l’API de la classe CakeResponse](https://api20.cakephp.org/class/cake-response).

Ces 2 classes sont désormais passées en paramètre des constructeurs des contrôleurs.

## La pagination extraite dans un composant

La fonction de pagination fait désormais partie des composants de Cake 2 via le PaginationComponent. Il est ainsi plus simple de l’étendre et de le personnaliser. Plus d’infos sur la [documentation CakePHP sur la pagination](https://book.cakephp.org/2.0/en/core-libraries/components/pagination.html)

## Gestion des exceptions

Plutôt que d’utiliser la méthode cakeError(), Cake 2 encourage à utiliser les exceptions PHP5. Ainsi cette fonction a été supprimée et une véritable gestion des exceptions a vu le jour. Une évolution radicale mais indispensable pour l’avenir du framework.

## Chargement des classes

Une nouvelle méthode fait son apparition : App :: uses(). A l’instar de l’instruction PHP 5.3 **use**, elle permet d’indiquer le chemin vers une classe à charger. App :: uses() prend 2 paramètres : le nom du composant (composants, helpeurs, contrôleurs, etc.) et le chemin dans l’arborescence CakePHP 2. On sent que l’équipe de développement prépare la migration vers PHP 5.3. 😉

## Conclusion

CakePHP 2.0 est donc bien une évolution majeure du framework. Un gros travail a été réalisé sur le code afin de le rendre compatible avec les dernières versions de PHP. L’influence de PHP 5.3 se fait largement sentir. On appréciera également la compatibilité PHP 5.4-rc1, ce qui en fait l’un des frameworks les plus avancés sur ce point.  
Un léger temps d’adaptation est à prévoir puisque des fonctionnalités importantes du framework ont été réécrites. C’était un passage obligé pour retrouver un framework performant, stable, évolutif et surtout en adéquation avec son temps.

En bonus, <b>la migration des applications en Cake 1.3 pourra être effectuée via un shell</b> : bien pensé !

[important]Vous retrouverez la liste complète des changements sur [le guide de migration de CakePHP 2.0](https://book.cakephp.org/2.0/en/appendices/2-0-migration-guide.html) (en anglais). Cet article en est d’ailleurs largement inspiré.[/important]
