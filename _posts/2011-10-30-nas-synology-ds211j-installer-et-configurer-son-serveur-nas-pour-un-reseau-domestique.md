---
id: 196
title: 'NAS Synology DS211j : installer et configurer son serveur NAS pour un réseau domestique'
date: '2011-10-30T17:16:20+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=196'
permalink: /blog/developpement-php/nas-synology-ds211j-installer-et-configurer-son-serveur-nas-pour-un-reseau-domestique/
categories:
    - 'NAS'
---

[![NAS Synology DS211j](/wp-content/uploads/2011/10/1-286x300.png "NAS Synology DS211j")](/wp-content/uploads/2011/10/1.png)NAS Synology DS211j

Au coeur du réseau, le NAS (Network Attached Storage) offre des possibilités sans limite : stockage de photos, vidéos, musiques, radios, téléchargements, etc. J’ai testé pour vous l’installation et la mise en place d’un serveur NAS **Synology DS211j** pour mon réseau domestique. Ordinateurs, consoles de jeux, téléphones portables et utilisation à distance sont au menu de cet article.

## Matériels utilisés : serveur, disques durs et périphériques externes

Voici le matériel dont je dispose pour installer mon réseau :

- NAS **Synology DS211j**
- 2 disques durs **Hitachi 3k7000 7200 RPM 2To**
- Routeur **freebox V5**
- Ordinateur portable **Sony VAIO**
- Téléphone portable **Sony Ericsson Xperia X10**
- Console de jeu **Sony PS3**

Tout ce petit monde va donc être connecté au serveur NAS via mon réseau interne existant.

## Installation du serveur

[![Synology](/wp-content/uploads/2011/10/2-150x150.png "Synology")](/wp-content/uploads/2011/10/2.png)Synology

Après déballage, l’installation du Synology DS211j est très simple. La notice d’installation sur CD-Rom accompagnant le serveur est claire et ne nécessite aucune connaissance particulière.  
Une fois les disques mis en place et le serveur connecté au réseau, vous devrez cependant installer le DSM du serveur (téléchargeable sur le site de Synology), c’est en quelques sortes son système d’exploitation. Il vous faudra compter sur une vingtaine de minutes pour cela.

Toutes ces opérations sont accessibles depuis l’interface d’administration du serveur : https://XX.XX.XX.XX:5000/webman/index.cgi où XX.XX.XX.XX est l’adresse IP du serveur, généralement de la forme 192.168.0.XX.

Ensuite, vous devez créer un volume (une partition),- dans mon cas j’ai choisi d’utiliser mes 2 disques Hitachi en RAID 1 (sécurisation des données par duplication d’un disque sur l’autre) -, et lancer l’opération de formatage/préparation des disques. Cette opération s’avère très longue : compter environ **5 heures pour 2 disques de 2 To**. Si vous étiez pressé de tester la bête, une peu de patience sera de mise !

Une fois ces opérations complétées avec succès, le matériel est prêt à être utilisé sans problème.

## Gestion des accès et création d’utilisateurs

Le NAS propose de créer une arborescence de fichiers et d’y autoriser l’accès à certains utilisateurs. C’est très pratique pour autoriser l’accès aux fichiers à des amis, de la famille ou même des clients.  
Pour profiter de cette fonctionnalité, il suffit de créer des utilisateurs sur l’interface d’administration et de leur donner des droits de lecture/écriture sur les dossiers de votre choix.  
Les utilisateurs ne voient alors que les fichiers sur lesquels ils ont une autorisation.

[![Panneaude configuration](/wp-content/uploads/2011/10/3-300x171.png "Interface de configuration")](/wp-content/uploads/2011/10/3.png)Synology DS211j – Interface de configuration

## Configuration et paramétrage des ordinateurs du réseau

L’utilisation du NAS sur les ordinateurs du réseau est enfantine. Il vous suffira d’ajouter un nouveau lecteur réseau en utilisant les utilisateurs/mots de passe créés précédemment pour y accéder.  
Le serveur apparait alors comme un lecteur classique.  
Notez que 3 dossiers "systèmes" sont actifs sur le serveur si vous utilisez les applications correspondantes : music, photo et video. Synology propose d’activer ces 3 applications via le panneau de configuration du NAS.

A noter que, par défault, le nom réseau du serveur est **DiskStation**. Ainsi vous pourrez y accéder en tapant \\\\diskstation dans votre explorateur de fichiers préféré.

Vous pouvez alors vous connecter simplement via le système de fichiers Windows (ou Mac ou Linux).

[![Emplacement réseau sous Windows 7](/wp-content/uploads/2011/10/4-300x54.png "Emplacement réseau sous Windows 7")](/wp-content/uploads/2011/10/4.png)Emplacement réseau sous Windows 7

## Connecter tous les appareils de votre réseau interne

Grâce à la certification DLNA, votre serveur NAS Synology fait office de disque dur pour tous vos appareils supportant cette norme. Consoles de jeux, lecteurs DVD, télévisions, tous vos appareils peuvent désormais se connecter au serveur afin d’y lire les fichiers photos, audios et vidéos (avec les sous-titres) ! Il faut activer la fonction DLNA sur votre serveur et effectuer une recherche de serveur sur les appareils à synchroniser. Voici un exemple avec une Sony PS3 :

[![Playstation 3 et synology ds211j](/wp-content/uploads/2011/10/5-300x176.png "Playstation 3 & synology ds211j")](/wp-content/uploads/2011/10/5.png)Le NAS Synology DS211j est compatible avec la PS3 de Sony

Le serveur est reconnu automatiquement et les données sont accessibles très facilement via la XMB de Sony : musique, photos, vidéos, divX, tout est lisible sur votre Sony PS3 ! 🙂

## Connecter vos appareils mobiles !

Synology a prévu des applications pour téléphones portables afin de se connecter au serveur via le réseau 3G. Ainsi vous aurez accès à vos playslits ainsi qu’à vos photos de n’importe où sur la planète.

Les applications sont disponibles sur l’Android Market :

- [DS Photo+ pour Android](https://market.android.com/details?id=com.synology.dsphoto&feature=search_result)
- [DS Audio pour Android](https://market.android.com/details?id=com.synology.DSaudio&feature=search_result)

Coté réseau, une petite configuration des redirections de ports au niveau de votre routeur sera nécessaire (exemple ici avec une freebox v5). La plupart des services proposés sont activés sur le serveur

[![](/wp-content/uploads/2011/10/6-229x300.png "ds211j - freebox V5")](/wp-content/uploads/2011/10/6.png)Configuration des ports sur une freebox V5

La liste des ports à forwarder est disponible sur le site de Synology : [Ports réseau utilisés par le Synology DS211j](https://www.synology.com/support/faq_show.php?q_id=299&lang=fre)

## Conclusion

Le Synology DS211j et les NAS en général deviendront rapidement un élément indispensable de votre réseau domestique. Au coeur de votre système domestique ou de petite entreprise, leurs fonctionnalités, leur puissance et le faible coût feront des heureux qui, comme moi, ne pourront plus s’en passer.

Pour un prix très abordable, le Synology DS211j remplira ses fonctions à merveille.
