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

Des environnements 
 - différents
 - isolés 
 - possédant leur propre Ubiquitous Language

**

(Schema représentant les différents bounded contexts : e-boutique, stock, facturation, reporting, etc)

**
##Entity dans E-Boutique
 - Produit
 - Commentaire
 - Note
 - Commande
 ...

**
##Entity dans Stock-Fournisseur
 - Produit 
 - Fournisseur
 - Lieu (de stockage)
 ...

**

Stock  =>   E-Boutique

Note: Schema représentant la communication entre les bounded context => domain event) Que se passe t il quand je change le nom du produit dans le stock ? dois je réellement être dépendant de l'e-boutique 

**

E-Boutique  => Stock

Note: L'E-Boutique doit elle tomber si le stock tombe ?

***

# Eventual consistency

**

Stock =  lance  =>  NomProduitModifiéDomainEvent

Note: Le stock envoi un domain event pour dire que le nom du produit a été
modifié

**

E-Boutique  <=   ecoute = Stock domain event

Note: L'E-Boutique ecoute le domain event et se mets à jour quand il le reçoit

**
Code d'un domain event : NomProduitModifiéDomainEvent

**
Code d'un listener de domain event : E-Boutique product

**
### Avantages
* faible couplages entre les bounded context
* ajout de fonctionnalités sans changements dans le code existant
* robuste
* tolérence aux pannes
* scalabilité 

***
## Avec un broker

* RabbitMQ
* Kafka
* ZeroMQ
...

**
### RabbitMQ

**
 - exchange
 - queue
 - fanout
 - channel
 - virtual host
 - cluster
 - ...

Note: peut etre en 2 slides pour plus de complexité

**

Pas envie de gérer tout ça


***
Domain Event sans MQ : c'est possible

**
##Un peu **event sourcing**

**

##Stockage des events (synchrone)
Note: Rappel de ce que c'est ?

**

##Tous les events sur votre entity

Note: En effet, le but est de pouvoir reconstruire tout

**

## Comment utiliser ça dans les autres bounded context

**

## Api REST

**

```json
{
}
```

**
##Pagination
Note: Hateos ?

**
## Remember

Note: La seule chose dont à besoin de se souvenir le bounded context client,
c'est le dernier event traité

**
## Crontab

**
## Exemple boutique nom / produit

**

## Les + et les -

**

## Conclusion
