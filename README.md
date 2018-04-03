
## Mots Clés

-   Squelette de site

- framework : infra de dev, ensemble cohérent de composants logiciels structurels != biblio, framework: non spé (pas autant), impose l'archi logicielle 
    
-   Module de connexion : contexte, parle de PDO
    
-   Workflow : représentation d'une suite de tâces ou opérations effectuées par une personne/groupe de personnes/organisme
    
-   Revue de code qualitative
    
-   PDO : PHP Data Object 
    
-   Communauté : -
    
-   Object : -
    
-   ORM object relational mapping: créé des objets correspondants aux tables d'une BDD
      

##  Contexte

Quoi

-   Fabriquer un model du site
    

Comment

-   En créant un squelette de site
    
-   En incluant PHP (Puzzle style ! #fantou)
    
Pourquoi

-   Éviter de recréer un site pour chaque projet
    
-   Gagner du temps
     

##  Contraintes

-   Garder tout ce qu’on a déjà fait
    

  

##  Problématique

-   Comment gagner du temps en fabriquant un squelette / modèle de site ?
    
## Généralisation

-   Optimisation (Temps)
    
-   Productivité
    
## Hypothèses

-   Il existe plusieurs framework en fonction du type d’application.
    
-   Utilisation d’un framework pour le squelette.
    
-   On va créer des modules PHP réutilisables.
    
-   On peut utiliser Symfony pour regrouper différents frameworks.
    
-   Framework = squelette.
    

  

## Plan d’action

## Etudes

###  Différents frameworks

**Lravel** : créé en 2011,"le framework artisans du web"
+:

*  courbe d'apprentissage rapide
* doc détaillée
* syntaxe claire et expressive
* moteur de templat intégré : Blade
* ORM dédié pour interagir avec les BDD : Eloquent

installation :
step 1: dl composer (gestionnaire de dépendance php)
step 2: <code>composer global require "laravel/installer"</code>

projet:

	laravel new blog
ou
	
	composer create-project --prefer-dist laravel/laravel blog "5.5.*"

ou

	php artisan serve


**Symfony** : créé en 2005, "la" référence PHP
+ : 

* archi flexible: composants flexibles et réutilisables (Laravel, Drupal, eZ Publish utilisent sont basés sur (la page dit 'ces' mais je pense 'ses') composants
* mature et réputé
* basé sur des compo indépedants et réutilisables devenus un standard parmi les dev PHP
* grande flexibilité
* moteur de template intégré : Twig
* associé à l'ORM Doctrine
* grande communautée : plus de 300k dev
* doc très détaillée
* beaucoup de bundles à disposition du dev


    
###   ORM

Object relational mapping: un framework ORM est écris dans un langage orienté objet (PHP, Java, C#, etc)

Un ORM génère des objets qui mappent les tables d'une BDD, on peut ensuite utiliser ces objets pour interagir avec la BDD. Le but est donc d'ajouter une couche d'abstraction pour ne pas avoir à faire de requêtes SQL full opti. 

Ex: si on à une bdd avec 2 tables : clients et produits. L'ORM créera 2 objets clients_object et produits_object pour gérer les interctions avec la bdd

ajouter un client peut être aussi simple que de faire (syntaxe dépendante de l'ORM): 

	client = new clients_object("Stefan","Mischook");
	client.save();

comme on peut le voir: pas de SQL

autres avantages d'utiliser un framework ORM:

* harmonisation des types de donnée entre le langage OO et le sql
* facilite le débug en gardant un code consistant (pas de mélange de code SQL et autre langage OO, juste le langage OO)
* protèges des injections SQL

désavantages:

* couche d'abstraction peut entrainer des pertes de perf
* peut être peu flexible
* dépendant du framework
* généralement assez verbeux

/!\ l'ORM ne remplace pas toujours le SQL: il le fait dans 80-90% des cas mais il faut parfois nécessaire de faire les requêtes en SQL ou langages similaires. Les framework ORM ont souvent leur propre langage de requête ressemblant au SQL. ex: Doctine (framework PHP) utilise DQL, Hibernate (framework .net et Java) utilise HQL et Hybernate utilise le SQL classique

quand utiliser un framework ORM : plus la complexité augmente plus il est recommendé (quasi nécessaire) d'en utiliser :

* team de 3+
* BDD avec 10+ tables
* 10+ requêtes


liste nn exaustive de framework ORM :

* Doctrine
* Zend_Db
* CakePHP
* RedBean
* PDO (pdo est un database access abstraction layer mais peut être upgrade en ORM apparement, mais j'ai pas confiance en la ressource)
* Propel
* Kohana ORM
    
###  Symfony (fonctionnement, implémentation, tout ca tout ca)
    


### Doctrine 

installation: composer require doctrine maker

The database connection information is stored as an environment variable called DATABASE_URL. For development, you can find and customize this inside .env:


	# .env
	# customize this line!
	DATABASE_URL="mysql://db_user:db_password@127.0.0.1:3306/db_name"
	# to use sqlite:
	# DATABASE_URL="sqlite:///%kernel.project_dir%/var/app.db"


Now that your connection parameters are setup, Doctrine can create the db_name database for you:

	 php bin/console doctrine:database:create

Without even thinking about Doctrine or databases, you already know that you need a Product object to represent those products. Use the make:entity command to create this class for you:

	 php bin/console make:entity Product
 
You now have a new src/Entity/Product.php file
    
###  Laravel


so co a une bdd

dans le .env ligne 7

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=hero
DB_USERNAME=root
DB_PASSWORD=0000


on peut utiliser des shortcuts : @ corresponds à <\?php ?>


	php artisan make:migration create_tasks_table --create=tasks
créé une migration et laravel va créer du code template pour créer la table

on peut ensuite créer la table avec 
	
	php artisan migrate


*récup data*

	$tasks = DB::table('tasks')->get();

	return $tasks

on récup tous les records de la table 'tasks' ,laravel convertit l'objet en JSON

on pourrait recup la description avec 
	
	$tasks->description

###   Routage (Gestion de requêtes)

sur symfony:

il faut installer le packet annotation :

	composer require annotations

sur laravel:
    
Pour Laravel on veut que toutes les requêtes aboutissent obligatoirement sur le fichier index.php situé dans le dossier public. Pour y arriver on peut utiliser une URL de ce genre :

http://monsite.fr/index.php/mapage

Mais ce n’est pas très esthétique avec ce index.php au milieu.

Si vous avez un serveur Apache lorsque la requête du client arrive sur le serveur où se trouve notre application Laravel elle passe en premier par le fichier .htaccess, s’il existe, qui fixe des règles pour le serveur. Il y a justement un fichier .htaccess dans le dossier public de Laravel avec une règle de réécriture de telle sorte qu’on peut avoir une url simplifiée :

http://monsite.fr/mapage

Pour que ça fonctionne il faut que le serveur Apache ait le module mod_rewrite activé.


Lorsque la requête atteint le fichier public/index.php l’application Laravel est créée et configurée et l’environnement est détecté. Ensuite le fichier routes/web.php est chargé. Par défaut on y trouve : 


	Route::get('/', function () {
	    return view('welcome');
	});

comprende: si on reçoit un get sur '/' (le nom de domaine seul) renvoyer le fichier de vue welcome, et on a bien dans le dossier view un fichier welcome.blade.php

on peut aussi passer des paramètres : 

	Route::get('/', function () {
		    return view('welcome', [ 'name' => 'World' ]);
		});

ou

	Route::get('/', function () {
		return view('welcome')->with('name','World');
	});
ou

	Route::get('/', function () {
		$name = 'World';
		return view('welcome', compact('name'));
	});

Laravel accepte les verbes suivants : get, post, put, patch, delete, options, any (on accepte tous les verbes).



A l’installation Laravel a une seule route qui correspond à l’url de base composée uniquement du nom de domaine. Imaginons que nous ayons 3 pages qui doivent être affichées avec ces urls :

http://monsite.fr/1

http://monsite.fr/2

http://monsite.fr/3


on utilisera le code:

	Route::get('1', function() { return 'Je suis la page 1 !'; });
	Route::get('2', function() { return 'Je suis la page 2 !'; });
	Route::get('3', function() { return 'Je suis la page 3 !'; });

On peut utiliser un paramètre pour une route qui accepte des éléments variables en utilisant des accolades :


	Route::get('{n}', function($n) {
	    return 'Je suis la page ' . $n . ' !'; 
	});

On peut rendre un paramètre optionnel en lui ajoutant un point d’interrogation mais il ne doit pas être suivi par un paramètre obligatoire. Dans ce cas pour éviter une erreur d’exécution il faut prévoir une valeur par défaut pour le paramètre:

	
	Route::get('{n?}', function($n = 1) {

n est optionnel et par dfat sa valeur est 1

on peut aussi prendre des expressions régulières:

	Route::get('{n}', function($n) { 
	    return 'Je suis la page ' . $n . ' !'; 
	})->where('n', '[1-3]');

/!\ les routes sont analysée dans leur ordre dans le fichier route 

	
	Route::get('{n}', function($n) { 
	    return 'Je suis la page ' . $n . ' !'; 
	});
 
	Route::get('contact', function() {
	    return "C'est moi le contact.";
	});

ici si on cherche contact on tombera sur "Je suis la page contact" et non pas "C'est moi le contact"



**404**

il existe un fichier error (au même tite qu'il existe le fichier view) , il est apparmeent par défaut dans view/erro mais moi il est dans \vendor\laravel\framework\src\Illuminate\Foundation\Exceptions\view et ne s'appelle pas error du coup. Si une erreur survient laravel va chercher si un fichier à un nom correspondant (404) et l'affiche

### Espace de nomage

analogue à un dossier

leur but est de résoudre 2 pbs des auteurs de biblio et d'app lors de la réutilisation des éléments tels que des classes ou biblio:

* collisions de nom 
* créer des alias ou raccourcis de noms longs pour la lisibilité

		<\?php
		namespace mon\nom;

## Réalisation

 -   Corbeille de workshop
