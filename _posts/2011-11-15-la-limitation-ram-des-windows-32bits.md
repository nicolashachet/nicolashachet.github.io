---
id: 304
title: 'La limitation RAM des Windows 32bits'
date: '2011-11-15T12:08:19+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=304'
permalink: /blog/developpement-php/la-limitation-ram-des-windows-32bits/
categories:
    - 'Windows'
tags:
    - Windows
---

Aujourd’hui je relaie un excellent article sur l’utilisation de la mémoire par les Windows 32bits. Ca commence à dater (2008) mais c’est toujours bon de s’en rappeler. Je me souviens en effet de longues discutions sur l’utilisation de la RAM par Windows XP 32bits. Certains pensaient que seuls **2Gb** pouvait être gérés par Windows tandis que d’autres étaient sûrs que **4Gb** passaient. Comme souvent la vérité est ailleurs, entre les 2… Tous étaient néanmoins d’accord sur le fait qu’il était impossible à Windows de gérer plus de 4Gb, la limitation sans conteste des systèmes 32 bits.

Ainsi vous pouvez retrouver cet article en anglais de [Mark Russinovich](https://blogs.technet.com/b/markrussinovich/) sur technet :   
**[Pushing the Limits of Windows: Physical Memory](https://blogs.technet.com/b/markrussinovich/archive/2008/07/21/3092070.aspx)**

Bonne lecture.

## Résumé rapide

Pour ceux qui n’auraient pas la force de lire l’article en entier, voici un petit résumé en quelques lignes. L’article explique comment **Windows prend bien en charge les 4Gb de RAM** installés sur l’ordinateur mais utilise une partie de ces ressources pour un usage interne au système. Ainsi, le gestionnaire de tâches n’affiche que la mémoire disponible pour les applications utilisateurs mais ne prend pas en compte l’usage interne qui en est fait.
