---
id: 2690
title: 'Quels systèmes de paiement pour votre projet Web ?'
date: '2016-10-10T17:40:27+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2690'
permalink: /blog/developpement-php/quels-systemes-de-paiement-psp-projet-web/
dsq_thread_id:
    - '5212017325'
image: /wp-content/uploads/2016/10/ecommerce-paiement-en-ligne-573x300.jpg
categories:
    - 'PHP'
tags:
    - e-Commerce
    - 'Paiements en ligne'
    - PHP
---

Les **prestataires de paiement**, ou **PSP** pour Payment Service Provide, permettent d’**accepter les paiements en ligne** sur les sites **e-commerce**. Il existe deux sortes de solutions de transfert d’argent : les produits proposés par les banques et les solutions dédiées en ligne. Au delà du paiement classique par carte bancaire, ces solutions proposent de nombreux moyens de paiement alternatifs [comme le dévoile 1and1](https://www.1and1.fr/digitalguide/web-marketing/vendre-sur-internet/apercu-des-services-de-paiement-en-ligne/) dans son guide digital : Paypal, Bitcoin, Skrill, etc. Le choix d’un PSP nécessite donc une analyse fine qui se base sur les fonctionnalités proposées et sur les habitudes de paiement de vos clients. Dans tous les cas, la sécurité et la simplicité d’utilisation font parties des enjeux majeurs du paiement en ligne. Afin de vous aiguiller, petit tour d’horizon des systèmes de paiement pour votre site Web e-commerce.

## Paypal

[![paypal](/wp-content/uploads/2016/09/paypal.png)](/wp-content/uploads/2016/09/paypal.png)Quand on pense paiement en ligne, on pense généralement à Paypal. Cette solution de paiement a envahi le e-commerce grâce à sa simplicité d’usage pour les consommateurs. En effet, inutile de disposer de sa carte bancaire pour effectuer un paiement en ligne : Paypal se charge de stocker les précieuses données et de dialoguer avec le site e-commerce pour procéder au paiement. Grâce à ce rôle d’intermédiaire, c’est clairement l’un des acteurs incontournables du marché des PSP. Techniquement, les connecteurs pour de nombreuses plateformes e-commerce sont disponibles, ce qui le rend simple à mettre en place coté webmaster. La tarification est cependant moins avantageuse que les autres PSP listés ci-dessous : 3.4% + 0.25€ / transaction.

## Stripe

[![stripe](/wp-content/uploads/2016/09/stripe.jpg)](/wp-content/uploads/2016/09/stripe.jpg)Stripe est un prestataire de paiement qui s’est fait un nom grâce à son système de paiement en marque blanche. Concrètement, Stripe fournit une [API REST](https://www.nicolashachet.com/blog/niveaux/confirme/larchitecture-rest-expliquee-en-5-regles/) permettant d’accepter des paiements depuis de nombreux pays via différents types de carte : CB, Visa et American Express (Amex) notamment. Les coûts réduits (1.4% + 0.25€ / transaction) ont achevé d’en faire, à mon sens, l’autre incontournable des PSP.

## MangoPay

[![mangopay](/wp-content/uploads/2016/09/mangopay.png)](/wp-content/uploads/2016/09/mangopay.png)Dans la même veine que Stripe, Mangopay est un PSP proposé par Leetchi en marque blanche dont la particularité est de simplifier la gestion des cagnottes et des marketplaces. Les moyens de paiement acceptés sont Visa, Mastercard et Paylib, ce qui autorise principalement des paiements issus de l’Union Européenne, Amex n’étant pas encore supporté. Basé sur une API REST et sur une inscription minimaliste, la tarification est de 1.8% + 0.18€ par transaction. Une bonne alternative à Stripe.

## PayLine

[![payline](/wp-content/uploads/2016/09/payline.jpg)](/wp-content/uploads/2016/09/payline.jpg)Payline est un PSP dédié aux entreprises gérant plusieurs boutiques en ligne ou avec de gros volumes de transactions. Il accepte tous les moyens de paiement imaginables et propose dans son pack "Maxi" la possibilité de traiter les transactions par lot, ce qui en fait l’allié idéal des vendeurs multi-boutiques ou des PSP en marque blanche… Payline est ainsi le support pour d’autres PSP dont la plus value est la gestion de la fraude et la simplicité d’usage. Sa tarification est légèrement différente des autres : 35€ / mois + 0.8€ / transaction au delà de 300.

## BitPay

[![bitpay](/wp-content/uploads/2016/09/bitpay.jpg)](/wp-content/uploads/2016/09/bitpay.jpg)Enfin, comme son nom l’indique, BitPay permet d’accepter des paiements via BitCoin, le sulfureux moyen de paiement connu pour son utilisation répandue dans le Darknet. Avec des frais de 1% / transaction et une conversion bitcoin/devise quasiment instantanée, les intérêts d’accepter les BitCoin sont réels au delà du caractère anonyme des paiements. Le fonctionnement de BitCoin en fait l’une des monnaies les plus sûres en terme de sécurité de paiement.

Vous pouvez désormais envisager d’intégrer un PSP sur votre site e-commerce. Par ailleurs, n’oubliez pas de prendre en compte les nouveaux moyens de paiement : paiement mobile, paiement en 1 clic, etc. Dans les années à venir, l’émergence de ces nouveaux moyens de paiement pourrait révolutionner le marché des prestataires de paiement en ligne.
