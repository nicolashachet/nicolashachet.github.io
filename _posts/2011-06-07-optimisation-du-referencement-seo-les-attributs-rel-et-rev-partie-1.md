---
id: 171
title: 'Optimisation du référencement (SEO) : les attributs HTML rel et rev'
date: '2011-06-07T15:03:52+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=171'
permalink: /blog/seo/optimisation-du-referencement-seo-les-attributs-rel-et-rev-partie-1/
dsq_thread_id:
    - '1285640499'
categories:
    - SEO
tags:
    - Google
---

Les **attributs HTML** **rel** et **rev** prennent de plus en plus d’importance dans la construction des pages Web et dans l’optimisation du référencement **SEO (Search Engine Optimisation)**. Cet article a pour but de vous éclairer sur l’utilisation des **attributs REL et REV sur les balises HTML <a>**.

## Quelle différence entre attributs REL et REV ?

Placés sur **la balise a (<a>)**, ces deux attributs permettent de spécifier une **relation logique** entre la page sur laquelle est présent le lien et la cible de l’attribut **href**.

La balise **rel** permet de spécifier une relation entre la page du **href** et la page courante (rel = relation).  
La balise **rev** permet de spécifier une relation "retour" entre la page du **href** et la page courante (rev = retour).

Les deux balises précises quelle est la relation de la cible du lien, la valeur de l’attribut **href** donc.

**Un exemple vaut mieux qu’un long discours**

```html
Page d’accueil : <a href="table_matieres.html" rel="contents">Table des matières</a>

Page article – Retour : <a href="table_matieres.html" rev="contents">Retour à la table des matières</a>  
Page article – Chapitre 1 : <a href="chapitre1.html" rel="chapter">Chapitre 1</a>  
```

**REV indique donc une relation inverse à REL.**

## Quelles sont les valeurs possibles pour les attributs rel et rev ?

Les relations suivantes sont possibles :

- rel="**contents**" indique: lien à la table des matières
- rel="**chapter**" indique: lien au chapitre
- rel="**section**" indique: lien à la partie
- rel="**subsection**" indique: lien à la sous-section
- rel="**index**" indique: lien à l’index des mots clés
- rel="**glossary**" indique: lien au glossaire
- rel="**appendix**" indique: lien à l’annexe (
- rel="**copyright**" indique: liens à la mention des droits
- rel="**ext**" indique: lien au fichier suivant dans la "visite guidée"
- rel="**prev**"indique: lien au fichier précédent dans la "visite guidée"
- rel="**start**" indique: lien au premier fichier dans la "visite guidée"
- rel="**help**" indique: lien à l’aide contextuelle
- rel="**bookmark**" indique: lien à un point d’orientation générale
- rel="**alternate**" indique: lien à un fichier avec le même contenu que le fichier actuel mais dans une autre version du document
- rel="**canonical**" indique: lien à un fichier avec le même contenu que le fichier actuel
- rel="**nofollow**" indique: lien à ne pas suivre pour l’indexation (et donc le report du pageRank du site source)

## Et à quoi ça sert de spécifier ces fameux rel et rev ?

Et bien, pour les moteurs de recherches comme Google, ces attributs permettent de **hiérarchiser le contenu d’un site Web**. Ils permettent à Google et aux autres de faciliter leur "compréhension" du site Internet, de son contenu et de son organisation. De plus en plus, **les moteurs de recherche sont friands de toutes ces informations invisibles pour l’utilisateur qui structurent le contenu**. L’objectif est d’aider le moteur de recherche à se faire une représentation fidèle des contenus qu’ils parcourent, dans l’optique d’en améliorer le classement et la restitution lors d’une recherche utilisateur.

Les balises rel et rev ne sont qu’une petite partie de la stratégie nécessaire à un bon positionnement. Il est notamment possible de citer l’utilisation des balises structurantes **h1**, **h2**, **h3**, etc. Ça fera sous doute l’objet d’un prochain article.

Dans la partie 2, nous reviendrons sur l’utilisation des attributs **rel="alternate"**, **rel="canonical"** et **rel="nofollow"**.
