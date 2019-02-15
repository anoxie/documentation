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
Permet de faire un calcul d'agragation sur un sous ensemble du résultat de la requête. Par exemple obtenir la m
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUyMzc2OTEzNF19
-->