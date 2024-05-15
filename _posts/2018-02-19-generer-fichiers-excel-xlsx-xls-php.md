---
id: 2998
title: 'Comment générer des fichiers Excel (XLSX, XLS) en PHP ?'
date: '2018-02-19T21:33:13+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2998'
permalink: /blog/developpement-php/generer-fichiers-excel-xlsx-xls-php/
dsq_thread_id:
    - '6490810545'
image: /wp-content/uploads/2018/02/generer-fichier-excel-xlsx-xls-en-php-700x300.png
categories:
    - 'PHP'
tags:
    - Excel
    - PHPExcel
---

Cet article liste les principales **solutions pour écrire des fichiers Excel aux formats XLS et XLSX à partir d’une application PHP**.  
Si vous développez des applications de gestion en PHP, vous vous êtes probablement déjà retrouvés face au choix de la librairie permettant d’**exporter des fichiers Excel**. Certaines librairies sont **puissantes** mais peu **performantes**, d’autres sacrifient les **fonctionnalités** pour obtenir de très bonnes performances. Quelques éléments de réponse dans l’article ci-dessous qui vous permettront de vous simplifier cette tâche.

## PHPExcel

Commençons par mettre les choses au clair sur ce qui fut la librairie référence il y a quelques années : **il ne faut plus utiliser PHPExcel pour écrire des fichiers Excel en PHP**.  
En effet, celle librairie est abandonnée. La dernière version date du 1er mai 2015… Mais pas de panique, l’abandon de cette version s’accompagne également de la sortie de la librairie **PhpSpreadsheet** qui n’est autre qu’une réécriture de PHPExcel.  
Passons donc directement au nouveau venu.

## PhpSpreadsheet

C’est donc le successeur de PHPExcel. Cette librairie est une réécriture en profondeur pour coller aux standards actuels en termes de codage et de normes de développement. Vous retrouverez les namespaces, l’application des PSR, une compatibilité avec les dernières versions de PHP…  
Coté prérequis, il vous faudra **PHP 5.6** **ou +**, **php_zip**, **php_xml** et **php_gd2**.  
L’installation se fait via composer et le code ressemble à ceci :

```php
require 'vendor/autoload.php';

use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;

$spreadsheet = new Spreadsheet();
$sheet = $spreadsheet->getActiveSheet();
$sheet->setCellValue('A1', 'Hello World !');

$writer = new Xlsx($spreadsheet);
$writer->save('hello world.xlsx');
```

Fonctionnalités :

- Formats d’écriture : **XLS, XLSX, ODS, HTML, CSV et PDF** avec une librairie complémentaire
- Styles : **oui**
- Feuilles de travail multiples : **oui**
- Support des images : **[oui](https://phpspreadsheet.readthedocs.io/en/develop/topics/recipes/#add-a-drawing-to-a-worksheet)** via l’objet Drawing
- Support des formules de calculs : **[oui](https://phpspreadsheet.readthedocs.io/en/develop/topics/recipes/#write-a-formula-into-a-cell)**
- Performances : consommations mémoire et CPU plutôt importantes mais possibilité d’ajouter du cache lors de la génération (APCu, Redis, Memcached…)

Disons le tout de suite, c’est la plus complète au niveau des fonctionnalités et la plus mauvaise au niveau des performances. Si vous n’avez pas besoin d’exporter des images, des formules ou des composants complexes, les librairies qui suivent pourront vous convenir.

[→ Voir le github de PhpSpreadsheet ](https://github.com/PHPOffice/PhpSpreadsheet)

## mk-j PHP_XLSXWriter

La première version majeure est sortie en 2014. L’objectif de cette librairie est de proposer des fonctionnalités minimalistes avec une signature mémoire minimale. La documentation annonce un traitement de 1.4 secondes pour 50k lignes exportées et une consommation mémoire sous 1M. Si vous souhaitez avoir des fonctionnalités avançées, passez votre chemin.

Voici un exemple de code :

```php
$header = array(
  'created'=>'date',
  'product_id'=>'integer',
  'quantity'=>'#,##0',
  'amount'=>'price',
  'description'=>'string',
  'tax'=>'[$-1009]#,##0.00;[RED]-[$-1009]#,##0.00',
);
$data = array(
    array('2015-01-01',873,1,'44.00','misc','=D2*0.05'),
    array('2015-01-12',324,2,'88.00','none','=D3*0.05'),
);

$writer = new XLSXWriter();
$writer->writeSheetHeader('Sheet1', $header );
foreach($data as $row)
	$writer->writeSheetRow('Sheet1', $row );
$writer->writeToFile('example.xlsx');
```

Fonctionnalités :

- Formats d’écriture : **XLSX**
- Styles : **oui**, **mais basiques** sur les cellules
- Feuilles de travail multiples : **oui**
- Support des images : **non**
- Support des formules de calculs : **non**
- Performances : **bonnes**, faible consommation mémoire

[→ Voir le github de mk-j XLSWriter](https://github.com/mk-j/PHP_XLSXWriter)

## Spout

Le but de cette librairie est de proposer un composant rapide et scalable, c’est à dire permettant d’encaisser des pics de charge. Les fonctionnalités sont basiques et l’auteur annonce une consommation inférieure à 3M gràce à un mécanisme de streaming.

Prérequis : **PHP 5.4 ou +**, **php_zip**, **php_xmlreader**.

Exemple de code :

```php
use Box\Spout\Writer\WriterFactory;
use Box\Spout\Common\Type;

$writer = WriterFactory::create(Type::XLSX); // for XLSX files
//$writer = WriterFactory::create(Type::CSV); // for CSV files
//$writer = WriterFactory::create(Type::ODS); // for ODS files

$writer->openToFile($filePath); // write data to a file or to a PHP stream
//$writer->openToBrowser($fileName); // stream data directly to the browser

$writer->addRow($singleRow); // add a row at a time
$writer->addRows($multipleRows); // add multiple rows at a time

$writer->close();
```

Fonctionnalités :

- Formats d’écriture : **XLSX**, **CSV**, **ODS**
- Styles : **oui, mais basiques** sur les cellules
- Feuilles de travail multiples : **oui**
- Support des images : **non**
- Support des formules de calculs : **non**
- Performances : **bonnes**, faible consommation mémoire

[→ Voir le github de Spout](https://github.com/box/spout)

## Ellumilel Excel Writer

php-excel-writer est une librairie que j’ai trouvé en écrivant cet article. L’auteur annonce des performances excellentes avec 3.2M de lignes exportées en 120 secondes pour une consommation mémoire de 0.84M… Les fonctionnalités sont basiques mais peuvent répondre à des cas d’utilisation simples.

Prérequis : **PHP 5.4 ou +**, **ZipArchive**.

Exemple de code :

```php
$header = [
    'test1' => 'YYYY-MM-DD HH:MM:SS',
    'test2' => 'string',
    'test3' => 'string',
    'test4' => 'string',
    'test5' => 'string',
    'test6' => 'money',
];

$wExcel = new Ellumilel\ExcelWriter();
$wExcel->writeSheetHeader('Sheet1', $header);
$wExcel->setAuthor('Your name here');
for ($i = 0; $i < 5000; $i++) {
    $wExcel->writeSheetRow('Sheet1', [
        (new DateTime())->format('Y-m-d H:i:s'),
        rand(100, 10000),
        rand(100, 10000),
        rand(100, 10000),
        rand(100, 10000),
        rand(100, 10000),
    ]);
}

$wExcel->writeToFile("example.xlsx");
```

Fonctionnalités :

- Formats d’écriture : **XLSX**
- Styles : **oui, mais basiques** sur les cellules
- Feuilles de travail multiples : **oui**
- Support des images : **non**
- Support des formules de calculs : **oui**, simples
- Performances : **excellentes**, faible consommation mémoire

[→ Voir le github de php-excel-writer](https://github.com/ellumilel/php-excel-writer)

## OneSheet

J’ai également découvert cette librairie qui me parait intéressante lors de la rédaction de cet article. Comme les autres librairies, l’objectif n’est pas de proposer de nombreuses fonctionnalités mais de sélectionner celles qui consommeront le moins de CPU et de mémoire.

Prérequis : **PHP 5.4.4, PHP 5.6 ou 5.7 ou +**.

Exemple de code :

```php
require_once '../vendor/autoload.php';

$onesheet = new \OneSheet\Writer('/optional/fonts/directory');
$onesheet->addRow(array('hello', 'world'));
$onesheet->writeToFile('hello_world.xlsx');
```

Fonctionnalités :

- Formats d’écriture : **XLSX**
- Styles : **oui**, mais basiques sur les cellules
- Feuilles de travail multiples : **non**
- Support des images : **non**
- Support des formules de calculs : **non**
- Performances : **excellentes**, faible consommation mémoire
- En plus : **autosizing possible** sur les colonnes si vous êtes prêts à concéder quelques secondes d’export

[→ Voir le github de OneSheet](https://packagist.org/packages/nimmneun/onesheet)

## xlsxwriter (Python)

On quitte les librairies pures PHP pour se tourner vers cette librairie **Python**. Je n’ai pas eu l’occasion de la tester mais la documentation est prometteuse.

Voici un aperçu du code :

```python
import xlsxwriter

# Create an new Excel file and add a worksheet.
workbook = xlsxwriter.Workbook('demo.xlsx')
worksheet = workbook.add_worksheet()

# Widen the first column to make the text clearer.
worksheet.set_column('A:A', 20)

# Add a bold format to use to highlight cells.
bold = workbook.add_format({'bold': True})

# Write some simple text.
worksheet.write('A1', 'Hello')

# Text with formatting.
worksheet.write('A2', 'World', bold)

# Write some numbers, with row/column notation.
worksheet.write(2, 0, 123)
worksheet.write(3, 0, 123.456)

# Insert an image.
worksheet.insert_image('B5', 'logo.png')

workbook.close()
```

Fonctionnalités :

- Formats d’écriture : **XLSX**
- Styles : **oui, mais basiques** sur les cellules
- Feuilles de travail multiples : **oui**
- Support des images : **oui**, PNG / JPEG
- Support des formules de calculs : **[oui](https://xlsxwriter.readthedocs.io/working_with_formulas.html)**
- Performances : **?**

[→ Voir le site de xlswriter pour Python](https://xlsxwriter.readthedocs.io/index.html)

## exceljs (NodeJS)

Pour finir, on quitte encore le monde PHP avec cette librairie qui me parait très prometteuse et qui tourne sous **NodeJS**. L’écosystème OpenSource s’est profondément ouvert et NodeJS fait office de parfait complément à PHP. Rien n’empêche donc d’appeler un composant NodeJS en PHP via de l’event sourcing ou un gestionnaire de queue. En ce qui concerne la librairie, les fonctionnalités sont aussi nombreuses que phpSpreadsheet et sauront contenter les plus exigeants.

Exemple de code :

```javascript
var Excel = require('exceljs');

var workbook = new Excel.Workbook();
workbook.creator = 'Me';
workbook.lastModifiedBy = 'Her';
workbook.created = new Date(1985, 8, 30);
workbook.modified = new Date();
workbook.lastPrinted = new Date(2016, 9, 27);

var sheet = workbook.addWorksheet('My Sheet');
```

Fonctionnalités :

- Formats d’écriture : **XLSX**
- Styles : **oui**
- Feuilles de travail multiples : **oui**
- Support des images : **oui**
- Support des formules de calculs : **oui**
- Performances : **?**

[→ Voir le github de exceljs](https://github.com/guyonroche/exceljs)

## Conclusion

Nous avons vu plusieurs librairies pour exporter des fichiers Excel en **PHP**, en **Python** et en **NodeJS**. Ces dernières années, plusieurs alternatives à PHPExcel ont fait leur apparition et certaines sont très prometteuses. Selon les fonctionnalités attendues, le choix du composant s’imposera de lui-même puisque aucune n’arrive à allier **fonctionnalités avancées et performances** de l’export que ce soit en termes de consommation mémoire ou CPU.
