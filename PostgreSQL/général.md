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
CREATE TABLE capitales (etats char(2))INHERITS(villes);
```
Pour exclure les tables enfants d'une requête il faut utiliser le mot clef ONLY dans la clause FROM

Il est possible de créer des fonctions en SQL

> Définition des structures de données :
> Les contraintes : elles permettent d'appliquer des tests pour vérifier le formatage des données, tests qui offrent plus de flexibilité que les types de données (INT, VARCHAR,...)
> ex: prix_numeric CHECK (prix > 0)
> donnée un nom à la contrainte facilite la recherche d'erreurs :
> prix numeric CONSTRAINT prix_positif CHECK (prix>0)

## Sécurité :
Il est possible de régler finement les droits des différents utilisateurs de la base, et de créer des rôles qui peuvent être valables pour un utilisateur ou un groupe.

CREATE POLICY
Row Security Policies

## Partitionnement :
Il est possible de partitionner une table trop volumineuse pour la stocker sur plusieurs support et d'augmenter la réactivité en séparant les données
<!--stackedit_data:
eyJoaXN0b3J5IjpbODQyODEyNDE2XX0=
-->