# Intro Service et injection de dépendances
Un service est une catégorie qui apporte les données, fonction ou fonctionnalité dont une app à besoin. Un service à un périmètre bien délimité, il s'occupe d'une seul chose, et peut le faire pour plusieurs autres composants.
Distinguer les services des composants, permet d'obtenir davantage de modularité, et réutilisant un même service pour plusieurs composants.

Concrètement la logique d'un composant devrait concerner quasi-exclusivement la gestion de la vue. Tout le reste en dehors des traitements strictement spécifique à la vue devrait être délégué aux services.

## Services exemples :
Un service qui journalise la console du navigateur :
```ts
export class Logger {
  log(msg: any)   { console.log(msg); }
  error(msg: any) { console.error(msg); }
  warn(msg: any)  { console.warn(msg); }
}
```

Un service peut dépendre d'autres services, par exemple le service Hero suivant dépend du service Logger, et du service BackendService, qui lui même dépend du service HttpClient :

```ts
export class HeroService {
  private heroes: Hero[] = [];

  constructor(
    private backend: BackendService,
    private logger: Logger) { }

  getHeroes() {
    this.backend.getAll(Hero).then( (heroes: Hero[]) => {
      this.logger.log(`Fetched ${heroes.length} heroes.`);
      this.heroes.push(...heroes); // fill cache
    });
    return this.heroes;
  }
}
```
## Injection de dépendance

L'injection de dépendance est très présente dans Angular, elle permet de garder des composants léger et donc de rendre le code plus clair. Pour définir une class comme un service dans Angular, il faut utiliser la décoration : ==@Injectable( )== . Cette même décoration permet de déclarer une dépendance dans un autre service, pipe ou module.

- l'injection est un des mécanisme principaux de Angular, les injections de dépendance sont gérer par Angular au moment de l'amorçage.
- un injecteur créer les dépendances et les réutilises si possible
- un provider est un objet qui indique à l'injeteur comment obtenir ou créer une dépendance.
 Pour toutes les dépendances nécessaire dans une application, il faut renseigner un provider. Pour un service, le provider est généralement la class du service elle-même.
 > Une dépendance n'est pas forcément un service, il peut s'agir d'une valeur, ou d'une fonction.

Exemple comment injecter une dépendance :
```ts
constructor(private service: HeroService) { }
```
Quand Angular découvre qu'un composant à besoin d'un service, il vérifie que le service n'a pas d'instance dans Injector, si ce n'est pas le cas, il crée une instance qu'il ajoute à Injector.

![enter image description here](https://angular.io/generated/images/guide/architecture/injector-injects.png)

## Providing Services

Il faut enregistrer au moins un provider par service que l'on souhaite utiliser. Le provider peut être enregistrer dans le service dans ce cas il sera disponible dans toute l'application, ou il peut être enregistrer pour un module ou un composant spécifique. L'enregistrement du provider peut se faire dans les métadatas de :

- ==@Injectable== : par défaut Angular Cli ```ng generate service``` enregistre le provider avec l'injecteur root. Angular crée alors une instance partager et l'inject dans toutes les class qui l'utilise. Utiliser cette méthode permet à Angular d'optimiser l'application en supprimant le service des parties de l'application qui n'en ont pas besoin
```ts
@Injectable({
	provideIn: 'root',
})
```
- ==@NgModule==
- ==@Component==


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTczMDk3MDk5MSw4MzMzOTc1MzMsMTcwNz
M5MTIwMywtMzAxMTAzMzE1XX0=
-->