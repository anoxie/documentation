# Introduction aux pattern des observables

> source :
> https://putaindecode.io/fr/articles/js/observable/


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

Dans cette exemple l'API renvoie une [Promise](https://putaindecode.io/fr/articles/js/es2015/promises/): une structure représentant une valeur potentielle. Si la promesse est remplie, les callbacks .then seront exécuté, dans le cas contraire c'est le callback .catch qui sera levé.

Les promises ne permettent cependant pas de traiter de la donnée au fur et à mesure de son arrivé: elle est remplie une seule fois.

C'est là que les observable arrivent à la rescousse. Un observable est un objet implémentant une méthode .subscribe qui prend comme paramètre un Observer. Ce dernier a cette forme :
```js
const observer = {
    next: val => console.log(val), //une fonction à exécuter à chaque nouvel évenement
    error: err => console.error(err), // une fonction à exécuter en cas d'erreur
    complete: () => cosole.info("Complete !"), // une fonction à exécuter lorsque l'observable à fini
};
```
exemple d'implémentation d'un observable qui va réagir à chaque entré clavier et sera terminé quand l'utilisateur pressera enter
```javascript
const KeyboardObservable = {
  subscribe: observer => {
    const handleKeyUp = event => {
      if (typeof event.keyCode === "number") {
        if (event.keyCode === 13 /* Enter */) {
          document.removeEventListener("keyup", handleKeyUp);
          observer.complete();
        } else {
          observer.next(event.keyCode);
        }
      } else {
        observer.error(new Error("No keyCode found"));
      }
    };
    document.addEventListener("keyup", handleKeyUp);
    // subscribe retourne la "soucription", contenant une fonction pour la stopper
    return {
      unsubscribe: () => document.removeEventListener("keyup", handleKeyUp),
    };
  },
};

let keys = [];
KeyboardObservable.subscribe({
  next: keyCode => keys.push(String.fromCharCode(keyCode)),
  error: error => console.error(error),
  complete: () => alert(keys.join("")),
});
```

## La programmation reactive avec RxJS

>source :
>https://openclassrooms.com/fr/courses/4668271-developpez-des-applications-web-avec-angular/5089331-observez-les-donnees-avec-rxjs
> https://putaindecode.io/fr/articles/js/observable/programmation-reactive/

Il s'agit d'un paradigme de programmation, qui repose sur l'émission de données depuis une ou plusieurs sources à destinations d'autres éléments appelés consommateurs. Elle repose sur le design pattern ==Observable - Observer==

Dans se paradigme on traite toutes les données, quelles qu'elles soient, de la même façon: au travers de flux. Un flux, c'est en gros une structure qui balance une ou plusieurs données dans le temps au travers d'observables.

![enter image description here](https://i.imgur.com/NLqK4bF.png)

Un flux c'est simplement de la donnée qui arrive de manière ordonné dans le temps. Un flux peut émettre 3 types de données :
- une valeur
- une erreur
- un signal de fin

## La bibliothèque RxJs
Il s'agit d'une implémentation en javascript de ReactiveX, qui vise à porter sous différents langage, les concepts de la programmation Reactive. Aussi appelé Lodash des données asynchrone.

exemple :
```js
const Rx = require('rxjs')

//on écoute les clics
const button$ = Rx.Observable.fromEvent(document.getElementById("button")
//scan est l'équivalent de reduce; il va garder l'accumulateur et retourner le nouveau à chaque clic
.scan(count => count +1, 0)
.subscribe(clickCount => {
    // on met ça dans le DOM à chaque Changement
    doucment.getElementById("count").innerHTML = "You clicked" + clickCount + "times." ;
})
```

button$ est une convention permettant d'indiquer qu'il s'agit d'un flux.

## RxJS dans angular

Un observable est un objet qui émet des informations auxquelles on souhaite réagir.

Exemple simple d'intégration :

```ts
import { Component, OnInit } from '@angular/core';
import { Observable } from 'rxjs/Observable';
import 'rxjs/add/observable/interval';

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app.component.scss']
})

export class AppComponent implements OnInit {
    ngOnInit() {
        const counter = Observable.interval(1000);
	counter.subscribe(
	    (value) => {
	        this.secondes = value;
	    },
	    (error) => {
	        console.log('Uh-oh, an error occurred! :' + error);
	    },
	    () => {
	        console.log('Observable complete!');
	    }
	);
    }
}

```

template :
```html
<ul class="nav navbar-nav">
    <li routerLinkActive="active">
        <a routerLink="auth">
            Authentification
        </a>
    </li>
    <li routerLinkActive="active">
        <a routerLink="appareils">
	    Appareils
	</a>
    </li>
</ul>
<div class="navbar-right">
    <p> Vous êtes connecté depuis {{ secondes }} secondes ! </p>
</div>
```

l'implémentation ci-dessus pose un problème dans le sens ou elle ne s'arrête jamais.

De plus la donnée retourner par le service souscrit n'est pas stocké dans une variable. Pour y remédier il faut réaliser l'implémentation suivante :
```ts
import { OnDestroy } from '@angular/core';
import { subscription } from 'rxjs/Subscription';

export class AppComponent implements OnInit, OnDestroy {
secondes: number;
counterSubscription: Subscription;

ngOnInit(){
    const counter = Observable.interval(1000);
    this.counterSubscription = counter.subscribe(
        (value) => {
           this.secondes = value;
        },
        (error) => {
           console.log('Uh-oh, an error occured! : ' + error);
        },
        () => {
           console.log('Observable complete!');
        }
    );
}

ngOnDestroy(){
    this.counterSubscription.unsubscribe();
}
} 
```
## Subjects

Il existe un type d'observable qui permet de réagir à de nouvelles information mais également d'en émettre, il devient ainsi possible de mettre à jour les informations d'un service pour tout les composants qui y ont souscrit.

Pour mettre en place un subject, il faut réaliser plusieurs étapes :

- mettre en private les données relatives au service que l'on veut implémenter
- créer un Subject dans le service,
- créer une méthode qui fait émettre ces données par le Subject pour mettre à jour toutes les méthodes qui en ont besoin
- souscrire à ce Subject pour recevoir les données émises, et émettre les données
- implémenter OnDestroy pour détruire la souscription

```ts
import { Subject } from 'rxjs/Subject';

export class AppareilService {

appareilsSubject = new Subject<any[]>();

private appareils = [
     {
         id: 1,
         name: 'Machine à laver',
         status: 'éteint'
     },
     {
         id: 2,
         name: 'Frigo',
         status: 'allumé'
     },
     {
         id: 3,
         name: 'Ordinateur',
         status: 'éteint'
     }
 ];
emitAppareilSubject(){
    this.appareilsSubject.next(this.appareils.slice());
}

switchOnAll(){
    for(let appareil of this.appareils){
        appareil.status = 'allumé';
    }
    this.emitAppareilSubject();
}

switchOffAll(){
    for(let appareil of this.appareils) {
        appareil.status = 'éteint';
        this.emitAppareilSubject();
    }
}

switchOnOne(i:number){
    this.appareils[i].status = 'allumé';
    this.emitAppareilSubject();
}

switchOffOne(i:number) {
    this.appareils[i].status = 'éteins';
    this.emitAppareilSubject();
}
```

dans le component utilisant le service :
```ts
import { Component, OnDestroy, OnInit } from '@angular/core';
import { AppareilService } from '../services/appareil.service';
import { Subscription } from 'rxjs/Subscription';

@Component({
    selector: 'app-appareil-view',
    templateUrl: './appareil-view.component.html',
    styleUrl: ['./appareil-view.component.scss']
})
export class AppareilViewComponent implements OnInit, OnDestroy {

appareils: any[];
appareilSubscription: Subscription;

lastUpdate = new Promise((resolve, reject)=>{
    const date = new Date();
    setTimeout(
        ()=> {
            resolve(date);
        }, 2000
    );
});

constructor(private appareilService: AppareilService){ }

ngOnInit() {
    this.appareilSubscription = this.appareilService.appareilSubject.subscribe(
        (appareils: any[]) => {
            this.appareils = appareils;
        }
    );
    this.appareilService.emitAppareilSubject();
}

onAllumer(){
    this.appareilService.switchOnAll();
}

onEteindre(){
    if(confirm('Etes-vous sûr de vouloir éteindre tous vos appareils ?')){
        this.appareilService.switchOffAll();
    } else {
        return null;
    }
}

ngOnDestroy() {
    this.appareilSubscription.unsubscribe();
}
```


## Opéra

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMTc2MTY2MTAsMjAwODc0MTgwMywtMT
AyNTYxNTA4NCwxODIxODAxOCwtMTE4MjQ1OTQ0MCwtNjY3MzE3
NTU1LDEzMDQ3NjY0NzIsNDU3NzEyMzNdfQ==
-->