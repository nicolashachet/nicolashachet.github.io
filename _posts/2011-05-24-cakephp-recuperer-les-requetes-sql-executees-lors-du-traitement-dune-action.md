---
id: 158
title: 'CakePHP : récupérer les requêtes SQL exécutées lors du traitement d&rsquo;une action'
date: '2011-05-24T15:31:38+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=158'
permalink: /blog/developpement-php/cakephp-recuperer-les-requetes-sql-executees-lors-du-traitement-dune-action/
categories:
    - 'PHP'
tags:
    - CakePHP
---

CakePHP stocke toutes les requêtes SQL exécutées lors de l’appel d’une action dans un tableau qui se nomme "_queriesLog". Ce tableau est disponible sur n’importe quel modèle. Il est possible de renvoyer l’ensemble des requêtes SQL comme ceci :

**Fichier app/app_model.php**  
{% highlight php linenos %}  
public function geQueries ()  
 {  
 $dbo = $this->getDatasource();  
 return $dbo->_queriesLog;  
 }  
{% endhighlight %}

La fonction getQueries() peut alors être appelée sur un modèle.  
{% highlight php linenos %}  
debug($this->Model->getQueries());  
{% endhighlight %}

Par extension, vous pouvez seulement renvoyer la dernière requête SQL exécutée :  
{% highlight php linenos %}  
public function getQueries ()  
 {  
 $dbo = $this->getDatasource();  
 $logs = $dbo->_queriesLog;

 return end($logs);  
 }  
{% endhighlight %}
