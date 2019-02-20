# This
En javascript la valeur que représentera this est avant tout dépendant du contexte d'appel de la fonction et non de son contexte de déclaration.

## Règles de définition de this
### Default binding
Cette règle de définition de this, est le mode par défaut, elle s'applique quand aucune des autres règles ne s'applique.

```js
function foo(){
    console.log(this.a);
}

var a = 2;

foo(); //2
```

Concrètement this.a fait référence à la variable global a, ici le fonctionnement de this, n'est pas différent de celui de la scope lexical. Si le mode d’exécution strict est activé, this.a aura pour valeur undefined

### Implicit binding
Cette règle s'applique quand l'appel à this, est relatif au contexte d'un objet.

```js
function foo(){
    console.log(this.a);
}

var obj = {
    a:2,
    foo: foo
};

obj.foo(); //2
```

#### Implicitly lost
Il peut assez facilement arriver de perdre l'implicit binding, ce qui modifiera la valeur de this, du context local vers le context global, exemple :
```js
function foo(){
    console.log(this.a);
}

var obj = {
    a: 2,
    foo: foo
};

var bar = obj.foo; //function reference/alias!
var a = "oops, global"; //'a' also property on global object

bar(); //"oops, global"
    
```
Dans l'exemple précédent bar, n'est pas une référence à l'objet obj, mais uniquement à la fonction foo(), de fait le context de foo() quand invoqué via bar, et le contexte global, et non celui de l'objet obj.

```js
var obj = {
    a: 2,
    foo: function (){console.log(this.a);}
};

var bar = obj.foo; //function reference/alias!
var a = "oops, global"; //'a' also property on global object

bar(); //"oops, global"
```
De la même manière dans cette exemple, alors qu'on pourrait s'attendre à ce que le fonction foo soit lié au contexte de l'objet obj, ce n'est pas le cas, il est possible de passer la fonction foo, comme si elle était déclarer dans bar, faisant ainsi de son contexte non plus obj, mais le lieu d'invocation de bar();

Le contexte le plus subtile, commun et inattendu au se produit la perte de lien, est le passage d'une fonction callback :

```js
function foo() {
	console.log( this.a );
}

function doFoo(fn) {
	// `fn` is just another reference to `foo`

	fn(); // <-- call-site!
}

var obj = {
	a: 2,
	foo: foo
};

var a = "oops, global"; // `a` also property on global object

doFoo( obj.foo ); // "oops, global"
```
### Explicit Binding
Le prototype des fonctions javascript définit 2 méthodes capable d'invoqué le contexte d'un objet pour exécuter une fonction, il s'agit de call() (qui permet d'appeler des arguments séparer par une virgule (c comme coma)) et d' apply() qui permet d'utiliser des array dans le passage des arguments (a comme array)), il faut faire appel à la fonction, puis spécifier la méthode (call ou apply) puis lui passé l'objet en paramètre.

Exemple :
```js
function foo(){
    console.log(this.a);
}

var obj = {
    a:2
}

foo.call( obj ); //2
```
#### Hard Binding
Consiste à utiliser l'explicit Binding pour lier la fonction à l'objet obj, évitant ainsi la la perte du lien implicite.

```js
function foo(){
    console.log( this.a );
}

var obj = {
    a: 2
};

var bar = function() {
    foo.call(obj);
};

bar(); //2
setTimeout( bar, 100 ); //2

//'bar' hard binds 'foo' 's 'this' to 'obj'
// so that it cannot be overriden
bar.call(window); //2
```
Depuis ES5 il existe une fonction native dans javascript pour réaliser le hard binding, il s'agit de bind(), exemple :
```js
function foo(something){
    console.log(this.a, something);
    return this.a + something;
}

var obj = {
    a: 2
};

var bar = foo.bind(obj);

var b = bar(3); // 2 3
console.log(b); // 5
```

### API Call "Contexts"
De nombreuse API, permettent de passer un context, dans l'appel au varible permettant d'éviter le recours à bind. Exemple :
```js
function foo(el) {
    console.log(el, this.id);
}

var obj = {
    id: "awesome"
};

//use 'obj' as 'this' for 'foo(..)' calls
[1, 2, 3].forEach( foo, obj); // 1 awesome 2 awesome 3 awesome
```

## new Binding

En JS à la différence des autres langage de programmation orienté objet, l'utilisation de new ne dépend pas forcément de la déclaration d'une class, et la fonction constructor, n'est qu'une simple fonction. De fait il est possible d'utiliser le mot clef new pour appeler une fonction.

Ce qui va entrainer les actions suivantes :

- une nouvelle instance de l'objet sera créer, en suivant les instructions du constructor s'il existe
- le nouvel objet est [[Prototype]] -linked
- le nouvel objet est lié au context de l'appel de cette fonction
- sauf si la fonction retourne elle même son objet, c'est l'objet nouvellement créer qui sera retourné

De fait il est possible de lier un contexte à une fonction en utilisant new. Exemple :

```js
function foo(a){
    this.a = a;
}

var bar = new foo(2);
var a = "je suis une variable global"; //n'a pas d'impact sur bar, puisque a a été lié via new
console.log(bar.a); //2
```

## Précédence
new binding > explicit binding > implicit binding > default binding

### Déterminer this
Il faut se poser ces questions dans l'ordre et s'arrêter quand l'on trouve une réponse positive :

- est-ce que la fonction est appelé avec new ? Si oui, this est l'objet nouvellement construit.
- est-ce que la fonction est appelé avec call, apply ou bind ? Si oui, il s'agit d'un hard-binding, this est l'objet explicitement  spécifié.
- est-ce que la fonction est appelé via un objet ? Si oui, il s'agit d'un implicit binding, this est l'objet d'où la fonction est invoquée.
- Dans tout les autres cas, il s'agit d'un défault binding, le context est global.

### Binding exceptions
#### Ignored this
Si on passe null, undefined dans un explicit binding, ces instructions sont ignorées, et l'on passe au default binding :
```js
function foo(){
    console.log(this.a);
}

var a = 2;

foo.call(null);//2
```
### Safer this

Au lieu de passer null, il est préférable de passer un objet vide, pour créer une sorte de DMZ, qui évitera d'éventuelles sideEffects qui serait lié au contexte global. 

La manière la plus simple de créer un objet vide est ```Object.create(null)``` Exemple :
```js
function foo(a,b){
    console.log("a:" + a + ", b:" + b);
}

//our DMZ empty object
var ø = Object.create(null);

//spreading out array as parameters
foo.apply(ø, [é,3]); // a:2, b:3

//currying with `bind(..)
var bar = foo.bind(ø, 2);
bar(3); // a:2, b:3
```

### Indirection

Il peut arriver que l'on fasse de manière intentionnelle ou non, des références indirect à une fonction. Dans ce cas également les règles de précédences s'appliquent.
Exemple :
```js
function foo(){
    console.log( this.a );
}

var a = 2;
var o = { a: 3, foo: foo };
var p = { a: 4 };

o.foo(); // 3
(p.foo = o.foo)(); //2
```
## Lexical this

ES6 int
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MjIwMTMxNDksNzY3MDk1NjM3LC0xOT
gxMjI5MzE2LDE2ODk5MDM4NzUsNjk0MjU2Mzg3LDE3Njc3MjI1
MTQsMTUyNDIwMTYyMCwtMjA1ODQ4Mjc4OCw0MDY2MzE0NDksLT
IwMjQwMjY1MDAsLTExMTM3OTMxOTMsLTQ0NzE3MDczLC02ODQ1
NjI4MDQsLTEyMTM0MDEyNzIsLTEzNDQ5OTM2MjUsLTE2NzkyNz
E0OTksLTg0NjMwMzQwNCwtMTQzMTc2NzU0MSwxNDMxNjEwMTEs
MjEyODQ1ODA3MV19
-->