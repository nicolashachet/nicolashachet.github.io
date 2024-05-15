---
id: 2289
title: 'Optimiser un traitement d&rsquo;import ou batch PHP'
date: '2014-08-05T12:27:00+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2289'
permalink: /blog/developpement-php/optimiser-un-traitement-dimport-ou-batch-php/
dsq_thread_id:
    - '2902083324'
image: /wp-content/uploads/2014/08/batch-php-windows-200x150.png
categories:
    - 'PHP'
tags:
    - 'Performances Web'
    - PHP
---

Après un petit détour par le [responsive design](https://blog.nicolashachet.com/ergonomie-design/les-frameworks-css-responsive-design/ "Les frameworks CSS responsive design"), retour à la technique avec un article sur **comment optimiser un import PHP** (ou un traitement batch). En effet, les imports de données sont des traitements bien particuliers qui nécessitent des techniques de développement spécifiques si vous souhaitez des **performances** acceptables. Tour d’horizon des règles à respecter pour optimiser vos traitements et imports PHP !

*Dans cette article je prends comme exemple un import basique d’articles liés à des catégories. Nous imaginons une règle de gestion simple :*

- *RG1 : la catégorie de l’article doit exister pour que la ligne soit importée, sinon la ligne est rejetée.*

## Gare aux boucles…

Qui dit import, dit **boucle** permettant d’appliquer un ensemble de règles et de traitements sur les données en entrée : fichier texte, import XLS, flux XML. Les boucles, qu’il s’agisse de structure **while**, **for** ou **foreach,** sont un des fondamentaux de l’informatique mais constituent des pièges dès lors que votre code nécessite de bonnes performances. En effet, nous sommes souvent concentrés sur le traitement à effectuer, et on oublie parfois que le code PHP écrit à l’intérieur des boucles sera exécuté autant de fois que la boucle. Et ça peut conduire à des performances catastrophiques ! Il est donc nécessaire d’analyser en détail les traitements effectués dans chaque boucle pour maîtriser les performances. C’est ce que nous allons voir ci-après.

Pour illustrer ceci, voici un exemple d’import parfaitement fonctionnel mais non optimisé (pseudo code) :

{% highlight php linenos %}  
<?php  
$file = new File(‘mes_articles.csv’);  
while ($ligne = $file->readLine()) {

 $ligneValide = true; // Optimiste

 // RG1  
 // Requête vers la base  
 if (!$categorie->codeExiste($ligne->categorieCode)) {  
 $ligneValide = false;  
 }

 // Ligne OK  
 if ($ligneValide) {  
 // Enregistrement en base  
 $this->Article->save($ligne);  
 }  
}  
{% endhighlight %}

Cet exemple peut sembler correct au premier abord mais on va voir qu’il peut être nettement optimisé !

## Supprimer les requêtes des boucles

La première règle est de supprimer autant que possible les requêtes vers la base de données. En effet, une requête placée dans une boucle sera exécutée autant de fois que la boucle sera appelée : si vous importez 10 lignes, elle sera exécutée 10 fois, si c’est 100000 lignes, ce sera 100000 fois ! Ça peut monter très vite et c’est généralement un désastre pour les **performances de votre import de données**. Il n’est bien sûr pas possible de supprimer toutes les requêtes des boucles. Mais nous allons voir une technique permettant d’éviter les requêtes inutiles juste après.

## Préparer les données référentielles avant la boucle

Pour éviter les requêtes dans les boucles, il est possible de **préparer les données** qui seront utilisées dans la boucle avant celle-ci. Ainsi, la requête est exécutée une seule fois et le nombre d’exécution de la requête ne sera pas dépendant du nombre de données traitées. Cette technique est particulièrement pertinente quand on travaille avec les données référentielles et avec des données qui n’évoluent pas au cours du traitement.

Voici un exemple qui prépare les données référentielles en amont du traitement:

{% highlight php linenos %}  
$file = new File(‘mes_articles.csv’);

// Préparation des catégories en amont de la boucle  
$categories = $categorie->getAll();  
// Tableau $categories de la forme array(‘CATEGORIE1’, ‘CATEGORIE2’, etc.)

while ($ligne = $file->readLine()) {

 $ligneValide = true; // Optimiste

 // RG1  
 // Vérification de la catégorie  
 if (!in_array($ligne->categorieCode, $categories) {  
 $ligneValide = false;  
 }

 // Ligne OK  
 if ($ligneValide) {  
 // Enregistrement en base  
 $this->Article->save($ligne);  
 }  
}  
{% endhighlight %}

On a supprimé l’appel à la base de données dans la boucle, on évite ainsi de nombreuses requêtes avec un gain considérable à la clef. Mais on pourrait encore faire mieux…

## Supprimez les in_array()

En effet, quand on développe des règles de gestion, on a souvent tendance à utiliser l’instruction **in_array**() car elle simple à lire et à comprendre. Cependant, cette fonction PHP est particulièrement **coûteuse en temps d’exécution** car ce temps dépend du nombre d’entrée dans le tableau pointé par la fonction. Lors d’un appel à in_array, le système parcours tout le tableau à la recherche de la valeur pointée.

Il existe une solution bien plus performante : la fonction **isset**(). En effet, en utilisant isset sur une clef de tableau, on ne parcourt plus le tableau en entier pour rechercher une valeur, mais on détecte la présence d’une clef, ce qui est quasi instantané !

A noter que pour l’avoir expérimenté récemment, le gain est monstrueux, même sur de petits imports de quelques milliers de lignes ! On peut facilement perdre plusieurs dizaines de secondes sur moins de 20000 lignes..

Notre exemple peut ainsi être réécrit de la sorte :

{% highlight php linenos %}  
<?php  
$file = new File(‘mes_articles.csv’);

// Préparation des catégories en amont de la boucle  
$categoriesOptimized = array_flip($categorie->getAll());  
// Tableau $categoriesOptimized de la forme array(‘CATEGORIE1’ => null, ‘CATEGORIE2’ => null, etc.)

while ($ligne = $file->readLine()) {

 $ligneValide = true; // Optimiste

 // RG1  
 // Vérification de la catégorie  
 if (!isset($categoriesOptimized[$ligne->categorieCode])) {  
 $ligneValide = false;  
 }

 // Ligne OK  
 if ($ligneValide) {  
 // Enregistrement en base  
 $this->Article->save($ligne);  
 }  
}  
{% endhighlight %}

## Insérez vos données en masse ou par lot

L’enregistrement des données est généralement la finalité d’un import. Souvent on a tendance à enregistrer ligne à ligne : c’est une erreur. En effet, l’**enregistrement par groupe de lignes** (ou par lot) est bien plus performant car il évite les allers/retours incessant avec la base de données.

Finalement, notre traitement peut avantageuse être écrit de la sorte :

{% highlight php linenos %}  
<?php  
$file = new File(‘mes_articles.csv’);  
$imports = array();

// Préparation des catégories en amont de la boucle  
// On passe le champ à vérifie en tant que clef  
$categoriesOptimized = array_flip($categorie->getAll());

while ($ligne = $file->readLine()) {

 $ligneValide = true; // Optimiste

 // RG1  
 // Vérification de la catégorie  
 if (!isset($categoriesOptimized[$ligne->categorieCode])) {  
 $ligneValide = false;  
 }

 // Ligne OK  
 if ($ligneValide) {  
 $imports[] = $ligne;  
 }  
}

// Enregistrement par lot de ligne  
$this->Article->saveAll($imports);  
{% endhighlight %}

Ainsi, en conservant un nombre de lignes de code constant, on vient d’optimiser un import qui aurait pu prendre des dizaines de secondes…

## N’utilisez pas d’ORM !

Enfin, dernier conseil avant de partir, n’oubliez pas que les ORM comme Doctrine par exemple ne sont absolument pas conçus pour **effectuer des traitements lourds**. Voici d’ailleurs une extrait de la documentation Doctrine :

{% highlight text %}
> An ORM tool is not primarily well-suited for mass  
> inserts, updates or deletions. Every RDBMS has its own, most  
> effective way of dealing with such operations and if the options  
> outlined below are not sufficient for your purposes we recommend you use the tools for your particular RDBMS for these bulk operations.
{% endhighlight %}


https://docs.doctrine-project.org/en/2.0.x/reference/batch-processing.html
Oubliez donc les traitements batchs ou d’import utilisant Doctrine et passez directement par votre SGBD.
