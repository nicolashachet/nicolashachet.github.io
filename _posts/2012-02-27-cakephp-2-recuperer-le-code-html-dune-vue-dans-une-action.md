---
id: 657
title: 'CakePHP 2 : récupérer le code HTML d&rsquo;une vue dans une action'
date: '2012-02-27T16:31:55+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=657'
permalink: /blog/developpement-php/cakephp-2-recuperer-le-code-html-dune-vue-dans-une-action/
dsq_thread_id:
    - '1287574649'
categories:
    - 'PHP'
tags:
    - CakePHP
    - PHP
---

Pour une raison x ou y, vous souhaitez **récupérer le code HTML d’un template donné**. Ca peut s’avérer pratique pour envoyer un template complet formaté en JSON via AJAX. N’ayant trouvé que peu de doc sur le sujet, je vous livre ici une solution :

{% highlight php linenos %}  
public function fragment() {  
 // Assignation de vos données  
 $this->set(‘datas’, $vos_donnees);

 // Appel d’un élément particulier (facultatif)  
 $this->render(‘/Elements/datas_fragment’);

 // Récupération du code HTML généré par l’appel à render()  
 $view = $this->View->output;

 debug($view);  
 exit;  
}  
{% endhighlight %}

Ici il vous faudra un élément datas_fragment.ctp mais vous pouvez également utiliser le template par défault en appelant render() sans paramètre. Ainsi, vous pouvez récupérer le code HTML qui sera renvoyé par la Vue. Cela peut être pratique pour envoyer du code HTML en AJAX.
