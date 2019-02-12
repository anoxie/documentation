# Template Syntax
Les composants sont la partie Controller et View de l'application de le cadre d'une architecture MVC, les templates des components sont les views. Ils sont rédigé en HTML, toutes les balises sont permises hormis ```<script>``` à fin d'éviter les attaques par injection de script. Certaines balise HTML, n'ont pas de sens dans le cadre d'un template par exemple <html\>, <body\> ou <base\>.

Il est possible de créer de nouvelle balise html, <app-root\> par exemple.

## Interpolation {{ ... }}
Remplace tout simplement le texte entre les deux accolades par la valeurs correspondante. Il est possible de réaliser une interpolation, dans l'affichage aussi bien que dans les attributs html, par exemple :
```html
<p>{{ titl }}</p>
<div><img src="{{ itemImageUrl }}"></div>
```
L'interpolation va évaluer l'expression avant de l'afficher, il est donc possible d'effectuer des calcules, ou d'appeler des fonctions.
```html
<!-- "The sum of 1 + 1 is 2" -->
<p>The sum of 1 + 1 is {{1+1}}.</p>
<!-- "The sum of 1 + 1 is not 4" -->
<p>The sum of 1 + 1 is not {{ 1 + 1 + getVal() }}.</p>
```

## Template expressions

Une expression produit une valeur sans utiliser l'in
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxODQ1MTM4LC0xNjUwNjA5ODQzXX0=
-->