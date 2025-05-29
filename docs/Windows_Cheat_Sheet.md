# 🖥️ Windows Command Cheat Sheet

## 🛠️ Commandes essentielles pour l'administration système et la sécurité

| Commande | Description |
|----------|-------------|
| `xfreerdp /v:<target IP> /u:htb-student /p:<password>` | Connexion RDP à une machine distante |
| `Get-WmiObject -Class win32_OperatingSystem` | Obtenir des informations sur le système d'exploitation |
| `dir C:\ /a` | Lister tous les fichiers et dossiers sur `C:\` |
| `tree <directory>` | Afficher la structure arborescente d'un répertoire |
| `tree C:\ /f | more` | Parcourir l'arborescence page par page |
| `icacls <directory>` | Voir les permissions d'un dossier |
| `icacls C:\users /grant joe:f` | Donner à l'utilisateur `joe` un accès complet sur un dossier |
| `icacls C:\users /remove joe` | Retirer les permissions de `joe` sur un dossier |
| `Get-Service` | Lister les services en cours d'exécution |
| `help <command>` | Afficher l'aide d'une commande spécifique |
| `get-alias` | Lister les alias disponibles dans PowerShell |
| `New-Alias -Name "Show-Files" Get-ChildItem` | Créer un alias personnalisé dans PowerShell |
| `Get-Module | select Name,ExportedCommands | fl` | Lister les modules importés et leurs commandes associées |
| `Get-ExecutionPolicy -List` | Voir les politiques d'exécution PowerShell |
| `Set-ExecutionPolicy Bypass -Scope Process` | Modifier la politique d'exécution PowerShell pour le processus actuel |
| `wmic os list brief` | Obtenir des informations système via `wmic` |
| `Invoke-WmiMethod` | Exécuter des méthodes sur des objets WMI |
| `whoami /user` | Afficher le SID de l'utilisateur actuel |
| `reg query <key>` | Consulter une clé dans le registre Windows |
| `Get-MpComputerStatus` | Vérifier l'état de la protection Windows Defender |
| `sconfig` | Lancer le menu de configuration de Windows Server Core |

---

## 📁 Utilisation

Ce document est une référence rapide pour mes travaux en **Windows Administration** et **Sécurité**.  

