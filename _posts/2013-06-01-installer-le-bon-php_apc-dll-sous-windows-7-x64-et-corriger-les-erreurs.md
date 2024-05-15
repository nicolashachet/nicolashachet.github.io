---
id: 1754
title: 'Installer le bon php_apc.dll sous Windows 7 (x64) et corriger les erreurs'
date: '2013-06-01T11:12:21+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1754'
permalink: /blog/developpement-php/installer-le-bon-php_apc-dll-sous-windows-7-x64-et-corriger-les-erreurs/
dsq_thread_id:
    - '1347501994'

image: /wp-content/uploads/2013/06/PHP-Caching-With-APC.png
categories:
    - 'PHP'
tags:
    - 'Wamp Serveur'
    - Windows
---

<span style="font-size: 16px;">Je ne sais pas vous, mais moi, dès que j’essaie d’</span>**installer APC**<span style="font-size: 16px;"> (another PHP cache) sur un environnement </span>**Windows**<span style="font-size: 16px;"> (x86 ou x64) , je passe des heures à trouver l’extension DLL correcte… Le fichier à installer s’appelle </span>**php_apc.dll**<span style="font-size: 16px;"> et peut provoquer des erreurs aussi variées qu’agaçantes au démarrage d’Apache :</span>
- PHP Startup: Unable to load dynamic library ‘D:/…/ext/php_apc.dll’ – %1 n’est pas une application Win32 valide.
- PHP Startup: Unable to load dynamic library ‘D:/…/ext/php_apc.dll’ – Le module spécifié est introuvable.
- PHP Startup: Unable to load dynamic library ‘D:/…/ext/php_apc.dll’ – La procédure spécifiée est introuvable.

Ça prend un temps fou à résoudre et c’est systématiquement un calvaire. Pour vous aider à corriger tout ça, je vais compiler plusieurs choses :

1. <span style="line-height: 13px;">les repositories où vous pouvez **télécharger php_apc.dll** pour différents systèmes</span>
2. une explication de comment **choisir son extension apc** (x64 / x86 ? TS / NTS ? VC6 / VC9 ?)

## Ou trouver le ficher php_apc.dll ?

Ci dessous une petite compilation des dépôts où vous trouverez l’extension APC précompilée pour Windows (format DLL donc).

**Extension PHP pour Windows 64bits (Windows 7)**  <https://www.mediafire.com/php-win64-extensions>

**Site de Pierre**  
<https://downloads.php.net/pierre/>

**GitHub de stealth35**  
<https://github.com/stealth35/stealth35.github.com/downloads>

**Anindya** <https://www.anindya.com/>

Avec ces 4 repos, vous devriez trouver votre bonheur. Passons maintenant au choix de l’extension adpatée à votre système.

## Comment choisir son extension php_apc.dll ?

Avant tout, ce qu’il faut savoir, c’est qu’**une extension compilée pour un système n’est pas compatible avec un autre système**. C’est ce qui provoque toutes ces erreurs. Il y a plusieurs paramètres qui influent :

- Le compilateur : VC6 ou VC9
- L’architecture du système : x86 ou x64
- La version de PHP cible : 5.2, 5.3, 5.4
- La gestion des threads : Thread Safe (TS) ou Non Thread Safe (NTS)

Ça devient donc vite un problème de choisir l’extension correcte. D’autant plus que la version d’APC entre également en jeu (3.1.9, 3.1.13, etc.).

Pour faire son choix, c’est "facile" :

### <span style="line-height: 13px;">1. Identifier votre compilateur et votre architecture</span>

<span style="font-size: 1.17em;">Lancer votre serveur Apache (Wampserver par exemple) et accéder au phpinfo() de votre serveur : </span><https://localhost/?phpinfo=1>

[![phpinfo_archi_et_compilateur](/wp-content/uploads/2013/06/phpinfo_archi_et_compilateur.png)](/wp-content/uploads/2013/06/phpinfo_archi_et_compilateur.png)

Ici, on est sur un compilateur VC9 et une architecture x64 (64 bits) sous Windows 7.

### 2. Identifier votre version PHP

Toujours sur votre phpinfo(), vous trouverez également la version de PHP actuellement en cours d’exécution. Ici du PHP 5.3.13 (donc du PHP 5.3).

### 3. Identifier votre type de gestion de threads : TS ou NTS

Là c’est plus obscur… Il semblerait qu’il faille prendre des extensions **Thread Safe sur les Windows 7 et supérieur**. Je vous laisse essayer les 2. Sachez que, sur mon ordinateur perso Windows 7, x64 avec un apache x64, j’ai du prendre l’extension Thread Safe (TS). Si quelqu’un à des infos la dessus, je suis preneur. 😉

### 4. Télécharger la bonne extension

Muni de toutes ces infos, vous êtes prêts à choisir correctement votre extension APC qui fonctionnera sur votre système.  
Un petit exemple, vous avez les infos suivantes :

- <span style="line-height: 13px;">Compilateur VC9</span>
- Architecture x64
- PHP 5.3
- Windows 7 Thread Safe

Vous pouvez vous tourner vers l’extension **php_apc-3.1.13-5.3-VC9-x64-win7-2008.zip** disponible sur le site de mediafire.

Pour la partie installation/configuration APC, je vous laisse zieuter sur le Web, il y a plein de tutos qui l’explique.
