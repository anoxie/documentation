# Angular
## Architecture
Le bloc de base d'angular est le NgModule, qui fournit un context de compilation pour les composants. Une application Angular n'est en fait qu'un assemblage de NgModules. Toutes les applications Angular ont au moins, un module racine, permet l'amorçage, mais il y a généralement davantage de modules. Les modules peuvent sont composé de composant qui peuvent être  :

- views component, il s'agit des templates html, qui peuvent contenir des binding markup, qui permettent de récupérer ou d'afficher des données, fournit par d'autres partie de l'application. Angular gérer les views et peut les modifier en accord avec la logique et les données relatives à chacune d'entre elles.
- services component, un service est un ensemble de code qui fournit des fonctionnalités qui ne sont pas directement relative à la vue. Les services peuvent être injecter comme une dépendance dans une vue, rendant le code modulaire, réutilisable et efficace.

Ces deux composants sont en fait de simples classe, avec des décorateurs spécifiques à Angular, qui lui permettent de savoir quel traitement effectuer.

### Modules
Un modules est un ensemble de composant, qui peuvent recourir à différent services pour créer un module fonctionnel. Un module peut importer les fonctionnalités d'autres modules. Par exemple Router est un NgModule

### Components
Chaque component, definit une class qui contient ces données et ça logique, ainsi que d'un template (html) qui définira de quelle manière il sera afficher par Angular en fonction du contexte.

==@Component()==
est le décorateur qui identifie un composant.

#### Templates, directives and data binding
Un template combine du html avec des marqueur angular, qui permettent de créer des liens avec le DOM, permettant d'afficher ou d'enregistrer des données. Il y a deux types de liens : 

- les liens d'événements, font que l'application répond au entrée utilisateur en modifiant les données en fonction de l'évènement levé.
- les liens de propriété, permet d'interpoler des valeurs qui ont été calculé par la partie logique du code, et de les introduires dans les éléments HTML.
Enfin, il est possible d'utiliser des pipes dans les templates, un pipe est grossièrement un masque qui permet de formater des données avant de les afficher, typiquement passer un typestamp dans un format date, ou mettre des majuscules avec uppercase.

### Services et injections de dépendances
Quand un ensemble de fonction ou d'information ne sont pas associer à une vue spécifique, on peut créer un service, typiquement la logique relative à un utilisateur, n'est pas strictement relative à une vue login, mais à néanmoins besoin des informations de l'utilisateur.

==@Injectable()==
ce décorateur permet d'indiquer à angular qu'il s'agit d'un service qui peut être injecté dans un autre module.

Les injections de dépendance permettent de garder le code aussi propre que possible en déléguant au service les parties récurrente de la logique applicative. Afficher des données depuis un serveur, vérifier la validité d'une entré utilisateur,...

#### Routing
Le module Angular Router fourni un service qui permet de définir les chemins nécessaire à la navigation dans l'application. Le router fournit des chemins URL-likes, et pas juste la page, à fin de permettre la navigation classique par navigateur. Le router gère également le chargement des modules nécessaire au bon fonctionnement d'Angular. (lazy-load : chargement de module à la demande) Pour définir les règles de navigation, il faut ajouter les chemin de navigation au components.

## Résumé en image :

![enter image description here](https://angular.io/generated/images/guide/architecture/overview2.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk3ODM5MDgzLDkyNTg5NzEwMV19
-->