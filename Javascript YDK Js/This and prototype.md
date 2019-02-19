# This
En javascript la valeur que représentera this est avant tout dépendant du contexte d'appel de la fonction et non de son contexte de déclaration.

## Règles de définition de this
### Default binding
Cette règle de définition de this, est le mode par défaut, elle s'applique quand aucune des autres règles ne s'applique.

````js
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
Le prototype des fonctions javascript définit 2 méthodes capable d'invoqué le contexte d'un objet pour exécuter une fonction, il s'agit de call() et d' apply(), dans les deux cas (globalement leur fonctionnement est le même, la différence se trouve dans les options d'appel de la fonction), il faut faire appel à la fonction, puis spécifier la méthode (call ou apply) puis lui passé l'objet en paramètre.

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


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcyNzI1MzA2MiwtODQ2MzAzNDA0LC0xND
MxNzY3NTQxLDE0MzE2MTAxMSwyMTI4NDU4MDcxLDE5MDYxODUx
ODMsMTc4NDU1NzU0MywtMTc3NjU0OTY0MCwtMzA0NzE1OTI1LC
0yMDg4NzQ2NjEyXX0=
-->