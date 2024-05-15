---
id: 1562
title: '6 conseils pour résoudre vos bugs complexes'
date: '2013-01-15T14:36:00+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1562'
permalink: /blog/developpement-php/6-conseils-pour-resoudre-vos-bugs-complexes/
dsq_thread_id:
    - '1286671180'

image: /wp-content/uploads/2013/01/bugs.jpg
categories:
    - 'PHP'
tags:
    - 'SSII / ESN'
---

En informatique, les **bugs complexes** paraissent souvent inextricables. On ne sait pas où chercher, on se prend la tête et, au final, on occulte les véritables raisons du problème. Si vous vous entêtez à résoudre vos problèmes sans changer vos méthodes, cela sera source de stress et d’inefficacité. Je vous livre ici **6 conseils pour vous aider résoudre vos bugs**. Vous pouvez les appliquer à l’informatique ou à n’importe quel domaine d’activité.

# 1. Restez calme et coupez toutes sources de déconcentration

**Garder votre calme** est le prérequis indispensable au bon déroulement du débogage et d’une réflexion intense. Si vous commencez à vous énerver, allez faire un tour et revenez apaisé 15 minutes plus tard. L’énervement, l’agacement et la perte du contrôle de soi sont des facteurs qui vous empêcheront de résoudre correctement votre bug car ils ne permettent pas d’avoir les idées claires.

Il est également primordial de **se mettre en conditions favorables**. Coupez donc la télévision, les mails, le téléphone et tout ce qui pourrait vous perturber lors de votre analyse. De manière général, coupez toutes source de déconcentration n’ayant pas de rapport avec votre problème. Si cela vous aide ou que vous êtes en open-space, vous pouvez écouter un peu de musique calme, idéalement sans paroles, à un volume raisonnable.

Une fois votre environnement apaisé, vous pouvez **dédier toute votre attention à votre tâche d’analyse**.

# 2. Imaginez une solution de contournement

Avoir une **solution de contournement** est un libérateur qui permet une analyse plus efficace. Les contraintes de délai nous soumettent à une pression qui nous empêche d’avoir une vision claire du problème et de toutes les solutions possibles. En effet, ne pas avoir de solution de contournement nous incite à identifier les solutions le plus vite possible et à tester celles qui nous paraissent les plus pertinentes. Nous réduisons donc le nombre de solutions afin de gagner du temps. C’est une erreur car la solution est peut être très éloignée de là où nous cherchons.

A l’inverse, une résolution du problème sans contrainte de délai ou en ayant un plan B nous permet d’**identifier toutes les solutions possibles** et d’accorder à chacune l’attention qu’elle mérite.

Prévoir un plan B est donc une bonne chose avant d’entamer vos recherches.

# 3. Découpez votre problème complexe en plusieurs problèmes simples

**Tout problème complexe peut être divisé en plusieurs problèmes simples.** Gardez cette phrase à l’esprit. Plutôt que d’essayer de traiter les choses de manière globale, divisez le problème en problèmes simples que vous essayez de résoudre petit à petit. Même si cela ne vous apporte pas directement de solution globale, cela vous permettra d’explorer de nouvelles pistes et vous incitera à **changer de point de vue**.

# 4. Changez de point de vue

Quand on travail depuis plusieurs heures voire plusieurs jours voire plusieurs mois sur un sujet, notre cerveau s’habitue et à tendance à prendre des raccourcis afin d’aller plus vite. Dès lors qu’un problème survient, il est important de déconnecter ces raccourcis pour avoir une vision complète du sujet. C’est ici qu’il convient de **prendre du recul**.

Pour vous aider, il est nécessaire de **penser différemment ce que vous faites**. Par exemple, si vous écrivez un algorithme complexe, plutôt que de le penser de la fonction d’appel vers le résultat, partez du résultat pour remonter la pile d’appels.

Dans d’autres circonstances, par exemple un bug d’affichage que vous ne reproduisez pas, mettez vous à la place de l’utilisateur et à quelqu’un qui ne connait pas l’application. Irait-il cliquer là où vous cliquez instinctivement depuis plusieurs jours ? Ces actions seraient-elles ordonnées à l’identique des vôtres ?

# 5. Appelez de l’aide

Même si votre amour propre va en prendre un coup : **appelez quelqu’un à la rescousse** ! Alors oui, vous n’aimez pas ça, votre code est votre code, vos bugs sont vos bugs, mais il est parfois utile d’avoir un avis extérieur. Cela permet justement de changer de point de vue et de prendre un peu de recul sur son code.

Ce n’est pas une solution miracle car, sur des problèmes complexes, vous passerez plus de temps à expliquer le problème et ce que vous avez tenté… D’autant que **votre explication influencera votre interlocuteur** et qu’il est possible qu’il se braque dans la même logique que vous, ce qui n’est bien évidement pas le but.

N’empêche qu’un peu aide permet de ne pas se sentir seul face son problème.

# 6. Attendez le lendemain

Si le problème persiste, **laisser passer une nuit et revenez plein d’espoirs,** motivé par le fait que vous avez peut être une bonne étoile. Il arrive que le bug se soit résolu de lui même. Si si, ça arrive. Par exemple en PHP, les problèmes viennent parfois de la session PHP qui, le lendemain, a expiré…

Deuxièmement il arrive aussi que vous ayez enfin les idées claires et que la solution vienne d’elle même, sans effort. Dans ces cas là, saluez votre chance mais testez et re-testez ce qui ne fonctionnait pas : il arrive aussi que vous ne reproduisiez pas exactement le même mode opératoire.

Si le problème persiste encore, consultez un médecin. Il est en effet possible que votre vision de la réalité soit altérée ou que vous ayez choisi la pilule bleue plutôt que la pilule rouge… 😉
