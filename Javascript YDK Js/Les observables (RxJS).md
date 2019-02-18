# Introduction aux pattern des observables

> source :
> https://putaindecode.io/fr/articles/js/observable/
> https://putaindecode.io/fr/articles/js/observable/programmation-reactive/

En JS, il est possible d'exécuter du code de manière synchrone (bloquante : l'exécution du code s'arrête jusqu'à la résolution de l'instruction) ou asynchrone (non-bloquante : quand une partie du code est susceptible de demander beaucoup de temps pour s'exécuter, il est possible de passer à la suivante, et d'y revenir quand son exécution sera terminé).

exemple :
```js
function logValue(value){
console.log(value)
}

// exécution synchrone
const arrayOfValue = [1,2,3,4,5];

arrayOfValue.forEach(logValue);

// exécution asynchrone
setTimeout(logValue, 3000, "Hello world!");
logValue("How are you ?");
//output : 
//How are you ?
//Hello world! 3second plus tard
```

dans le second cas, l'exécution du code ne s'arrête pas à setTimeout, la fonction est lu et interprété, puis l'exécution du code se poursuit et reviens à 


## La programmation reactive avec RxJS
Il s'agit d'un paradigme de programmation, qui repose sur l'émission de données depuis une ou plusieurs sources à destinations d'autres éléments appelés consommateurs. Elle repose sur le design pattern ==Observable - Observer==
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk5MzI5MzQ0N119
-->