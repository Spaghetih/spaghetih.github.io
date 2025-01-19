
# SQL : Requêtes Essentielles

## Requête SELECT
La requête **SELECT** est utilisée pour récupérer des données d'une base de données.

### Requête de base
```sql
SELECT * FROM users;
```
Renvoie toutes les colonnes de la table `users`.

### Requête ciblée
```sql
SELECT username, password FROM users;
```
Renvoie uniquement les colonnes `username` et `password`.

### Utilisation de la clause LIMIT
```sql
SELECT * FROM users LIMIT 1;
```
- Renvoie uniquement la première ligne de données.

Pour ignorer des résultats :
- `LIMIT 1,1` : Ignore la première ligne et retourne la deuxième.
- `LIMIT 2,1` : Ignore les deux premières lignes et retourne la troisième.

### Utilisation de la clause WHERE

#### Exemple : Égalité
```sql
SELECT * FROM users WHERE username='admin';
```
Renvoie uniquement les lignes où `username` est égal à `'admin'`.

#### Exemple : Différent de
```sql
SELECT * FROM users WHERE username != 'admin';
```
Renvoie uniquement les lignes où `username` n'est **pas** égal à `'admin'`.

#### Exemple : Plusieurs conditions avec OR
```sql
SELECT * FROM users WHERE username='admin' OR username='jon';
```
Renvoie uniquement les lignes où `username` est égal à `'admin'` ou `'jon'`.

#### Exemple : Plusieurs conditions avec AND
```sql
SELECT * FROM users WHERE username='admin' AND password='p4ssword';
```
Renvoie uniquement les lignes où `username` est égal à `'admin'` **et** `password` est égal à `'p4ssword'`.

#### Exemple : Utilisation avec LIKE
- Nom d'utilisateur commençant par `a` :
```sql
SELECT * FROM users WHERE username LIKE 'a%';
```
- Nom d'utilisateur se terminant par `n` :
```sql
SELECT * FROM users WHERE username LIKE '%n';
```
- Nom d'utilisateur contenant `mi` :
```sql
SELECT * FROM users WHERE username LIKE '%mi%';
```

---

## Requête UNION
L'instruction **UNION** combine les résultats de plusieurs requêtes SELECT.

### Exemple
```sql
SELECT name, address, city, postcode FROM customers
UNION
SELECT company, address, city, postcode FROM suppliers;
```
- Combine les résultats des deux tables `customers` et `suppliers`.
- Les colonnes doivent correspondre en nombre, type et ordre.

---

## Requête INSERT
L'instruction **INSERT** ajoute de nouvelles lignes à une table.

### Exemple
```sql
INSERT INTO users (username, password) VALUES ('bob', 'password123');
```
Ajoute un utilisateur avec le nom `bob` et le mot de passe `password123`.

---

## Requête UPDATE
L'instruction **UPDATE** modifie les données existantes dans une table.

### Exemple
```sql
UPDATE users SET username='root', password='pass123' WHERE username='admin';
```
Met à jour le nom d'utilisateur et le mot de passe pour les lignes où `username` est `'admin'`.

---

## Requête DELETE
L'instruction **DELETE** supprime des lignes d'une table.

### Supprimer une ligne spécifique
```sql
DELETE FROM users WHERE username='martin';
```
Supprime la ligne où `username` est `'martin'`.

### Supprimer toutes les lignes
```sql
DELETE FROM users;
```
Supprime toutes les données de la table `users`.
