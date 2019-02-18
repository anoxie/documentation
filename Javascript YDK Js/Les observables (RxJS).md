# Introduction aux pattern des observables

> source :
> https://putaindecode.io/fr/articles/js/observable/
> https://putaindecode.io/fr/articles/js/observable/programmation-reactive/

En JS, il est possible d'exécuter du code de manière synchrone (bloquante : l'exécution du code s'arrête jusqu'à la résolution de l'instruction) ou asynchrone (non-bloquante : quand une partie du code est susceptible de demander beaucoup de temps pour s'exécuter, il est possible de passer à la suivante, et d'y revenir quand son exécution sera terminé.


## La programmation reactive avec RxJS
Il s'agit d'un paradigme de programmation, qui repose sur l'émission de données depuis une ou plusieurs sources à destinations d'autres éléments appelés consommateurs. Elle repose sur le design pattern ==Observable - Observer==
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU4MjUzNTExOF19
-->