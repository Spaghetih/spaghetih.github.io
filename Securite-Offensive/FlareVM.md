# 🛡️ FlareVM – Environnement pour l'Analyse de Malware et la Forensique

> Ce document est une synthèse en français du module *FlareVM: Arsenal of Tools* de TryHackMe. Il présente FlareVM, un environnement spécialisé pour l'analyse de logiciels malveillants, la rétro-ingénierie, la réponse aux incidents et la forensique.

---

## 🎯 Objectifs d'apprentissage

- Comprendre ce qu'est FlareVM et à quoi il sert.
- Explorer les outils inclus dans FlareVM et leurs catégories.
- Apprendre à utiliser des outils essentiels pour l'analyse de fichiers et processus malveillants.
- Mettre en pratique ces outils sur des fichiers suspects.

---

## 🧭 Introduction

FlareVM (Forensics, Logic Analysis, and Reverse Engineering) est un environnement Windows préconfiguré avec des outils spécialisés pour :

- **Ingénierie inverse et débogage** (Ghidra, x64dbg, OllyDbg, etc.)
- **Analyse statique et dynamique** (PEStudio, Process Hacker, HxD...)
- **Forensique et réponse aux incidents** (Volatility, FTK Imager...)
- **Analyse réseau** (Wireshark, Nmap...)
- **Scripting et automatisation** (Python, PowerShell Empire)
- **Outils Sysinternals** (Autoruns, Process Explorer, Process Monitor)

FlareVM est préinstallé dans la VM du module TryHackMe. Les fichiers d'exercices sont disponibles dans `C:\\Users\\Administrator\\Desktop\\Sample`. **⚠️ Attention : ne jamais exécuter ces fichiers en dehors de la VM isolée.**

---

## 🛠️ Outils Essentiels par Catégorie

### 🔎 Investigation et Analyse

| Outil            | Description |
|------------------|-------------|
| **Procmon**      | Surveille l'activité des fichiers, registres et processus en temps réel. |
| **Process Explorer** | Visualise les processus en cours, leur hiérarchie et les DLL associées. |
| **HxD**          | Éditeur hexadécimal pour analyser et modifier des fichiers binaires. |
| **Wireshark**    | Capture et analyse le trafic réseau pour détecter des anomalies. |
| **CFF Explorer** | Analyse et modifie les fichiers PE, génère des hachages, vérifie l'intégrité. |
| **PEStudio**     | Analyse statique des fichiers exécutables sans exécution. |
| **FLOSS**        | Extrait et dé-obfusque les chaînes de caractères dans les exécutables. |

---

## 🔬 Analyse de Fichiers et Processus

### 🧪 PEStudio

- Permet l'analyse statique des fichiers sans les exécuter.
- Détecte des métadonnées comme l'entropie, les API utilisées, et le hachage des fichiers.
- Exemple d'alertes : présence de texte en russe, absence de "rich header", fonctions suspectes comme `set_UseShellExecute` ou `RijndaelManaged`.

### 🧩 FLOSS

- Extrait des chaînes de caractères obfusquées et détecte des informations sensibles comme des adresses IP, des clés, des chemins.

### 🖥️ Process Explorer et Process Monitor

- Permettent de suivre l'activité des processus et vérifier les connexions réseau.
- Exemple : `cobaltstrike.exe` a pour parent `explorer.exe` et communique avec l'adresse IP `47.120.46.210` sur le port `81`.

### 🧰 Autres outils clés

- **CFF Explorer** : vérifie les en-têtes, les hachages, et les fonctions importées.
- **HxD** : édite et visualise les fichiers binaires.
- **Wireshark** : observe les connexions réseau suspectes, comme TLS chiffré.

---

## 📊 Résumé des Fonctions et API Notables

- **set_UseShellExecute** : permet au processus d'exécuter d'autres programmes.
- **RijndaelManaged** : utilisation de l'AES pour le chiffrement.
- **CryptoStream, CipherMode, CreateDecryptor** : fonctions liées au chiffrement.

---

## 📝 Notes Importantes

- FlareVM est un environnement sécurisé et isolé : ne jamais exécuter ou extraire les fichiers malveillants ailleurs.
- Chaque outil a une utilité spécifique : analyse statique (PEStudio), dynamique (Process Monitor), réseau (Wireshark), hexadécimal (HxD), et chaînes (FLOSS).
- Combine plusieurs outils pour valider les résultats et détecter des activités suspectes.


