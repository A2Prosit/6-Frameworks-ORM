## Mots Clés
- Client Web
- Module Symfony
- API Rest : Representational State Transfer
- Requête HTTP : Emise par le client
- Reponse HTTP : Emise par le serveur
- Laravel : Framework PHP : pour les artisants du web
- PHP Web Service

## Contexte
Quoi ?
- Interroger les ressources du site

Comment ?
- En faisant des requêtes http
- En utilisant une API

Pourquoi ?
- Afin de requêter les articles en vente
- Interfacer facilement les données sur tous les supports actuels

Contraintes
- Utiliser une architecture donnée

## Problématique
Comment interroger des ressources à l’aide d’une API

## Généralisation
Communication

## Hypothèses
- Une API est une interface de programmation
- Une API -> Interface en Java
- ‘’ sert à utiliser l’application depuis un environnement extérieur

## Plan d'action

Etudes :
- REST
- API
- Laravel/Symfony -> Interaction avec REST
- Requêtes HTTP


Réalisation :
- WS

## Les Webs Services :

Une API (ou service Web) permet d'accéder à des données d'une application sur une autre application. Par exemple, si on a une API météo, on peut récupérer la température {...} de manière rapide, sur n'importe quelle plateforme, en passant par des technologies standardisées du Web (pas lié à un OS ou un langage).

⇒ **UDDI** (Universal Description Discovery and Integration Service) : Norme qui définit le mécanisme pour découvrir dynamiquement des services. Ce sont l'équivalent des pages jaunes des services. Chaque entité proposant des services devra s'y enregistrer.

![](https://benoitpiette.com/labo/img/arch-typique.png)

Un service web est donc définit sur les caractéristiques suivantes :
- Utilisable via internet
- Interface publique décrite d'une manière interprétable par tous.
- Faiblement couplés, le client ne connaît pas le fournisseur
- Repose sur des protocoles du web (HTTP / STP / SMTP)
- Échange via XML / JSON / HTML...
- Le client est chargé d'analyser / traiter / afficher les données reçus
- Le serveur reçoit les requêtes, traduit, normalise.
- Indépendant des plates-formes et des langages

Il existe deux leader sur le marché : SOAP et REST.
## API - REST :

REST [Representational State Transfer) a été crée en 2000 par Roy Fielding.
- REST est une architecture basée sur HTTP (uniquement),  opposé à SOAP (protocole) :
- REST utilise du XML ou du JSON pour envoyer ou recevoir de la data
- REST est basé sur le principe client/serveur, utilisant le HTTP uniquement
- REST peut faire des requêtes via un URL
- REST est sans état (Stateless) ⇒ Serveur n'a aucune idée de l'état du client entre deux requêtes.
- Nécessité d'avoir une mémoire cache cliente ⇒  Le client doit pouvoir conserver données en mémoire.
- Très bonnes performances (CPU) par rapport à SOAP
⇒ **Restful** = Application respectant pleinement REST.

![](https://s3-eu-west-1.amazonaws.com/sdz-upload/prod/upload/clients_servers2.png)

![](https://www.supinfo.com/articles/resources/164943/2422/0.png)
**Entête de REST** :
-   GET : Récupération
-   POST: Ajout
-   PUT/PATCH: Modification ⇒ Le corps d'une requête PUT contient la nouvelle représentation de la ressource. Le corps d'une requête PATCH contient juste des instructions permettant au serveur d'effectuer la modification. CAD que PATCH ne peut pas créer une nouvelle ressource.
-   DELETE: Suppression

**Fonctionnement :**

![](https://github.com/A2Prosit/7-WebService/blob/Emilien/Images/2.PNG)

![](https://s3-eu-west-1.amazonaws.com/sdz-upload/prod/upload/Screenshot%202016-01-06%2015.05.031.png)
*Exemples*:

- GET: /livre/SF/harrypotter/
- DELETE: /livre/SF/harrypotter/2
 

##  API - SOAP :

SOAP [Simple Object Access Protocol] ou 'enveloppe' est :
- Protocolaire (et non structuré), en utilisant le **WSDL** [STANDARD], il définit une communication entière et des règles strictes.
- Offre le transport d'objet sérialisées et données en XML.
 - Encapsule les données dans une enveloppe qui peut-être chiffrée et contenir des pièces jointes.
- Ressemble à un logiciel d'ordinateur car il est liée à un serveur (logiciel des deux côtés)
- Si on modifie un logiciel d'un côté, il faut faire la MAJ de l'autre
- Il doit connaître tout les éléments qu'il va utiliser.
 - Standardisé par le W3C
 - Invoque des services en utilisant du Remote Procédure Control. (Fonctions appellés sur une autre machine).
 - Peut utiliser SMTP / FTP {...}
 - Faible performances par rapport à REST.

⇒ Le langage **WSDL** (Web Service Definition Language) décrit l'interface au service, en utilisant XML, il fait passer ses entrées et les retours d'appel de service au Web. Il utilise les numéros de port pour définir la connexion au service web.

**Fonctionnement** :
![](https://github.com/A2Prosit/7-WebService/blob/Emilien/Images/1.PNG)

![](https://user.oc-static.com/files/202001_203000/202693.png)


**Service Provider** 
- Définit le service et ses interfaces
- Publie sa description dans l'annuaire (UDDI)
- Effectue traitement
- Renvoyer réponse

**Annuaire (UDDI)**
- Maintenir la liste à jour des services
- Recevoir et enregistrer la description des services
- Reçoit et répond aux recherche de service

**Programme client**
- Obitent la description du service
- Fait la requête auprès des service provider
- Reçoit et traite les réponses

##  Que choisir ? :

**SOAP :**
- Standardisé
- Interopérabilité
- Sécurité (chiffre l'enveloppe)

MAIS :
- Mauvaises performances (nécessité d'encapsuler)
- Complexité / lourdeurs de mise en place / maintenances
- Cible l'appel de service

**REST:**
- Simplicité de mise en place / maintenance
- Repose sur des principes web (connus)
- Services facilement identifiables

MAIS : 
- Pas vraiment de standard (ne suit pas WSDL)
- Sécurité restreinte (HTTP)


⇒ En 2010, 75% des services web passaient par REST, contrairement à 15% de SOAP.


## Framework & REST :
https://github.com/CircleOfNice/DoctrineRestDriver

**Module à installer:** composer require circle/doctrine-rest-driver
- Configurer la database

- Si on souhaite faire du PATCH à la place de PUT :
⇒ doctrine:
  dbal:
    options:
      use_patch: true

- Configurer les routes de la manière suivante: `{apiHost}/{pathToApi}/{tableName}`
	- Si PUT/PATCH ou Get (seul) : `/{id}`
	- POST et GET (tous) reste sur la manière basique
	
**Comment ça marche:**
- Utilise le JSON par défaut
- Fait les bonnes réponses (cf HTTP)
- Transforme les URL en requêtes
- Utilisable via des fonctions doctrines, directement dans un contrôleur (cf ex - lien au dessus)

## Framework & Laravel:
https://github.com/dingo/api
- 4600 étoiles sur Github
- Valable à partir de la V5
- Gestion authentification (HTTP...)
- Transformation de la réponse via "fractal"
- Pouvoir versionner son API
- Pouvoir limiter l'accès à l'API à des heures
- Permet d'effectuer des requêtes internes
- Documentation détaillée

**Module à installer**
```
composer require dingo/api
```
Toute la configuration :

https://jolicode.com/blog/initialiser-rapidement-une-api-rest-avec-laravel

## Rappels HTTP :
**Codes basiques HTTP :**
- 100 : Afficher la suite de la requête
- 200 :  OK
- 300 : Redirection
- 400 : Bad Request
- 500 : Erreur interne du serveur

https://fr.wikipedia.org/wiki/Liste_des_codes_HTTP

- GET + PUT ⇒ 200
- POST => 201
- DELETE ⇒ 204
