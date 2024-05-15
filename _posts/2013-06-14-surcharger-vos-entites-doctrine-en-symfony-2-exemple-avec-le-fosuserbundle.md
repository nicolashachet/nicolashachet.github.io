---
id: 1770
title: 'Surcharger vos entités Doctrine en Symfony 2, exemple avec le FOSUserBundle'
date: '2013-06-14T15:37:10+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1770'
permalink: /blog/developpement-php/surcharger-vos-entites-doctrine-en-symfony-2-exemple-avec-le-fosuserbundle/
dsq_thread_id:
    - '1401319106'
image: /wp-content/uploads/2013/06/doctrine.jpg
categories:
    - 'PHP'
tags:
    - PHP
    - Symfony
---

Voici un exemple montrant comment **surcharger une entité Doctrine en PHP**. Pour illustrer le propos, rien de tel qu’un cas concret : on va donc utiliser le FOSUserBundle, ami fidèle des utilisateurs de Symfony2. Dans notre cas de figure, on créé un bundle héritant du [bundle FOSUserBundle](https://github.com/FriendsOfSymfony/FOSUserBundle).

Pour hériter d’un bundle la méthode est la suivante :  
{% highlight php linenos %}  
\# Fichier src/NicolasHachet/UserBundle.php  
namespace NicolasHachet\\UserBundle;

use Symfony\\Component\\HttpKernel\\Bundle\\Bundle;

class NicolasHachetUserBundle extends Bundle  
{  
 public function getParent()  
 {  
 return ‘FOSUserBundle’;  
 }  
}  
{% endhighlight %}

Dans notre exemple, on souhaite utiliser l’entité User du FOSUserBundle en rendant l’email optionnel (par défaut, il est obligatoire). Pour cela, on va faire hériter notre objet User de l’objet User du FOSUSerBundle. On modifie ensuite les directives de l’objet père via l’**annotation AttributeOverrides**. Voici le code :

{% highlight php linenos %}  
\# Fichier src/NicolasHachet/UserBundle/Entity/User.php  
namespace NicolasHachet\\UserBundle\\Entity;

use FOS\\UserBundle\\Entity\\User as BaseUser;  
use Doctrine\\ORM\\Mapping as ORM;

/*\*  
 \* @ORM\\Entity  
 \* @ORM\\Table(name="fos_users")  
 \* @ORM\\AttributeOverrides({  
 \* @ORM\\AttributeOverride(name="email",  
 \* column=@ORM\\Column(  
 \* name = "email",  
 \* type = "string",  
 \* length = 255,  
 \* nullable = true  
 \* )  
 \* ),  
 \* @ORM\\AttributeOverride(name="emailCanonical",  
 \* column=@ORM\\Column(  
 \* name = "emailCanonical",  
 \* type = "string",  
 \* length = 255,  
 \* nullable = true  
 \* )  
 \* ),  
 \* })  
 \*/  
class User extends BaseUser  
{  
}  
{% endhighlight %}

Ici, on écrase les 2 colonnes *email* et *emailCanonical* en modifiant leur définition via les **annotations Doctrine**. Ainsi, on peut rendre l’email optionnel en indiquant "nullable = true".

Ceci est rendu possible car l’objet hérité (FOS\\UserBundle\\Entity\\User) est défini comme suit :  
{% highlight php linenos %}  
\# Fichier vendor/friendofsymfony/user-bundle/FOS/UserBundle/Entity/User.php  
namespace FOS\\UserBundle\\Entity;

use FOS\\UserBundle\\Model\\User as AbstractUser;

abstract class User extends AbstractUser  
{  
}  
{% endhighlight %}

Et la configuration Doctrine de l’entité FOS\\UserBundle\\Entity\\User ressemble à ça :  
{% highlight php linenos %}  
\# Fichier vendor/friendofsymfony/user-bundle/FOS/UserBundle/Resources/config/doctrine/User.orm.xml  
namespace FOS\\UserBundle\\Entity;

<?xml version="1.0" encoding="UTF-8"?>  
<doctrine-mapping xmlns="https://doctrine-project.org/schemas/orm/doctrine-mapping"  
 xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"  
 xsi:schemaLocation="https://doctrine-project.org/schemas/orm/doctrine-mapping  
 https://doctrine-project.org/schemas/orm/doctrine-mapping.xsd">

 <mapped-superclass name="FOS\\UserBundle\\Entity\\User">  
 // …  
 <field name="email" column="email" type="string" length="255" />  
 <field name="emailCanonical" column="email_canonical" type="string" length="255" unique="true" />  
 // …

 </mapped-superclass>

</doctrine-mapping>  
{% endhighlight %}

Le noeud XML important est le **mapped-superclass** qui indique qu’une entité peut être héritée. A ce sujet, je vous invite à lire la documentation sur l’[héritage Doctrine](https://docs.doctrine-project.org/en/latest/reference/inheritance-mapping.html).

Lors de la création de la base de données via un "php app\\console doctrine:schema:update –force", les champs email et emailCanonical seront désormais nullables, ce qui est bien le résultat attendu.

C’est tout ! L’héritage et la modification des propriétés de l’entité parente ne nécessitent pas plus de code. Si vous souhaitez créer une entité Doctrine héritable, l’annotation **MappedSuperclass** est utilisée comme ceci :

{% highlight php linenos %}  
\# Fichier : votre entité héritable

/*\*  
 \* @ORM\\MappedSuperclass  
 \*/  
class MonEntiteHeritableBase {  
 // …  
}

{% endhighlight %}

Vous savez maintenant comment hériter d’une entité Doctrine et comment vous pouvez modifier ses propriétés pour répondre à votre propres besoins.
