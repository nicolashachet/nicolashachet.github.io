---
id: 501
title: 'Comment megaupload va-t-il réouvrir son service de téléchargement ?'
date: '2012-01-21T13:51:20+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=501'
permalink: /blog/fonctionnement-du-web/comment-megaupload-va-t-il-reouvrir-son-service-de-telechargement/
dsq_thread_id:
    - '1285640326'

image: /wp-content/uploads/2012/01/megaupload_bloque-641x198.png
categories:
    - 'Web'
tags:
    - MegaUpload
---

*Mise à jour : 24 septembre 2012*

![](/wp-content/uploads/2012/01/pirate-190x300.gif "pirate")C’est l’actu de la semaine : [le **FBI** a bloqué l’accès au site **megaupload.com**](https://www.lefigaro.fr/societes/2012/01/19/20005-20120119ARTFIG00753-la-justice-americaine-bloque-le-site-megaupload.php) ! Je rappelle que megaupload est un service de téléchargement direct : les fichiers sont stockés sur les serveurs MU que l’internaute va chercher directement. Les réactions hostiles contre cette décision ne se sont pas fait attendre, notamment via le groupe [Anonymous](https://www.franceinfo.fr/societe/fermeture-de-megaupload-anonymous-organise-la-riposte-504981-2012-01-21). Question : comment le site megaupload va-t-il remettre en ligne son service de téléchargement ?

## Comprendre le blocage

Pour comprendre comment le FBI a bloqué megaupload, je vous conseille cet article très clair paru sur Le Monde : [comment le FBI a bloqué megaupload ?](https://www.lemonde.fr/technologies/infographie/2012/01/20/comment-le-fbi-a-t-il-bloque-megaupload_1632639_651865.html)

En résumé, ce qui a été bloqué ce n’est pas le site en lui-même, c’est le moyen d’y accéder. Concrètement, le nom de domaine megaupload.com ne pointe plus vers les serveurs megaupload mais vers une page que le FBI a créée :


[![](/wp-content/uploads/2012/01/megaupload_bloque-300x225.png "megaupload_bloque")](/wp-content/uploads/2012/01/megaupload_bloque.png)

Ce blocage est rendu possible par le fait que l’entreprise qui gère les registres des noms de domaine en **.com**, **Verisign**, se trouve sur le sol américain. Voici l’état du nom de domaine megaupload.com via une requête WHOIS dans la base de Verisign :

WHOIS information for megaupload.com :  
[Querying whois.verisign-grs.com]  
[whois.verisign-grs.com]

Whois Server Version 2.0

Domain names in the .com and .net domains can now be registered  
with many different competing registrars. Go to https://www.internic.net  
for detailed information.

Domain Name: MEGAUPLOAD.COM  
Registrar: DOTREGISTRAR, LLC.  
Whois Server: whois.dotster.com  
Referral URL: https://www.dotster.com  
Name Server: NS1.MEGAUPLOAD.COM  
Name Server: NS2.MEGAUPLOAD.COM  
Name Server: NS3.MEGAUPLOAD.COM  
Name Server: NS4.MEGAUPLOAD.COM  
Status: clientDeleteProhibited  
Status: clientTransferProhibited  
Status: clientUpdateProhibited  
Updated Date: 28-nov-2011  
Creation Date: 21-mar-2005  
Expiration Date: 21-mar-2014



## Comment mégaupload va réapparaître sur le net ?

Et bien ce n’est pas gagné car les serveurs sont sous scellés, aux mains de la justice Américaine. Il fut question, un temps, d’autoriser les utilisateurs à récupérer les fichiers légaux mais nous n’avons pas plus d’informations pour l’instant.

On reste en attente de plus amples informations. En attendant faites bien attention aux sites hameçons (phishing) qui fleurissent sur le net.

*Mise à jour : 24 septembre 2012*  
Voilà du nouveau ! Enfin ! Il semblerait que MegaUpload se prépare à lancer un nouveau service. Selon le [Blog des Nouvelles Technologies](https://www.blog-nouvelles-technologies.fr/archives/18350/megaupload-serait-pret-a-faire-son-retour-son-code-source-termine-a-90/) qui cite [TorrentFreak](https://torrentfreak.com/megaupload-readies-for-comeback-code-90-done-120923/), le code source du nouveau MegaUpload serait terminé à 90%. Un retour imminent qui ne serait réservé qu’aux usagers non américains :

> We are building a massive global network. All non-US hosters will be able to connect servers &amp; bandwidth

– Kim Dotcom

Bref, wait &amp; see…

## Adresses IP des serveurs megauploads

Ancienne adresse IP de megaupload.com : <https://107.21.243.42>  
Nouvelle adresse IP : aucune pour l’instant…

## Alternatives à MegaUpload

Vous trouverez ci-dessous des **sites similaires à MegaUpload**. Il s’agit d’une shortlist des services de stockages et de téléchargements en ligne.

- RapidShare
- 4shared
- filedropper
- [ZippyShare](https://www.zippyshare.com/)
