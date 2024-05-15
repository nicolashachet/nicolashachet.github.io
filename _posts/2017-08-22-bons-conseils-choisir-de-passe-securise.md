---
id: 2914
title: 'Les bons conseils pour choisir un mot de passe sécurisé'
date: '2017-08-22T14:41:28+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=2914'
permalink: /blog/fonctionnement-du-web/bons-conseils-choisir-de-passe-securise/
dsq_thread_id:
    - '6086275121'
image: /wp-content/uploads/2017/08/mot-de-passe-password-securise-573x322.jpg
categories:
    - 'Sécurité'
---

Vous avez peut être vu l’information sortir un peu partout sur les sites de news il y a quelques jours : les vrais conseils pour **choisir un mot de passe sécurisé** ont (enfin) été révélés ! Ou plutôt les anciennes préconisations ont été dézinguées par l’auteur lui-même. Exit les mots de passe de 8 caractères contenant majuscules, minuscules, caractères spéciaux, chiffres, donc impossibles à retenir… Ces recommandations de 2003 avaient été publiées par le NIST (National Institute of Standards and Technology) et faisaient jusqu’alors office de référence. L’auteur du rapport, Bill Burr, a même fait son méa culpa dans le [Wall Street Journal… ](https://www.wsj.com/articles/the-man-who-wrote-those-password-rules-has-a-new-tip-n3v-r-m1-d-1502124118)

## Les mots de passe actuels sont faibles

Le constat est clair : les mots de passe actuels sont faibles. Le rapport a été écrit il y a 15 ans sur la base de fondement théorique et les préconisations édictées n’ont jamais été validées. Les anciennes préconisations étaient les suivantes : longueur minimale de 8 caractères avec lettres en majuscule, lettres en minuscule, chiffres, caractères spéciaux et le tout devait être changé tous les 90 jours.

Sauf qu’en tant qu’utilisateurs, nous nous sommes mis à créer systématiquement de mots de passe de la longueur minimale avec des "techniques" pour mieux retenir celui-ci : "mot2passe!", "Azerty123", etc. Et à cause du fait de devoir changer son mot de passe a intervalle très régulier, on s’est mis à simplement modifier un caractère de son mot de passe : "Password!1", "Password!2", "Password!3", etc.

Problème : tout ça n’a rien de très sécurisé puisque la liste des "astuces" pour retrouver facilement son mot de passe est connue des pirates. Les virus et kits de hack embarquent des [listes des mots de passe faibles](https://www.developpez.com/actu/112390/Classement-des-mots-de-passe-les-plus-utilises-123456-en-tete-suivi-de-123456789-et-qwerty-quels-sont-selon-vous-les-pires-mots-de-passe-a-bannir/) ainsi que des algorithmes générant les variantes les plus utilisées à travers le monde. La sécurité n’est pas donc au rendez-vous et il est temps de changer les habitudes.

## Conseils pour choisir un mot de passe sécurisé

Voici donc les nouvelles règles qui permettent de créer un bon mot de passe, c’est à dire **un mot de passe robuste, sécurisé et facile à retenir**.

### Privilégiez la longueur du mot de passe

On s’en doutait, la longueur du mot de passe est primordiale. C’est même la clef d’un mot de passe sécurisé et robuste. A l’instar des nombres premiers très longs qui permettent de sécuriser les transactions (et qui régissent la sécurité sur Internet, soit dit en passant), il est nécessaire de choisir un mot de passe le plus long possible. Oubliez les 8 pauvres caractères et construisez des phrases ou des suites de mots. En toute logique "Z#!P4d9z" est moins sécurisé que "J’aime bien les mots de passe !". Et pourtant le second est beaucoup plus facile à retenir que le premier…

Néanmoins, attention car utiliser une phrase très connue n’est pas non plus un gage de sécurité. Préférez construire votre propre phrase. Et si le service vous refuse de créer un mot de passe avec plus de 20 caractères, quittez le !

### N’utilisez pas un mot de passe unique

C’est un conseil généralement agaçant mais il est fortement déconseillé d’utiliser un seul mot de passe pour l’ensemble de vos comptes. Préférez un mot de passe unique par service. Pour ça, les gestionnaires qui retiennent l’ensemble de vos mots de passe sont de bons alliers.

### Évitez d’utiliser des informations personnelles

Vos noms, prénoms, date et ville de naissance, etc. ne devraient jamais être utilisées pour créer vos mots de passe sécurisés. Et pour cause, toutes ces informations peuvent être retrouvées facilement pour peu que vous ayez un compte Facebook, Twitter ou LinkedIn. Même une information donnée en message privé d’un forum ou d’un réseau social peut se retourner contre vous. Si vous n’êtes pas porteur d’informations sensibles, le risque est certes faibles, mais mieux vaux être prudent.

## Calculer la force d’un mot de passe

Une fois un mot de passe construit, il est possible de **calculer la force d’un mot de passe**, c’est à dire sa capacité à résister à un brut force (un essai complet de toutes les possibilités). Cette formule est très simple et donne une bonne vision de la robustesse de son mot de passe. La voici :

**N<sup>L</sup>**

avec N = l’alphabet du mot de passe (les caractères disponibles)  
et L = la longueur du mot de passe.

Ainsi, on peut calculer la force typique des mots de passe avec l’ancienne norme et avec la nouvelle norme :

<span style="text-decoration: underline;">Avec l’ancienne méthode :</span>

**90**<sup>**8 = 4304672100000000**  
</sup>avec 90 symboles (0..9, A à Z, a à z et &#128; ! #$\*% ? &amp;[|]@^µ§ :/ ;.,<>°²³) sur une taille de 8 caractères.

<span style="text-decoration: underline;">Avec la nouvelle méthode :</span>

**62**<sup>**25 = 6,45e+44**  
</sup>avec 62 symboles (0..9, A à Z et a à z) sur une taille de 25 caractères.

C’est à dire une force immensément plus grande qu’un simple mot de passe sur 8 ou 10 caractères. Vous l’aurez compris, il n’y a pas de comparaison possible au niveau de la force du mot de passe, même si vous n’utilisez pas de caractères spéciaux, de chiffres ou même de majuscules !

Un calculateur assez bien fait est disponible sur le [site Web de l’ANSSI](https://www.ssi.gouv.fr/administration/precautions-elementaires/calculer-la-force-dun-mot-de-passe/) (Agence Nationale de la Sécurité de Systèmes d’Information).

En résumé, ce qui fait un mot de passe robuste et sécurisé c’est sa longueur et non le nombre de caractères. **On n’utilise plus un mot de passe mais plutôt une phrase de passe**. Cependant attention à ne pas utiliser une phrase célèbre ou passe partout !
