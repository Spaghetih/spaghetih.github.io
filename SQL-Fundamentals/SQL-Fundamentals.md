
# 🧠  SQL Fundamentals 

> Ce document est une synthèse du module *SQL Fundamentals* de TryHackMe, rédigée en français. Il couvre les bases des bases de données, les commandes SQL essentielles, les opérations CRUD, les clauses, les opérateurs et les fonctions.([Medium][1])

---

## 📚 Tâche 1 : Introduction

Les bases de données sont omniprésentes dans le domaine de la cybersécurité. Que ce soit pour sécuriser une application web, analyser des menaces dans un SOC ou empêcher un utilisateur curieux d'accéder à des données sensibles, les bases de données jouent un rôle crucial.([Medium][2])

---

## 🗃️ Tâche 2 : Bases de Données 101

### 🔸 Bases de Données Relationnelles vs Non-Relationnelles

* **Bases de Données Relationnelles** : Stockent les données dans des tables avec des lignes et des colonnes. Idéales pour des données structurées et prévisibles.

* **Bases de Données Non-Relationnelles** : Stockent les données dans des formats flexibles, souvent utilisés pour des contenus générés par les utilisateurs.

### 🔸 Tables, Lignes et Colonnes

Dans une base de données relationnelle, les données sont organisées en tables. Chaque ligne représente un enregistrement, et chaque colonne représente un champ de données.

### 🔸 Clés Primaires et Étrangères

* **Clé Primaire** : Identifiant unique pour chaque enregistrement dans une table.([Medium][3])

* **Clé Étrangère** : Lien entre deux tables, assurant l'intégrité référentielle des données.

---

## 💻 Tâche 3 : SQL

SQL (Structured Query Language) est le langage standard pour interagir avec les bases de données relationnelles. Il permet de créer, lire, mettre à jour et supprimer des données.

### 🔸 Pourquoi SQL est-il important ?

* **Rapide** : Peut gérer de grandes quantités de données efficacement.

* **Simple** : Syntaxe proche de l'anglais, facile à apprendre.([Medium][4])

* **Précis** : Permet des requêtes complexes pour des analyses approfondies.

### 🔸 Connexion à MySQL

```bash
mysql -u root -p
# Mot de passe : tryhackme
```

---

## 🛠️ Tâche 4 : Commandes de Base de Données et de Table

### 🔸 Commandes de Base de Données

* **Créer une base de données** :

```sql
CREATE DATABASE nom_de_la_base;
```

* **Afficher les bases de données** :

```sql
SHOW DATABASES;
```

* **Utiliser une base de données** :

```sql
USE nom_de_la_base;
```

* **Supprimer une base de données** :

```sql
DROP DATABASE nom_de_la_base;
```

### 🔸 Commandes de Table

* **Créer une table** :

```sql
CREATE TABLE nom_de_la_table (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(255) NOT NULL,
    date_publication DATE
);
```

* **Afficher les tables** :

```sql
SHOW TABLES;
```

* **Décrire une table** :

```sql
DESCRIBE nom_de_la_table;
```

* **Modifier une table** :

```sql
ALTER TABLE nom_de_la_table ADD colonne INT;
```

* **Supprimer une table** :

```sql
DROP TABLE nom_de_la_table;
```

---

## 🔄 Tâche 5 : Opérations CRUD

### 🔸 Créer (INSERT)

```sql
INSERT INTO livres (id, nom, date_publication, description)
VALUES (1, "Sécurité Android", "2014-10-14", "Guide approfondi de la sécurité Android.");
```

### 🔸 Lire (SELECT)

* **Tout afficher** :

```sql
SELECT * FROM livres;
```

* **Colonnes spécifiques** :

```sql
SELECT nom, description FROM livres;
```

### 🔸 Mettre à jour (UPDATE)

```sql
UPDATE livres
SET description = "Guide mis à jour de la sécurité Android."
WHERE id = 1;
```

### 🔸 Supprimer (DELETE)

```sql
DELETE FROM livres WHERE id = 1;
```

---

## 🧮 Tâche 6 : Clauses

### 🔸 DISTINCT

Élimine les doublons dans les résultats.

```sql
SELECT DISTINCT nom FROM livres;
```

### 🔸 GROUP BY

Regroupe les résultats selon une ou plusieurs colonnes.

```sql
SELECT nom, COUNT(*) FROM livres GROUP BY nom;
```

### 🔸 ORDER BY

Trie les résultats.([Medium][1])

* **Ascendant** :

```sql
SELECT * FROM livres ORDER BY nom ASC;
```

* **Descendant** :

```sql
SELECT * FROM livres ORDER BY nom DESC;
```

### 🔸 HAVING

Filtre les groupes après l'utilisation de GROUP BY.([Medium][1])

```sql
SELECT nom, COUNT(*) FROM livres GROUP BY nom HAVING COUNT(*) > 1;
```

---

## 🔍 Tâche 7 : Opérateurs

### 🔸 Opérateurs de Comparaison

* **Égal** : `=`

* **Différent** : `!=` ou `<>`

* **Supérieur à** : `>`

* **Inférieur à** : `<`

* **Supérieur ou égal à** : `>=`

* **Inférieur ou égal à** : `<=`

### 🔸 Opérateurs Logiques

* **ET** : `AND`

* **OU** : `OR`

* **NON** : `NOT`

### 🔸 LIKE

Recherche de motifs.

```sql
SELECT * FROM livres WHERE nom LIKE '%Sécurité%';
```

---

## 🧠 Tâche 8 : Fonctions

### 🔸 Fonctions d'Agrégation

* **COUNT** : Compte le nombre d'enregistrements.([Medium][2])

```sql
SELECT COUNT(*) FROM livres;
```

* **SUM** : Somme des valeurs.([Medium][5])

```sql
SELECT SUM(prix) FROM livres;
```

* **AVG** : Moyenne des valeurs.

```sql
SELECT AVG(prix) FROM livres;
```

* **MAX** : Valeur maximale.

```sql
SELECT MAX(prix) FROM livres;
```

* **MIN** : Valeur minimale.

```sql
SELECT MIN(prix) FROM livres;
```

### 🔸 Fonctions de Chaîne

* **LENGTH** : Longueur d'une chaîne.

```sql
SELECT LENGTH(nom) FROM livres;
```

* **CONCAT** : Concatène des chaînes.

```sql
SELECT CONCAT(nom, ' - ', auteur) FROM livres;
```

---

