---
id: 126
title: 'MySQL : mise à jour d&rsquo;un champ avec contrainte d&rsquo;unicité (UPDATE)'
date: '2011-04-22T12:33:40+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=126'
permalink: /blog/developpement-php/mysql-mise-a-jour-dun-champ-avec-contrainte-dunicite-update/
dsq_thread_id:
    - '1285642120'
categories:
    - 'MySQL'
---


[![](/wp-content/uploads/2011/04/mysql-update-command-150x150.png "mysql-update-command")](/wp-content/uploads/2011/04/mysql-update-command.png)  
Hier, j’ai eu un problème lors de la mise à jour de plusieurs enregistrements. L’idée était d’incrémenter un numéro d’ordre dans une table, le numéro d’ordre étant associé à une contrainte d’unicité. Le problème est qu’une erreur **Duplicate entry ‘3’ for key ‘ordre’**  était levé dès la modification du premier enregistrement. Logique : la modification des lignes se fait séquentiellement…

## Reproduction de l’erreur

La table a la structure suivante : id, ordre, code  
La contrainte d’unicité est placée sur le champ ordre.

**Script de création de la table**  
[sql]  
CREATE TABLE `test` (  
`id` SMALLINT NOT NULL ,  
`ordre` SMALLINT NOT NULL ,  
`code` VARCHAR( 2 ) NOT NULL  
) ENGINE = MYISAM;

ALTER TABLE `test` ADD UNIQUE (`ordre`);  
[/sql]

Afin d’illustrer mon propos, voici un jeu de données permettant de reproduire l’exemple.  
**Jeu de données**  
[sql]  
INSERT INTO `test` (`id` ,`ordre` ,`code`) VALUES  
(‘1’, ‘1’, ‘A0’),  
(‘2’, ‘2’, ‘A1’),  
(‘3’, ‘3’, ‘A2’);  
[/sql]

## Mise à jour séquentielle des données 

Imaginons que nous voulions déplacer les lignes dont l’ordre est supérieur ou égal à 2 afin d’insérer un enregistrement à la place. Instinctivement nous écrivons une requête comme celle-ci :

[sql]  
UPDATE test SET ordre = ordre + 1 WHERE ordre >= 2;  
[/sql]

Et voici la réponse de MySQL :  
[sql]  
\#1062 – Duplicate entry ‘3’ for key ‘ordre’  
[/sql]

**Logique, MySQL exécute ligne à ligne les updates et vérifient après chaque enregistrement les contraintes sur les données.** Argh, que faire ?

## UPDATE … SET … ORDER BY …

La solution se trouve sur la doc MySQL : le cas de figure a été prévu. Il est en effet possible de spécifier l’ordre dans lequel seront traitées les lignes. On utilise pour cela la clause ORDER BY, plus connu avec un SELECT mais qui fonctionne également très bien avec l’UPDATE. Ainsi, notre requête peut s’exécuter sans problème.

**La requête correcte**  
[sql]  
UPDATE test SET ordre = ordre + 1 WHERE ordre >= 2 ORDER BY ordre DESC;  
[/sql]  
[sql]  
Nombre d’enregistrements affectés : 2 (Traitement en 0.0004 sec.)  
[/sql]

Le tour est joué ! MySQL a bien modifié nos données selon notre volonté.

Pour en savoir plus : [la documentation MySQL](https://dev.mysql.com/doc/refman/5.0/fr/update.html)
