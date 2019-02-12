# Afficher les données
## Interpolation
La manière la plus simple d'afficher des données avec Angular, est l'interpolation. Elle consiste à ajouter le nom de la variable que l'on souhaite ajouter dans le template entre double accolades : ```{{ heroName }}```, il faut également que la variable soit déclarer dans le component, par exemple avec une déclaration de template inline :
```ts
import { Component } from '@angular/core';

@Component({
   selector: 'app-root',
   template: `
	   <h1> {{ title }}</h1>
	   <h2> My favorite hero is: {{ myHero }} </h2>
	   `
})
export class AppComponent {
    title = 'Tour of Heroes';
    myHero = 'Windstorm';
}
```

## Template Inline vs in file ?

C'est avant tout une question de choix et d'organisation, mais il est généralement préférable d'utiliser un fichier séparé à moins qu'il n'y ai que quelques ligne de code html dans le template du component. Angular CLI génère automatiquement un fichier de template avec la commande ```ng generate component <name>```, il est possible d'inhiber cette génération en renseignant l'option inline template comme suit : ```ng generate component <name> -it```


## Afficher un array avec ==*ngFor==
Angular comporte une directive permettant d'afficher simplement un array dans un template, par exemple pour la déclaration d'array suivante :
```ts
export class AppComponent {
    title = 'Tour of Heroes';
    heroes = ['Windstorm', 'Bombasto', 'Magneta', 'Tornado'];
    myHero = this.heroes[0];
}
```
et dans le template :
```html
<h1> {{ title }}</h1>
<h2> My favorite hero is : {{ myHero }} </h2>
<p> Heroes: </p>
<ul>
   <li *ngFor="let hero of heroes">
      {{ hero }}
   </li>
</ul>
```

## Créer une class pour les données
Dans les exemples les données sont stockées dans un tableau écrit directement dans le code, mais ce n'est pas une bonne pratique, dans une application réel, il est préférable que les données soit structuré en objet, de sorte que ce soit un tableau de ces objets qui soit retourné à la directive ==*ngFor==, pour créer une class avec Angular CLI ```ng generate class hero```, puis de compléter la classe suivante :
```ts
export class Hero {
    constructor(
        public id: number,
        public name: string) { }
    )
}
```
### Utilisation de la class Hero
Création des héros :
```ts
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY0Mzk3MTcyOSw3NzU0ODgwOTFdfQ==
-->