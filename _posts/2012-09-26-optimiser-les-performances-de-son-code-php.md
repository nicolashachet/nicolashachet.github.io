---
id: 1227
title: 'Optimiser les performances de son code PHP'
date: '2012-09-26T21:27:10+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1227'
permalink: /blog/developpement-php/optimiser-les-performances-de-son-code-php/
dsq_thread_id:
    - '1285642172'
image: /wp-content/uploads/2012/09/php.png
categories:
    - 'PHP'
tags:
    - 'Performances Web'
    - PHP
---

Quand une application PHP nécessite des **performances optimales**, il faut recourir à certaines mesures techniques d’optimisations. Il est souvent préférable de passer outre certaines bonnes pratiques. Cet article regroupe des astuces algorithmiques afin d’**optimiser les performances de son code PHP**. Si vous en avez d’autres, n’hésitez pas à commenter.

## Optimiser son code PHP

Voici les astuces pour **optimiser son code PHP** :

- supprimer les **include_once** et **require_once** de votre code  
    {% highlight php linenos %}  
    // Non optimisé  
    require_once ‘/php/core/class.php’;  
    // Optimisé  
    require ‘/php/core/class.php’;  
    {% endhighlight %}
- déclarer vos méthodes en **static** quand vous le pouvez
- utiliser des **chemins absolus** lors de vos inclusions (require, include, autoload)
- éviter les **expressions régulières**
- bannissez l’utilisation de **@** (masquer les erreurs)  
    {% highlight php linenos %}  
    // Non optimisé  
    @move_uploaded_file(‘D65edsqDDSQ’, ‘/tmp/file.csv’);  
    // Optimisé  
    move_uploaded_file(‘D65edsqDDSQ’, ‘/tmp/file.csv’);  
    {% endhighlight %}
- préférer `‘ à "`   
    {% highlight php linenos %}  
    // Non optimisé  
    echo "Je suis une chaine\\n";  
    // Optimisé  
    echo ‘Je suis une chaine’ . PHP_EOL;  
    {% endhighlight %}
- utilisez **echo**() plutôt que print()
- traquer et corriger les **erreurs PHP** (notice, deprecated, warning, etc.)
- n’utilisez **pas de fonction dans des boucles**  
    {% highlight php linenos %}  
    // A bannir absolument  
    for ($x=0; $x < count($array); $x++)  
    {% endhighlight %}
- évitez les **boucles imbriquées**
- évitez les **méthodes magiques** _get(), __set(), __call(), __autoload()
- évitez les **accesseurs** et **modifieurs** inutiles, préférez les paramètres de classes **public**  
    {% highlight php linenos %}  
    class dog {  
     public $name =";  public function setName($name) {  
     $this->name = $name;  
     }
    
     public function getName() {  
     return $this->name;  
     }  
    }  
    // Notice that setName() and getName() do nothing more than store and return the name property, respectively.  
    $rover = new dog();  
    $rover->setName(‘rover’);  
    echo $rover->getName();
    
    // Setting and calling the name property directly can run up to 100% faster, as well as cutting down on development time.  
    $rover = new dog();  
    $rover->name = ‘rover’;  
    echo $rover->name;  
    {% endhighlight %}
- tenez votre version de **PHP à jour**
- utilisez des gestionnaires de **cache** : memcached, APC, etc.
- évitez d’utiliser des **variables** **inutiles**  
    {% highlight php linenos %}  
    // Non optimisé  
    $description = strip_tags($_POST[‘description’]);  
    echo $description;  
    // Optimisé  
    echo strip_tags($_POST[‘description’]);  
    {% endhighlight %}
- décharger la mémoire en utilisant **unset**()
- utilisez **strtr**() plutôt que str_replace() ou preg_replace()
- utilisez le **switch/case**() plutôt que des if() multiples  
    {% highlight php linenos %}  
    // Non optimisé  
    if ($a < $b &amp;&amp; !$c) {} if ($a > $b &amp;&amp; !$c) {}  
    if ($a < $b &amp;&amp; $c) {} if ($a > $b &amp;&amp; $c) {}  
    // Optimisé  
    switch(true) {  
     case ($a < $b &amp;&amp; !$c): break; case ($a > $b &amp;&amp; !$c): break;  
     case ($a < $b &amp;&amp; $c): break; case ($a > $b &amp;&amp; $c): break;  
    }  
    {% endhighlight %}
- utilisez les **‘** lors des accès tableaux  
    {% highlight php linenos %}  
    $array[‘id’] /* plutôt que \*/ $array[id];  
    {% endhighlight %}
- évitez les variables globales
- préférer les pages **HTML** statiques aux scripts PHP
- vérifiez si les variables sont disponibles via **isset**() (si besoin)
- remplacez strlen($var) < 2 par **$var{2}**  
    {% highlight php linenos %}  
    // Non optimisé  
    if (strlen($var) < 2) { echo "var is too short"; }  
    // Optimisé  
    if (!isset($var{2})) { echo "var is too short"; }  
    {% endhighlight %}
- **++$i** et plus rapide que $i++
- n’abusez pas de la Programmation Orientée Objet (POO), le **procédural** est plus rapide
- utilisez le design pattern **singleton ou l’injection de dépendances**
- [utilisez du **cache**](https://blog.nicolashachet.com/gestion-de-caches/optimisation-web-php-des-caches-a-tous-les-niveaux/ "Optimisation Web PHP : des caches à tous les niveaux")
- utilisez du cache **!**
- utilisez du cache **!!!**

## Sources

- <https://prendreuncafe.com/blog/post/2006/11/22/12-astuces-optimisation-performances-php>  
- <https://developers.google.com/speed/articles/optimizing-php>  
- <https://phplens.com/lens/php-book/optimizing-debugging-php.php>  
- <https://www.chazzuka.com/63-best-practice-to-optimize-php-code-performances-58/>
