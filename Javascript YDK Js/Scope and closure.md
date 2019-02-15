# Closure
>Une fonction continue à accéder à son scope lexical (là où elle a été déclaré) même en dehors de cette scope.

exemple :
```javascript
function wait (message) {
    setTimeout(function timer(){
        console.log(message);
    }
}
wait
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE5NjA0NzIyMV19
-->