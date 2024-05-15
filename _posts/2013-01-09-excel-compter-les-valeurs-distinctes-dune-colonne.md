---
id: 1532
title: 'Excel : compter les valeurs distinctes d&rsquo;une colonne'
date: '2013-01-09T14:30:25+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1532'
permalink: /blog/developpement-php/excel-compter-les-valeurs-distinctes-dune-colonne/
dsq_thread_id:
    - '1286463296'
image: /wp-content/uploads/2013/01/excel_icon.png
categories:
    - 'Excel'
tags:
    - Excel
---

Une fois n’est pas coutume, voici une petite **astuce Excel** permettant de **compter les valeurs distinctes d’une colonne** dans une feuille de calculs XLS.

# Formule pour compter les valeurs uniques

Disons que l’on souhaite **compter le nombre de lignes ayant des valeurs uniques** (ce qui revient à faire un SELECT COUNT(DISTINCT()) en MySQL) sur la colonne A allant de la ligne 20 à la ligne 200. La formule Excel doit ressembler à celle-ci :

=SOMMEPROD(1/NB.SI(A20:A200;A20:A200))


[![](/wp-content/uploads/2013/01/excel_compter_valeur_unique.png "excel_compter_valeur_unique")](/wp-content/uploads/2013/01/excel_compter_valeur_unique.png)

# Formule pour compter toutes les lignes d’une plage

Pour mémoire, voici comment on compte toutes les lignes d’une colonne :

=NBVAL(A20:A200)

Il y a peut être d’autres moyens pour réaliser ceci : les commentaires sont ouverts.
