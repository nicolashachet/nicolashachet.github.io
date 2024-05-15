---
id: 140
title: 'Comment appeler une procédure stockée en CakePHP ?'
date: '2011-04-28T19:44:52+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=140'
permalink: /blog/developpement-php/comment-appeler-une-procedure-stockee-en-cakephp/
dsq_thread_id:
    - '1289722822'
categories:
    - 'PHP'
tags:
    - CakePHP
---

Les applications Web nécessitent parfois l’appel à des procédures stockées. CakePHP ne propose pas de mécanisme "magique" pour effectuer l’appel aux procédures stockées et aux fonctions MySQL. Il est cependant tout à fait possible de réaliser cette opération en utilisant du SQL classique.

### Exécuter une fonction et récupérer le résultat

Ici l’idée est d’appeler une fonction sur un modèle (peu importe lequel mais il est d’usage d’avoir un modèle en rapport avec les données) et de récupérer le résultat de son exécution, c’est tout simple :  
{% highlight php linenos %}  
$conditions = array(‘fields’ => array(‘MA_FONCTION_MYSQL("PARAM") as resultat’));  
$exec = $this->Model->find(‘first’, $conditions);  
$resultat = $exec[0][‘resultat’];  
{% endhighlight %}

$resultat contiendra ainsi le retour de votre fonction MySQL.

Il est également possible d’utiliser la fonction **query()** :  
{% highlight php linenos %}  
$exec = $this->Model->query(‘SELECT MA_FONCTION_MYSQL("PARAM") as resultat’);  
$resultat = $exec[0][‘resultat’];  
{% endhighlight %}

### Exécuter une procédure stockée

L’idée est la même pour les procédures stockées. Il est cependant nécessaire d’utiliser la clause CALL plutôt qu’un SELECT :  
{% highlight php linenos %}  
$exec = $this->Model->query(‘CALL MA_PROCEDURE_STOCKEE("PARAM")’);  
$resultat = $exec[0][‘resultat’];  
{% endhighlight %}

Dans ce cas, il n’est pas possible de récupérer de paramètres de sorties, contrairement aux fonctions MySQL.

Plus sur le sujet : [la documentation CakePHP sur la fonction **query()**](https://book.cakephp.org/view/1027/query)

[La documentation MySQL sur les procédures et fonctions](https://dev.mysql.com/doc/refman/5.0/fr/stored-procedure-syntax.html)
