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
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTQ3ODk5NzIsMTc4NDU1NzU0MywtMTc3Nj
U0OTY0MCwtMzA0NzE1OTI1LC0yMDg4NzQ2NjEyXX0=
-->