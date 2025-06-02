
# 🪟 Commandes Windows Utiles

## 🔑 Utilisateurs et Système
- **Dernier utilisateur connecté** : `PowerShell : Get-LocalUser`
- **Lister les utilisateurs** : `lusrmgr.msc`
- **Gestion des utilisateurs locaux** : `lusrmgr.msc`
- **Gestion des stratégies locales** : `secpol.msc`
- **Modifier un mot de passe utilisateur** : `net user <utilisateur> *`
- **Utilisateur actuel** : `WHOAMI`
- **Nom de l’hôte** : `HOSTNAME`
- **Configuration système** : `MSCONFIG`
- **Informations système** : `MSINFO32`
- **Moniteur de ressources** : `RESMON`
- **Gestion des tâches** : `taskmgr`
- **Événements système** : `eventvwr`
- **Accès rapide aux outils d’administration** : `control admintools`

## 📂 Fichiers et Disques
- **Gestion des disques** : `diskmgmt.msc`
- **Nettoyage disque** : `cleanmgr`
- **Vérification du disque** : `chkdsk`
- **Analyse et réparation des fichiers système** : `sfc /scannow`
- **Restauration de l’image système** : `DISM /Online /Cleanup-Image /RestoreHealth`
- **Ouvrir l'explorateur** : `explorer.exe`
- **Dossier des tâches planifiées** : `taskschd.msc`

## 🌐 Réseau
- **Configuration IP** : `ipconfig /all`
- **Table de routage** : `route print`
- **Connexions actives** : `netstat -ano`
- **Test de connectivité** : `ping`, `tracert`, `pathping`
- **Pare-feu Windows** : `wf.msc`
- **Group Policy Management** : `gpedit.msc`
- **Raccourci vers les paramètres réseau** : `ncpa.cpl`

## 🔍 Registre et Hôtes
- **Fichier Hosts ou Registre** :  
  - `HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > Windows > CurrentVersion > Run`
- **Ouvrir le registre** : `regedit.exe` ou `regedt32.exe`

## 🔒 Sécurité et Contrôle d'Accès
- **Gestion de l’UAC** : `useraccountcontrolsettings`
- **Stratégies de sécurité locales** : `secpol.msc`

## 🔧 Autres commandes utiles
- **Informations système rapide** : `systeminfo`
- **Ouvrir un prompt admin rapidement** : `Win + X` puis `A`
- **Propriétés système** : `sysdm.cpl`

---

🧠 *Cette cheat sheet est conçue comme un rappel rapide pour l'administration et le diagnostic sous Windows.*

