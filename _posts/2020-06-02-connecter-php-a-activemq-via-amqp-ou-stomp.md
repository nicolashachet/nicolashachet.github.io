---
id: 3632
title: 'Connecter PHP à ActiveMQ via AMQP ou STOMP ?'
date: '2020-06-02T22:06:17+02:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=3632'
permalink: /blog/developpement-php/connecter-php-a-activemq-via-amqp-ou-stomp/

image: /wp-content/uploads/2020/06/apache-activemq-logo-573x180.png
categories:
    - 'PHP'
---

J’ai récemment travaillé sur une application PHP qui devait envoyer des messages vers [ActiveMQ](https://activemq.apache.org/). Le choix du protocole s’est naturellement porté vers AMQP (Advanced Message Queuing Protocol) qui semblait parfait pour traiter ce type d’interconnexion. D’autant plus que l’application utilisait Symfony et que le composant Symfony Messenger est nativement compatible AMQP.

Je vous le dis tout de suite : ce fut un échec et, à l’heure où je rédige ces lignes, ça le sera aussi pour vous.

## Une histoire de protocole…

En effet, après installation et activation de l’[extension PHP AMQP](https://pecl.php.net/package/amqp), installation d’Apache ActiveMQ en local, et configuration du composant Symfony Messenger, le message suivant apparut coté application PHP :

```
In AmqpSender.php line 74:
Could not connect to the AMQP server. Please verify the provided DSN. ({"host":"localhost","port":5672,"vhost":"f","login":"guest","password":""})
In Connection.php line 400:
Could not connect to the AMQP server. Please verify the provided DSN. ({"host":"localhost","port":5672,"vhost":"f","login":"guest","password":""})
In Connection.php line 394:
Library error: unexpected method received - Potential login failure.
```

Et coté ActiveMQ, voici le rendu de la console :

```
WARN | Connection attempt from non AMQP v1.0 client. AMQP,0,0,9,1
WARN | Transport Connection to: tcp://127.0.0.1:61557 failed: org.apache.activemq.transport.amqp.AmqpProtocolException: Connection from client using unsupported AMQP attempted
```

En faisant des recherches sur le Web, je trouvais [un sujet](https://stackoverflow.com/questions/43873400/unable-to-connect-to-apache-activemq-with-node-js) qui traitait d’une mystérieuse authentification `saslMethod` ou `saslMecanism` et qui renvoyait une erreur similaire. Oubliez tout ça, **en réalité, la vérité était ailleurs (et même dans le message d’erreur en fait).**

Et pour cause, si on lit correctement les informations données par chacun, c’est clair : **PHP-AMQP et ActiveMQ ne partagent pas le même protocole**. Les deux utilisent bien AMQP mais dans des versions différentes :

- L’extension PHP est en version **0.9.1**.
- ActiveMQ est en version **1.0**.

ActiveMQ l’indique clairement :

```
WARN | Connection attempt from non AMQP v1.0 client. AMQP,0,0,9,1
```

Sauf qu’à priori, les deux protocoles n’ont rien à voir et ne sont pas capables de discuter : <https://stackoverflow.com/questions/28402374/amqp-0-9-1-vs-1-0>

Et quand le sujet d’une réconciliation entres les deux est abordés, il n’en est pas question : [ni coté ActiveMQ](https://issues.apache.org/jira/browse/AMQ-5332), [ni coté PHP-AMQP](https://github.com/php-amqplib/php-amqplib/issues/583).

L’échec est acté. 🙁

## Solution pour faire discuter PHP et ActiveMQ via STOMP

Du coup, on change de stratégie et on opte pour un protocole différent : STOMP que je ne connaissais pas. C’est pourtant bien le [protocole recommandé pour se connecter via PHP](https://activemq.apache.org/php). Parfois, il faut simplement lire la doc et ne pas en faire qu’à sa tête.

Exit le Symfony Messenger, même s’il aurait été possible de [développer un transport personnalisé](https://symfony.com/doc/current/messenger/custom-transport.html), et on se tourne vers le [bundle Enqueue](https://github.com/php-enqueue/enqueue-bundle) qui permet de faire exactement ce que l’on souhaite sans extension PHP supplémentaire. Bref, c’est la solution fonctionnelle pour faire dialoguer du PHP avec ActiveMQ.

Un petit coup de config dans le fichier .env pour la connexion avec ActiveMQ via STOMP :

```
###> enqueue/enqueue-bundle ###

ENQUEUE_DSN=stomp://guest:password@localhost:61613
###< enqueue/enqueue-bundle ###
```

Et ensuite on injecte le service qui va bien pour l’envoi des messages :

```
class MessengerService
{
    public function __construct(Enqueue\Client\ProducerInterface $producer)
    {
        $this->producer = $producer;
    }

    public function sendMessage(MessageInterface $message): void
    {
        $enqueueMessage = new \Enqueue\Client\Message('pouet');
        $this->producer->sendEvent('topic', $enqueueMessage);
    }
}
```

Et le tour est joué. 😉
