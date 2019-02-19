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

Concrètement this.a fait référence à la variable global a, ici le fonctionnement de this, n'est pas différent de celui de la scope lexical.

### Implicit binding
Cette règle s'applique quand l'appel à this, est relatif au contexte d'un objet.

```js
function foo(){
    console.log(this.a);
}

var obj = {
    
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMDg4OTAzMDksLTMwNDcxNTkyNSwtMj
A4ODc0NjYxMl19
-->