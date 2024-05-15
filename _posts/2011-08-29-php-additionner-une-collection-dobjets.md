---
id: 230
title: 'PHP : additionner une collection d&rsquo;objets'
date: '2011-08-29T17:19:22+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=230'
permalink: /blog/developpement-php/php-additionner-une-collection-dobjets/
categories:
    - 'PHP'
---

Aujourd’hui un peu de code permettant d’additionner les valeurs d’une méthode de plusieurs objets. En d’autres termes **additionner une collection d’objets** suivant une fonction donnée.  
L’idée m’est venue suite à une question posée sur le [forum PHP France](https://forum.phpfrance.com/php-debutant/faire-somme-propriete-groupe-objet-t260177.html).

## Code de la classe

{% highlight php linenos %}
/*\*  
 \* Classe permettant d’additionner les valeurs d’une propriété d’un objet  
 \*/  
class AddObj {

 /*\*  
 \* Méthode privé utilisée pour réaliser la somme des objets  
 \* @param unknown_type $property  
 \*/  
 private static function _getValue($obj, $property) {  
 return $obj->$property();  
 }

 /*\*  
 \* Ajoute les propriétés d’une liste d’objets donnés  
 \* @param $array Le tableau contenant les objets  
 \* @param $property La propriété à utiliser pour effectuer l’addition  
 \*/  
 public static function add(Array $array, $property) {  
 return array_sum(array_map(array(__CLASS__, ‘_getValue’), $array, array_fill(0, count($array), $property)));  
 }

}{% endhighlight %}

Ainsi, il suffit de passer un tableau d’objets ainsi que la propriété à utiliser pour effectuer l’addition : la classe s’occupe du reste et vous renvoi le total.

**La méthode add() s’occupe d’effectuer l’opération pour vous**  
{% highlight php linenos %}$total = AddObj :: add($tab, ‘getValue’);{% endhighlight %}  
Dans ce cas, le tableau s’appelle $tab et contient des objets contenant une méthode getValue(). Peu importe leur type, l’important est qu’ils possèdent une méthode getValue().

## Code de test complet

{% highlight php linenos %}<?php

// Classe MonObj  
class MonObj {

 private $value = 0;

 public function __construct($value) { $this->value = $value; }  
 public function getValue() { return $this->value; }

}

/*\*  
 \* Classe permettant d’additionner les valeurs d’une propriété d’un objet  
 \*/  
class AddObj {

 /*\*  
 \* Méthode privé utilisée pour réaliser la somme des objets  
 \* @param unknown_type $property  
 \*/  
 private static function _getValue($obj, $property) {  
 return $obj->$property();  
 }

 /*\*  
 \* Ajoute les propriétés d’une liste d’objets donnés  
 \* @param $array Le tableau contenant les objets  
 \* @param $property La propriété à utiliser pour effectuer l’addition  
 \*/  
 public static function add(Array $array, $property) {  
 return array_sum(array_map(array(__CLASS__, ‘_getValue’), $array, array_fill(0, count($array), $property)));  
 }

}

// Tableau contenant les objets  
$tab = array(  
 new MonObj(4),  
 new MonObj(7),  
 new MonObj(1),  
 new MonObj(2)  
);

// Total  
echo AddObj :: add($tab, ‘getValue’);{% endhighlight %}

## Evolution du code

Ce code est perfectible car il n’effectue aucun contrôle sur les données passées ou sur la méthode à utiliser. Il est cependant très simple de le sécuriser et de l’améliorer.
