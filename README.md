# Homeostasis Framework
A language agnostic preprocessor based on handlebars.

## Abstract

Écrire un contrôleur pour chaque page web est une tâche très répétitive qui consiste à consulter une couche model pour assigner des variables dans des templates. Homeostasis fournit un moyen simple pour les templates d'atteindre "l'auto-suffisance alimentaire" : Un entête déclaratif indique au préprocesseur les méthodes qu'il doit appeler (via l'attribut `by="service.method"`), à quelles variables du template la valeur de retour de ces méthodes devra être assigner, et sous quelle forme (typage via l'attribut `as="type"`).

En outre, le préprocesseur réalise ces opérations durant une phase dédiée, avant que le template ne soit utiliser pour générer le page. Ainsi, le **design pattern MVC est respecté**. Mais en traitant le template via un contrôleur générique, nous n'avons plus besoin d'écrire un contrôleur spécifique pour chaque page.

Il est recommander d'utiliser des standards tels que JSONAPI (pour les données) ou WebDAV (pour les fichiers). Ainsi, vous pouvez réutiliser les méthodes d'un contrôleur RESTFULL existant.

 1. Vos templates peuvent alors être utilisés indifféremment côté client et côté serveur en mode couplé ou découplé ("headless")
 2. Vos templates peuvent être utiliser dans différentes applications, dans différents frameworks indépendamment du langage de leur langage de programmation.
 
 En effet, Homeostasis est basé sur Handlebars. Ce moteur de template est lui même porté sur de très nombreux langages (JS, PHP, Python, JAVA, RUST, C ...)
 Ainsi, en utilisant des API standards qui ne sont liées à aucun langage en particulier, on obtient des templates extrêmement interopérables. 

Notez que l'usage d'Homeostasis n'est pas restreint à la génération de page web, et peut être utiliser pour n'importe quelle type de réponse utilisant des templates.
