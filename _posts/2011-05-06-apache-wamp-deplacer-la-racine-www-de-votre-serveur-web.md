---
id: 143
title: 'Apache WAMP : déplacer la racine WWW (webroot) de votre serveur Web'
date: '2011-05-06T08:00:46+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=143'
permalink: /blog/developpement-php/apache-wamp-deplacer-la-racine-www-de-votre-serveur-web/
dsq_thread_id:
    - '1285640396'
image: /wp-content/uploads/2011/05/wamp.png
categories:
    - 'Wamp'
tags:
    - 'Wamp Serveur'
    - Windows
---

[![](/wp-content/uploads/2011/05/wamp.png "wamp")](/wp-content/uploads/2011/05/wamp.png)

Lorsqu’on réinstalle un WAMP ([wampserver](https://www.wampserver.com/)), il n’est pas rare de vouloir déplacer le **répertoire www**, correspondant à la racine du serveur Web (webroot). L’ objectif est de ne pas mélanger les fichiers applicatifs (apache, mysql, php) et les applications Web présentes sur votre serveur (dans www donc). Cet article a pour objectif de vous montrer **comment déplacer le répertoire www sous wamp (wampserver)**.

## Editer le fichier Apache httpd.conf pour modifier le DocumentRoot

Après une installation toute fraîche de wampserver, vous vous retrouvez avec un répertoire **www** se trouvant à la racine du dossier wamp (celui étant placé par défaut directement sur C:\\). L’idée est de déplacer ce **C:\\wamp\\www** disgracieux vers **D:\\www**.

Il est possible de réaliser cette opération en disant à Apache de déplacer le **DocumentRoot** vers n’importe quelle dossier.

> Par défaut, le fichier httpd.conf se situe dans le dossier suivant : C:\\wamp\\bin\\apache\\Apache2.2.11\\conf\\httpd.conf
> 
> *Veuillez à remplacer Apache2.2.11 par votre version d’Apache*.

**Fichier httpd.conf**

  
\#  
\# DocumentRoot: The directory out of which you will serve your  
\# documents. By default, all requests are taken from this directory, but  
\# symbolic links and aliases may be used to point to other locations.  
\#  
DocumentRoot "D:/www/"  


Relancez les services du serveur, votre dossier racine est désormais D:/www. **Mais ça ne fonctionne toujours pas** : normal il faut également modifier les balises Directory. En fait, il faut modifier toutes les références qui pointaient vers C:/wamp/www. A l’installation vous n’en aurez que 2 mais si vous avez créé des virtualhosts ou des alias, il faudra sans doute en modifier plus.

**Fichier httdp.conf**

  
\#  
\# Note that from this point forward you must specifically allow  
\# particular features to be enabled – so if something’s not working as  
\# you might expect, make sure that you have specifically enabled it  
\# below.  
\#

\#  
\# This should be changed to whatever you set DocumentRoot to.  
\#  
<Directory "D:/www/">  


Si vous avez des **virtualhosts ou des alias**, pensez bien à vérifier les dossiers inclus. Par défaut :

  
Include "C:/wamp/alias/*"  


Vous voilà maintenant avec un dossier webroot (www) placé où vous le souhaitez !

## Déplacer son webroot vers un dossier réseau

Suite au commentaire de beni, sachez que si vous souhaitez placer votre webroot sur un disque réseau, il vous faudra utiliser le **nom réseau complet du dossier**. Exemple : **//Nom_reseau/service/repertoire**
