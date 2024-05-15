---
id: 363
title: 'PHPExcel : préserver les zéros en début de chaîne'
date: '2011-11-24T10:37:44+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=363'
permalink: /blog/developpement-php/phpexcel-preserver-les-zeros-en-debut-de-chaine/
dsq_thread_id:
    - '1285641115'
image: /wp-content/uploads/2012/11/phpexcel_logo-180x80.jpg
categories:
    - 'Excel'
tags:
    - Excel
    - PHPExcel
---

Une petite astuce PHPExcel aujourd’hui : **comment préserver les zéros en début de chaîne de caractères sous PHPExcel dans un texte** ? Vous devez exporter un code type nombre ou un chiffre avec zéro initial tel que 000987 et vous souhaitez que les zéros ne soient pas effacés et que la cellule affiche 987 ? Il suffit de déclarer le type de données explicitement.

## Valeur de cellule avec type explicite

{% highlight php linenos %}  
// Déclare le type de données explicitement.  
$objPHPExcel->getActiveSheet()->setCellValueExplicit(‘A1’ , ‘000987’, PHPExcel_Cell_DataType :: TYPE_STRING);

// Modifie le format de la cellule  
$objPHPExcel->getActiveSheet()->getStyle(‘A1’)->getNumberFormat()->setFormatCode(PHPExcel_Style_NumberFormat::FORMAT_TEXT);  
{% endhighlight %}

Et le tour est joué. La cellule sera interprétée comme un format texte, et les zéros seront conservés. Les deux lignes sont importantes pour afficher correctement les zéros.

Les types de données suivants son supportés (voir la classe PHPExcel_Cell_DataType) :

- TYPE_STRING
- TYPE_FORMULA
- TYPE_NUMERIC
- TYPE_BOOL
- TYPE_NULL
- TYPE_INLINE
- TYPE_ERROR

## Mise à jour du style de la cellule

Il est également possible d’assigner un style particulier à la cellule contenant les zéros à préserver :

{% highlight php linenos %}  
// Force l’affichage de la cellule sur 6 caractères.  
$objPHPExcel->getActiveSheet()->setCellValue(‘A1’, 000987);  
$objPHPExcel->getActiveSheet()->getStyle(‘A1’)->getNumberFormat()->setFormatCode(‘000000’);  
{% endhighlight %}

La cellule n’est pas explicitement déclarée comme étant du texte, mais son style permet de préserver les zéros. A vous de choisir la méthode qui vous convient le mieux !
