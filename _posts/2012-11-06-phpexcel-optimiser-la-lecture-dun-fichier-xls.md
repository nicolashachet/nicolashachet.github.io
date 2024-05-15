---
id: 1411
title: 'PHPExcel : optimiser la lecture d&rsquo;un fichier XLS'
date: '2012-11-06T16:34:31+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1411'
permalink: /blog/developpement-php/phpexcel-optimiser-la-lecture-dun-fichier-xls/
dsq_thread_id:
    - '1285642150'
image: /wp-content/uploads/2012/11/phpexcel_logo-180x80.jpg
categories:
    - 'PHPExcel'
tags:
    - PHPExcel
---

[![](/wp-content/uploads/2012/11/phpexcel_logo.jpg "phpexcel_logo")](/wp-content/uploads/2012/11/phpexcel_logo.jpg)

Si vous utilisez régulièrement [**PHPExcel**](https://phpexcel.codeplex.com/ "PHPExcel"), vous savez que les **performances** de la librairie de lecture / écriture de fichiers Excel sont très moyennes. PHPExcel utilise de nombreuses classes PHP permettant de décrire les composants d’un fichier XLS ou XLSX, ce qui alourdit la **consommation processeur et la consommation mémoire**. A la décharge de la team PHPExcel, la structure des fichiers Microsoft est peu adaptée à ce genre de manipulation. En outre, c’est une excellente librairie qui rend bien des services aux **développeurs PHP** que nous sommes (ou pas).

Dans cet article, publié volontairement vide, je vous laisse la parole afin de **connaitre vos techniques d’optimisations de lecture d’un fichier Excel avec PHPExcel**.

L’idée est de connaitre les **astuces** et les **techniques d’optimisation** qui permettent d’obtenir des **performances acceptables**.

**<span style="color: #008000;">Les commentaires sont ouverts !</span>**

## Techniques pour optimiser PHPExcel

- Utiliser **PHP 5.4**
- Travaillez sur un **document existant**
- Privilégier la **mise en forme des cellules par groupe** (Range) plutôt que cellule par cellule
- Utiliser la fonction ***applyFromArray***

```
$objPHPExcel->getActiveSheet()->getStyle(‘C5:R95′)->applyFromArray(
    array(‘fill’ => array(
        ‘type’ => PHPExcel_Style_Fill::FILL_SOLID,
        ‘color’ => array(‘argb’ => ‘FFFFFF00′)
    ),
));
```

## Alternatives à PHPExcel

Source : [https://stackoverflow.com/questions/3930975/alternative-for-php-excel](https://stackoverflow.com/questions/3930975/alternative-for-php-excel "Alternatives à PHPExcel") (actualisée par Mark Baker). *N’hésitez pas à consulter l’original pour une version à jour et complète.*

Il s’agit de librairies moins complètes que PHPExcel mais qui correspondent peut être à vos besoins. J’ai sélectionné celles qui paraissent pertinentes dans un contexte de production.

<style>table.custom td { padding: 12px; 5px; }</style>| #### Librairie | #### Remarque |
|---|---|
| [PEAR’s PHP_Excel_Writer](https://pear.php.net/package/Spreadsheet_Excel_Writer) | Format : **XLS**   Action : écriture |
| XLS File [Generator](https://paggard.com/projects/xls.generator/) &amp; [Reader](https://paggard.com/projects/xls.reader/) | Format : **XLS**   Action : **<span style="color: #3366ff;">écriture et lecture   </span>**<span style="color: #3366ff;"><span style="color: #ff0000;">Payant</span></span> |
| [Excel Writer XML for PHP](https://sourceforge.net/projects/excelwriterxml/) | Format : **XLS** (XML)   Action : écriture |
| [Ilia Alshanetsky’s Excel extension basé sur LibXL](https://github.com/iliaal/php_excel) | Format : **XLS**   Composant LibXL <span style="color: #ff0000;">payant</span>   Action : **<span style="color: #3366ff;">écriture et lecture</span>** |
| [php-spreadsheetreader](https://code.google.com/p/php-spreadsheetreader/) | Format : **XLS**, **ODS**, **CSV** |
| [PHP-ExcelReader](https://sourceforge.net/projects/phpexcelreader/) | Format : **XLS** |
| [PHP_Excel_Reader 2.21](https://code.google.com/p/php-excel-reader/) / [PHP_Excel_Reader 2.22](https://code.google.com/p/php-excel-reader2/) | Format : **XLS** |
