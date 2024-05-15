---
id: 1544
title: 'Qu&rsquo;est-ce que les recommandations PSR en PHP ?'
date: '2013-01-10T21:16:55+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1544'
permalink: /blog/developpement-php/quest-ce-que-les-recommandations-psr/
dsq_thread_id:
    - '1288609371'
image: /wp-content/uploads/2013/01/php-300x158.jpg
categories:
    - 'PHP'
tags:
    - PHP
---

Les **PSR** (pour "Propose a Standards Recommendation") sont des **recommandations** validées par le [PHP Framework Interoperability Group](https://blog.nicolashachet.com/2013/01/10/technologies/php/quest-ce-que-le-php-framework-interoperability-group-fig/ "PHP Framework Interoperability Group") (PHP fig :[ site officiel](https://github.com/php-fig/fig-standards/blob/master/README.md "PHP fig")) ayant pour objectif d’améliorer l’interopérabilité entre les frameworks PHP, et plus généralement entre les développeurs PHP. Il ne s’agit aucunement de normes ou de standards *établis* mais de recommandations qui tendent à le devenir. D’un sens, les PSR sont similaires aux RFC (Request For Comment) qui régulent désormais le monde des réseaux.

A ce jour, les [recommandations PSR validées](https://github.com/php-fig/fig-standards/tree/master/accepted "PSR validées") sont aux nombres de 4 :

- PSR-0 : qui traite du chargement des classes PHP et de l’autoloading ;
- PSR-1 : qui fixe les conventions minimales de codage ;
- PSR-2 : qui défini le style et l’organisation du code ;
- PSR-3 : qui s’occupe de l’interface des loggers.

Ces recommandations font débat dans la communauté. Vous pouvez lire du contre [par là](https://www.geek-directeur-technique.com/2012/06/19/normes-php-psr-2-aie-rate/) et [par là](https://blog.mageekbox.net/?post/2012/06/19/%C3%80-propos-de-PSR-0%2C-PSR-1-et-PSR-2). L’une des raisons est que ces recommandations qui, à la base, doivent traiter de l’interopérabilité entre frameworks PHP traitent naturellement de sujets sensibles, tels que les conventions de codage qui restent très subjectives. Reste que la démarche est intéressante et qu’il est toujours bon d’aller dans le sens d’une **harmonisation des méthodes de développements**.

Si vous souhaitez contribuer aux recommandations PSR ou simplement connaitre l’avancement des débats, vous pourrez trouver de l’information sur Google group : <https://groups.google.com/forum/?fromgroups=#!forum/php-fig>. Vous pouvez également consulter le github qui regroupe les recommandations, celles en débat ainsi que des infos utiles sur le FIG : <https://github.com/php-fig/fig-standards>
