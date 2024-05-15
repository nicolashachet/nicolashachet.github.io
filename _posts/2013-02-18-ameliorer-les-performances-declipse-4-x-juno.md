---
id: 1666
title: 'Améliorer les performances d&rsquo;Eclipse 4.x (Juno)'
date: '2013-02-18T11:11:28+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1666'
permalink: /blog/developpement-php/ameliorer-les-performances-declipse-4-x-juno/
dsq_thread_id:
    - '1285642110'
image: /wp-content/uploads/2012/09/eclipse.png
categories:
    - 'Eclipse'
tags:
    - 'Eclipse IDE'
    - IDE
    - 'Performances Web'
---

Eclipse a été frappé par des **problèmes de performances** de son IDE. Les **lenteurs** lors de l’ouverture de fichiers et/ou l’ouverture de vues étaient rédhibitoires à une utilisation normale. Une phase d’optimisation de l’interface d’Eclipse a donc été menée par les membres de le Team et a conduit à la **publication d’un patch améliorant les performances d’Eclipse**.

Je vous invite à lire cet article sur le Wiki Eclipse : https://wiki.eclipse.org/Platform_UI/Juno_Performance_Investigation

La procédure d’installation du patch est la suivante :

1. Vérifier que vous êtes sur un Eclipse Juno SR1 (Septembre 2012)
2. Aller à Help > Install New Software
3. Sélectionner ce repository : <https://download.eclipse.org/eclipse/updates/4.2>
4. Déplier **Juno SR1 Patches** and installer **Eclipse UI Juno SR1 Optimizations**

**Pour moi, la manipulation a fonctionné et l’utilisation d’Eclipse est (re)devenue possible.[  ](/wp-content/uploads/2012/09/eclipse.png)**

A noter que ces optimisations seront bien évidement présentes sur les prochaines releases de l’IDE, notamment Eclipse Kepler en Juin 2013.
