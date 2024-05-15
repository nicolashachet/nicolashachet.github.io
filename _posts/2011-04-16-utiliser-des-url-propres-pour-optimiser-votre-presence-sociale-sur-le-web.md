---
id: 120
title: "Utiliser des URL propres pour optimiser votre présence sociale sur le Web"
date: '2011-04-16T10:03:18+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=120'
permalink: /blog/seo/utiliser-des-url-propres-pour-optimiser-votre-presence-sociale-sur-le-web/
dsq_thread_id:
    - '1285640318'

image: /wp-content/uploads/2011/04/url.jpg
categories:
    - SEO
---

Beaucoup de sites Web ou de blogs utilisent les réseaux sociaux afin d’**accroître leur visibilité sur le Web.** C’est désormais une pratique courante et intéressante pour faire tourner les informations rapidement à peu de frais. L’idée de ce post est de former des URL propres pour que l’**utilisateur retienne simplement les adresses**.

# Créer des sous-domaines du site principal

Les sous-domaines sont terriblement pratiques. D’une part ils sont courts ; d’autre part ils permettent de segmenter distinctement des parties ou des fonctionnalités de vos sites. L’idée est donc d’associer un réseau social à un sous-domaine du site, comme ceci :

```
https://facebook.nicolashachet.com/
https://twitter.nicolashachet.com/
```

Vous pouvez bien évidement faire ça avec n’importe quel autre partie de votre site Web : forum, boutique, etc. Cela permet de **hiérarchiser les contenus**.

Tous les hébergeurs proposent de créer des sous-domaines. Chez 1and1 (par exemple), il suffit de se rendre sur la gestion des domaines et de créer un sous-domaine.

[![Sous domaine 1and1](/wp-content/uploads/2011/04/ssdom1and1-300x73.png "Sous domaine 1and1")](/wp-content/uploads/2011/04/ssdom1and1.png)

# Rediriger vos sous-domaines vers vos pages sur les réseaux sociaux

Une fois vos sous-domaines créés, vous pouvez : soit définir une **redirection** vers une URL directement, soit pointer vers un **répertoire particulier** de votre hébergement.

Dans le premier cas, il suffit d’indiquer l’URL de votre page facebook par exemple. Ainsi **https://facebook.nicolashachet.com/** pointera vers

```
https://www.facebook.com/pages/Le-blog-de-Nicolas-Hachet/193381087370803
```

Dans le second, **https://facebook.nicolashachet.com/** pointera vers un répertoire, **/redirection/facebook/** par exemple. Il faut ensuite créer un fichier **index.php** pour faire la redirection "à la main" :

```
header('Status: 301 Moved Permanently', false, 301);
header('Location: https://www.facebook.com/pages/Le-blog-de-Nicolas-Hachet/193381087370803');
```

C’est terminé, vous devriez maintenant vous retrouver avec des URL propres vers vos pages sur les réseaux sociaux !

[Nicolas Hachet sur Facebook](https://facebook.nicolashachet.com/)  
[Nicolas Hachet sur Twitter](https://twitter.nicolashachet.com/)
