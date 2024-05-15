---
id: 2944
title: "Partage de connexion Internet en Wifi : problème pas d&rsquo;Internet &#8211; Configuration APN"
date: '2017-11-10T11:23:45+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2944'
permalink: /blog/telephone/partage-de-connexion-internet-wifi-probleme-dinternet-configuration-apn/
dsq_thread_id:
    - '6274832818'
image: /wp-content/uploads/2017/11/android-wifi-pas-internet-700x485.png
categories:
    - Smartphone
tags:
    - Android
    - Windows
---

Lors du [partage d’une connexion Internet via son téléphone portable](https://www.nicolashachet.com/blog/telephone/connecter-son-ordinateur-a-internet-via-la-4g-de-son-telephone/), il est possible de rencontrer une erreur indiquant "**Pas d’Internet**" dans la barre de notifications Windows alors que la connexion Wifi a bien été effectuée. Je suis récemment tombé sur ce problème, voici donc la solution pour récupérer Internet via son smartphone.

## Étapes pour résoudre le problème "Pas d’Internet"

Les étapes pour résoudre le **problème "pas d’Internet"** lors d’une partage de connexion Internet via Wifi doivent être réalisées sur votre téléphone **Android** :

1. Ouvrez l’application "Paramètres" ;
2. Accédez à l’écran "Connexions" ;
3. Accédez à l’écran "Réseaux mobiles" ;
4. Accédez à l’écran "Nom des points d’accès" ;
5. Trouvez votre point d’accès (celui qui est coché) et cliquez sur son nom (ici, Orange World) ;
6. Les paramètres du point d’accès s’ouvre, défilez l’écran jusqu’au paramètre "Type d’APN" ;
7. Vous devriez voir "default,supl" si vous êtes chez Orange ;
8. Cliquez sur "Type d’APN" pour le modifier et ajoutez : "**,dun**" (virgule "dun") pour avoir ceci : "**default,supl,dun**
9. Quittez l’écran en enregistrant ;
10. Le problème est résolu, vous avez Internet via votre connexion mobile 😉

## Étapes en images pour résoudre le problème "Pas d’Internet"

Et voilà l’enchaînement correspondant en images :

Dans **Paramètres**, cliquez sur **Connexions** :


[![](/wp-content/uploads/2017/11/1.android-parametres-connexions-576x1024.jpg)](/wp-content/uploads/2017/11/1.android-parametres-connexions.jpg)

Dans **Connexions**, cliquez sur **Réseaux mobiles** :


[![](/wp-content/uploads/2017/11/2.android-parametres-connexions-reseaux-mobiles-576x1024.jpg)](/wp-content/uploads/2017/11/2.android-parametres-connexions-reseaux-mobiles.jpg)

Dans **Réseaux mobiles**, cliquez sur **Nom des points d’accès** :


[![](/wp-content/uploads/2017/11/3.android-parametres-connexions-reseaux-mobiles-nom-point-access-576x1024.jpg)](/wp-content/uploads/2017/11/3.android-parametres-connexions-reseaux-mobiles-nom-point-access.jpg)

Dans **Nom des points d’accès**, cliquez sur **Orange World (ou ce qui est sélectionné)** :


[![](/wp-content/uploads/2017/11/4.android-parametres-connexions-reseaux-mobiles-nom-point-access-orange-world-576x1024.jpg)](/wp-content/uploads/2017/11/4.android-parametres-connexions-reseaux-mobiles-nom-point-access-orange-world.jpg)

Dans **Modifier le points d’accès**, cliquez sur **Type d’APN** :


[![](/wp-content/uploads/2017/11/5.android-parametres-connexions-reseaux-mobiles-nom-point-access-orange-world-type-apn-576x1024.jpg)](/wp-content/uploads/2017/11/5.android-parametres-connexions-reseaux-mobiles-nom-point-access-orange-world-type-apn.jpg)

Dans la pop-up **Type d’APN** qui s’ouvre, ajoutez "**dun**" :


[![](/wp-content/uploads/2017/11/6.android-parametres-connexions-reseaux-mobiles-nom-point-access-orange-world-type-apn-dun-576x1024.png)](/wp-content/uploads/2017/11/6.android-parametres-connexions-reseaux-mobiles-nom-point-access-orange-world-type-apn-dun.png)

Cliquez sur **OK** puis **Enregistrez** : c’est terminé, vous devriez pouvoir accéder à Internet depuis votre ordinateur connecté en Wifi 🙂
