# FORUMPHP2016

Note:

***
## DOMAIN EVENT

***
### DDD : Domain Driven Design
(image des 2 bouquins d'Evans et Vernon)

***
(Quelques termes important pour expliqué qu'on ne s'intéresse qu'à un petit morceau récent : les domain events)
* Ubiquitous language
* Bounded context
* Model Driven Design
* Layered Architecture
* Entities
* Value Objects
* Domain Events
* Aggregates
* Anti Corruption Layer

***
Présentation du thème de l'exemple : la boutique en ligne
(il faudrait trouver un thème de boutique pour essayer de rendre l'exemple un peu fun)

***
(Schema représentant les différents bounded contexts : e-boutique, stock, facturation, reporting, etc)

***
(Schema représentant la communication entre les bounded context => domain event)

***
### Qu'est-ce qu'un Domain Event
* un message publié
* représente un événement passé
* lié à une transaction
* asynchrone

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