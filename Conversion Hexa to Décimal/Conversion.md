# 🔢 Conversion entre Hexadécimal et Décimal

## 📌 Introduction
Le système **décimal** (base 10) est le système de numération que nous utilisons quotidiennement, tandis que le système **hexadécimal** (base 16) est souvent utilisé en informatique (ex : adresses mémoire, couleurs, etc.).

## 🔄 Conversion Hexadécimal → Décimal
Chaque chiffre en hexadécimal a une **valeur selon sa position**, basée sur des puissances de 16.

### Exemple : Convertir **2F** en décimal
1. Assigner les valeurs :
   - **F** = 15
   - **2** = 2
2. Appliquer la formule :
   ```
   (2 × 16^1) + (15 × 16^0)
   (2 × 16) + (15 × 1)
   32 + 15 = 47
   ```
✅ **Résultat :** `2F` en hexadécimal = `47` en décimal.

---

## 🔄 Conversion Décimal → Hexadécimal
On divise par **16** et on garde le reste.

### Exemple : Convertir **47** en hexadécimal
1. **47 ÷ 16** = `2`, reste `15`
2. `15` correspond à **F** en hexadécimal.
✅ **Résultat :** `47` en décimal = `2F` en hexadécimal.

---

## 🎯 Résumé
| Conversion | Méthode |
|------------|------------|
| **Hexa → Décimal** | Multiplier par des puissances de 16 |
| **Décimal → Hexa** | Diviser par 16 et prendre les restes |

---

💡 **Astuce :** Sur Windows/Linux, utilisez la commande `echo "ibase=16; 2F" | bc` pour convertir un nombre hexadécimal en décimal.

🔥 N’hésite pas à tester ces conversions par toi-même !
