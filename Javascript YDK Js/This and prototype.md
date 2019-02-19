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
Il peut assez facilement arriver de perdre l'implicit binding, ce qui modifiera la valeur de this, du context lo
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNDQwNjEzNzYsLTE3NzY1NDk2NDAsLT
MwNDcxNTkyNSwtMjA4ODc0NjYxMl19
-->