---
id: 155
title: 'PHP : gérer les sessions PHP'
date: '2011-05-20T19:28:00+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=155'
permalink: /blog/developpement-php/php-gerer-les-sessions-php/
categories:
    - 'PHP'
---

Dans les développements PHP actuels, il est très fréquent d’utiliser le mécanisme des sessions afin de stocker des données utilisateurs. L’une des applications principale est la sauvegarde des données sur plusieurs écrans pour un enregistrement final. Je vous propose ici une petite classe tout simple permettant d’ajouter/modifier/supprimer des données en session.

## Le code PHP de la classe gérant les sessions

**Fichier Session.php**  
{% highlight php linenos %}  
/*\*  
 \*  
 \* Classe utilitaire permettant de gérer la session  
 \* @author Nicolas Hachet  
 \*  
 \*/  
class Session  
{

 /*\*  
 \*  
 \* Stocke une donnée en session  
 \*  
 \* @param $key  
 \* @param $value  
 \*/  
 public static function set ($key, $value) {  
 $_SESSION[$key] = serialize($value);  
 return true;  
 }

 /*\*  
 \*  
 \* Récupère une donnée de la sessin  
 \*  
 \* @param unknown_type $key  
 \*/  
 public static function get ($key) {  
 if (self :: check($key)) {  
 return unserialize($_SESSION[$key]);  
 } else {  
 return false;  
 }  
 }

 /*\*  
 \*  
 \* Vérifie qu’une données est présente en session  
 \*  
 \* @param $key  
 \*/  
 public static function check ($key) {  
 return isset($_SESSION[$key]);  
 }

 /*\*  
 \*  
 \* Supprime une donnée en session  
 \* @param unknown_type $key  
 \*/  
 public static function delete ($key) {  
 if (self :: check($key)) {  
 unset($_SESSION[$key]);  
 return !self :: check($key);  
 } else {  
 return false;  
 }  
 }

 /*\*  
 \*  
 \* Ajoute un message d’erreur en session  
 \*  
 \* @param $message  
 \* @param $type  
 \*/  
 public static function message($message = null, $type = null) {

 if (is_null($message) &amp;&amp; is_null($type)) {  
 return self :: get(‘messages’);  
 }

 self :: set(‘messages’, array($type => $message));  
 }  
}  
{% endhighlight %}

Il s’agit d’un code simple mais fiable. Les méthodes sont statiques ci qui n’implique aucune instanciation de la classe.
