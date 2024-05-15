---
id: 2830
title: 'Quels outils pour développer en PHP sous Windows ?'
date: '2017-06-08T16:47:02+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2830'
permalink: /blog/developpement-php/outils-developper-php-windows/
dsq_thread_id:
    - '5891655402'
image: /wp-content/uploads/2017/06/outil-developpement-php-677x427.jpg
categories:
    - 'PHP'
tags:
    - PHP
---

Les outils liés à la conception et aux développements informatiques sont légions. La composition de son **environnement de travail**  est très importante puisque de la performance des outils dépendent la productivité et l’efficacité du développeur. Que vous ayez déjà vos outils ou que vous soyez en recherche des vôtres, cet article liste les principaux outils que j’utilise pour **développer en PHP sous Windows**.

C’est la **liste des logiciels gratuits et payants qui constituent mon poste de développement**. N’hésitez pas à décrire vos outils de développement en commentaire, que vous soyez sous **Windows**, sous **Mac** ou sous **Unix**.

## Logiciels gratuits et payants pour développer sous Windows

### Cmder

Invite de commande ou plus précisément émulateur de console, cet outil permet d’afficher plusieurs consoles à l’écran en mode split, de créer des alias personnalisés et propose un design plutôt sympa. Les options de configuration sont nombreuses, on peut noter la possibilité de créer des groupes de consoles paramétrées selon vos besoins.

### Notepad++

Éditeur de texte incontournable. Très pratique pour ouvrir tout type de documents. Pour de gros fichiers, j’utilise `vi` sous Unix ainsi que tous les commandes permettant d’éditer un fichier sans l’ouvrir (`sed` pour effectuer des modifications, `zcat | sed | mysql` pour modifier des dumps à la volée notamment).

### PHPStorm

Développé par jetBrains, PHPStorm est l’IDE dédié à PHP. C’est actuellement l’IDE le plus performant du marché avec des plugins puissants permettant de simplifier le développement, le déploiement, l’accès aux bases de données… PHPStorm ouvre l’ensemble de vos fichiers : PHP, Twig, Javascript, HTML, bash, tpl, etc. et propose des fonctions riches d’édition, refactoring, navigation. Par ailleurs, il intègre nativement des outils très utiles : GIT compare, déploiement de sources, administration de base de données, historique local, etc.

## mRemoteNG

Gestionnaire de terminal, mRemoteNG supporte différents protocoles (RDP, Telnet, SSH, rlogin, HTTP, etc.). Il permet de sauvegarder les mots de passe et supporte les onglets. Bref, indispensable pour remplacer Putty.

### WinSCP

WinSCP est un client FTP et SFTP qui stocke également les mots de passe. Son gros avantage est de supporter les tunnels SSH ainsi que différents type de shell : *bash*, *ksh* et *sudo su -.*

### XAMPP / Wamp

Le serveur Web est la pierre angulaire de votre développement local. J’utilise personnellement XAMPP et WAMP. Ces deux outils sont très similaires et proposent une stack **Apache, PHP, MySQL pour Windows**.

### SQLYog

Quand il s’agit d’accéder aux bases de données, phpMyAdmin a ses limites, phpStorm aussi. Pour combler ce manque, SQLYog est l’allier parfait du développeur MySQL. Il permet de se connecter aux bases de données via un tunnel SSH et propose 2 outils de copie et synchronisation de bases de données qui peuvent vite devenir addictifs.

### MySQL Workbench

Quand il s’agit de concevoir une base de données MySQL, MySQL Workbench est idéal. Malgré sa lourdeur, je n’ai pour l’instant pas trouver mieux pour designer les bases de données et les synchroniser avec un serveur MySQL. Il permet également de faire du reverse engineering sur une base existante.


### Suite Office Word, Excel, Power Point

Ça peut paraître idiot, mais la suite Office est quasiment indispensable pour les développeurs. Deux raisons à cela :

1. elle permet de lire les documents de spécifications, cahier des charges, expression de besoin, etc.
2. elle permet également de tester les exports ou génération de fichier DOC, DOCX et surtout XLS, XLSX. Quand on a développé des exports Excel complexes, on sait qu’un Libre Office ne peut pas remplacer Excel pour les tests.

### Chrome, Firefox, IE, Safari

En tant que développeur Web, il est évident qu’il convient de tester ses développements sur l’ensemble des navigateurs cibles. Il est donc nécessaire d’installer à minima les navigateurs Chrome, Firefox et Internet Explorer (Edge). A noter que pour Safari, j’emprunte le Mac Book Pro de ma femme… En effet, la version Windows s’est arrêtée à Safari 5 et n’est plus supportée depuis plusieurs années.

### Redis Desktop Manager

Pour aller voir ce qu’il se passe sous le capot de Redis, Redis Desktop Manager est l’utilitaire parfait. Il permet simplement d’aller consulter les clefs d’une base sans possibilité de les modifier.

### NodeJS

J’utilise NodeJS de deux manières :

1. Pour effectuer des développements sous Node, par exemple pour tout ce qui est développement de chatbots ;
2. Comme langage de programmation utilitaire. NodeJS fourmille d’outils à destination des technologies Front (Pré compilation Less/Sass, Bower, etc.) et de la gestions de tâches (Gulp notamment).

### TortoiseGIT

Car non je n’aime pas la ligne de commande GIT Bash, même si elle peut s’avérer pratique. Dans le cas de GIT, Tortoise est très complet et propose des fonctions assez puissantes (cherry-pick, etc.). C’est une question de goût, mais je ne suis globalement pas un fanatique de la ligne de commande.

### nGrok

nGrok est un outil que j’ai découvert récemment lorsque j’ai développé mon premier chatbot pour Messenger. Il s’agit d’un petit utilitaire autonome qui permet d’exposer une URL publique vers votre poste local. Concrètement, nGrok ouvre un tunnel entre votre machine est les serveurs nGrok. L’accès se fait sur une URL temporaire utilisable en HTTP ou HTTPS. Bref que du bon !

## Et vous ?

C’est terminé pour cette liste des logiciels qui constituent mon poste de développement. J’en ai probablement oublié mais les principaux outils sont là. Je tiens à préciser que cette stack n’est nullement figée. J’ai commencé à développer sous Eclipse, ensuite sous Netbeans, j’ai fait un tour par Sublime Text, bref avant d’arriver à cet liste, j’ai testé et éprouvé (ou pas) de nombreux autres logiciels. Et ils vont sans nul doute évoluer dans les prochains mois !
