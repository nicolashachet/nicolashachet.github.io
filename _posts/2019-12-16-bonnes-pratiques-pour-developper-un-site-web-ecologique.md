---
id: 3420
title: 'Bonnes pratiques pour développer un site Web écologique'
date: '2019-12-16T09:50:00+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=3420'
permalink: /blog/numerique-responsable/bonnes-pratiques-pour-developper-un-site-web-ecologique/
dsq_thread_id:
    - '7766523974'
image: /wp-content/uploads/2019/12/bonnes-pratiques-informatique-internet-web-ecologie-700x525.jpg
categories:
    - 'GreenIT'
---

L’impact écologique des services informatiques est désormais connu. En prenant conscience des conséquences environnementales des outils informatiques, l’**écologique numérique** prend tout son sens. Lorsqu’on développe un site Internet, une application ou tout autre service informatique, nous avons vu que l’[éco-conception nécessite une prise en compte au plus tôt dans le projet](https://www.nicolashachet.com/blog/ecologie/comment-concevoir-un-site-internet-ecologique/). Aujourd’hui, abordons les **bonnes pratiques à respecter pour développer un site Web écologique**.

## Objectif : réduire les ressources utilisées par le site

L’objectif est simple : il faut **réduire la consommation d’énergie**, donc réduire le nombre d’équipements et la puissance cumulée nécessaire à l’exécution de l’application Web. Autrement dit :

- Réduire le nombre de requêtes,
- Diminuer le volume de données échangées,
- Limiter les traitements, notamment coté serveur.

En 2012, j’écrivais l’article [Optimiser les performances de son site Web](https://www.nicolashachet.com/blog/developpement-php/optimiser-les-performances-de-son-site-web-google/), dans le contexte de sobriété numérique, il n’a pas bougé d’un iota…

## Utilisez un référentiel de bonnes pratiques pour l’écologie numérique

Avant de rentrer dans le vif du sujet, sachez qu’il existe un référentiel de règles éditées par CNumR ([Collectif Conception Numérique Responsable](https://collectif.greenit.fr/)). A noter que les règles ci-dessous ne proviennent pas de ce référentiel mais sont issues de mon expérience en conception et développement. Je vous invite donc à les compléter en vous procurant [Ecoconception web : les 115 bonnes pratiques](https://www.eyrolles.com/Informatique/Livre/ecoconception-web-les-115-bonnes-pratiques-9782212678062/).

## Utilisez les caches navigateurs

Première étape vers un site moins consommateur : **utilisez du cache**. Ou plutôt des caches ! En 2014, je vous expliquais qu’il existe une multitude de [mécanismes de cache permettant d’optimiser les performances de votre site](https://www.nicolashachet.com/blog/developpement-php/optimisation-web-php-des-caches-a-tous-les-niveaux/). Ce point est crucial : un site Web moderne pèse plusieurs Mo, voire dizaine de Mo pour les plus gourmands. En utilisant les caches mis à notre disposition, on évite le transfert de nombreux fichiers durant la navigation.

Vous devez jouer sur les niveaux de caches suivants :

- le **cache navigateur** qui consiste à utiliser le stockage des fichiers sur le navigateur Web du client via les entêtes HTTP **Cache-Control** et **Expires**. Il est géré par le navigateur lui-même et évite le chargement systématiquement des ressources statiques : CSS, JS, images, etc.
- le **stockage navigateur** qui consiste à utiliser un espace mis à disposition par le navigateur pour vous permettre de stocker des données (SessionStorage ou LocalStorage). Par exemple, plutôt que de charger X fois une liste déroulante, chargez là une fois et stockez là coté client, vous éviterez des requêtes sur le serveur.

## Utilisez les caches applicatifs

Dans la lignée de la bonne pratique précédente, il est impératif de mettre en place des caches coté serveur. Ainsi, on évite de nombreux traitements inutiles : appels à la base de données, calculs de données, génération de pages, gestion de données référentielles, etc.

Vous devez jouer sur les niveaux de caches suivants :

- le **cache OPCode** (OPcache) désormais embarqué en natif depuis [PHP 5.5](https://www.php.net/manual/fr/intro.opcache.php),
- les **caches applicatifs** de votre architecture : cache de bases de données (**Mysql Query Cache** par exemple), caches de données applicatives (**APCu, Redis, Memcached**, …).

## Utilisez les caches serveurs 

Dernier niveau de cache : le stockage des pages coté serveur Web. Les serveurs modernes permettent de stocker les pages statiques sans faire appel au backend qui génère la page HTML : Varnish, Nginx, Apache proposent de mettre en cache les pages statiques afin d’éviter leur génération systématique ([Apache mod_cache](https://httpd.apache.org/docs/2.4/fr/caching.html) ou [Nginx proxy_cache](https://docs.nginx.com/nginx/admin-guide/content-cache/content-caching/)).

Vous pouvez également utiliser les **ESI (Edge Side Includes)** ou **SSI (Server Side Includes)** pour mettre en cache des morceaux de pages tandis que les éléments dynamiques sont chargés de manière asynchrone. L’exemple le plus courant est celui d’un composant "panier" sur un site Web e-commerce qui est nécessairement dynamique tandis que le reste de la page est statique (page produit, catégorie, etc.).

## Limiter le nombre de requêtes

La bonne requête, c’est celle qui ne part pas. Les caches permettent de les réduire lors de la navigation, mais le chargement initial des pages n’échappe pas à cette règle. Il faut donc :

- **Concaténer et minifier** vos assets (JS et CSS),
- <span style="text-decoration: underline;">Selon les cas</span>, supprimez complètement vos fichiers JS et CSS et **incluez directement le code JS et CSS** en tant qu’inline dans le code HTML (avec la compression GZIP active),
- Utiliser des **sprites** pour vos icônes. le mieux étant d’utiliser des polices d’icônes incluant uniquement les icones utilisés),

## Activer la compression GZIP

Autre bonne pratique pour réduire la bande passante nécessaire au chargement de votre site : activer la **compression GZIP** sur votre serveur Web. Sous Apache, il s’agit du module [mod_deflate](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html). Sous Nginx, regardez du coté du module [ngx_http_gzip](https://nginx.org/en/docs/http/ngx_http_gzip_module.html).

## Redimensionner et compresser les images

Les images sont des ressources très consommatrices de bande passante. Vous aurez beau appliquer les techniques énoncées ci-dessus et vous retrouvez avec une page HTML initiale à 20Ko, si vous chargez ensuite des images de plusieurs mégas, votre travail sera inutile. Veillez donc à :

- **Redimensionner vos images** en fonction de l’utilisation qui en est faite. Une image de 1600×900 utilisée en tant que logo de 250×100 est inutile : redimensionnez l’image dans la bonne taille directement. D’autant qu’on réduit également le traitement effectué par le navigateur qui n’aura plus à forcer le redimensionnement à l’affichage.
- **Compresser vos images**. Sur du JPEG vous pouvez facilement descendre à une qualité entre 80 et 90% sans grosse perte. Sur du PNG, veillez à utiliser un outil de compression sans perte (TinyPNG par exemple).

## Chargez les images en lazy-loading

Le **lazy-loading des images** est une technique qui consiste à charger les images uniquement quand vous en avez besoin, c’est à dire que vous scrollez votre page dessus. Ainsi, les images non affichées sur votre navigateur ne sont pas chargées à l’initialisation de la page, mais uniquement quand elles deviennent visibles (en fait, un tout petit peu avant).

Cette technique simple à mettre en place est intéressante sur tous les périphériques d’accès, mais particulièrement sur smartphone pour 2 raisons :

- la **bande passante en 3G ou 4G est plus faible** : votre site se chargera donc plus rapidement si les images invisibles ne sont pas chargées,
- la **surface du site affichée est plus petite sur un smartphone** (le **viewport** qui désigne la surface visible dans votre navigateur) : donc potentiellement vous devrez charger moins d’image)

## Utilisez des images responsives

La configuration des **images responsives** permet de laisser aux navigateurs **le choix des images à charger** selon différents critères : la taille de l’écran, la densité de pixels (pour les écrans HD ou 4K par exemple), la surface réelle utilisée par l’image lors de son affichage. Cette technique ajuste les images chargées, et donc la quantité de données transférées, au besoin : vous n’avez pas besoin d’une image de plusieurs Mo sur un mobile par exemple.

Cette technique se met en place via les attributs HTML5 de la balise <img> **srcset** et **sizes**. Vous trouverez des informations utiles à leur sujet [ici](https://www.alsacreations.com/article/lire/1621-responsive-images-srcset.html) et [là](https://www.hteumeuleu.fr/attribut-srcset-images-responsive/).

## Eviter les sliders d’images

On a souvent tendance à mettre un slider d’images en début de site afin de donner un coté dynamique. Écologiquement parlant, c’est une erreur (et **ergonomiquement également** soit dit en passant, les images autres que la première étant rarement vues par les utilisateurs).

## Supprimer les vidéos

Exit les vidéos lues automatiquement à l’initialisation de la page ou les fonds de pages animés. Les flux vidéos représentent quasiment [60% du trafic mondial sur Internet](https://www.sandvine.com/hubfs/downloads/phenomena/2018-phenomena-report.pdf). Rien qu’à lui seul, Netflix c’est 15%… Dans de nombreuses situations, les vidéos n’ont aucun intérêt, autre que celui de voir quelque chose qui bouge à l’écran. Supprimez-les et, si elles sont vraiment utiles, désactivez l’autoplay.

## Évitez les rechargements de page complets

Vous avez mis en place un reload automatique de votre page toutes les 60 secondes ? D’une part, c’est insupportable pour les utilisateurs… D’autre part c’est inutilement consommateur de ressources. Quand c’est nécessaire, privilégiez les requêtes AJAX ne chargeant que ce qui est utile ou les websocket si vous avez besoin de temps réel. *Sur cette dernière solution, je cherche de l’information concernant la consommation de ressources, contactez-moi si vous en avez !*

## Soyez sobre sur les tâches programmées : AJAX, CRON…

Que ce soit pour les requêtes AJAX ou pour les CRON, il ne sert à rien de prévoir un rafraîchissement des données toutes les 10 secondes si l’information ne se met à jour que 2 fois par jour. Peut-être qu’un délai de 30 minutes est suffisant. Toutes **les tâches programmées récurrentes doivent être minutieusement dimensionnées** afin d’éviter des consommations inutilement excessives.

## Evitez de stocker des données inutiles

Les serveurs informatiques hébergent un nombre incalculable de données inutiles (pensez à votre boite mail). Les bases de données : c’est pareil. Nous récoltons généralement bien plus de données que nécessaires au strict fonctionnement de l’application. Soyez donc raisonné sur les données collectées, et notamment sur **les logs et traces applicatives qui grossissent sans cesse**. Non seulement, la planète vous remerciera mais vous ferez également un pas vers la conformité RGPD (qui implique de justifiez l’usage des données personnelles des utilisateurs).

## Conclusion

Vous l’aurez compris : la ligne de conduite à adopter quand on développe un site Internet ou une application éco-responsable est de **limiter le transfert de ressources entre le client et le serveur**.

La bonne nouvelle, c’est que ces recommandations sont non seulement utiles dans le cadre de l’**écoconception numérique**, mais jouent également un rôle majeur dans les **performances du site Web**, dans l’**expérience utilisateur**, dans le **SEO** et dans le **coût global** de votre projet. Bref, vous n’avez aucune raison valable de ne pas les mettre en place dans vos projets informatiques.

**On en discute ?**  
N’hésitez pas à commenter et à partager cet article.
