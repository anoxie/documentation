# Intro components
Un composant concerne un ensemble de fichier qui permettent de générer une vue. La logique relative à la vue est définit dans une class, cette class interagit avec la vue au travers d'une API (application programming interface) de propriétés et de méthode.

Exemple de définition d'un composant le fichier *src/app/hero-list.component.ts* :

```ts
@Component({
  selector: 'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers: [ HeroService ]
})

export class HeroListComponent implements OnInit {
  heroes: Hero[];
  selectedHero: Hero;

  constructor(private service: HeroService) { }

  ngOnInit() {
    this.heroes = this.service.getHeroes();
  }

  selectHero(hero: Hero) { this.selectedHero = hero; }
}
```
L’implémentation de OnInit permet de gérer le cycle de vie du composant, il doit obligatoirement implementer ngOnInit().
Le service HeroService, est déclarer dans les Métadata du component, et dans le constructeur par :
```ts
cosntructor(private service: HeroService){ }
```

## Component Metadata
- selector: un sélecteur css qui indique à Angular de créer et d'insérer une instance du composant, à l'emplacement ou il trouve le tag correspondant dans le template.
- templateUrl: adresse du template relatif au component
- providers: un tableau des éventuels services nécessaire à l'alimentation du composant.

### Template et vues
Un template est un fichier HTML qui indique à Angular comment générer le composant. Les vues sont organisé de manière hiérarchique, se qui permet de modifier ou afficher / cacher  toute la partie concerné.
![enter image description here](https://angular.io/generated/images/guide/architecture/component-tree.png)

### Template syntax
Il s'agit de HTML avec des marqueurs spécifiques à Angular (directives, data-binding, selector) exemple :

```html
<h2>Hero List</h2>

<p><i>Pick a hero from the list</i></p>
<ul>
  <li *ngFor="let hero of heroes" (click)="selectHero(hero)">
    {{hero.name}}
  </li>
</ul>

<app-hero-detail *ngIf="selectedHero" [hero]="selectedHero"></app-hero-detail>
```
- directive: ==*ngFor==, ==*ngIf==, directive de structure permettant de faire des traitements sur les données ici une boucle et une conditionnelle.
- data-binding: =={{hero.name}}== = interpolation, ==(click)== = event binding, ==[hero]== = property binding permet de propager les données du component vers le template.
- tag: ==<app-hero-detail\>== = imbrique une vue complémentaire.

### Data binding
Angular gère le data binding, à savoir faire la liaison entre les élements du template et les données, provenant du service.

![enter image description here](https://angular.io/generated/images/guide/architecture/databinding.png)

L'exemple précédent utilise les 3 premiers types de data binding, voici le 4e, le two-way binding :
```html
<input [(ngModel)]="hero.name">
```
Le two way binding utile notamment dans les formulaires, il permet de récupérer l'entré utilisateur comme un event biding, et de retourner en temps réel les modifications au template, avec le property binding.

![enter image description here](https://angular.io/generated/images/guide/architecture/component-databinding.png)


### Pipes
Permet de formater les données dans le template dans le but de les afficher, sans les modifier pour autant, par exemple, rendre lisible un timestamp, ou mettre des majuscules,...

### Directives
Les directives permettent de transformer dynamiquement le DOM, on distingue deux types de directives :

- les directive de structure, identifiable par le *, ces directives, modifie le rendu en ajoutant, supprimant, déplaçant ou remplaçant des éléments du DOM.  L'exemple suivant utilise les 2 directive de structure suivante :
	+ ==*ngFor== = qui parcours tout les éléments du tableau hereos
	+ ==$ngIf== = qui inclue les informations du héro uniquement si celui-ci existe.

```html
<li *ngFor="let hero of heroes"></li>
<app-hero-detail *ngIf="selectedHero"></app-hero-detail>
```
- les directives d'attribut : elles modifie l'apparence ou le comportement d'un élément existant, elle s'insère dans une balise html comme un attribut normal. On a par exemple :
	+ ==ngModel== = qui modifie le comportement de la balise input
	+ ==ngStyle== = qui permet de modifier les propriétés css d'un élément
	+ ==ngClass== = qui permet d'ajouter une class à un élément.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxNzgxNDA1OSwxNDY2NDIwMjQ1XX0=
-->