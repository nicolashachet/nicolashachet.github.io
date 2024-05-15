---
id: 543
title: 'CakePHP 2 : récupérer les requêtes exécutées dans un contrôleur ou un modèle'
date: '2012-01-27T11:20:00+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=543'
permalink: /blog/developpement-php/cakephp-2-recuperer-les-requetes-executees-dans-un-controleur-ou-un-modele/
dsq_thread_id:
    - '1288917660'
categories:
    - 'PHP'
tags:
    - CakePHP
---

En 2011, nous avions vu comment [récupérer les requêtes exécutées sous CakePHP 1](https://www.nicolashachet.com/blog/2011/05/24/niveaux/debutant/cakephp-recuperer-les-requetes-sql-executees-lors-du-traitement-dune-action/) lors du traitement d’une action. Aujourd’hui même combat mais sous Cake 2 !

Ainsi vous pouvez ajouter une fonction dans le fichier **AppModel** :  
{% highlight php linenos %}  
class AppModel extends Model {  
public function getQueries ()  
 {  
 $dbo = $this->getDatasource();  
 return $dbo->getLog();  
 }  
}  
{% endhighlight %}

Vous aurez alors la possibilité d’appeler la fonction **getQueries()** sur n’importe quel modèle. Ici, nous travaillons sur le modèle ‘Content’.  
 {% highlight php linenos %}  
debug($this->Content->getQueries()); exit;  
{% endhighlight %}

Ce qui provoque l’affichage suivant :  
  
Array  
(  
 [log] => Array  
 (  
 [0] => Array  
 (  
 [query] => SELECT \* FROM `contents` AS `Content` WHERE `Content`.`id` = 6 AND `Content`.`type` = 2 LIMIT 1  
 [affected] => 1  
 [numRows] => 1  
 [took] => 0  
 )  
 )  
)  

