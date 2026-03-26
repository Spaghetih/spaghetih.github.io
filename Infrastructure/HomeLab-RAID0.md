# 🚀 Installation RAID 0 sur serveur Fujitsu

Ce guide explique comment configurer un RAID matériel (RAID 0 dans notre cas) sur mon serveur Fujitsu avec un contrôleur LSI MegaRAID via le BIOS WebBIOS Utility.

---

## 🖥️ Matériel utilisé

- Serveur : Fujitsu PRIMERGY TX2540 M1
- RAID Controller : LSI MegaRAID SAS 6Gbps (D3116C)
- Batterie BBU : Tecate PowerBurst TPL 13.5V 6.4F (connectée sur le port J2B1)
- Disques durs : 6× TOSHIBA SAS 300GB

---

## 🛠️ Étapes de configuration

### 1. Accéder au BIOS WebBIOS Utility
- Au démarrage du serveur, appuyez sur `Ctrl+H` lorsqu'on vous le demande pour entrer dans l’utilitaire RAID.

---

### 2. Sélection du contrôleur
- Choisissez le contrôleur détecté (ex: RAID Ctlr1 SAS 6G 1GB D3116C)
- Cliquez sur **Start**

---

### 3. Scan et état des disques
- Vérifiez que tous les disques sont en statut `Unconfigured Good`
- Cliquez sur **Configuration Wizard**

---

### 4. Choix du mode de configuration
- Sélectionner : `Manual Configuration`
- Redundancy : `Redundancy when possible` puis **Next**

---

### 5. Création du groupe RAID
- Sélectionner tous les disques (Ctrl + clic si la souris fonctionne, sinon espace + flèches)
- Cliquer sur **Add to Array**
- Puis **Accept DG**

---

### 6. Ajout à un Span
- Sélectionner le groupe créé
- Cliquer sur **Add to Span**
- Puis **Next**

---

### 7. Définir le volume RAID virtuel
- RAID Level : `RAID 0` (⚠️ Pas de tolérance de panne)
- Write Policy : `Write Back with BBU`
- Strip Size : 64KB (par défaut)
- Cliquer sur **Accept**

⚠️ Si la BBU n’est pas détectée, le système repassera automatiquement en `Write Through`.

---

### 8. Initialisation et démarrage
- Retour sur le menu principal
- Sélectionner votre volume RAID
- Cocher : `Fast Initialize`
- Lancer avec le bouton **Go**
- Cocher ensuite `Set Boot Drive` pour le disque RAID virtuel

---

## 📊 Schéma de la configuration

![RAID setup diagram](raid_setup.png)

---

## ✅ Résultat

Votre volume RAID 0 de **1.361 TB** est maintenant actif et prêt à être utilisé pour l’installation d’un OS ou stockage avancé.

---

## 📎 À noter

- Le RAID 0 maximise les performances mais n’offre **aucune sécurité** en cas de panne disque.
- Pensez à surveiller la santé des disques et la charge de la BBU régulièrement.
