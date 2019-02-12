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
Une expression produit une valeur sans utiliser l'interpolation, il s'agit d'un propriety binding, en terme de syntax, l'expression se rapproche du javascript. Exemple :
```javascript
[property] = "expression"
```
il est possible d'utiliser les expressions Javascript suivantes :

- assignation (=, +=, -=, ...)
- les opérateur tel que new, typeof, instanceof, etc
- les chaines avec ; et ,
- l'incrémentation ++ et décrémentation -\-
- certain des opérateur d'ES2015

il n'est par contre pas possible d'utiliser :

- || et &&
- ni les nouveau template d'expression tel que |, ?, !

## Context de l'expression
Le contexte d'expression est l'instance du component à laquelle appartient le template.
Une expression peut aussi faire référence à une variable relative au template lui même c'est notamment le cas lors de l'usage de ```*ngFor="let customer of customers"``` ou via une référence à une variable dans le template :
```html
<input #customerInput> {{customerInput.value}}</label>
```
## Expression guidelines
### No visible side effects
Une expression de template, ne doit changer aucun autre élément de l'application que la valeur qu'elle cible expressément. Plusieurs appel successif de la même donnée doivent afficher la même valeur.

### Quick execution
Angular exécute les expressions du template à chaque nouveau cycle, dès que quelque chose change, une promesse qui arrive à terme, une requête http, un temps donné,... 
### Simplicity
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM0OTk5MzI4NSwtMTY2MzY5NTQwNywtOD
Y1MTkxNTk4LC0xNjUwNjA5ODQzXX0=
-->