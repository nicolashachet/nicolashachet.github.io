---
id: 160
title: 'Connecter son ordinateur à Internet via son téléphone portable Android 3G (tethering)'
date: '2011-06-05T11:27:41+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=160'
permalink: /blog/telephone/connecter-son-ordinateur-a-internet-via-son-telephone-portable-android-3g/
dsq_thread_id:
    - '1285640518'
image: /wp-content/uploads/2011/06/sony-installation.jpg
categories:
    - Smartphone
tags:
    - Android
---

Il est frustrant d’avoir Internet en 3G, 3G+ ou Edge sur son téléphone portable et de ne pas pouvoir accéder à Internet de son ordinateur portable. J’ai testé pour vous une application permettant d’utiliser Internet sur son ordinateur via son téléphone portable Android : EasyTether. Grâce à EasyTether, **votre smartphone se transforme en modem** !

[![](/wp-content/uploads/2011/06/sony-vaio-ericson.jpg "sony vaio ericson")](/wp-content/uploads/2011/06/sony-vaio-ericson.jpg)

## Configuration requise

Pour surfer sur le Web en utilisant son portable ou son smartphone, voici le matériel et les logiciels nécessaires :

- Un ordinateur portable
- Un téléphone portable **sous système Android**
- Un câble USB reliant ordinateur et téléphone
- L’application EasyTether Lite installée sur votre téléphone et les drivers sur votre ordinateur


[![](/wp-content/uploads/2011/06/sony-installation.jpg "sony installation")](/wp-content/uploads/2011/06/sony-installation.jpg)L’installation nécessite un ordinateur, un téléphone et un câble USB

C’est tout. La seule contrainte forte est d’utiliser un OS Android sur son téléphone smartphone.

## Installation

Pour la partie téléphone portable, il suffit de télécharger [l’application gratuite sur l’Android Market](https://market.android.com/details?id=com.mstream.easytether_beta&feature=search_result).

Coté ordinateur, il vous faudra installer les drivers EasyTether (Windows, Mac ou Linux). Il existe des versions 32 et 64 bits.  
Vous pouvez suivre ce lien pour [télécharger les drivers EasyTether pour son ordinateur](https://www.mobile-stream.com/easytether/drivers.html). Lors de l’installation de la partie téléphone, l’application vous proposera de télécharger les drivers via la 3G et de les récupérer sur votre ordinateur : pas besoin de connexion Internet donc 😉

N’oubliez pas de **passer votre téléphone en mode débogage USB** : Menu > Paramètres > Applications > Développement > Cocher "Débogage USB".

[![](/wp-content/uploads/2011/06/icone-easytether.png "icone easytether")](/wp-content/uploads/2011/06/icone-easytether.png)La barre de statut vous indique que la connexion avec le téléphone est correctement effectuée

Dès lors, vous pouvez connecter votre téléphone à votre ordinateur via USB. L’ordinateur détectera automatiquement cette connexion et basculera dessus si aucun autre réseau n’est connecté : magique ! Bien évidement n’oubliez pas d’allumer la 3G sur votre téléphone si, comme moi, vous utilisez une application permettant de la couper (APNdroid par exemple).

## EasyTether : version gratuite ou payante ?

EasyTether est disponible en 2 versions : l’une gratuite, l’autre payante. La seule différence est que la version gratuite bloque tout le traffic https… Une lourde limitation si vous avez besoin d’aller voir vos mails (ça dépend de votre fournisseur de messagerie).

## Si vous rencontrez un 403 forbidden avec EasyTether…

Certains opérateurs semblent bloquer le traffic 3G ne provenant de téléphones portables. Pour cela, la solution consiste à masquer son véritable navigateur en modifiant le ‘User Agent’ des requêtes HTTP. Le [plugin Firefox User agent Switcher](https://addons.mozilla.org/fr/firefox/addon/user-agent-switcher/) le fait pour vous.

1. installer le plugin : [plugin Firefox User agent Switcher](https://addons.mozilla.org/fr/firefox/addon/user-agent-switcher/)
2. dans les paramètre du plug-in, ajouter un user agent avec comme caractéristiques:  
    Description : Tether (ou ce que vous voulez)  
    **User Agent : aller sur Whatismyuseragent.com depuis votre mobile et recopier votre useragent**  
    App Code Name : Android  
    App Name : Android  
    App Version : 2.1.1  
    Platform : Android  
    Vendor :  
    Vendor Sub :
3. valider puis redémarrer Firefox.
4. aller dans Outils/Defaut user agent/Tether (ou le nom choisi plus haut dans Description) et c’est fait !

N’hésitez pas à commenter si vous avez d’autres solutions de ce type.
