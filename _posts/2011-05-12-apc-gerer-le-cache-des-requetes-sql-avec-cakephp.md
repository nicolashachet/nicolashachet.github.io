---
id: 152
title: 'APC : gérer le cache des requêtes SQL avec CakePHP'
date: '2011-05-12T15:19:16+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=152'
permalink: /blog/developpement-php/apc-gerer-le-cache-des-requetes-sql-avec-cakephp/
categories:
    - 'PHP'
tags:
    - CakePHP
---

La gestion de cache est très importante dans les sites d’envergure. Il est possible de stocker les résultats de requêtes SQL fréquemment utilisées afin de supprimer le temps de traitement lié à l’appel à la base de données. Il existe différentes solutions telles que APC ou memcache. Nous allons voir ici comment utiliser automatiquement APC pour cacher nos requêtes sur nos modèles.

### Redéfinir la fonction find() dans app_model.php

On suppose que APC est installé et configuré correctement sur le serveur PHP (l’installation et la configuration de l’extension php_apc fera l’objet d’un nouveau post). L’idée est de redéfinir la fonction find() de CakePHP afin de ne faire les requêtes que si les données ne sont pas en cache et, le cas échéant, de stocker les résultats récupérés. Dans la pratique, c’est très simple !

**Fichier app_model.php**  
{% highlight php linenos %}
public function find($type, $params = array())  
{  
  // Détermine si les données de ce modèle peuvent être cachées  
  $cachedModel = array(‘Model1’, ‘Model2’);
  
  if (in_array($this->name, $cachedModel)) {
  
    // Détermine la clef de stockage  
    $key = md5($this->useTable . serialize($type) . serialize($params));
    
    $data = apc_fetch($key, $success);
    
    // Les données ont été trouvées, on les renvoi  
    if ($success) {  
      return unserialize($data);  
    } else {  
      $data = parent::find($type, $params);  
      apc_store($key, serialize($data));
      
      return $data;  
    }  
  }
  
  return parent::find($type, $params);  
}
{% endhighlight %}

Vos requêtes vont désormais s’exécuter une première fois puis les résultats seront stockés dans le cache APC. La même requête exécutée plus tard ira piocher dans le cache et non sur le base de données. Les 2 fonctions clefs sont **apc_fetch** qui récupère des données stockées et **apc_store** qui stocke les données en cache.
