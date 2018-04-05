
## Mots Clés

-   Squelette de site

-   Module de connexion
    
-   Workflow : Représentation d'une suite de tâche
    
-   Revue de code qualitative : Consiste à faire relire son code afin d’y trouver le maximum de défauts
    
-   PDO : PHP Data Objects
    
-   Communauté
    
-   Object
    
-   ORM : mapping objet-relationnel, technique de programmation informatique qui crée l'illusion d'une Base de données orientée objet à partir d'une Base de données relationnelle en définissant des correspondances entre cette base de données et les objets du langage utilisé. 
      

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

-   Différents frameworks
    
-   ORM
    
-   Symfony (fonctionnement, implémentation, tout ca tout ca)
    
-   Laravel
    
-   Routage (Gestion de requêtes)
    

## Réalisation

 -   Corbeille de workshop


# 1 - Les principaux framework :

- **Laravel** : Framework des artisans du web, simple et élégant :
	- Courbe d'apprentissage très rapide
	- Documentation très détaillée
	- Syntaxe claire et expressive
	- Moteur de template intégré : blade
	- ORM dédié pour intéragir avec BDD : Eloquent
	- SGBD via migrations
	- Grande communauté
	- Écosystèmes très fourni (VM, Site apprentissage, Cloud...)
- **Symfony** : Framework PHP, architecture flexible basée sur tous un ensemble de composants indépendants et réutilisables. De nombreux frameworks sont basés sur ses composants. Populaire par sa maturité & ses bonnes performances :
	- Maintenue (En évolution)
	- Un standard
	- Grande flexibilité
	- Moteur de template intégré : Twig
	- ORM Doctrine
	- + de 300 000 développeurs
	- Documentation très détaillée
	- Beaucoup de bundles (plugins) à disposition du développeur.

- **CodeIgniter** : Performant & flexible :
	- Très léger (moins de 2 Mo)
	- Très bonnes performances
	- Simplicité d'utilisation
	- Excellente doc
	- Flexibilité & grande liberté dans structuration du code
	- Grosse communauté

- **Yii** : Rapide & extensible, pensé pour réduire le temps de dev d'applications PHP
	- Très bonnes performances
	- DAO pour intéragir avec la BDD
	- Gestion intégrée de l'authentification
	- Support natif de Jquery & Ajax
	- Outil de génération de code automatique, notamment pour les interfaces de type CRUD
	- De nombreux modules à disposition

- **Phalcon** : Dev en C, performant, framework le plus rapide
	- Excellentes performances couplées à un faible usage en mémoire
	- Moteur de template très rapide (dev C)
	- ORM intégré : PHQL
	- Gestion native des micro-applications
	- Tous les autres les autres composants d'un framework classique (architecture MVC, routeur, cache, formualaires)...
	
	
# 2 - Les ORM  :

*"mapping objet-relationnel, technique de programmation informatique qui crée l'illusion d'une Base de données orientée objet à partir d'une Base de données relationnelle en définissant des correspondances entre cette base de données et les objets du langage utilisé"*

C'est une base de données écrite par exemple en PHP, via des objets : 

![](https://www.killerphp.com/wp-content/uploads/2009/12/orm-framework.png)

On crée un client directement dans le code pour interagir avec ces données 
`client = new clients_object("Stefan","Mischook");  
client.save();`


=> On a "Doctrine" qui est un framework ORM et qui est inclus dans Symfony et Laravel.

**3 avantages des ORM :**

1. Harmonisation des types de données, pas besoin de cast.

2. Plus facile à débuger car écrit dans le même langage 

3. ORM s'occupe de protéger contre les injections SQL


**Quand l'utiliser** :

-   You have 3 or more programmers on a web application.
-   Your database consist of 10+ tables.
-   You have say 10+ queries to make.

	
	
# 3 - Framework symfony  :

- Avoir PHP v7.1 au mini + 'Composer' installé
- On peut dispose de nombreuses fonctions supplémentaires, mais le langage est semblable au php 	(avec $ pour variables) ==> {mt_random...}
- Il faut associer les pages de code avec des URL 
- On peut mettre en place des contrôleur ou des routings.
- Symfony propose de nombreux templates et de nombreuses configurations
- On retrouve du YAML et du XML pour compléter certaines fonctionnalités de symfony.

**Principe du routage**
Pour cacher des URL avec les paramètre dedans, on peut faire des associations d'URL avec des pages. Pour ne pas faire toutes les associations à la main, il existe un routeur. On peut faire de même pour les gestions de réponses (mettre telle URL si telle réponse du serveur).

# 4 - Framework Laravel:

Laravel est inspiré de symfony pour l'entendre et créer un système de routage efficace.
On retrouve :
- Espaces de nom (bien ranger son code pour éviter conflits de nomages).
- Fonctions anonymes = fonctions closures. Pour améliorer le code
- Méthodes magiques : méthodes qui n'ont pas été écrites dans une classe mais qui peuvent-être appellées et résolues.
- Interface, Laravel est basé sur des interfaces.
- Les traits, pour ajouter des propriétés et méthodes à une classe sans passer par l'héritage.


⇒ Laravel est basé sur de la POO, proposant du MVC, mais ne l'imposant pas. Il est judicieu de s'en éloigner.



# 5 - Routage & espace de nommage :

Laravel ne contient que l'url de base composée uniquement du nom de domaine.
Pour naviguer, il faut donc faire des routes : 
`Route::get(``'1'``,` `function``() {` `return` `'Je suis la page 1 !'``; });`

`Route::get(``'2'``,` `function``() {` `return` `'Je suis la page 2 !'``; });`

`Route::get(``'3'``,` `function``() {` `return` `'Je suis la page 3 !'``; });`

![](https://s3-eu-west-1.amazonaws.com/sdz-upload/prod/upload/img0629.JPG)


**Espaces de nomages**

Représenter un moyen d'encapsuler les élements =>
On peut avoir des conflits sur les utilisations de bibliothèques thierces (deux noms de classe sur la même fonction).

On peut donc mettre des chemins pour utiliser des classes spécifiques, ou définir des alias sur une des fonctions.

```
<?php
namespace mon\nom; // Voyez la section "Définition des espaces de noms"

class MaClasse {}
function mafonction() {}
const MACONSTANTE = 1;

$a = new MaClasse;
$c = new \mon\nom\MaClasse; // Voyez la section "Espace global"

$a = strlen('bonjour'); // Voyez "Utilisation des espaces de noms : retour
       // à l'espace global

$d = namespace\MACONSTANTE; // Voyez "L'opérateur namespace et la constante __NAMESPACE__

$d = __NAMESPACE__ . '\MACONSTANTE';
echo constant($d); // Voyez "Espaces de noms et fonctionnalités dynamiques"
?>
```
