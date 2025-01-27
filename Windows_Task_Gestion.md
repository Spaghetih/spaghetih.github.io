Voici un résumé des commandes de gestion des tâches et processus sous Windows, formaté en Markdown (`.md`), prêt à être copié-collé dans ton fichier :

```markdown
# Gestion des Tâches et Processus sous Windows

Ce document explique comment gérer les processus en ligne de commande sous Windows, en utilisant `tasklist` pour lister les processus et `taskkill` pour les terminer.

---

## 1. Lister les processus avec `tasklist`

La commande `tasklist` affiche tous les processus en cours d'exécution.

### Exemple :
```bash
C:\>tasklist
```
**Sortie :**
```
Image Name           PID Session Name    Session# Mem Usage
=================== ==== =============== ======== ============
System Idle Process    0 Services                0         8 K
System                 4 Services                0        88 K
Registry              84 Services                0    50,700 K
smss.exe             276 Services                0     1,132 K
csrss.exe            372 Services                0     5,264 K
wininit.exe          448 Services                0     6,892 K
csrss.exe            456 Console                 1     5,028 K
winlogon.exe         516 Console                 1    11,144 K
services.exe         584 Services                0     7,492 K
lsass.exe            592 Services                0    16,108 K
svchost.exe          704 Services                0    23,432 K
fontdrvhost.exe      736 Console                 1     4,256 K
```

---

## 2. Filtrer les processus avec `tasklist /FI`

Pour filtrer les processus, utilisez `tasklist /FI` avec un critère de filtre.

### Exemple : Rechercher les processus `sshd.exe`
```bash
C:\>tasklist /FI "imagename eq sshd.exe"
```
**Sortie :**
```
Image Name           PID Session Name    Session# Mem Usage
=================== ==== =============== ======== ============
sshd.exe            2116 Services                0     6,992 K
sshd.exe            2712 Services                0     7,668 K
sshd.exe            4752 Services                0     7,372 K
```

---

## 3. Terminer un processus avec `taskkill`

Pour terminer un processus, utilisez `taskkill /PID` suivi de l'identifiant du processus (PID).

### Exemple : Terminer le processus avec PID `4867`
```bash
C:\>taskkill /PID 4867
```
**Sortie :**
```
SUCCESS: The process with PID 4867 has been terminated.
```

---

## 4. Questions pratiques

### a. Comment trouver les processus liés à `notepad.exe` ?
```bash
C:\>tasklist /FI "imagename eq notepad.exe"
```

### b. Comment terminer le processus avec PID `1516` ?
```bash
C:\>taskkill /PID 1516
```

---

## 5. Aide supplémentaire

- Pour afficher l'aide de `tasklist`, utilisez :
  ```bash
  C:\>tasklist /?
  ```
- Pour afficher l'aide de `taskkill`, utilisez :
  ```bash
  C:\>taskkill /?
  ```
