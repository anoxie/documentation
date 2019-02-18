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

dans le second cas, l'exécution du code ne s'arrête pas à setTimeout, la fonction est lu et interprété, puis l'exécution du code se poursuit et reviens à logValue une fois le temps écoulé, ici 3 secondes.

En JS les fonctions sont dites agnostique, c'est à dire qu'elles peuvent être exécuté indifféremment de manière synchrone, ou asynchrone, c'est le contexte qui déterminera la manière dont elle sera exécuté.

## Intérêt des appels asynchrone
Typiquement tout ce qui va avoir un rapport avec des appels réseaux, les téléchargement de fichiers dont les durées dépendent de paramètre inconnu au moment du développement de l'application.

exemple le téléchargement d'un fichier avec node.js, qui propose l'API suivante : ``` fs.readFile(fileToRead, options, callback) ```
```js
fs.readFile("./alphabet.txt, {encoding: "utf-8"}, {err, data) => {
    if (err){
        onError(err);
    } else {
        onData(data);
    }
})
```
Dans cette exemple, l'API va lancer le téléchargement d'un fichier puis appeler la fonction de callback quand celui-ci a réussi ou s'il a échoué.

Autre exemple :
```js
function logValue(value){ console.log(value)}
function logError(err) { console.error(err)}

fetch('https://api.github.com/users/wyeo") //fetch = API js qui permet de faire des appels au réseau
    .then(res => res.jon()) //fonction de callback relative à une promesse => fetch
    .then(logValue)
    .catch(logError)
```

Dans cette exemple l'API renvoie une [Promise](https://putaindecode.io/fr/articles/js/es2015/promises/):

## La programmation reactive avec RxJS
Il s'agit d'un paradigme de programmation, qui repose sur l'émission de données depuis une ou plusieurs sources à destinations d'autres éléments appelés consommateurs. Elle repose sur le design pattern ==Observable - Observer==
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM1MDI3OTQ4LDQ1NzcxMjMzXX0=
-->