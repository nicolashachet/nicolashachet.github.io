---
id: 1684
title: 'MVC : la couche métier en PHP'
date: '2013-04-09T14:12:22+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1684'
permalink: /blog/developpement-php/mvc-la-couche-metier-en-php/
dsq_thread_id:
    - '1285689854'
image: /wp-content/uploads/2013/04/mvc_business.jpg
categories:
    - 'PHP'
tags:
    - CakePHP
    - PHP
    - Symfony
    - 'Zend Framework'
---

En **PHP**, la **couche métier** est une **évolution du modèle MVC qui dissocie la** **logique technique et la logique fonctionnelle** (ie, les classes métier). Elle est parfois appelée, à tord à mon sens, **couche service.** Pour moi, les services peuvent être *techniques* ou *fonctionnels* et je préfère donc l’appellation de **couche métier** ou **service métier**. L’objectif de cette couche supplémentaire est de stocker le code métier de l’application en donnant au contrôleur un rôle de **coordination**.

## Représentation d’une couche métier

Le placement de la couche métier (ici en rouge, nommée **Business**) se situe entre la couche modèle et la couche contrôleur du modèle MVC. Elle se compose des **classes métiers** qui contiennent la logique applicative.


[![](/wp-content/uploads/2013/04/mvc_couche_service_metier.png "mvc_couche_service_metier")](/wp-content/uploads/2013/04/mvc_couche_service_metier.png)

*Notez que **le schéma est simplifié** pour ne pas être surchargé, notamment au niveau du modèle. Il se focalise sur le placement de la couche métier et n’a pas vocation à être exhaustif.*

### Fonctionnement théorique

1. Une requête arrive sur l’action du contrôleur.
2. Le contrôleur appelle le **service métier** qui réalise les traitements associés à l’action. Ce service métier pourra appelé N autre service selon ses besoins.
3. Un service métier peut appeler (ou non) la **couche modèle** si des interactions doivent être effectuées avec la base de données (récupération de données, mise à jour). Il peut également appelé des services techniques (ex : service d’envoi de mails).
4. La couche modèle interagit avec la **base de données** par l’intermédiaire d’une couche d’abstraction plus ou moins grande (ex : PDO pour être près de la base ; Doctrine ORM pour être plus abstrait).
5. L’application gère les données issues de la base de données via les notions **d’objets** (appelée entités en Symfony / Zend) ou de tableaux (par défaut en CakePHP).
6. Une fois remonté jusqu’au contrôleur, celui-ci appelle une **vue** pour l’affichage. La vue peut utiliser les données issues de la base, toujours par l’intermédiaire des entités (ou des tableaux en CakePHP). La vue peut être au format HTML, JSON, XML, etc.
7. La réponse est envoyée au client.

### Un peu de concret

Bon la théorie c’est bien mais avec un exemple on comprend mieux. Je vais utiliser le classique du produit ajouté au panier… Oui, c’est dans les vieux pots qu’on fait les meilleures crèmes !

1. Un client demande à ajouter un produit à un panier (exemple de requête : PUT /paniers/123/produit)
2. Le contrôleur appelle le service métier "panier > ajouter un produit par référence". Le service métier panier fait appel au service métier "produit" pour savoir si le produit est en stock.
3. Le service métier "produit" demande au modèle "produit" de vérifier si le produit est dispo.
4. Le modèle "produit" fait sa requête en base de données et retourne le nombre de produits dispos.
5. L’application renvoi le nombre de produit dispo sans passer par une entité (notez que c’est tout de même possible en utilisant une collection).
6. Une fois la vérification effectuée, le service panier fait appel au modèle "panier" pour ajouter le produit en base.
7. Si tout s’est bien passé (pas d’exception), le contrôleur récupère une vue JSON qui permettra de confirmer l’ajout du produit au client : "{‘msg’ : ‘Ok votre produit est bien ajouté au panier’}" .
8. La réponse est envoyée au client "HTTP 200 OK".

Notez bien que les services métiers ne correspondent pas forcément à des modèles physiques en base. Il est plus pertinent des les associer aux classes issues du **diagramme de classes** en conception UML.

## Quelques règles d’écriture

L’écriture d’une couche métier suit plusieurs règles :

- garder à l’esprit que cette couche est **purement métier**, il est donc déconseillé d’interagir directement avec le [*framework* utilisé](https://www.nicolashachet.com/blog/2013/04/05/technologies/php/pourquoi-utiliser-un-framework-php/ "Pourquoi utiliser un framework PHP ?"). Dans l’absolu, il devrait être possible de **changer de framework sans changer une ligne de code de la couche métier.** L’*injection de dépendances* est une réponse à cette problématique **;**
- la couche métier est organisée en **service métier** qui peuvent s’appeler les uns les autres, il est également possible d’appeler des **services techniques** (ex : envoi de mails, logs, etc.) ;
- les exceptions PHP apportent de la souplesse à la gestion des erreurs.

En théorie, tout ça fonctionne très bien. Dans la pratique, pour des applications complexes qui nécessitent de nombreux services, il est souvent nécessaire de passer par une **phase d’architecture technique** en **cartographiant les services métiers et techniques** de l’application.
