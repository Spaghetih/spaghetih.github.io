
# 🛡️ TryHackMe — JavaScript Essentials | Cyber Security 101

> 💡 Ce guide est une synthèse du module *JavaScript Essentials* de TryHackMe, destiné aux débutants souhaitant comprendre les bases du JavaScript sous l'angle de la cybersécurité. Il couvre les concepts fondamentaux, l'intégration du JS dans le HTML, les fonctions de dialogue, le contournement des structures de contrôle, l'obfuscation, et les bonnes pratiques.

## 📚 Prérequis

- Module *Linux Fundamentals*
- Notions de base sur les applications web
- Compréhension du fonctionnement des sites web

---

## 1. 🔰 Concepts Essentiels

### 🔹 Variables & Types

- **Déclaration** : `var`, `let`, `const`
- **Types** : chaînes (`string`), nombres (`number`), booléens (`boolean`), objets (`object`), tableaux (`array`)
- **Typage dynamique** : le type est déterminé à l'exécution

```javascript
let age = 25;
let nom = "Alice";
function saluer(personne) {
    console.log("Bonjour, " + personne + " !");
}
saluer(nom); // Affiche : "Bonjour, Alice !"
```

### 🔹 Fonctions

Les fonctions sont des blocs de code conçus pour effectuer une tâche spécifique.

```javascript
function afficherRésultat(numÉlève) {
    alert("L'élève numéro " + numÉlève + " a réussi l'examen");
}
```

### 🔹 Boucles

Permettent d'exécuter un bloc de code plusieurs fois tant qu'une condition est vraie.

```javascript
for (let i = 0; i < 100; i++) {
    afficherRésultat(numÉlève[i]);
}
```

### 🔹 Cycle Requête-Réponse

Le navigateur (client) envoie une requête au serveur, qui répond avec les données demandées (page web, données, etc.).

---

## 2. 🧪 Aperçu de JavaScript

JavaScript s'exécute principalement côté client, permettant une interaction directe avec le HTML via le navigateur.

### 🔸 Console Chrome

- Ouvrir les outils de développement : `Ctrl + Shift + I` (Windows) ou `Cmd + Option + I` (Mac)
- Accéder à l'onglet **Console** pour tester du code JS

```javascript
let x = 5;
let y = 10;
let résultat = x + y;
console.log("Le résultat est : " + résultat);
```

---

## 3. 🧩 Intégration du JavaScript dans le HTML

### 🔸 JavaScript Interne

Le code JS est inclus directement dans le fichier HTML.

```html
<script>
    let x = 5;
    let y = 10;
    let résultat = x + y;
    document.getElementById("résultat").innerHTML = "Le résultat est : " + résultat;
</script>
```

### 🔸 JavaScript Externe

Le code JS est placé dans un fichier séparé et lié au HTML via l'attribut `src`.

```html
<script src="script.js"></script>
```

Cela favorise la réutilisation du code et une meilleure organisation.

---

## 4. ⚠️ Abus des Fonctions de Dialogue

Les fonctions `alert()`, `prompt()` et `confirm()` peuvent être exploitées à des fins malveillantes, comme le phishing.

```javascript
alert("Attention : Zone sécurisée !");
let nomUtilisateur = prompt("Entrez votre nom :");
if (nomUtilisateur) {
    alert("Bienvenue, " + nomUtilisateur);
}
let confirmation = confirm("Acceptez-vous les conditions ?");
if (confirmation) {
    alert("Merci pour votre accord.");
} else {
    alert("Vous n'avez pas accepté.");
}
```

---

## 5. 🔓 Contournement des Structures de Contrôle

Les structures conditionnelles (`if-else`, `switch`) et les boucles peuvent être manipulées pour modifier le comportement du programme.

### 🔸 Exemple `if-else`

```javascript
let âge = prompt("Entrez votre âge :");
if (âge >= 18) {
    console.log("Adulte");
} else {
    console.log("Mineur");
}
```

### 🔸 Exemple `switch`

```javascript
let jour = prompt("Entrez un jour (1-7) :");
switch(jour) {
    case '1':
        alert("C'est lundi !");
        break;
    case '2':
        alert("C'est mardi !");
        break;
    default:
        alert("Jour non valide.");
}
```

---

## 6. 🕵️‍♂️ Exploration des Fichiers Minifiés

Les fichiers JS peuvent être minifiés ou obfusqués pour réduire leur taille ou masquer leur logique.

### 🔸 Minification

Suppression des espaces, commentaires, etc., pour réduire la taille du fichier.

### 🔸 Obfuscation

Transformation du code pour le rendre difficile à lire, tout en conservant sa fonctionnalité.

### 🔸 Outils de Déobfuscation

- [JS Beautifier](https://beautifier.io/)
- [Obfuscator.io](https://obfuscator.io/)

---

## 7. ✅ Bonnes Pratiques

- **Validation côté serveur** : ne pas se fier uniquement à la validation côté client
- **Sanitisation des entrées utilisateur** : prévenir les attaques XSS
- **Utilisation de bibliothèques fiables** : préférer des sources reconnues et maintenues
- **Minification et obfuscation** : pour la production, améliorer la performance et la sécurité
- **Éviter le stockage de données sensibles dans le code** : ne pas inclure de clés API ou de secrets directement dans le JS

