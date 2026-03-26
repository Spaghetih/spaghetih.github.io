
# SQL : Récupération de Données

## Requête SELECT
La requête **SELECT** est utilisée pour récupérer des données d'une base de données.

### Requête de base
```sql
SELECT * FROM users;
```
Cette requête renvoie toutes les colonnes de la table `users`.

### Requête ciblée
```sql
SELECT username, password FROM users;
```
Cette requête renvoie uniquement les colonnes `username` et `password`.

### Utilisation de la clause LIMIT
```sql
SELECT * FROM users LIMIT 1;
```
- Renvoie uniquement la première ligne de données.

Pour ignorer des résultats :
- `LIMIT 1,1` : Ignore la première ligne et retourne la deuxième.
- `LIMIT 2,1` : Ignore les deux premières lignes et retourne la troisième.

### Utilisation de la clause WHERE
La clause **WHERE** permet de filtrer les résultats en fonction de conditions spécifiques.
```sql
SELECT * FROM users WHERE username='admin';
```
Cette requête retourne les lignes où le champ `username` est égal à `'admin'`.
