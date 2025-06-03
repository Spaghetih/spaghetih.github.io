# 🛡️ FlareVM – Arsenal d'Outils pour l'Analyse de Malware 🛡️

> Ce document est une synthèse du module *FlareVM: Arsenal of Tools* de TryHackMe, rédigée en français. Il couvre les outils inclus dans FlareVM, leur utilisation pour l'analyse de logiciels malveillants et propose des exercices pratiques.

---

## 🎯 Objectifs d'apprentissage

* Explorer les outils inclus dans FlareVM.
* Apprendre à utiliser ces outils pour analyser efficacement des processus potentiellement malveillants.
* Se familiariser avec les outils utilisés pour l'analyse statique de documents et de binaires malveillants.

---

## 🧰 Arsenal d'Outils

### 🔄 Ingénierie Inverse & Débogage

* **Ghidra** : Suite d'ingénierie inverse open-source développée par la NSA.
* **x64dbg** : Débogueur open-source pour les binaires aux formats x64 et x32.
* **OllyDbg** : Débogueur pour l'ingénierie inverse au niveau de l'assembleur.
* **Radare2** : Plateforme open-source sophistiquée pour l'ingénierie inverse.
* **Binary Ninja** : Outil pour désassembler et décompiler des binaires.
* **PEiD** : Outil de détection de packers, cryptors et compilateurs.

### 🧩 Désassembleurs & Décompilateurs

* **CFF Explorer** : Éditeur PE conçu pour analyser et éditer des fichiers exécutables portables (PE).
* **Hopper Disassembler** : Débogueur, désassembleur et décompilateur.
* **RetDec** : Décompilateur open-source pour le code machine.

### 🧪 Analyse Statique & Dynamique

* **Process Hacker** : Éditeur de mémoire sophistiqué et observateur de processus.
* **PEview** : Visionneuse de fichiers PE pour l'analyse.
* **Dependency Walker** : Outil pour afficher les dépendances DLL d'un exécutable.
* **DIE (Detect It Easy)** : Outil de détection de packers, compilateurs et cryptors.

### 🕵️ Forensique & Réponse aux Incidents

* **Volatility** : Cadre d'analyse de dumps RAM pour la forensique mémoire.
* **Rekall** : Cadre pour la forensique mémoire dans la réponse aux incidents.
* **FTK Imager** : Outils d'acquisition et d'analyse d'images disque à des fins forensiques.

### 🌐 Analyse Réseau

* **Wireshark** : Analyseur de protocoles réseau pour l'enregistrement et l'examen du trafic.
* **Nmap** : Outil de détection de vulnérabilités et de cartographie réseau.
* **Netcat** : Lire et écrire des données à travers des connexions réseau avec cet outil utile.

### 📁 Analyse de Fichiers

* **FileInsight** : Programme pour examiner et éditer des fichiers binaires.
* **Hex Fiend** : Éditeur hexadécimal léger et rapide.
* **HxD** : Visualisation et édition de fichiers binaires avec un éditeur hexadécimal.

### ⚙️ Scripting & Automatisation

* **Python** : Principalement axé sur l'automatisation avec des modules et outils Python.
* **PowerShell Empire** : Cadre pour l'exploitation post-exploitation avec PowerShell.

### 🧰 Suite Sysinternals

* **Autoruns** : Affiche les exécutables configurés pour s'exécuter au démarrage du système.
* **Process Explorer** : Fournit des informations sur les processus en cours d'exécution.
* **Process Monitor** : Surveille et enregistre l'activité des processus/threads en temps réel.

---

## 🛠️ Outils Couramment Utilisés pour l'Investigation

| Outil                | Valeur Investigative                                                                                                                                 |                            |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| **Procmon**          | Outil utile pour suivre l'activité du système, en particulier pour la recherche de logiciels malveillants, le dépannage et les enquêtes forensiques. |                            |
| **Process Explorer** | Permet de voir le processus de la relation parent-enfant, les DLL chargées et son chemin.                                                            |                            |
| **HxD**              | Les fichiers malveillants peuvent être examinés ou modifiés via l'édition hexadécimale.                                                              |                            |
| **Wireshark**        | Observer et enquêter sur le trafic réseau pour détecter une activité inhabituelle.                                                                   |                            |
| **CFF Explorer**     | Peut générer des hachages de fichiers pour la vérification de l'intégrité, authentifier la source des fichiers système et valider leur validité.     |                            |
| **PEStudio**         | Analyse statique ou étude des propriétés des fichiers exécutables sans exécuter les fichiers.                                                        |                            |
| **FLOSS**            | Extrait et désobfusque toutes les chaînes des programmes malveillants en utilisant des techniques d'analyse statique avancées.                       |

---

## 🔬 Analyse de Fichiers Malveillants

### 🧪 Analyse avec PEStudio

* **Valeur d'entropie** : 7.999
* **requestedExecutionLevel** : requireAdministrator
* **Fonction notable** : set\_UseShellExecute
* **API cryptographique** : RijndaelManaged

### 🧵 Analyse avec FLOSS

* Extrait des chaînes statiques et identifie des fonctions telles que `set_UseShellExecute` et `RijndaelManaged`.

### 🧩 Analyse avec Process Explorer et Process Monitor

* **Imphash de cobaltstrike.exe** : 92EEF189FB188C541CBD83AC8BA4ACF5
* **Adresse IP défangée** : 47\[.]120\[.]46\[.]210
* **Port de destination** : 81
* **Processus parent de cobaltstrike.exe** : explorer.exe([Medium][3], [Medium][1])

---

