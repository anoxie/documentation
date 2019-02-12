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
myHero = 'Windstorm
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxNzk3MjA1Ml19
-->