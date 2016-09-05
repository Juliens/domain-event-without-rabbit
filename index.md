# FORUMPHP2016

Note:

***
## DOMAIN EVENT

***
### DDD : Domain Driven Design
(image des 2 bouquins d'Evans et Vernon)

***
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
(Exemple code d'une entité pas DDD avec setter/getter uniquement)

***
(Exemple entité équivalente avec code orienté métier)

***
Présentation du thème de l'exemple : shop, OAV capvita ?

***
(Schema représentant les différents bounded contexts : boutique, stock, facturation, reporting, etc)

***
(Schema représentant la communication entre les bounded context => domain event)

***
### Qu'est-ce qu'un Domain Event
* un message publié
* représente un événement passé
* lié à une transaction
* asynchrone

***
(Exemple code d'un domain event : ProduitAcheteEvent ?)

***
(Exemple code publication domain event)

***
(Schema architecture avec message bus entre les bounded context)

***
(Même schema avec domain events)
Le stock écoute le domain event ProduitAcheteEvent pour se mettre à jour, la facturation pour éditer la facture du client, etc

***
### Avantages
* faible couplages entre les bounded context
* ajout de fonctionnalités sans  changements dans le code existant
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