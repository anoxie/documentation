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
 



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcwNzM5MTIwMywtMzAxMTAzMzE1XX0=
-->