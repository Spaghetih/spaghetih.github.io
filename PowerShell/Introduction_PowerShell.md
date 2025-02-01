
# Introduction à PowerShell

## Syntaxe de base : Verbe-Nom
Les commandes PowerShell sont appelées **cmdlets** (prononcées *command-lets*). Elles sont plus puissantes que les commandes traditionnelles de Windows et permettent une manipulation avancée des données.

Les cmdlets suivent une convention de nommage **Verbe-Nom** :
- **Verbe** : Décrit l'action effectuée.
- **Nom** : Spécifie l'objet sur lequel l'action est réalisée.

Exemple :
- `Get-Content` : Récupère (get) le contenu d'un fichier et l'affiche dans la console.
- `Set-Location` : Modifie (set) le répertoire de travail actuel.

---

## Cmdlets de base
Pour lister toutes les cmdlets, fonctions, alias et scripts disponibles, utilisez la commande suivante :

```powershell
Get-Command
```

Exemple de sortie :

```plaintext
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           Add-AppPackage                                     2.0.1.0    Appx
Alias           Add-AppProvisionedPackage                          3.0        Dism
Function        Add-BCDataCacheExtension                           1.0.0.0    BranchCache
Cmdlet          Add-AppxPackage                                    2.0.1.0    Appx
...
```

---

## Filtrer les commandes par type
Vous pouvez filtrer les commandes selon leur propriété **CommandType**. Par exemple, pour afficher uniquement les fonctions, utilisez :

```powershell
Get-Command -CommandType "Function"
```

Exemple de sortie :

```plaintext
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Function        Add-BCDataCacheExtension                           1.0.0.0    BranchCache
Function        Add-DnsClientDohServerAddress                      1.0.0.0    DnsClient
Function        Add-DnsClientNrptRule                              1.0.0.0    DnsClient
...
```

---

## Utiliser `Get-Help`
La cmdlet `Get-Help` fournit des informations détaillées sur d'autres cmdlets, y compris leur utilisation, paramètres et exemples.

Exemple d'utilisation :

```powershell
Get-Help Get-Date
```

Exemple de sortie :

```plaintext
NOM
    Get-Date

SYNOPSIS
    Récupère la date et l'heure actuelles.

SYNTAXE
    Get-Date [[-Date] <System.DateTime>] [-Day <System.Int32>] ...
    ...

DESCRIPTION
    La cmdlet `Get-Date` récupère un objet DateTime qui représente la date actuelle ou une date spécifiée.
    ...
```

---

## Alias dans PowerShell
PowerShell inclut des alias (raccourcis ou noms alternatifs pour les cmdlets). Utilisez `Get-Alias` pour lister tous les alias disponibles.

Exemple :

```powershell
Get-Alias
```

Exemple de sortie :

```plaintext
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           % -> ForEach-Object
Alias           ? -> Where-Object
Alias           cat -> Get-Content
Alias           cd -> Set-Location
...
```

---

## Trouver et télécharger des cmdlets
PowerShell peut étendre ses fonctionnalités en téléchargeant des cmdlets supplémentaires depuis des dépôts en ligne.

Pour rechercher des modules :

```powershell
Find-Module -Name "PowerShell*"
```

Exemple de sortie :

```plaintext
Version    Nom                                 Dépôt               Description
-------    ----                                ----------          -----------
0.4.7      powershell-yaml                     PSGallery           Module PowerShell pour YAML
2.2.5      PowerShellGet                       PSGallery           Module pour découvrir, installer...
...
```

Pour installer un module :

```powershell
Install-Module -Name "PowerShellGet"
```

---

Avec ces outils essentiels, vous pouvez commencer à explorer les capacités de PowerShell.
