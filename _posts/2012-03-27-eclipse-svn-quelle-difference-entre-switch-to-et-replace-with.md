---
id: 670
title: "Eclipse SVN : quelle différence entre Switch to et Replace with ?"
date: '2012-03-27T10:03:23+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=670'
permalink: /blog/developpement-php/eclipse-svn-quelle-difference-entre-switch-to-et-replace-with/
dsq_thread_id:
    - '1286010208'
image: /wp-content/uploads/2012/03/eclipse.png
categories:
    - 'Eclipse'
tags:
    - 'Eclipse IDE'
    - IDE
---

[![Logo Eclipse](/wp-content/uploads/2012/03/eclipse.png "eclipse")](/wp-content/uploads/2012/03/eclipse.png)Logo Eclipse

Que vous travailliez en équipe ou de façon autonome, vous utilisez probablement un gestionnaire de sources comme SVN ou CVS. Eclipse possèdent 2 fonctions nommées **"Switch to" et "Replace with"** ("Basculer vers" et "Remplacer par" en français). Elles permettent de basculer le version de travail locale vers une version taguée ou une branche de développement. Quelle est la différence entre ces fonctions ?

[![](/wp-content/uploads/2012/03/Eclipse_team.png "Eclipse_team")](/wp-content/uploads/2012/03/Eclipse_team.png)Les 2 fonctions sous Eclipse

## Replace with

**Replace with** permet de remplacer la version de travail locale avec une version taguée ou une branche de développement. Il s’agit d’un **replacement brut** : les fichiers sont systématiquement replacés avec la version demandée sans crier gare.

## Switch to

**Switch to** permet de remplacer la version de travail locale avec une version taguée ou une branche de développement,**<span style="color: #ff0000;"> tout en conservant les modifications non commitées</span>**. Cela signifie que si vous avez des modifications en cours sur un fichier, <span style="color: #000000;">elles ne seront pas écrasées par le Switch to</span>. Si vous avez des paramètres non commités, dédiés au développement (typiquement les infos de connexion à la base de données), vous n’aurez pas à les re-modifier après le changement de version ou de branches, ils seront automatiquement déplacés.

Plus d’infos en anglais : [https://help.eclipse.org/indigo/index.jsp?topic=/org.eclipse.platform.doc.user/tasks/tasks-103.htm](https://help.eclipse.org/indigo/index.jsp?topic=/org.eclipse.platform.doc.user/tasks/tasks-103.htm "https://help.eclipse.org/indigo/index.jsp?topic=/org.eclipse.platform.doc.user/tasks/tasks-103.htm")
