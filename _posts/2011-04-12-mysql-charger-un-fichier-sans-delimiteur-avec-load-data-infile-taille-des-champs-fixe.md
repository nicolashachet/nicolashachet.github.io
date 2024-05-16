---
id: 93
title: 'MySQL : charger un fichier sans délimiteur avec LOAD DATA INFILE (taille des champs fixe)'
date: '2011-04-12T15:09:15+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=93'
permalink: /blog/developpement-php/mysql-charger-un-fichier-sans-delimiteur-avec-load-data-infile-taille-des-champs-fixe/
dsq_thread_id:
    - '1285594177'
categories:
    - 'MySQL'
---

MySQL permet d’importer des fichiers grâce à l’instruction LOAD DATA INFILE. Il arrive fréquement que les fichiers d’import ne possèdent pas de délimiteur et qu’il faille se baser sur la taille des champs afin de retrouver la correspondance entre champ et donnée.  
MySQL permet de charger ce type de fichier sans problème mais il existe une petite subtilité à connaitre.

## Utiliser l’encodage latin1 pour les tables d’import

Prenons l’exemple d’un fichier très simple (id, nom, prenom). Chaque ligne fait 35 caractères et respecte le format suivant :  
  
ID = 5 caractères  
NOM = 15 caractères  
PRENOM = 15 caractères  


Voici un fichier de test (/home/nhac/utilisateurs.import):  
  
00001 Travolta John  
00002 Dylan Bob  
00003 Murhpy Eddy  


L’astuce pour charger le fichier sous MySQL est d’indiquer **CHARSET ‘latin1’** lors de la création de la table. En effet, si vous spécifiez **CHARSET ‘UTF8’**, le chargement ne se fera pas correctement.

```sql  
— Creation de la table cible  
DROP TABLE IF EXISTS utilisateurs;  
CREATE TABLE IF NOT EXISTS utilisateurs (  
 `id` CHAR(5),  
 `nom` CHAR(15),  
 `prenom` CHAR(15)  
) ENGINE=MyISAM CHARSET ‘latin1’;

— Chargement du fichier  
LOAD DATA LOCAL INFILE ‘/home/nhac/utilisateurs.import’  
INTO TABLE utilisateurs  
 FIELDS TERMINATED BY" ENCLOSED BY"  
(  
 `id`, `nom`, `prenom`  
);  
````

Rien ne vous empêche de transférer ces données encodées en **latin1** vers une table en **UTF8** après l’import.

## Pourquoi faut-il utiliser latin1 lors des imports de taille fixe ?

Vous trouverez de l’info sur les liens Wikipedia ci-dessous. La chose à retenir est qu’en UTF8 les caractères sont codés sur un nombre d’octets variables (entre 1 et 4). MySQL ne peut donc pas savoir à l’avance combien il doit prévoir pour stocker les données, et donc combien de caractères il doit lire dans le fichier.  
A l’inverse en latin1 (dit ISO-8859-1), les caractères sont codées sur un seul octet. MySQL sait donc qu’il doit lire un et un seul octet à partir du fichier.

[Lien Wikipédia vers l’ISO-8859-1](https://fr.wikipedia.org/wiki/ISO-8859-1)  
[Lien Wikipédia vers l’UTF8](https://fr.wikipedia.org/wiki/UTF-8)  
[Aller plus loin sur le sujet](https://balusc.blogspot.com/2009/05/unicode-how-to-get-characters-right.html)
