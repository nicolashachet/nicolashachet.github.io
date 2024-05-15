---
id: 1737
title: 'Tester l&rsquo;existence d&rsquo;une fonction Javascript'
date: '2013-05-13T23:27:17+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1737'
permalink: /blog/developpement-php/tester-lexistence-dune-fonction-javascript/
dsq_thread_id:
    - '1286083884'
image: /wp-content/uploads/2013/05/javascript.png
categories:
    - 'JS'
tags:
    - Javascript
---

Ci-dessous une petite astuce **Javascript** pour vérifier qu’une fonction est définie ou non. Le comportement rappelle la fonction "function_exists()" en PHP. Le test se base sur la fonction Javascript typeof() qui renvoie *function*si le handler passé est déclaré comme fonction.

```javascript
function test(){  
 return (typeof(mafonction) == "function") ? alert(‘mafonction existe’) : alert("mafonction n’existe pas");  
}  
test();  
//function mafonction() {}  
```

Il suffit de décommenter ‘mafonction’ pour constater que l’existence de la fonction est correctement prise en compte.

Pour vérifier si un handler est utilisé comme une fonction ou comme une variable, vous pouvez utiliser le même principe en testant la valeur de retour "undefined" de la fonction typeof().

```javascript
function test() {  
 return (typeof(mafonction) == "undefined") ? alert(‘mafonction existe’) : alert("mafonction n’existe pas");  
}  
test();  
function mafonction() {}  
var mafonction = "";  
```
