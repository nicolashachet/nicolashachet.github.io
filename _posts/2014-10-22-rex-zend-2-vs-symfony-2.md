---
id: 2393
title: 'Zend 2 vs Symfony 2 : sont-ils comparables ?'
date: '2014-10-22T12:35:22+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2393'
permalink: /blog/developpement-php/rex-zend-2-vs-symfony-2/
dsq_thread_id:
    - '3143551410'
image: /wp-content/uploads/2014/10/rex-zend2-symfony2-200x150.png
categories:
    - 'PHP'
tags:
    - PHP
    - Symfony
    - 'Zend Framework'
---

Dans le monde des **frameworks PHP**, **Zend** et **Symfony** sont deux références incontournables. L’un profite de sa gloire passée et tente de suivre le mouvement avec sa version 2, l’autre est à son apogée, avec une version 2 qui rencontre un joli succès.

Depuis 2011 et la sortie de SF 2.0, j’ai eu l’occasion de travailler sur Symfony et Zend en environnement professionnel. C’est ce qui m’incite aujourd’hui à proposer un retour d’expérience visant à comparer les différences entre ces deux frameworks. Alors, Zend et Symfony sont-ils comparables ?

## Retour d’expérience Zend 2 vs Symfony 2

Comparables, les frameworks le sont forcément. Encore faut-il trouver des critères de comparaison. Pour ce retour d’expérience, j’ai choisi arbitrairement 6 critères :

- Architecture
- Philosophie
- Simplicité d’apprentissage
- Documentation
- Communauté
- Stabilité

### Architectures

Nativement, **les deux architectures sont très proches** avec un dossier dédié à la configuration, un autre pour les sources applicatives, un autre pour le dossier web public et le répertoires des composants tiers. En passant de l’un à l’autre, on est dans la même structure. De ce coté là, pas de surprise : les approches sont similaires.

Si on rentre un peu plus dans le cœur du sujet, on constate toujours peu d’écart : quand Zend propose des *modules*, Symfony préfère les *bundles* ; quand Zend propose un dossier *public*, Symfony préfère un dossier *web*. Seul le dossier *vendor* fait l’unanimité mais, sur le fond, on est dans des architectures similaires.

Les modules / bundles intègrent l’ensemble des fichiers permettant de les rendre "autonomes" : configuration, assets, i18n, entités, services, vues.

### Philosophie

Philosophie est probablement un mot un peu pompeux pour définir leur approche. Reste que celle-ci est très proche dans Zend et Symfony : **le framework est un conteneur** qui permet d’organiser les développements. Point. Pour le reste, les composants ready-to-use sont proposés comme des librairies tierces.

Symfony et Zend se placent comme des chefs d’orchestre servant de guide aux développements et s’appuient sur des composants tiers pour bâtir une application. Symfony a particulièrement réussi cette approche en construisant son framework comme une multitude de **composants génériques indépendants**. A l’inverse, Zend garde des composants fortement "typés Zend" avec des *librairies* Zend_Form, Zend_Db, Zend_Cache, etc plutôt que des *composants* autonomes.

### Simplicité d’apprentissage

Dans les 2 cas, on se trouve en face d’un **framework complexe** qui nécessite un solide bagage en PHP ainsi qu’une bonne dose d’abstraction pour s’y retrouver. J’avais estimé la durée d’apprentissage de Symfony 2 pour atteindre une efficacité maximale à environ 3 mois, mon avis ne change pas pour Zend 2. Ces frameworks en version 2 sont clairement **orientés techniques**, avec des **concepts abstraits** poussés et ne peuvent pas être mis entre toutes les mains.

### Documentation

Que serait un framework sans sa documentation ? Pas grand chose et c’est là que les choses se gatent du coté de Zend. Autant en 2011 quand j’ai commencé sur Symfony 2, la documentation était parcellaire et il fallait s’accrocher, autant désormais la **documentation Symfony 2** est très bien faite. Complète, détaillée et illustrée d’exemples plutôt pertinents, ce que vous ne trouverez pas sur la doc officielle se trouvera facilement sur le net : articles techniques, blog, retours d’expériences, les sources sont légions.

D’autant plus que Symfony 2 a décidé d’orienter son framework "composant", se placant comme chef d’orchestre des composants plutôt que comme structure rigide. Ainsi, chaque composant est utilisable en **standalone** ou à l’intérieur de son **framework "standard edition"**. Du coup, la documentation couvre l’ensemble des usages et s’avère très complète.

Coté Zend, c’est la déception. La **documentation Zend 2** est peu clair, on n’y trouve pas grand chose, il y a peu d’exemple, bref c’est en chantier et ça se voit. Malheureusement l’utilisation du framework s’avère complexe sans cette aide précieuse. Dès lors que vous sortez de l’usage simple, accrochez-vous pour développer ce que vous voulez.

### Communauté

La différence de qualité entre les 2 documentations s’explique nécessairement par une communauté moins importante coté Zend. Symfony a clairement frappé fort en sortant une version 2 un peu balbutiante mais rencontrant l’adhésion des utilisateurs de PHP. Les défauts du début ont alors rapidement été gommés par une **communauté grandissante et hyperactive**.  
Phagocyté par Symfony, Zend semble peiner à rencontrer la même agitation autours de son framework, ce qui explique sans doute les errements documentaires.

### Stabilité

Je me sens forcé de faire un petit laïus sur la stabilité des frameworks car lors de mon expérience Zend 2, j’ai été confronté à quelques bugs et à des comportements plutôt étonnants, principalement sur la gestion des formulaires. Ces bugs rencontrés autant de temps après la sortie du framework m’ont paru étonnant et assez révélateurs d’un framework en manque de maturité. Pourtant [sorti il y a 2 ans]((https://framework.zend.com/blog/zend-framework-2-0-0-stable-released.html), ZF2 semble encore en phase de rodage.

A noter que j’avais rencontré des problèmes similaires sur Symfony lors des premiers mois d’utilisation.

## Un vainqueur en conclusion ?

Pour moi, [il n’y a pas de meilleur framework PHP](https://blog.nicolashachet.com/frameworks/non-il-ny-a-pas-de-meilleur-framework-php/ "Non, il n’y a pas de meilleur framework PHP"). Cela étant, on peut sans problème dire que **Symfony 2 est plus mature** que Zend 2, et que, même si cela reste un framework complexe, son utilisation est facilitée par une très bonne documentation et une communauté importante et active. La similarité entre les deux s’arrête à l’architecture et à la philosophie modulaire.

Le mieux est de vous faire votre opinion et je vous invite donc à télécharger les 2 releases et à tester les frameworks par vous même !
