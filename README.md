# Homeostasis Framework
A language agnostic preprocessor based on handlebars.

## Abstract

Écrire un contrôleur pour chaque page web est une tâche très répétitive qui consiste à consulter une couche model pour assigner des variables dans des templates. Homeostasis fournit un moyen simple pour les templates d'atteindre "l'auto-suffisance alimentaire" : Un entête déclaratif indique au préprocesseur les méthodes qu'il doit appeler (via l'attribut `by="service.method"`), à quelles variables du template la valeur de retour de ces méthodes devra être assigner, et sous quelle forme (typage via l'attribut `as="type"`).

En outre, le préprocesseur réalise ces opérations durant une phase dédiée, avant que le template ne soit utiliser pour générer le page. Ainsi, le **design pattern MVC est respecté**. Mais en traitant le template via un contrôleur générique, nous n'avons plus besoin d'écrire un contrôleur spécifique pour chaque page. Ce qui est un gain de temps considérable.

Il est recommandé d'utiliser des standards tels que JSONAPI (pour les données) ou WebDAV (pour les fichiers). Ainsi, vous pouvez réutiliser les méthodes d'un contrôleur RESTFULL existant pour nourrir vos templates.

 1. Vos templates peuvent alors être utilisés indifféremment côté client et côté serveur en mode couplé ou découplé ("headless")
 2. Vos templates peuvent être utiliser dans différentes applications, dans différents frameworks indépendamment de leur langage de programmation.
 
 En effet, Homeostasis est basé sur Handlebars. Ce moteur de template est lui même porté sur de très nombreux langages (JS, PHP, Python, JAVA, RUST, C ...)
 Ainsi, en utilisant des API standards qui ne sont liées à aucun langage en particulier, on obtient des templates extrêmement interopérables. 

Notez que l'usage d'Homeostasis n'est pas restreint à la génération de page web, et peut être utiliser pour n'importe quelle type de réponse utilisant des templates.

## How to use Homeostasis?

    <?homeostasis version="1.0"?>
	<constants>
	 
	 <static_cache_duration>"24h"</static_cache_duration>
	 <!-- (string) static_cache_duration="24" -->
	  
		<acl_right>"article.edit", "article.view"</acl_right>
	 <!-- (array) acl_right= ["article.edit", "article.view"] -->
	    
	</constants>
	<vars>
	 <!-- Some variables. The "by" attribute means that the definition is given as parameter(s) to a service, and the return value will be assign to the variable. -->
	 
	 <id by="request.get" as="integer">"id"</id>
	 <!-- (integer) id=request.get("id") -->
	 
	 <logs by="article.processRequest" as="dictionary" />
	 <!-- (dictionnary) logs=article.processRequest() -->
	 
	 <response by="article.get" as="dictionary">{"id" : "{{id}}"}</response>
	 <!-- (dictionnary) response=article.get({"id" : "3"}) -->
	 
	 <article as="dictionary">{{{json response.data}}}</article>
	 <!-- The "json" helper will translate dictionary to JSON String. -->
	 <!-- Assuming response follow the JSONAPI in this exemple -->		
	 
	 <title>"Article num {{id}} - {{article.title}}"</title>
	 <!-- Nested definition for variables (and constants) reusability -->
	 <!-- (you can use nested definitions on constant declarations too) -->
	 
	</vars>
	<?handlebars version="2.0"?>
	<!doctype html>
	<html>
	<head>
		<title>{{title}}</title>
	</head>
	<body>
		
		<p>Hello {{name}} !</p>
		
		<ul class="process_result">
		  {{#each logs}}
			<li class="{{type}}">{{message}}</li>
		  {{/each}}
		</ul>
		
		<h1>{{article.title}}</h1>
		<div>{{article.content}}</div>

	</body>
	</html>

## Explanations

Todo : Décrire le fichier précédent. (constants : as attribute disponible, mais pas by service. Quand by service, as attribute nécessaire)

Todo : Structured assignation (the "key" attribute)

## Implementations
Todo
HomeostasisPHP, HomeostasisJS ...
