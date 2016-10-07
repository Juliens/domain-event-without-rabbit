# FORUM PHP 2016
**

# PUBLIER DES DOMAIN EVENTS 

**

# SANS RABBITMQ, C’EST POSSIBLE !

**

- DDD
  - Domain Event
  - Bounded Context
  - Eventual consistency
- Broker
  - RabbitMQ
- Alternative au broker

Note: Nous allons donc vous parler de DDD et plus précisement etc...

***
# Qui sommes nous ?

**
Julien Salleyron
Architecte technique DSI Alptis
Note: On est des tueurs bla bla bla

**
Simon Delicata
Lead développeur / Référent technique Alptis Assurance
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
Domain Event dans la bible, très théorique

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
et dans IDDD : moins théorique, ex de code, ajout des Domain Events

**
### Domain Event : Kesako ?
<img src="./img/images/what.png" />

*Exemples de domain event orienté métier*

Note: Les domain events, ce sont tous les évenements métiers qui peuvent se
passer dans la vie de votre application
ex : client change d'adresse, change de sexe, etc
**

<!-- .slide: data-background="./img/images/message-bouteille.jpg" -->
###Un message publié <!-- .element: class="text-hover-image" -->
Note: on publie le message sans se pré-ocupper de qui va le recevoir

**
<!-- .slide: data-background="./img/images/back-to-the-future.jpg" -->
###Représente un événement passé et daté <!-- .element: class="text-hover-image" -->
Note: passé, daté : ordre important

**
###Lié à une entité ou un aggrégat <!-- .element: class="text-hover-image" -->
Note: concerne toujours une entité. ex: personne change de nom

**
<!-- .slide: data-background="./img/images/asynchrone.jpg" -->
###Contient les informations de l'évenement métier<!-- .element: class="text-hover-image" -->
Note: changement adresse => ancienne et nouvelle adresse

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
Note: example de code (interface) d'un Event (root_id, occured_on)

**
## Les Bounded Contexts

**
Schema avec Tactical Pattern / Strategic Pattern avec le bounded context
Note: les gens se focalisent sur les * patterns (doctrine) et oublient les * patterns (bounded contexts)
**

Des environnements métiers
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
 - Prix
 - Lieu (de stockage)
 ...

**
##Comment synchroniser tout ça ?

**
Stock  =>  E-Boutique

Note: Schema représentant la communication entre les bounded context => domain event) Que se passe t il quand je change le nom du produit dans le stock ? dois je réellement être dépendant de l'e-boutique 

**

E-Boutique  => Stock

Note: L'E-Boutique doit elle tomber si le stock tombe ?

***

# Eventual consistency
Note: les données ne sont pas consitantes entre les bounded contexts / désynchronise
**

Stock =  lance  =>  NomProduitModifiéDomainEvent

Note: Le stock envoi un domain event pour dire que le nom du produit a été
modifié

**

E-Boutique  <=   ecoute = Stock domain event

Note: L'E-Boutique ecoute le domain event et se mets à jour quand il le reçoit
Faible couplage

**
Code d'un domain event : NomProduitModifiéDomainEvent

**
Code d'un listener de domain event : E-Boutique product

**
<!-- .slide: data-background="./img/images/avantages.jpg" -->
## Avantages <!-- .element: class="text-hover-image" -->

**
Couplage faible entre les bounded context <!-- .element: class="text-hover-image" -->
Note: ex coupure du stock

**
Ajout de fonctionnalités sans changements dans le code existant <!-- .element: class="text-hover-image" -->
Note: nouveau bounded context : suivi du transport a besoin de connaître un changement de poids => rien à modifier dans le stock, il suffit de s'abonner

**
<!-- .slide: data-background="./img/images/robuste2.jpg" -->
Robuste <!-- .element: class="text-hover-image" -->
Note: robuste parce que...

**
<!-- .slide: data-background="./img/images/tolerance-pannes4.jpg" -->
Tolérant aux pannes <!-- .element: class="text-hover-image" -->
Note: ... tolérent aux pannes

**
<!-- .slide: data-background="./img/images/scalability.jpg" -->
Scalabilité <!-- .element: class="text-hover-image" -->
Note: Ouvrir la porte à la scalabilité de part le fonctionnement avec des events

***
## Broker

* RabbitMQ
* Kafka
* ZeroMQ
...
Note: implémente le pattern publishsubcribe, permet de gérer des events

**
### RabbitMQ

**
<img src="./img/images/rabbitmq-schema.png" width="600" style="float: left;" />
 - cluster
 - virtual host
 - exchange
 - queue
 - fanout
 - channel
 - ...

**
<!-- .slide: data-background="./img/images/pieces-detachees-auto.jpg" -->
Complexité <!-- .element: class="text-hover-image" -->
Note: Pas envie de gérer tout ça

**
Infrastructure

***
<!-- .slide: data-background="./img/images/possible.jpg" -->
Domain Event sans Broker : c'est possible <!-- .element: class="text-hover-image" -->

**
##Event sourcing
Note: on s'inspire du pattern l'event sourcing

**
##Stockage des events (synchrone)
Note: Enregistre tous les events liés à la transaction, tout le temps

**
##Tous les events sur votre entity
Note: Pour pouvoir reconstruire l'état de l'entité

**
##Comment utiliser ça dans les autres bounded context
Note: Ca vous rappelle rien, des events qui décrivent le changement d'une entité ? Qu'on peut rejouer dans l'ordre pour reconstruire un état ? C'est comme ça qu'on va synchroniser nos bounded contexts

**
## Api REST
Note: 

**
```json
{
}
```

**
##Pagination
Attention à l'ordre pour les rejouer
Note: Hateos ?

**
## Remember

Note: La seule chose dont à besoin de se souvenir le bounded context client,
c'est le dernier event traité

**
## Crontab
Note: déclenchement d'un script

**
Conseil : Utiliser des listeners plutot qu'un batch pour pouvoir ajouter facilement un broker
Schema sans broker

**
Schema avec broker


***
# Conclusion
+++: moins compliqué, pas besoin d'un broker, tout l'historique dispo
---: synchro moins rapide => possible d'ajouter un broker plus tard

***
# Questions ?