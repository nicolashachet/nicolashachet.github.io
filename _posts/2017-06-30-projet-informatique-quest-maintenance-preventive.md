---
id: 2879
title: 'Projet informatique : qu&rsquo;est-ce que la maintenance préventive ?'
date: '2017-06-30T15:31:49+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2879'
permalink: /blog/gestion-de-projets/projet-informatique-quest-maintenance-preventive/
dsq_thread_id:
    - '5953879853'
image: /wp-content/uploads/2017/06/maintenance-preventive-application-web-informatique-700x525.jpg
categories:
    - 'Gestion de projets'
---

En informatique, on parle souvent de **maintenance corrective** (ou MCO pour Maintien en Conditions Opérationnelles), mais beaucoup plus rarement de la notion de **maintenance préventive**. Coincée entre la MCO et l’exploitation, la maintenance préventive a toute sa place dans la vie d’une applicationPHP ou autre. Petite explication de ce que ça peut donner dans le cadre d’un projet informatique.

## Qu’est-ce que la maintenance préventive ?

La **maintenance préventive applicative** consiste à anticiper les problèmes qui pourraient affecter une application. Dans l’industrie, il s’agit par exemple de changer une pièce avant que l’appareil tombe en panne, ou bien d’arrêter une ligne de production pour inspecter et réparer ce qui doit l’être. C’est un entretien courant que l’on effectue naturellement pour de nombreux produits.

Pour différentes raisons (probablement liées aux coûts, à la nouveauté et à l’inexpérience), la maintenance préventive est beaucoup moins utilisée dans le cadre des projets informatiques. Lors de la construction des projets, on parle souvent de la notion de **risques**. Une fois le projet mis en exploitation, on parle de **maintenance corrective pour les aspects logiciels** et **d’infrastructure pour les aspects matériels .** Mais au delà de ça, on parle rarement de **maintenance préventive applicative**.

Globalement, les problèmes applicatifs qui peuvent survenir durant son exploitation sont liés à différentes évolutions :

- **Des évolutions technologiques** provoquant : 
    - Un décalage entre le besoin et la solution apportée ;
    - L’impossibilité de répondre à certaines demandes nouvelles ;
    - Un déficit de compétences sur la technologie ;
- **Des évolutions réglementaires** ;
- **Des évolutions de pratiques et méthodes de développements** :
- **Des évolutions d’intervenants** : 
    - Je n’ai plus la compétence nécessaire pour faire évoluer le projet ;
    - Les intervenants sont difficiles à trouver, leur coût explose ;
- **Des découvertes de failles qui impactent la sécurité de l’application.**

Certains problèmes ont une très forte probabilité de survenir durant la vie du projet. La technologie évolue très rapidement et il est fort probable que celle utilisée pour le développement initial du projet soit complètement obsolète dans 5 ou 10 ans, si elle n’est pas régulièrement mise à jour.

Pour palier à ces problèmes potentiels, la **maintenance préventive** apporte des solutions. L’idée est de consacrer deux budgets complémentaires :

- le budget de **Maintenance Corrective** pour corriger / faire évoluer l’application afin de répondre plus finement aux besoins ;
- le budget de **Maintenance Préventive** pour anticiper les problèmes.

## Quelle valeur ajoutée pour la maintenance préventive ?

En réalité, la maintenance préventive n’apporte pas de valeur ajoutée directe au projet. Elle permet en revanche d’allonger sa **durée de vie** ainsi que sa **capacité à embarquer des évolutions**. C’est cette durée de vie qui détermine le budget adéquat à investir dans une maintenance préventive. Vous prévoyez de jeter le projet dans 6 mois ? A quoi bon investir… En revanche, si vous vous projetez sur du moyen terme (ou s’il y a un risque pour que le projet que vous deviez jeter dans 6 mois devienne pérenne), alors il n’est pas inutile d’investir dans ce domaine.

## Concrètement, à quoi sert un budget de maintenance préventive ?

La maintenance préventive revêt deux objectifs :

1. **éviter le retard technologique** (ce qui permet d’éviter un bon nombre de risque : écart besoin / solutions possibles, déficit de compétences, performances, attentes des utilisateurs) ;
2. **garder un code simple**, clair et lisible par le plus grand nombre.

Les chantiers liés à la maintenance préventive sont donc nombreux et ne peuvent pas tous être menés en parallèle ni en permanence. Ce n’est d’ailleurs pas souhaitable car il est aussi très important de laisser "vivre" l’application, de s’en séparer pour jeter un œil neuf lors la prochaine phase de maintenance.

Voici quelques tâches qui peuvent entrer dans cette maintenance :

- **La migration des composants techniques** : 
    - L’architecture de l’application. OS, dimensionnement, proxy, cache… ;
    - Les composants socles. Vous avez une application PHP 5.4 => Basculez la en PHP 7 ;
    - Les composants logiciels. Vous avez une application en Symfony 2.2 => Basculez là en Symfony 3;
- **La migration des dépendances du projet** : 
    - Mettez à jour les versions de vos dépendances logicielles (bundles, librairies tierces…) ;
    - Montez les versions de vos services tiers (serveurs de cache, exécutables) ;

Pour chacune des ces migrations, vous aurez systématiquement à vous poser des questions : si je monte de version tel composant, y’a-t-il un risque de régression sur l’application ? Mon application doit-elle évoluer ? Est-ce transparent pour les utilisateurs ? Est-ce que cela apporte des nouveautés ?

- **Le refactoring du code source** : 
    - Retravailler le code qui n’est pas compréhensible ;
    - Retravailler le code obsolète ;
    - Retravailler le code instable ;
    - Retravailler le code dangereux ;
    - Retravailler la gestion de la configuration ;
    - Supprimer le code qui ne sert à rien ;

Très concrètement, vous devez **prendre soin du code source**. Le code source vie avec celles et ceux qui le font et le défont. En prendre soin est indispensable pour allonger la durée de vie de votre application. Dans le cas contraire, le *risque inexorable* est d’accumuler de la dette technique et de le voir se transformer en *legacy code*.

- **La veille sur la sécurité** : 
    - Analyser les faille détectées sur les composants ;
    - Identifier et corriger le code non sécurisé.

Les attaques informatiques progressent et celles-ci sont de plus en plus médiatiques. La sécurité des données et du matériel est clairement l’un des enjeux majeurs des prochaines années.

## Qu’est-ce qui bloque la mise en oeuvre d’une maintenance préventive ?

**Le syndrome du "ça fonctionne donc on n’y touche plus" est votre ennemi**. C’est tentant et très facile mais en y cédant vous perdrez la connaissance technique de votre application. Un système qui évolue bien est un système que l’on analyse, que l’on inspecte, que l’on améliore en permanence, même si ça ne se voit pas.

L’**absence de tests automatisés** sur votre application est également un frein particulièrement puissant. En effet, comment garantir que vous n’intégrerez pas de régression lors de votre phase de maintenance ? Les tests manuels sont une solution mais vous coûteront très chers à la longue. A méditer lorsque vous refuserez le surcoût initial des tests unitaire automatisés lors de la phase d’avant-vente…

## Conclusion

La **maintenance préventive** est un réel challenge des années à venir, pour les structures n’ayant pas encore passé le virage technologique comme pour les autres. Actuellement peu usitées en informatique, les phases de maintenance préventive méritent d’être étudiées. Dans le cas contraire, le risque est de devoir (re)développer votre projet tous les 5 ans ce qui, au niveau budgétaire, n’est pas forcément une meilleure idée.
