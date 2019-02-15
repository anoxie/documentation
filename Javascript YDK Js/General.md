# Objects

Il est possible en javascript d'appeler la propriété d'un objet de 2 manières différentes, soit avec un point, soit comme un tableau, le notation en tableau permet d'utiliser des éléments variables comme arguments :
```javascript
var obj ={
	    a: "hello world", // obj.a || obj["a"]
	    b: 42,
	    c: true
	};
```

# Immediatly Invoked Function Expression
Cette syntaxe permet d’exécuter immédiatement une fonction, exemple :
```javascript
(function IIFE(){
    do things;
}()
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NzAwNzk4NDgsMTA2ODEyNDYzOF19
-->