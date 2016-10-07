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
## DDD & Domain Events

** 
<img src="./img/images/livre-ddd.jpg" width="300" style="float: left;" />
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
<img src="./img/images/implementing-ddd.jpg" width="300" style="float: left;" />
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
<img src="./img/images/what.png" />

*Exemples de domain event*

Note: Les domain events, ce sont tous les évenements métiers qui peuvent se
passer dans la vie de votre application
**

### Qu'est-ce qu'un Domain Event techniquement ?

**
<!-- .slide: data-background="./img/images/message-bouteille.jpg" -->
###Un message publié <!-- .element: class="text-hover-image" -->

**
<!-- .slide: data-background="./img/images/back-to-the-future.jpg" -->
###Représente un événement passé <!-- .element: class="text-hover-image" -->

**
###Lié à une transaction <!-- .element: class="text-hover-image" -->

**
<!-- .slide: data-background="./img/images/asynchrone.jpg" -->
###Asynchrone <!-- .element: class="text-hover-image" -->

**
```php
interface \DomainEventInterface
{
    public function getType();
    public function getRootEntityId();
    public function occurredOn();
    public function getEventInformationsAsArray();
}
```
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
**
Différents <!-- .element: class="text-hover-image" --> 

**
<!-- .slide: data-background="./img/images/isolated.jpg" -->
Isolés <!-- .element: class="text-hover-image" -->

**
<!-- .slide: data-background="./img/images/coffee.jpg" -->
Avec leur propre Ubiquitous Language <!-- .element: class="text-hover-image" -->

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
<!-- .slide: data-background="./img/images/avantages.jpg" -->
## Avantages <!-- .element: class="text-hover-image" -->

**
Faible couplages entre les bounded context <!-- .element: class="text-hover-image" -->

**
Ajout de fonctionnalités sans changements dans le code existant <!-- .element: class="text-hover-image" -->

**
<!-- .slide: data-background="./img/images/robuste2.jpg" -->
Robuste <!-- .element: class="text-hover-image" -->

**
<!-- .slide: data-background="./img/images/tolerance-pannes4.jpg" -->
Tolérence aux pannes <!-- .element: class="text-hover-image" -->

**
<!-- .slide: data-background="./img/images/scalability.jpg" -->
Scalabilité <!-- .element: class="text-hover-image" -->

***
## Avec un broker

* RabbitMQ
* Kafka
* ZeroMQ
...

**
### RabbitMQ

**
<img src="./img/images/rabbitmq-schema.png" width="600" style="float: left;" />
 - exchange
 - queue
 - fanout
 - channel
 - virtual host
 - cluster
 - ...

Note: peut etre en 2 slides pour plus de complexité

**
<!-- .slide: data-background="./img/images/pieces-detachees-auto.jpg" -->
Pas envie de gérer tout ça <!-- .element: class="text-hover-image" -->


***
<!-- .slide: data-background="./img/images/possible.jpg" -->
Domain Event sans Broker : c'est possible <!-- .element: class="text-hover-image" -->

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
