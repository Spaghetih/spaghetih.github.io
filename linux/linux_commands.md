# Commandes Linux Utiles

## Navigation et Recherche
- **Répertoire actuel** : `pwd`
- **Recherche de fichiers** : `find -name *.txt`
- **Recherche dans un fichier** : `grep "XXX" NomDuFichier` (ex : `grep "81.143.211.90" access.log`)

## Opérateurs et Symboles
- `&` : Exécution en arrière-plan
- `&&` : Combinaison de commandes sur une seule ligne
- `>` : Redirection de sortie vers un fichier
- `>>` : Ajout à un fichier existant (sans écraser)

### Exemple d’utilisation de `>`
```bash
echo hey > welcome
cat welcome
```

## Commandes Diverses

### Permissions et utilisateurs
- **Afficher les permissions des fichiers** : `ls -lh`
- **Changer d'utilisateur** : `su user2`

### Planification de tâches
- **Modifier les tâches cron** : `crontab -e`

### Gestion des processus
- **Lister tous les processus** : `ps aux`
- **Terminer un processus** : `kill [PID]`
  - **Signaux courants** :
    - `SIGTERM` : Tente de terminer proprement un processus.
    - `SIGKILL` : Force l'arrêt immédiat.
    - `SIGSTOP` : Suspend un processus.

### Gestion des services
- **Commandes systemctl** :
  - **Démarrer un service** : `systemctl start [service]`
  - **Arrêter un service** : `systemctl stop [service]`
  - **Activer un service au démarrage** : `systemctl enable [service]`
  - **Désactiver un service au démarrage** : `systemctl disable [service]`

### Gestion des processus en arrière-plan
- **Exécuter une commande en arrière-plan** : `echo "text" &`
- **Suspendre une commande active** : `Ctrl + Z`
- **Ramener un processus en arrière-plan au premier plan** : `fg`

### Éditeurs de texte
- **Éditer un fichier avec nano** : `nano [fichier]`
- **Éditer un fichier avec vim** : `vim [fichier]`

## Réseaux
- **Remplacement de `netstat` : Utilisation de `ss`**  
  `ss` est utilisé pour afficher les connexions réseau, les ports ouverts, les sockets, et plus encore. Il remplace `netstat` sur les systèmes modernes Linux.

### Commandes `ss` courantes :
- **Lister toutes les sockets ouvertes** :
  ```bash
  ss -a
  ```
- **Afficher les ports en écoute** :
  ```bash
  ss -lt
  ```
- **Afficher les informations détaillées des connexions TCP** :
  ```bash
  ss -t -o
  ```
- **Afficher toutes les connexions UDP** :
  ```bash
  ss -u
  ```

## Remarque
`ss` fait partie du package `iproute2`, qui est inclus dans la plupart des distributions Linux modernes.
