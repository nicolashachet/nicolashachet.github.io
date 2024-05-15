---
id: 203
title: 'Unix bash : récupérer le pid d&rsquo;un script lancé par un script'
date: '2011-08-04T15:54:14+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=203'
permalink: /blog/developpement-php/unix-bash-recuperer-le-pid-dun-script-lance-par-un-script/

categories:
    - 'Unix'
---

Sous UNIX, voici une petite astuce permettant de **récupérer l’identifiant du processus (PID) ouvert par un script bash**.

- **$$** récupère le pid de script courant
- **$!** récupère le pid du dernier script lancé

Ainsi, il est possible de contrôler l’exécution d’une sous tâche grâce au PID du processus. Pour vous en convaincre, un petit exemple de script BASH :

```
#!/bin/bash
echo "PID du processus courant : $$"
echo "PID du processus lancé : $!"

# On lance une commande en background avec  &
# Ca peut être une commande, un autre script bash, un programme, etc...
ping localhost &
echo "PID du processus courant : $$"
echo "PID du processus lancé (ping localhost) : $!"
sleep 3
kill $!
exit 0
```
