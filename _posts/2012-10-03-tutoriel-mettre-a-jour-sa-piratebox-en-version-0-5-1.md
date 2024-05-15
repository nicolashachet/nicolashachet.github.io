---
id: 1259
title: 'Tutoriel : mettre à jour sa PirateBox en version 0.5.1'
date: '2012-10-03T22:08:38+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1259'
permalink: /blog/fonctionnement-du-web/tutoriel-mettre-a-jour-sa-piratebox-en-version-0-5-1/
dsq_thread_id:
    - '1285617622'
image: /wp-content/uploads/2012/10/piratebox.jpg
categories:
    - 'Piratebox'
tags:
    - Piratebox
---

Ce tutoriel présente la **mise à jour en version 0.5.1 de la PirateBox**.  
Il s’agit d’une traduction de l’[article original de David Darts (en)](https://forum.daviddarts.com/read.php?2,3820,4064#msg-4064).

1. Allumez la PirateBox et connectez-vous en SSH  
    [shell]ssh root @ 192.168.1.1[/shell]
2. Editer le fichier de configuration pour vérifier que l’on pourra se connecter à la PB par câble et accéder à Internet  
    [bash]  
    vi /etc/config/network  
    [/bash] Le fichier doit ressemble à ça.Ici, l’adresse IP de la box est **192.168.2.1** et l’adresse de la PirateBox est **192.168.2.111**:
    
    [shell]  
    config interface ‘loopback’  
     option ifname ‘lo’  
     option proto ‘static’  
     option ipaddr ‘127.0.0.1’  
     option netmask ‘255.0.0.0’
    
    config interface ‘lan’  
     option ifname ‘eth0’  
     option type ‘bridge’  
     option proto ‘static’  
     option ipaddr ‘192.168.2.111’  
     option netmask ‘255.255.255.0’  
     option gateway ‘192.168.2.1’  
     list dns ‘192.168.2.1’  
     list dns ‘8.8.8.8’  
    [/shell]
3. Brancher la PirateBox par câble ethernet puis redémarrer la PB et se connecter en SSH :  
    [shell]  
    ssh root @ 192.168.2.111  
    [/shell]
4. Arrêter l’application PirateBox et supprimer l’installation  
    [shell]  
    /etc/init.d/piratebox stop  
    opkg remove piratebox  
    [/shell]
5. Arrêter le service de résolution DNS  
    [shell]  
    /etc/init.d/piratebox nodns  
    [/shell]
6. Ping vers google pour s’assurer de la bonne connexion à Internet  
    [shell]  
    ping google.com  
    [/shell]
7. Installer PirateBox 0.5.1  
    [shell]  
    cd /tmp  
    wget https://piratebox.aod-rpg.de/piratebox_0.5.1_all.ipk  
    opkg install piratebox\*  
    [/shell]
8. Installer le forum Kareha  
    [shell]  
    /opt/piratebox/bin/install_piratebox.sh /opt/piratebox/conf/piratebox.conf imageboard  
    [/shell]
9. Editer la configuration du forum pour changer l’utilisateur / mot de passe (ADMIN_PASS et SECRET)  
    [shell]  
    vi /opt/piratebox/www/board/config.pl  
    [/shell]
10. Débrancher le câble ethernet et redémarrer.

C’est fini ! Vous pouvez vous connecter au réseau PirateBox. 😉
