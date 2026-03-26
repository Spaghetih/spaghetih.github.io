```markdown
# Commandes Windows Utiles

Ce document résume les commandes Windows mentionnées dans le fichier `image.png`.

## Vérifier le chemin système (Path)
Pour vérifier les répertoires inclus dans le `Path` de Windows, utilisez la commande `set` :
```bash
C:\>set
```
Cela affichera toutes les variables d'environnement, y compris le `Path`.

## Vérifier la version du système d'exploitation
Pour déterminer la version de Windows, utilisez la commande `wm` :
```bash
C:\>wm
```
Exemple de sortie :
```
Microsoft Windows [Version 10.0.17763.1821]
```

## Obtenir des informations détaillées sur le système
La commande `systeminfo` affiche des informations détaillées sur le système, telles que le nom de l'hôte, la version de l'OS, le fabricant, etc. :
```bash
C:\>systeminfo
```
Exemple de sortie :
```
Host Name:    MIN-SRV-2019
OS Name:    Microsoft Windows Server 2019 Datacenter
OS Version:    10.0.17763 W/A Build 17763
OS Manufacturer:    Microsoft Corporation
OS Configuration:    Standalone Server
OS Build Type:    Multiprocessor Free
[...]
```

## Astuces supplémentaires

### Paginer la sortie avec `more`
Si la sortie d'une commande est trop longue, vous pouvez la paginer en utilisant `more` :
```bash
C:\>driverquery | more
```
Appuyez sur la barre d'espace pour afficher la page suivante, et utilisez `CTRL + C` pour quitter.

### Commandes utiles
- **`help`** : Affiche des informations d'aide pour une commande spécifique.
  ```bash
  C:\>help <nom_de_la_commande>
  ```
- **`cls`** : Efface l'écran de l'invite de commande.
  ```bash
  C:\>cls
  ```
