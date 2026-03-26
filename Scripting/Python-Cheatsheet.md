# 🐍 Cheat Sheet Python

> Une fiche pratique pour maîtriser Python sans ouvrir 40 onglets Google.  

---

## 📌 Variables

```python
x = 42
nom = "Suleyman"
pi = 3.14
est_vrai = True
```

---

## 🔀 Conditions

```python
if x > 10:
    print("Supérieur à 10")
elif x == 10:
    print("Égal à 10")
else:
    print("Inférieur à 10")
```

---

## 🔁 Boucles

### For loop
```python
for i in range(5):
    print(i)
```

### While loop
```python
x = 3
while x > 0:
    print(x)
    x -= 1
```

---

## 🧙‍♂️ Fonctions

```python
def saluer(nom):
    return f"Bonjour {nom}"

print(saluer("Suleyman"))
```

---

## 🧺 Listes

```python
fruits = ["pomme", "banane"]
fruits.append("kiwi")
print(fruits[0])       # → pomme
print(len(fruits))     # → 3
```

---

## 🧾 Dictionnaires

```python
utilisateur = {"nom": "Suleyman", "âge": 23}
print(utilisateur["nom"])
utilisateur["ville"] = "Strasbourg"
```

---

## 📁 Fichiers

```python
# Lire un fichier
with open("fichier.txt", "r") as f:
    contenu = f.read()

# Écrire dans un fichier
with open("fichier.txt", "w") as f:
    f.write("Hello World")
```

---

## 📦 Import de modules

```python
import os
import math as m
from random import randint
```

---

## 🧯 Gestion des erreurs

```python
try:
    x = 1 / 0
except ZeroDivisionError:
    print("Oups, division par zéro !")
```

---

## 🧰 Modules utiles

| Module        | Utilité principale                     |
|---------------|----------------------------------------|
| `os`          | Interactions avec le système de fichiers |
| `sys`         | Paramètres et informations système      |
| `datetime`    | Manipulation des dates et heures       |
| `random`      | Générer du hasard                      |
| `requests`    | Requêtes HTTP (GET, POST...)           |
| `json`        | Manipulation de données JSON           |
| `argparse`    | Créer des CLI propres et puissantes    |

---

## ⚡ Bonus : Trucs malins

```python
# Compréhension de liste
carrés = [x**2 for x in range(5)]

# Ternary condition
age = 20
status = "majeur" if age >= 18 else "mineur"

# Unpacking
x, y = (1, 2)
```

---

## 🧠 Astuce finale

> Pratique > Lecture. Code chaque ligne que tu lis. Essaie → rate → recommence → maîtrise.
