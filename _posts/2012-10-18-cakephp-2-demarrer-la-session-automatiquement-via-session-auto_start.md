---
id: 1308
title: 'CakePHP 2 : démarrer la session automatiquement via session.auto_start'
date: '2012-10-18T11:26:14+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1308'
permalink: /blog/developpement-php/cakephp-2-demarrer-la-session-automatiquement-via-session-auto_start/
dsq_thread_id:
    - '1289217119'
categories:
    - 'PHP'
tags:
    - CakePHP
    - PHP
---

## La directive session.auto_start

**CakePHP 2.x** n’active plus la **session PHP** par défaut. Il vous faudra ainsi modifier les options de configuration afin de démarrer la session automatiquement. La directive **session.autostart** est là pour ça. Voici le code à placer dans votre fichier *bootstrap.php* :

{% highlight php linenos %}  
<?php  
Configure :: write(‘Session’, array(  
 ‘ini’ => arrray(  
 ‘session.auto_start’ => true  
 )  
));  
{% endhighlight %}

## Configurations par défaut

Par défaut, Cake propose des configurations "standards" : *php*, *cake*, *cache* et *database*. Vous les retrouverez dans la [classe CakeSession](https://niha.eu/Y8NR).  
Un petit exemple pour la config nommé ‘php’ :  
{% highlight php linenos %}  
<?php  
$defaults = array(  
 ‘php’ => array(  
 ‘cookie’ => ‘CAKEPHP’,  
 ‘timeout’ => 240,  
 ‘ini’ => array(  
 ‘session.use_trans_sid’ => 0,  
 ‘session.cookie_path’ => self::$path  
 )  
 )  
);  
{% endhighlight %}

Vous pouvez les surcharger sans problème :  
{% highlight php linenos %}  
<?php  
Configure::write(‘Session’, array(  
 ‘defaults’ => ‘php’,  
 ‘cookie’ => ‘my_app’,  
 ‘timeout’ => 4320 // 3 days  
));  
{% endhighlight %}

## Plus d’infos

Source de la [classe CakeSession](https://niha.eu/Y8NR)  
La manuel sur [les sessions CakePHP](https://niha.eu/L9TS)
