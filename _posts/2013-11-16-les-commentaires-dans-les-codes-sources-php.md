---
id: 1891
title: 'Les commentaires dans les codes sources PHP'
date: '2013-11-16T12:24:20+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1891'
permalink: /blog/developpement-php/les-commentaires-dans-les-codes-sources-php/
dsq_thread_id:
    - '1970717281'
image: /wp-content/uploads/2013/11/code-source-php.png
categories:
    - 'PHP'
tags:
    - PHP
---

Dans le cadre de mon activité en [centre de service PHP](https://www.nicolashachet.com/blog/gestion-de-projets/ssii-et-centre-de-services-php/ "SSII et centre de services PHP"), je réalise régulièrement des **audits de codes sources** PHP. La **documentation** du code source (ie. les **commentaires**) est un des critères utilisés pour qualifier la **qualité** d’un code source. Il y a de nombreuses pratiques usitées, allant du code noyé à un code brut, vide de tout commentaire… La vérité se trouve probablement au *milieu.* En attendant de le trouver, je vous donne ici un avis *forcément subjectif* sur la question.

## Quel est le but d’un commentaire ?

Avant toute chose, précisons pourquoi le commentaire est utile. Le commentaire a 2 missions :

- Présenter le **service** que rend le script, la classe ou la fonction ;
- Indiquer le fonctionnement **technique**

Les commentaires sont donc destinés à plusieurs publics : des **profils techniques** bien sûr mais également des **profils "fonctionnels"** qui n’ont pas besoin de comprendre les implications techniques d’une librairie ou d’une classe métier.

Quand on écrit un commentaire, il est donc important de penser à soi, de penser à ceux qui pourraient reprendre le code mais également à ceux qui vont l’utiliser. Pour cela, il existe 4 niveaux de commentaire à utiliser dans un code source.

## Le commentaire de script

Ce commentaire de haut niveau prend la forme d’un PHPDoc au début du fichier. L’objectif est de présenter le contenu du fichier, la licence, la package, etc. Ainsi, il place le fichier PHP dans son contexte. Voici un exemple :

{% highlight php linenos %}  
/*\*  
 \* Ce fichier fait partie du projet BIDULE.  
 \*  
 \* Dans le cas où le fichier est complexe ou important, ne pas hésiter à donner des détails ici…  
 \*  
 \* @package bidule  
 \* @copyright 2013 Mon super copyright  
 \*/  
{% endhighlight %}

Ainsi, chaque fichier du projet BIDULE est clairement identifiable, de même que la licence de distribution et d’utilisation.

## Le commentaire de classe

Le commentaire de classe prend place juste au dessus de chaque classe et doit permettre :

- de comprendre l’utilité de la classe ;
- d’identifier le ou les auteurs.

Il prend la forme d’une docBlock PHP:

{% highlight php linenos %}  
/*\*  
 \* La classe Bidule permet de gérer le bidulage d’un projet.  
 \*  
 \* @author Toto <toto[@]toto.com>  
 \*/  
class Bidule  
{  
…  
}  
{% endhighlight %}

Il est possible de rentrer dans le détail du fonctionnement tout en gardant à l’esprit que chaque fonction est également commentée. Le commentaire de classe permet de comprendre le composant avec un haut niveau d’abstraction. C’est le commentaire de fonction qui décrit plus précisément chaque méthode disponible sur la classe. Ca tombe bien, on en parle juste après…

## Le commentaire de fonction

Ce commentaire est très important puisqu’il remplit plusieurs fonctions essentielles :

- il renseigne sur l’utilité de la fonction ;
- il décrit les paramètres attendus en entrée ;
- il décrit le type de résultat en sortie ;
- il indique les exceptions levées.

Bref, c’est un incontournable qui s’écrit en PHPDoc, par exemple :

{% highlight php linenos %}  
/*\*  
 \* Démarre une session de bidulage.  
 \*  
 \* @param boolean $intensive Flag de bidulage intensif  
 \* @param MyObject $myObject Instance de MyObject  
 \*  
 \* @throws MyBiduleNotFoundException  
 \*  
 \* @return array Un super tableau  
 \*/  
public function startBidulage($intensive, MyObject $myObject)  
{  
…  
}  
{% endhighlight %}

Ici, rien qu’en lisant le commentaire : on sait à quoi va servir la fonction, comment elle doit être paramétrée ainsi que les sorties possibles (retour ou exception). Bref, on a une vision de haut niveau et la lecture du code n’est pas nécessaire pour comprendre le fonctionnement. Les balises @param et @return sont particulièrement importantes sous certains IDE qui les utilisent pour pré-remplir le code via auto-complétion. Ne vous en privez donc pas !

## Le commentaire en ligne

Enfin, pour descendre au plus profond du code source, il est possible d’utiliser les commentaires en ligne qui prennent les formes suivantes :

{% highlight php linenos %}  
// Je suis un commentaire en ligne  
/*  
 \* Je suis aussi un commentaire en ligne  
 \*/  
{% endhighlight %}

Les commentaires en ligne peuvent être utilisés directement dans le code source pour indiquer des précisions techniques, à destination des développeurs qui devront lire ou reprendre le code, ou à soi même. Il peut s’agir d’un fonctionnement particulier, d’une précision sur telle utilisée plutôt que telle autre, etc. Il est important de les utiliser avec parcimonie tout en ayant bien conscience qu’ils sont parfois indispensables pour garder une trace des choix de codage.

## Un exemple complet…

Voici un fichier qui compile les différents exemples de cet article :  
**Fichier src/Bidule.php :**

{% highlight php linenos %}  
<!–?php <br ?–>/*\*  
 \* Ce fichier fait partie du projet BIDULE.  
 \*  
 \* Dans le cas où le fichier est complexe ou important, ne pas hésiter à donner des détails ici…  
 \*  
 \* @package bidule  
 \* @copyright 2013 Mon super copyright  
 \*/  
namespace Bidule;

use Bidule\\Exceptions\\MyBiduleNotFoundException;

/*\*  
 \* La classe Bidule permet de gérer le bidulage d’un projet.  
 \*  
 \* @author Toto <toto[@]toto.com>  
 \*/  
class Bidule  
{

 /*\*  
 \* Démarre une session de bidulage.  
 \*  
 \* @param boolean $intensive Flag de bidulage intensif  
 \* @param MyObject $myObject Instance de MyObject  
 \*  
 \* @throws MyBiduleNotFoundException  
 \*  
 \* @return array Un super tableau  
 \*/  
 public function startBidulage($intensive, MyObject $myObject)  
 {  
 // On est bien d’accord que ce code est bidon…  
 if ($intensive &amp;&amp; $myObject->isEmpty()) {  
 throw new MyBiduleNotFoundException(‘Argh, MyObject is empty’);  
 }

 /*  
 \* Attention, on construit un tableau statique.  
 \* Cette gestion pourrait être déportée dans un objet Blablabla->getScalarArray()  
 \*/  
 return array(  
 ‘toto’ => ‘bidule power’  
 );  
 }  
}  
{% endhighlight %}
