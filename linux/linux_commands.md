
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
