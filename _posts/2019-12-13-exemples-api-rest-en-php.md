---
id: 3540
title: 'Exemples d&rsquo;API REST en PHP'
date: '2019-12-13T09:53:13+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=3540'
permalink: /blog/developpement-php/exemples-api-rest-en-php/
dsq_thread_id:
    - '7762053508'
image: /wp-content/uploads/2012/06/api-rest-architecture-700x248.png
categories:
    - 'PHP'
tags:
    - API
---

J’ai déjà abordé la **conception d’API REST**, et notamment les [5 règles pour structurer votre API REST](https://www.nicolashachet.com/blog/developpement-php/larchitecture-rest-expliquee-en-5-regles/). Plutôt que de vous présenter une énième fois des concepts théoriques, cet article liste plusieurs **exemples d’implémentations d’API REST en PHP** avec les repos Github qui vont bien pour aller s’inspirer !

## Qu’est-ce qu’une API REST ?

Succinctement, une API REST est une **application qui expose des ressources** via les URL avec lesquelles il est possible d’interagir. REST s’appuie sur le protocole HTTP pour décrire les **actions à réaliser sur les ressources** : GET, POST, PUT et DELETE pour récupérer, créer, modifier ou supprimer une ressource.

Ainsi, les actions suivantes permettront d’opérer des actions sur les enregistrements en base de données.

```
GET /contrats              -> Récupère tous les contrats
POST /contrats             -> Crée un contrat 
GET /contrats/12           -> Récupère le contrat identifié par 12
PUT /contrats/12           -> Modifie le contrat 12  
DELETE /contrats/12        -> Supprime le contrat 12
```

A noter que les routes exposées et le stockage en base de données peuvent être corrélés ou décoréllés. Si vous exposer une ressource "contrats", vous pouvez avoir une table "contrats" mais ce n’est pas automatique.

## Comment développe-t-on une API REST en PHP ? 

Pour exposer votre API, vous avez plusieurs solutions :

- partir de zéro et développer à la main votre **solution maison**
- utiliser un bundle par exemple **[FOSRestBundle](https://symfony.com/doc/master/bundles/FOSRestBundle/index.html)**
- utiliser un framework complet comme **[APIPlatform](https://api-platform.com/)**

Je vous déconseille de partir sur un développement spécifique. Les API REST sont fortement normées et l’utilisation d’une librairie comme ApiPlatform permet d’embarquer nativement la gestion des routes, la sécurité JWT ou OAuth, le versionning, la pagination, la validation, la documentation associée Swagger/OpenAPI, etc.

## Exemples d’API REST en PHP

Rentrons dans le cœur du sujet avec des exemples de codes PHP qui vous permettrons de développer rapidement votre API REST !

### [ApiPlatform Demo](https://github.com/api-platform/demo/tree/master/api)

Commençons avec le repo Github de démonstration d’Api Platform. Autant aller se servir à la source ! Trois choses à retenir.

Tout d’abord, la configuration d’API Platform dans le fichier **config/packages/api_platform.yaml**. Celle-ci décrit la configuration de votre API : les formats (JSON, XML, YAML, …), la gestion du cache, la pagination, la gestion de la documentation, etc.

```
api_platform:
    mapping:
        paths: ['%kernel.project_dir%/src/Entity']
    title: API Platform's demo
    version: 1.0.0
    description: |
      This is a demo application of ...
    formats:
		jsonld: ['application/ld+json']
        jsonhal: ['application/hal+json']
        jsonapi: ['application/vnd.api+json']
...
```

Ensuite, le routing déclaré par le code suivant dans le fichier **config/routes/api_platform.yaml** .

```
 api_platform:
    resource: .
    type: api_platform 
```

Enfin, la configuration de la ressource sur les entités, notamment l’annotation **ApiResource**. Ici, l’entité Book qui représente un livre.

```
/**
 * A book.
 *
 * @see https://schema.org/Book Documentation on Schema.org
 *
 * @ORM\Entity
 * @ApiResource(
 *     iri="https://schema.org/Book",
 *     normalizationContext={"groups": {"book:read"}},
 *     mercure=true,
 *     itemOperations={
 *         "get",
 *         "put",
 *         "patch",
 *         "delete"={"security"="is_granted('ROLE_ADMIN')"},
 *     },
 * )
 * @ApiFilter(PropertyFilter::class)
 * @ApiFilter(OrderFilter::class, properties={"id", "title", "author", "isbn", "publicationDate"})
 */
class Book
{...}
```

Remarquez également la présence de l’annotation **ApiFilter**. Celle-ci permet de configurer des comportements de l’API. Exemple : **PropertyFilter** ajoute la possibilité de sélectionner en entrée d’API les propriétés de l’objet à sérialiser en sortie. **OrderFilter** permet de trier selon la propriété sélectionnée. Il existe de nombreuses possibilités que je vous invite à découvrir sur la [documentation des filtres](https://api-platform.com/docs/core/filters/).

Et voilà, il ne faut pas plus de code pour exposer une API : pas de contrôleur, pas de repository… Vous écrivez uniquement le code utile à vos besoins métiers. Malgré tout, ApiPlatform propose des fonctionnalités extrêmement puissantes.

### [FOSRestBundleByExample](https://github.com/sdiaz/FOSRestBundleByExample)

On continue avec le repo de démonstration de **FOSRestBundle**. Attention cependant, le **dernier commit date de 2015** et l’application de démo tourne en Symfony 2.6… Légèrement obsolète, mais toujours intéressant sur le principe. Le [FOSRestBundle reste compatible avec Symfony 4 et 5](https://stackoverflow.com/questions/51343691/symfony-4-fosrestbundle).

Dans cet exemple, j’attire votre attention sur la configuration des contrôleurs :

```
/**
 * Return the overall user list.
 *
 * @Secure(roles="ROLE_API")
 * @ApiDoc(
 *   resource = true,
 *   description = "Return the overall User List",
 *   statusCodes = {
 *     200 = "Returned when successful",
 *     404 = "Returned when the user is not found"
 *   }
 * )
 *
 * @return View
 */
public function getUsersAction()
{
	$userManager = $this->container->get('fos_user.user_manager');
	$entity = $userManager->findUsers();
	if (!$entity) {
		throw $this->createNotFoundException('Data not found.');
	}
	$view = View::create();
	$view->setData($entity)->setStatusCode(200);
	return $view;
}
```

Tout est centralisé au niveau de contrôleur :

- la **sécurité** gérée via le *JMSSecurityExtraBundle*. Symfony 4 (et 5) possède désormais une annotation **IsGranted** que je vous invite à approfondir sur [la documentation dédiée à la sécurité](https://symfony.com/doc/current/security.html#securing-controllers-and-other-code).
- la **documentation**. On reconnait l’annotation *ApiDoc* fournie par le [NelmioApiDocBundle ](https://github.com/nelmio/NelmioApiDocBundle)(également utilisé par ApiPlatform soit dit en passant).
- la **vue** qui constituera la réponse applicative.
- le **code métier** de l’action qui répond.

### [RestServer](https://github.com/jacwright/RestServer)

Cette fois, je vous propose une librairie permettant d’**implémenter une API REST très légère**, le tout sans framework. La librairie fonctionne grâce à deux mécanismes.

Premièrement, le chargement de la librairie et sa **configuration** dans le fichier principal (index.php).

```
require __DIR__ . '/../source/Jacwright/RestServer/RestServer.php';
require 'TestController.php';
$server = new \Jacwright\RestServer\RestServer('debug');
$server->addClass('TestController');
$server->addClass('ProductsController', '/products');
$server->handle();
```

Deuxièmement, la configuration du routing en annotation sur le contrôleur.

```
/**
 * Gets the user by id or current user
 *
 * @url GET /users/$id
 * @url GET /users/current
 */
public function getUser($id = null)
{
	if ($id) {
	    $user = User::load($id); // possible user loading method
	} else {
	    $user = $_SESSION['user'];
	}
	return array("id" => $id, "name" => null); // serializes object into JSON
}
```

Et c’est tout : simple et efficace. En 2 fichiers, vous avez une API REST. Reste quand même à gérer l’authentification, le versionning, la documentation, la pagination, etc. 😉

### [Rest Api Slim PHP](https://github.com/maurobonfietti/rest-api-slim-php)

Dernier exemple, un exemple d’API basée sur [Slim](https://www.slimframework.com/), un micro-framework PHP qui utilise la notion de middleware. Ici, la mise en oeuvre en un peu plus verbeuse mais a le mérite d’être explicite.

Le routing est déclaré formellement en PHP dans un fichier **App/Routes.php**.

```
$app->get('/', 'App\Controller\DefaultController:getHelp');
$app->get('/status', 'App\Controller\DefaultController:getStatus');
$app->post('/login', 'App\Controller\User\LoginUser');
$app->group('/api/v1', function () use ($app) {
    $app->group('/tasks', function () use ($app) {
        $app->get('', 'App\Controller\Task\GetAllTasks');
        $app->get('/[{id}]', 'App\Controller\Task\GetOneTask');
        $app->get('/search/[{query}]', 'App\Controller\Task\SearchTasks');
        $app->post('', 'App\Controller\Task\CreateTask');
        $app->put('/[{id}]', 'App\Controller\Task\UpdateTask');
        $app->delete('/[{id}]', 'App\Controller\Task\DeleteTask');
    })->add(new App\Middleware\AuthMiddleware($app));
```

Chaque action de contrôle est ensuite déclinée dans une **classe séparée**. Ici, la création d’une tâche.

```
class CreateTask extends BaseTask
{
    public function __invoke(Request $request, Response $response, array $args): Response
    {
        $input = $request->getParsedBody();
        $task = $this->getTaskService()->createTask($input);
        return $this->jsonResponse($response, 'success', $task, 201);
    }
}
```

Voilà le cœur de l’API. L’implémentation complète nécessite un peu plus de code pour fonctionner : services et repositories, notamment.

## Conclusion

J’espère que vous aurez trouvé votre bonheur pour construire votre API REST. Nous avons vu 4 approches différentes :

- Api Platform,
- FosRestBundle,
- un développement spécifique basé sur le microframework Slim
- et enfin un développement complètement spécifique

A vous de choisir ce qui vous convient le mieux !

N’hésitez pas à [commenter l’article](#disqus_thread) ou à me [contacter](https://www.nicolashachet.com/blog/contact/) pour présenter une meilleure solution.
