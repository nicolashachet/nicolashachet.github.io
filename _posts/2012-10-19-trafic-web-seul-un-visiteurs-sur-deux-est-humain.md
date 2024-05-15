---
id: 1303
title: 'Trafic Web : seul un visiteur sur deux est humain'
date: '2012-10-19T11:03:45+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1303'
permalink: /blog/fonctionnement-du-web/trafic-web-seul-un-visiteurs-sur-deux-est-humain/
dsq_thread_id:
    - '1285640386'
image: /wp-content/uploads/2012/10/trafic_web.jpeg
categories:
    - 'Web'
---

Une étude de mars 2012 menée par le cabinet américain *Incapsula* révèle que seul un visiteur sur deux est humain. Le trafic généré par de véritables visiteurs ne constitue ainsi que la minorité du **trafic Web : seulement 49% des visiteurs sont d’origines humaines**.

## 31% du trafic Web dangereux

L’étude montre que les **agents de menace** constituent la seconde part du gâteau avec **31% du trafic**.

Parmi les menaces identifiées, les plus répandues sont liées à l’**espionnage économique** : relèves de prix automatisées, tracking d’informations sur l’état de santé de l’entreprise, étude des stratégies via analyse sémantique des contenus, capture de documents, etc.

Les "espions" profitent non seulement des **informations publiques** publiées par leur cible mais également des **failles de sécurité** liées aux mauvaises configurations des serveurs Web. Grâce à l’indexation automatisées de *contenus parfois égarés* sur les serveurs, ils peuvent ainsi avoir accès à des informations confidentielles ou stratégiques.

## Mais également 20% de trafic utile

La dernière part du trafic se révèle être beaucoup plus intéressante pour les sites testés : près de **20% de leur trafic est utilisé par les robots d’indexation** des moteurs de recherche. Il s’agit de **trafic utile non directement productif**.

Dans le cadre de sites Web à contenus fortement variables, cela constitue certes une charge importante mais évidemment un passage obligé pour un site Web correctement indexé. Pour les autres (sites de présentation sans contenu mis à jour), il est possible de spécifier l’*intervalle minimum de passage d’un robot* via la **balise HTML meta revisit-after** :

```
<meta content="30 days" name="revisit-after"></meta>
```

## Sources

[L’article Incapsula](https://www.incapsula.com/the-incapsula-blog/item/225-what-google-doesnt-show-you-31-of-website-traffic-can-harm-your-business)
