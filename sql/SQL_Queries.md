
# 🗃️ SQL – Requêtes Essentielles

Ce document regroupe les requêtes SQL fondamentales pour manipuler une base de données relationnelle : consultation, insertion, modification et suppression.

---

## 🔍 SELECT – Lire des données

### Sélection de toutes les colonnes
```sql
SELECT * FROM users;
```
Renvoie toutes les lignes et colonnes de la table `users`.

### Sélection de colonnes spécifiques
```sql
SELECT username, password FROM users;
```
Renvoie uniquement les colonnes `username` et `password`.

### Limiter les résultats
```sql
SELECT * FROM users LIMIT 1;
```
Renvoie uniquement la première ligne.

```sql
SELECT * FROM users LIMIT 1,1;
```
Ignore la première ligne et renvoie la suivante (la deuxième).

```sql
SELECT * FROM users LIMIT 2,1;
```
Ignore les deux premières et renvoie la troisième.

### Filtrage avec WHERE

#### Égalité
```sql
SELECT * FROM users WHERE username = 'admin';
```

#### Différent de
```sql
SELECT * FROM users WHERE username != 'admin';
```

#### Combinaison avec OR
```sql
SELECT * FROM users WHERE username = 'admin' OR username = 'jon';
```

#### Combinaison avec AND
```sql
SELECT * FROM users WHERE username = 'admin' AND password = 'p4ssword';
```

#### Recherche avec LIKE

| But                              | Requête                                       |
|----------------------------------|-----------------------------------------------|
| Commence par `a`                 | `WHERE username LIKE 'a%'`                   |
| Finit par `n`                    | `WHERE username LIKE '%n'`                   |
| Contient `mi`                    | `WHERE username LIKE '%mi%'`                 |

---

## 🔗 UNION – Fusionner plusieurs requêtes

```sql
SELECT name, address, city, postcode FROM customers
UNION
SELECT company, address, city, postcode FROM suppliers;
```
- Combine les résultats de deux requêtes.
- Les colonnes doivent correspondre (même nombre, ordre et type).

---

## ➕ INSERT – Ajouter des données

```sql
INSERT INTO users (username, password)
VALUES ('bob', 'password123');
```
Ajoute un utilisateur dans la table `users`.

---

## ✏️ UPDATE – Modifier des données

```sql
UPDATE users
SET username = 'root', password = 'pass123'
WHERE username = 'admin';
```
Modifie les informations de l'utilisateur `admin`.

---

## ❌ DELETE – Supprimer des données

### Supprimer une ligne précise
```sql
DELETE FROM users WHERE username = 'martin';
```

### Supprimer toutes les lignes
```sql
DELETE FROM users;
```

---

## 🧠 Astuces

- `LIMIT` est utile pour les tests ou paginations.
- `LIKE` permet des recherches souples avec `%` comme joker.
- Toujours utiliser `WHERE` avec `UPDATE` ou `DELETE` pour éviter des catastrophes.

---

## 👨‍💻 Auteur

**Suleyman UNVER** – Documentation personnelle sur les bases SQL
