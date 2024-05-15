---
id: 3040
title: 'Comment générer des fichiers PowerPoint (PPTX, PPT) en PHP ?'
date: '2018-11-23T17:00:10+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=3040'
permalink: /blog/developpement-php/comment-generer-des-fichiers-powerpoint-pptx-ppt-en-php/
dsq_thread_id:
    - '7067031557'
image: /wp-content/uploads/2018/11/generer-fichier-powerpoint-ppt-pptx-en-php-700x300.jpg
categories:
    - 'PHP'
---

En développement PHP, la génération de fichiers PowerPoint est relativement rare. Cependant, quand on a besoin de créer des fichiers de présentation, on se retrouve un peu bloqué… Cet article vous présente 3 solutions pour **générer des fichiers PowerPoint en PHP**. Contrairement à Excel et aux fichiers XLS et XLSX, il existe peu de librairies PHP qui permettent d’écrire des fichiers PPT et PPTX. Petit tour d’horizon des solutions OpenSource.

## PHPPresentation

PHPPresentation est une librairie PHP éditée par PHPOffice qui offre une solution complète pour la lecture et l’écriture de fichiers PowerPoint : images, fonts, tableaux, transitions, gestion des métadonnées, etc. Bref, les fonctionnalités sont puissantes et conviendront à la majorité des usages.

Prérequis :

- PHP 5.3+
- Zip extension
- XML Parser extension
- XMLWriter extension (optional, used to write DOCX and ODT)
- GD

```

use PhpOffice\PhpPresentation\PhpPresentation;
use PhpOffice\PhpPresentation\IOFactory;
use PhpOffice\PhpPresentation\Style\Color;
use PhpOffice\PhpPresentation\Style\Alignment;

$objPHPPowerPoint = new PhpPresentation();

// Create slide
$currentSlide = $objPHPPowerPoint->getActiveSlide();

// Create a shape (drawing)
$shape = $currentSlide->createDrawingShape();
$shape->setName('PHPPresentation logo')
      ->setDescription('PHPPresentation logo')
      ->setPath('./resources/phppowerpoint_logo.gif')
      ->setHeight(36)
      ->setOffsetX(10)
      ->setOffsetY(10);
$shape->getShadow()->setVisible(true)
                   ->setDirection(45)
                   ->setDistance(10);

// Create a shape (text)
$shape = $currentSlide->createRichTextShape()
      ->setHeight(300)
      ->setWidth(600)
      ->setOffsetX(170)
      ->setOffsetY(180);
$shape->getActiveParagraph()->getAlignment()->setHorizontal( Alignment::HORIZONTAL_CENTER );
$textRun = $shape->createTextRun('Thank you for using PHPPresentation!');
$textRun->getFont()->setBold(true)
                   ->setSize(60)
                   ->setColor( new Color( 'FFE06B20' ) );

$oWriterPPTX = IOFactory::createWriter($objPHPPowerPoint, 'PowerPoint2007');
$oWriterPPTX->save(__DIR__ . "/sample.pptx");

```

[→ Voir le Github PHPOffice/PHPPresentation](https://github.com/PHPOffice/PHPPresentation)

## OpenTBSBundle

Beaucoup moins complète, OpenTBS est une solution un peu à part qui permet de générer des fichiers PowerPoint (mais également des fichiers Excel, etc.) à partir d’un template de base. Il n’est pas possible de créer un fichier de zéro. L’objectif de cette librairie est simplement d’effectuer des remplacements de chaîne de caractères sur la base de placeholders dans le fichier. Un court exemple étant plus explicite qu’un long discours :

```

// get the service
$TBS = $this->get('opentbs');
// load your template
$TBS->LoadTemplate('template.pptx');
// replace variables
$TBS->MergeField('client', array('name' => 'Foo', 'fullname' => 'Bar'));
// send the file
$TBS->Show(OPENTBS_DOWNLOAD, 'file_name.pptx');
```

Ici les "client.name" sera remplacé par "Foo" et "client.fullname" sera remplacé par "Bar".

Prérequis :

- PHP 5.3.2+
- Symfony 2
- Zlib

[→ Voir le Github OpenTBSBundle](https://github.com/mbence/OpenTBSBundle)

## PptxGenJS

PptxGenJS est une solution Javascript (navigateur ou NodeJs) qui permet d’écrire des présentations PowerPoint. Les fonctionnalités sont puissantes et complètes : ajout de graphiques, images, médias, tableaux, etc. En revanche, il n’est pas possible d’ouvrir une présentation existante et de la modifier. Elle permet en outre d’ajouter un tableau sur une slide à partir d’un tableau HTML, ce qui peut s’avérer intéressant pour gagner du temps.

Prérequis :

- En cas d’utilisation via le navigateur, le polyfill sur les promesses (Promises) doit être installé.

Voici un court exemple qui illustre la simplicité de la lib :

```

var pptx = new PptxGenJS();
var slide = pptx.addNewSlide();
slide.addText('Hello World!', { x:1.5, y:1.5, fontSize:18, color:'363636' });
pptx.save('Sample Presentation');
```

[→ Voir le Github PptxGenJS](https://github.com/gitbrent/PptxGenJS)
