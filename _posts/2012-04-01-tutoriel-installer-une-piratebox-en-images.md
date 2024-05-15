---
id: 707
title: 'Tutoriel : installer une PirateBox en images'
date: '2012-04-01T23:23:28+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=707'
permalink: /blog/fonctionnement-du-web/tutoriel-installer-une-piratebox-en-images/
dsq_thread_id:
    - '1285616741'

image: /wp-content/uploads/2012/04/IMG_56631-400x198.jpg
categories:
    - 'Piratebox'
tags:
    - Piratebox
---

Ce tutoriel présente l’**installation et la configuration d’une [PirateBox](https://www.nicolashachet.com/blog/2012/03/28/fonctionnement-du-web/piratebox-le-partage-de-fichiers-via-reseau-wifi-local/)**, le dispositif de partage numérique libre, anonyme et gratuit. L’installation d’une **PirateBox** n’est pas si facile pour les non initiés, l’idée est donc d’illustrer le tuto afin de rendre l’installation de la PirateBox plus simple. Prévoyez environ 1h pour monter votre PirateBox de A à Z.

Ce tutoriel est basé sur le tuto de [David Darts, le créateur de PirateBox](https://wiki.daviddarts.com/PirateBox_DIY_OpenWrt).

## Prérequis

Voici la liste du matériel et des pré requis :

- TP-Link MR3020 ([ici](https://www.pixmania.com/fr/fr/11334376/art/tp-link/routeur-portable-3g-3-75g.html) ou [là](https://online.carrefour.fr/electromenager-multimedia/tp-link/tp-link-tl-mr3020-portable-3g-3-75g-wireless-n-router-routeur-sans-fil-802-11b-g-n-ordinateur-de-bureau_a11973406_frfr.html))
- Clé USB (formatée en **FAT32**, n’importe quelle taille, plus y’en a, plus on en met ;))
- Câble ethernet (fourni avec le MR3020)
- Câble USB pour l’alimentation (fourni avec le MR3020)
- Connexion Internet (uniquement nécessaire pour l’installation de la pirate box)
- Batterie USB (si vous souhaitez balader votre PirateBox)

[![TP-Link MR3020](/wp-content/uploads/2012/04/IMG_56631.jpg "IMG_5663")](/wp-content/uploads/2012/04/IMG_56631.jpg)Déballage du TP-Link MR3020

## Préparation du routeur MR3020 de TP Link

### 1. Mettre le MR3020 en mode WISP

Le bouton se situe sur le routeur. Il y a 3 modes : 3G, WISP et AP.
[![](/wp-content/uploads/2012/04/wisp.png "wisp")](/wp-content/uploads/2012/04/wisp.png)  
Pour info WISP c’est : Wireless Information Service Point ou Wireless Internet Service Provider, selon l’utilisation.

### 2. Connecter le MR3020 à votre ordinateur par câble réseau

Le MR3020 doit être sous tension (LED verte allumée), donc connecté à l’aide du câble mini USB à une source d’énergie (port USB de votre ordinateur ou adaptateur secteur fourni).

**Connecter le MR3020 à votre ordinateur grâce au câble réseau** (RJ45), attendez quelques secondes pour que votre ordinateur reconnaisse le périphérique et **ouvrez votre navigateur sur la page <https://192.168.0.254/>** (identifiant : **admin** ; mot de passe : **admin**)  
Vous êtes maintenant connecté à l’interface de configuration du routeur.

[![](/wp-content/uploads/2012/04/IMG_5676.jpg "IMG_5676")](/wp-content/uploads/2012/04/IMG_5676.jpg)Connecter le MR3020 à l’ordinateur via câble réseau

### 3. Mettre à jour le firmware du MR3020

**Télécharger le [Firmware OpenWRT pour MR3020](https://downloads.openwrt.org/snapshots/trunk/ar71xx/generic/openwrt-ar71xx-generic-tl-mr3020-v1-squashfs-factory.bin).**  
 **Naviguer vers System Tools > Firmware Upgrade** sur l’interface d’admin du MR3020  
**Uploader le nouveau firmware** grâce au formulaire prévu à cet effet

Après la mise à jour, le MR3020 va redémarrer.

### 4. Configurer le réseau du MR3020

**En telnet, connectez-vous à l’adresse 192.168.1.1**  
Vous aurez peut être besoin d’[activer telnet sous Windows 7](https://www.libellules.ch/seven_activer_telnet.php) si ce n’est pas déjà fait.

Pour vous connecter via telnet :

> Démarrer > Exécuter… > Tapez **cmd** (une fenêtre noire s’affiche)  
> puis **C:\\> telnet 192.168.1.1**

Vous êtes maintenant connecté au MR3020 via telnet.

**Tapez passwd pour changer le mot de passe**.

> **passwd**

Vous devez saisir le nouveau mot de passe 2 fois (attention, les caractères saisis n’apparaîtront pas à l’écran).

Nous allons maintenant éditer la configuration du réseau. Pour cela, munissez-vous des 2 informations suivantes :

- l’**adresse IP de votre routeur** (ie : l’adresse de votre box). Exemple : <span style="color: #ff0000;">192.168.1.254</span>
- **une adresse IP arbitraire appartenant au réseau**. Exemple : <span style="color: #339966;">192.168.1.55</span>

**Editer le fichier de configuration du résea**u (/etc/config/network).  
Tapez :

> **vi /etc/config/network**

Le fichier doit ressembler à ça :

> config interface ‘loopback’  
> option ifname ‘lo’  
> option proto ‘static’  
> option ipaddr ‘127.0.0.1’  
> option netmask ‘255.0.0.0’
> 
> config interface ‘lan’  
> option ifname ‘eth0’  
> option type ‘bridge’  
> option proto ‘static’  
> option ipaddr ‘<span style="color: #339966;">192.168.1.55</span>‘  
> option netmask ‘255.255.255.0’  
> option gateway ‘<span style="color: #ff0000;">192.168.1.254</span>‘  
> list dns ‘<span style="color: #ff0000;">192.168.1.254</span>‘  
> list dns ‘8.8.8.8’

Enregistrez, pour cela tapez :

> **[Echap]:wq[Entrée]**

Cela enregistrera le fichier **/etc/config/network** et quittera l’éditeur **vi**.  
*En tapant la commande **vi**, vous ouvrez un éditeur de texte (si, si).  
Tapez sur **i** ou touche **Inser** pour insérer du texte. Naviguer dans le texte à l’aide des flèches de votre clavier.*

### 5. Configurer le pare-feu du MR3020

On va maintenant modifier le pare-feu du routeur MR3020. Pour cela, on modifie le fichier **/etc/config/firewall**.  
Avant tout, on fait une copie de sauvegarde :

> **cp /etc/config/firewall /etc/config/firewall.bak**

On édite le fichier /etc/config/firewall (comme tout à l’heure on utilise **vi**)

> **vi /etc/config/firewall**

On appuie de nouveau sur **i** ou **Inser** pour passer en mode insertion et on modifie le fichier pour qu’il ressemble à ça (seules les 23 premières lignes sont modifiées) :

> config defaults  
> option syn_flood ‘1’  
> option input ‘ACCEPT’  
> option output ‘ACCEPT’  
> option forward ‘ACCEPT’  
> \# Uncomment this line to disable ipv6 rules  
> \# option disable_ipv6 1
> 
> config zone  
> option name ‘lan’  
> option network ‘lan’  
> option input ‘ACCEPT’  
> option output ‘ACCEPT’  
> option forward ‘ACCEPT’
> 
> config zone  
> option name ‘wan’  
> option network ‘wan’  
> option input ‘ACCEPT’  
> option output ‘ACCEPT’  
> option forward ‘ACCEPT’  
> option masq ‘1’  
> option mtu_fix ‘1’

On enregistre et on quitte l’éditeur :

> **[Echap]:wq[Entrée]**

### 6. Activer le Wifi du MR3020

On commence à avoir l’habitude, on modifie le fichier **/etc/config/wireless** :

> **vi /etc/config/wireless**

Et on change la ligne 12 pour qu’elle ressemble à ça :

> option disabled 0

Puis tapez :

> **[Echap]:wq[Entrée]**

Le Wifi sera activé au prochain démarrage.

**Débrancher le routeur de sa source d’énergie** (mini USB).

La configuration est maintenant terminée ! On va maintenant passer à l’installation de la PirateBox sur le routeur MR3020. 🙂

## Installation de l’application PirateBox

Pour installer PirateBox, il va nous falloir une connexion Internet.  
On va donc reconnecter notre routeur MR3020 à notre box Internet.

**Connectez le MR3020 directement à votre box Internet grâce au câble réseau**. Dans mon cas, c’est une Bbox.

[![](/wp-content/uploads/2012/04/IMG_5669.jpg "IMG_5669")](/wp-content/uploads/2012/04/IMG_5669.jpg)Le MR3020 est connecté à la box

**Mettre le MR3020 sous tension en le connectant à l’aide du câble mini USB** (ici connecté à mon PC).

### 1. Ajouter la compatibilité USB au routeur

Connectez-vous en SSH au routeur MR3020. Pour cela, vous aurez besoin de Putty ([télécharger Putty](https://the.earth.li/~sgtatham/putty/latest/x86/putty.exe) ou [voir le site](https://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)).

**Connectez-vous via Putty à l’adresse définie à l’étape 4 (ici <span style="color: #339966;">192.168.1.55<span style="color: #000000;">).</span></span>**

En nom d’utilisateur, mot de passe, tapez :

> login as: **root**  
> root@192.168.1.1’s password : **[le mot de passe saisi plus haut lors du passwd – étape 4]**

Attention, les caractères du mot de passe ne s’afficheront pas.

[![](/wp-content/uploads/2012/04/putty_connect.png "putty_connect")](/wp-content/uploads/2012/04/putty_connect.png)Accueil du MR3020 après connexion SSH via Putty

Assurez-vous que la connexion Internet est bien active.

> **ping google.com**

Si ce n’est pas le cas, quelque chose ne va pas dans la configuration du routeur. Je vous conseille de vérifier les informations de configuration du routeur, notamment les adresses IP du réseau.

Ajouter le support USB en tapant les commandes suivantes :

> **opkg update  
> opkg install kmod-usb-uhci  
> insmod usbcore  
> insmod uhci  
> opkg install kmod-usb-ohci  
> insmod usb-ohci**

En cas d’erreur, continuez quand même !  
Une fois toutes les commandes exécutées, le MR3020 a été mis à jour pour prendre en charge une clef USB. Cool 🙂

### 2. Connectez votre clef USB.

Elle doit être formattée en FAT32. Pour le savoir, connectez votre clef à un port USB de votre ordinateur, clic droit sur le lecteur puis Propriétés. Voir Système de fichiers = FAT32 sous Windows 7.

### 3. Installer PirateBox

Dans la fenêtre SSH toujours ouverte, tapez :

> **cd /tmp  
> wget https://piratebox.aod-rpg.de/piratebox_0.3-2_all.ipk  
> opkg update &amp;&amp; opkg install piratebox\***

Pour info, vous pouvez installer la version sans le chat en tapant ces commandes à la place :

> cd /tmp  
> wget https://cr.23bit.net/piratebox/piratebox_0.2-5_all.ipk  
> opkg update &amp;&amp; opkg install piratebox\*

L’installation peut prendre du temps. **Soyez patient** !

[![](/wp-content/uploads/2012/04/finish.png "finish")](/wp-content/uploads/2012/04/finish.png)L’installation de la PirateBox est terminée !

Débrancher le câble réseau que vous pouvez ranger et éteignez le MR3020 complètement.

**Attendez quelques secondes, le temps qu’il se repose, puis redémarrer le.**

### 4. Vous êtes l’heureux propriétaire d’une PirateBox fonctionnelle

Vous ou n’importe qui peut désormais se connecter au réseau **"PirateBox – Share Freely"** avec n’importe quel appareil possédant une carte Wifi.  
En ouvrant votre navigateur, vous devriez tomber sur cette page :

[![accueil piratebox](/wp-content/uploads/2012/04/accueil.png "accueil piratebox")](/wp-content/uploads/2012/04/accueil.png)La page d’accueil piratebox

Tout le traffic est routé vers cette page, donc peu importe l’URL que vous taperez, vous serez rediriger vers cette page. 😉

## Problème : ma PirateBox lente avec la version chat shoutbox (3.2)

Si votre PirateBox est lente avec la shoutbox (chat), modifier le fichier **/etc/config/network** comme ceci :

> config interface ‘loopback’  
> option ifname ‘lo’  
> option proto ‘static’  
> option ipaddr ‘127.0.0.1’  
> option netmask ‘255.0.0.0’
> 
> config interface ‘lan’  
> option ifname ‘eth0’  
> option type ‘bridge’  
> option ipaddr ‘192.168.1.1’  
> option netmask ‘255.255.255.0’  
> option proto ‘static’

[Source](https://forum.daviddarts.com/read.php?2,2415,2623,page=2#msg-2623)

## Mettre à jour sa PirateBox en version 0.5.1

Suite à cette installation, vous pouvez mettre à jour votre PirateBox en version 0.5.1. Je vous invite à découvrir le [tuto de mise à jour en PB 0.5.1](https://www.nicolashachet.com/blog/2012/10/03/fonctionnement-du-web/tutoriel-mettre-a-jour-sa-piratebox-en-version-0-5-1/).  
Il est également possible de remplacer l’étape d’installation de la PirateBox de ce tuto par l’action 7 du tuto de mise à jour.

