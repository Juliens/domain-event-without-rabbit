# FORUM PHP 2016
**
# PUBLIER DES DOMAIN EVENTS 

**

# SANS RABBITMQ, C’EST POSSIBLE !

**

- DDD
  - Domain Event
  - Bounded Context
- Broker
  - RabbitMQ
- Alternative au broker

Note: Nous allons donc vous parler de DDD et plus précisement ect...

***
# Qui sommes nous ?

**

Simon Delicata
...
Note: On est des tueurs bla bla bla

**
Julien Salleyron
Architecte technique DSI Alptis
Note: On est des tueurs bla bla bla

***
## DDD : Domain Event

** 
*(image bouquin Evans)*
* Ubiquitous language
* Bounded context
* Model Driven Design
* Layered Architecture
* Entities
* Value Objects
* Aggregates
* Anti Corruption Layer


Note: Quand on parle de DDD, très souvent, on cite la bible DDD mais pas de
Domain Event dans la bible

**
*(image bouquin Vernon)*
* Ubiquitous language
* Bounded context
* Model Driven Design
* Layered Architecture
* Entities
* Value Objects
* Aggregates
* Anti Corruption Layer
* **Domain Events**

Note: En fait, quand on parle de DDD, un livre important est celui de Vernon,
et dans IDDD il nous parle des Domain Events

**
### Domain Event : Kesako ?

*Exemples de domain event*

Note: Les domain events, ce sont tout les évenements métiers qui peuvent se
passer dans la vie de votre application
**

### Qu'est-ce qu'un Domain Event Techniquement
* un message publié
* représente un événement passé
* lié à une transaction
* asynchrone

**
*example de code (interface) d'un Event (root_id, occured_on)*

**
Présentation du thème de l'exemple : la boutique en ligne
(il faudrait trouver un thème de boutique pour essayer de rendre l'exemple un peu fun)

**
*Example du domain event*

***
## Les Bounded Contexts

**
Schema avec Tactical Pattern / Strategic Pattern avec le bounded context

**

(Schema représentant les différents bounded contexts : e-boutique, stock, facturation, reporting, etc)

***
(Schema représentant la communication entre les bounded context => domain event)

***

***
Code d'un domain event : ProduitAcheteEvent
(src/ProduitAcheteEvent.php)
(Matérialiser les bounded contexts avec des namespace par ex, pour que ca soit plus visuel ?)

***
Code d'un listener de domain event : FacturationProduitAcheteListener
(src/FacturationProduitAcheteListener.php)

***
(Schema architecture avec message bus entre les bounded context)
Le stock écoute le domain event ProduitAcheteEvent pour se mettre à jour, la facturation pour éditer la facture du client, etc

***
### Avantages
* faible couplages entre les bounded context
* ajout de fonctionnalités sans changements dans le code existant
* robuste
* tolérence aux pannes
* scalabilité 

***

## Service de MQ
* RabbitMQ
* Kafka
* ZeroMQ

***
Qu'est-ce que c'est ?

***
(Image représentant des Ops qui ne veulent pas gérer un RabittMQ)

***
Schema d'une architecture très simple avec seulement 2 bounded contexts

***
Domain Event sans MQ : c'est possible

***
(Code de dispatch d'un Domain Event sans MQ)

***
(Code de listener d'un Domain Event sans MQ)
