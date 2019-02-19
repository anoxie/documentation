# Objects

Il est possible en javascript d'appeler la propriété d'un objet de 2 manières différentes, soit avec un point, soit comme un tableau, le notation en tableau permet d'utiliser des éléments variables comme arguments :
```javascript
var obj ={
	    a: "hello world", // obj.a || obj["a"]
	    b: 42,
	    c: true
	};
```

## Définition des paramètres d'un objet

On peut affecter une fonction à un objet, comme s'il s'agissait d'un valeur primitive, il faut par contre omettre les parenthèses.
```js
function foo(){
    console.log(this.a);
}

var obj = {
    a:2,
    foo: foo //la fonction foo, pourra dès lors être appelé via obj
}

obj.foo();
```

On peut également définir la fonction directement dans l'objet :

```js
var obj = {
    a:2,
    foo: function (){ console.log(this.a);}
};

obj.foo(); //2
```

# Immediatly Invoked Function Expression
Cette syntaxe permet d’exécuter immédiatement une fonction, exemple :
```javascript
(function IIFE(){
    do things;
}()
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMTk1MjY2OCwtMTQ3MDA3OTg0OCwxMD
Y4MTI0NjM4XX0=
-->