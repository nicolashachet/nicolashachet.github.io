---
id: 1658
title: 'POO : les interfaces en PHP'
date: '2013-02-19T10:58:17+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1658'
permalink: /blog/developpement-php/poo-les-interfaces-en-php/
dsq_thread_id:
    - '1285606827'
image: /wp-content/uploads/2013/02/Php-POO.jpg
categories:
    - 'PHP'
---

En programmation orientée objet (POO) et en PHP 5 en particulier, les **interfaces** définissent le **comportement publique d’une classe**. Les interfaces regroupent donc la **signature des méthodes** qui pourront être utilisées sur l’instance d’une classe. En implémentant une interface, une classe s’oblige à définir l’ensemble des méthodes de l’interface. Voici un exemple d’interface à une seule méthode :

{% highlight php linenos %}  
interface AuthenticationInterface {  
 public function authenticate($user);  
}  
{% endhighlight %}

Et une classe l’implémentant :

{% highlight php linenos %}  
class CustomAuthentication implements AuthenticationInterface {  
 public function authenticate($user) {  
 if ($user === ‘test’) {  
 return true;  
 }  
 }  
}  
{% endhighlight %}

Rien de plus simple puisqu’il s’agit uniquement de définir les méthodes spécifiées dans l’interface. A noter qu’une interface ne définit que des **méthodes publiques**. Logique puisqu’on définit le comportement publique…

Ce qui est intéressant c’est que les interfaces peuvent être utilisées comme type dans les méthodes. Ceci est tout à fait autorisé :

{% highlight php linenos %}  
public function uneMethode(AuthenticationInterface $authentication) { … }  
{% endhighlight %}

Du coup ça ouvre des perspectives intéressantes : **on n’est pas obligé de connaitre la classe d’un objet pour l’utiliser, on peut se contenter de connaitre l’interface qu’il implémente**.

## A quoi ça sert ?

Prenons l’exemple de l’authentification d’un utilisateur via plusieurs biais : formulaire de login / mot de passe, Twitter, Facebook ou autre. Pour factoriser son code d’authentification et **s’abstraire du type** d’authentification, on définit les classes suivantes :

**Interface** :

{% highlight php linenos %}  
interface AuthenticationInterface {  
 public function authenticate($user);  
}  
{% endhighlight %}

**Implémentations :**

{% highlight php linenos %}  
class FormAuthentication implements AuthenticationInterface {  
 public function authenticate($user) {  
 // Traitement du formulaire  
 }  
}

class FacebookAuthentication implements AuthenticationInterface {  
 public function authenticate($user) {  
 // Authentification via Facebook (OAuth)  
 }  
}

class TwitterAuthentication implements AuthenticationInterface {  
 public function authenticate($user) {  
 // Authentification via Twitter (OAuth)  
 }  
}  
{% endhighlight %}

**Manager :**

{% highlight php linenos %}  
class AuthenticationManager {  
 public function authenticate(AuthenticationInterface $authentication, $user) {  
 return $authentication->authenticate($user);  
 }  
}  
{% endhighlight %}

C’est un peu raccourci, mais l’idée est là. Dans nos services ayant besoin d’un mécanisme d’authentification, on utilise **le manager AuthenticationManager qui s’abstrait du type d’authentification** puisque qu’il prend en paramètre une classe implémentant l’interface AuthenticationInterface. **Cela lui garantit que la méthode authenticate() est disponible**.

Dans ce cas, il est possible d’améliorer le code en ajoutant une **factory** (fabrique d’objets). Ce design pattern est intéressant car il permet de récupérer des objets sans avoir à instancier directement la classe. Voici un petit exemple :

{% highlight php linenos %}  
class AuthenticationFactory {  
 public static get($authName) {  
 switch ($authName) {  
 case "form" :  
 return new FormAuthentication();  
 break;  
 case "facebook" :  
 return new FacebookAuthentication();  
 break;  
 case "twitter" :  
 return new TwitterAuthentication();  
 break;  
 }  
 }  
}  
{% endhighlight %}

Et ainsi dans notre manager, on peut également s’abstraire de la création des classes correspondant aux types d’authentification.  
**Nouveau manager :**

{% highlight php linenos %}  
class AuthenticationManager {  
 public function authenticate($authType, $user) {  
 return AuthenticationFactory :: get($authType)->authenticate($user);  
 }  
}  
{% endhighlight %}

**Utilisation dans un service :**

{% highlight php linenos %}  
$isAuthenticated = $this->get(‘authentication_manager’)->authenticate(‘twitter’, ‘Nicolas Hachet’);  
{% endhighlight %}

Au final, le code métier utilisant le manager AuthenticationManager a une vision de haut niveau : il ne sait pas quelles sont les classes utilisées ni comment est faite l’implémentation. Son seul besoin est d’authentifier un utilisateur en fonction d’un type donné.
