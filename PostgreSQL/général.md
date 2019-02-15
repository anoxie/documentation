# Fonctions avancées :
## Transactions :
permet de considérer plusieurs transactions comme un tout, elles doivent être toute exécuté ou aune ne le sera. On Parle de bloc fonctionnel.

```sql
BEGIN;
requete1;
requete2;
COMMIT;

#il est aussi possible d'ajouter des étapes intermédiaires
BEGIN;
requete1;
SAVEPOINT save;
requete2;
ROLLBACK TO save;
requete3;
COMMIT;
```
## Fenêtrage :
Permet de faire un calcul d'agragation sur un sous ensemble du résultat de la requête. Par exemple obtenir la moyenne de prix de différents produit présent dans le même rayon par type, il est plus pertinent de comparer le prix d'une TV à la moyenne du prix des autres TV qu'à l'ensemble des produits du rayon.

```sql
Select type_prod, prod, prix AVG(prix) OVER (PARTITION BY type_prod)
From produits;
```

## Héritage :
Même fonctionnement qu'en orienté objet, une table enfant hérite des propriétés de ces parents, par exemple une table capitale pourra hériter des propriétés d'une table ville, reprenants tout ces champs et en ajoutants qui lui sont spécifiques.

```sql
CREATE TABLE capitales (etats char(2))I
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDAwNjk5MTgyXX0=
-->