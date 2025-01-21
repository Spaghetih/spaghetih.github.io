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
