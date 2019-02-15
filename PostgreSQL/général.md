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

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjM2NjY1NDg5XX0=
-->