---
id: 1588
title: 'A propos des tests unitaires automatisés'
date: '2013-01-18T10:56:00+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1588'
permalink: /blog/developpement-php/a-propos-des-tests-unitaires-automatises/
dsq_thread_id:
    - '1285642062'
image: /wp-content/uploads/2013/01/tests_unitaires_php_atoum_phpunit_simpletest.jpg
categories:
    - 'Développement'
tags:
    - PHP
    - Testing
---

# Les tests unitaires automatisés, c’est quoi ?

Les **tests unitaires automatisés (TUA)** sont une des composantes de l’outillage permettant de valider qu’une application répond aux exigences suivantes :

- Est-ce que mon application fonctionne ?
- Est-ce que mon application est stable ?
- Est-ce que mon application couvre mon besoin ?

Les TUA ne *répondent à aucune de ces questions* mais assurent le premier niveau de test qui permet de **valider qu’un composant fonctionne unitairement**.

Il existe différents tests : **unitaires, **d’intégration,** fonctionnels**. Chaque type de test est complémentaire et couvre un périmètre donné. Les tests unitaires sont la plus petite unité de test possible : il valide le bon fonctionnement d’un composant, d’une classe ou d’une fonction.

De manière très concrète, les TUA sont des fonctions ou des classes qui testent le résultat d’une fonction ou d’une classe en passant des données en entrée et en comparant les données en sortie. Si, en passant A j’obtiens B alors que j’attendais C, le test est faux. Au contraire, si en passant A j’obtiens C, le test est vrai.

Les tests sont donc faciles à écrire mais on entrevoit aisément **la complexité d’écrire des tests \*pertinents\* et la complexité de gérer un jeu de données cohérents.**

# Quels avantages ?

### Pouvoir tester à l’infini et facilement son code

Les tests sont travailleurs : qu’on les joue une ou mille fois, ils seront toujours d’accord et feront toujours leur travail de la même manière. Ils sont ainsi forts utiles dès qu’on ajoute, modifie ou supprime des fonctionnalités. Cela permet d’effectuer à minima une **validation de non-régression (VNR)**.

### Garantir le fonctionnement des briques logicielles de manière unitaire

Un test valide un fonctionnement. En listant tous les fonctionnements, il est possible de les couvrir complètement à l’aide de tests unitaires. En pratique, la couverture des tests automatisés est rarement complète (sauf pour les librairies distribuées). Cette couverture est doublement intéressante :

1. pour vérifier qu’un composant répond (qu’il réponde vrai ou faux)
2. pour vérifier qu’un composant répond de manière correcte

Toute la valeur ajouté des tests unitaires réside dans le choix des tests implémentés. Il est en effet intéressant de tester du code complexe alors que tester du code simple est généralement une perte de temps.

### Du code facile à écrire

Le troisième avantage des TUA est qu’ils sont faciles à écrire. Tout programmeur sait écrire un test. C’est, en définitive, aussi simple à écrire que la fonctionnalité elle-même. C’est ainsi que sont apparues de nouvelles méthodes de développements : les tests écrit avant le développement ou **TDD (Test Driven Development)**. Le concept est le suivant : puisque je connais les fonctions et méthodes à implémenter, pourquoi ne pas d’abord écrire le test qui valide le fonctionnement pour ensuite écrire le fonctionnement lui-même ? J’y reviendrai dans un article dédié.

# Quels inconvénients ?

Malheureusement, tout n’est pas si simple. Les tests automatisés ne sont pas la solution ultime aux bugs. La mise en place de TUA nécessitent en réalité des contreparties dont vous n’êtes peut être pas prêts à payer le prix…

### Croire que des tests OK garantissent une application stable

C’est là une erreur majeure. Les tests automatisés garantissent uniquement les composants testés unitairement. Il y a plusieurs choses qui ne sont pas pris en compte :

- **il ne peut pas y avoir 100% du périmètre fonctionnel couvert** par les tests automatisés. Pour des applications métiers, il est impossible d’écrire les tests correspondant à tous les fonctionnements. Imaginez testez toutes les structures conditionnelles imbriquées, toutes les fonctions, tous les enchaînements possibles…
- **les TUA ne garantissent pas que les composants fonctionnent ensemble**. Un code couvert à 100% par des TUA ne donnera pas forcément une application fonctionnelle. Ce niveau de test est pris en charge par les **tests d’intégration** : ils valident le fait que les composants fonctionnent correctement ensemble.
- les TUA ne garantissent pas que l’application répond aux besoins. C’est le rôle des **tests fonctionnels**.

### Ecrire des tests qui ne servent à rien

Ecrire un TUA est tellement simple qu’on oublie parfois leur objectif : **apporter une validation sur un fonctionnement complexe ou sensible**. Couvrir de tests une classe contenant des calculs simples n’apportent aucune valeur ajoutée et est donc une perte de temps.

{% highlight php linenos %}class Math {  
 public function somme($a, $b) {  
 return $a + $b;  
 }  
}{% endhighlight %}

Si vous écrivez un test unitaire automatisé pour cette fonction : vous n’avez rien compris.

### Maintenir le jeu de données (ou les fixtures)

Des tests sans données, c’est comme un parfum sans odeur : ça ne sert à rien. Les données et leur maintenance sont une des difficultés majeures des tests unitaires. La création du jeu de données initial est souvent complexe et fastidieuse. Par ailleurs, à chaque évolution du modèle de données, il faudra mettre à jour l’application, les tests unitaires \*et\* le jeu de données.

Ces éléments font que la maintenance des tests unitaires et fixtures prend du temps et constitue une **charge supplémentaire**.

### Coût d’écriture et de maintenance

Bien que difficile à chiffrer, le surcoût lié à l’écriture des TUA est important. Celui lié à leur maintenance l’est encore plus ! Le problème des tests est qu’ils nécessitent un investissement qui ne peut être récupéré qu’à long terme. Je considère qu’il représente à minima un **surcoût de 20% des charges de développements** sur des projets à engagement.

Ainsi, les tests automatisés sont à réserver à des domaines complexes ou sensibles. A titre d’exemple, les ajouts de TUA sur un moteur de calcul ou sur des fonctionnalités de paiement seront pertinents.

# Comment fait-on du test unitaire en PHP ?

Vous trouverez sur le Web de nombreux frameworks gratuits permettant de **tester unitairement votre code PHP**. Je vous propose ici une petite liste qui n’est pas exhaustive mais qui couvrira tous vos besoins :

- **[SimpleTest](https://simpletest.org/fr/)**

Exemple :  
{% highlight php linenos %}require_once(‘simpletest/autorun.php’);  
require_once(‘../classes/log.php’);

class TestOfLogging extends UnitTestCase {  
 function testLogCreatesNewFileOnFirstMessage(){  
 @unlink(‘/temp/test.log’);  
 $log = new Log(‘/temp/test.log’);  
 $this->assertFalse(file_exists(‘/temp/test.log’));  
 $log->message(‘Should write this to a file’);  
 $this->assertTrue(file_exists(‘/temp/test.log’));  
 }  
}  
{% endhighlight %}

- **[PHPUnit](https://www.phpunit.de/manual/3.8/fr/index.html)**

Exemple :  
{% highlight php linenos %}  
class PileTest extends PHPUnit_Framework_TestCase {  
 public function testerPushEtPop() {  
 $pile = array(); $this->assertEquals(0, count($pile));

 array_push($pile, ‘foo’);  
 $this->assertEquals(‘foo’, $pile[count($pile)-1]);  
 $this->assertEquals(1, count($pile));

 $this->assertEquals(‘foo’, array_pop($pile));  
 $this->assertEquals(0, count($pile));  
 }  
}  
{% endhighlight %}

- **[Atoum](https://github.com/atoum/atoum)**

Exemple :  
{% highlight php linenos %}namespace vendor\\project\\tests\\units;

require_once ‘path/to/mageekguy.atoum.phar’;

include ‘path/to/project/classes/helloWorld.php’;

use \\mageekguy\\atoum;  
use \\vendor\\project;

class helloWorld extends atoum\\test  
{  
 public function testSay()  
 {  
 $helloWorld = new project\\helloWorld();

 $this->string($helloWorld->say())->isEqualTo(‘Hello World!’)  
 ;  
 }  
}{% endhighlight %}

# Conclusion

Les **tests unitaires automatisés** sont un excellent moyen de **tester des composants** et de **valider leur bon fonctionnement**. Ils ne remplacent ni les tests unitaires manuels ni les tests d’intégration ni les tests fonctionnels mais permettent d’en alléger les charges et d’assurer un premier niveau de tests faciles à écrire et facile à rejouer.

Leur utilisation entraîne des contreparties, notamment des **surcoûts des développements**. Ainsi, il convient de bien réfléchir leur utilisation et de les réserver à des contextes nécessitant des taux de retours très faibles.
