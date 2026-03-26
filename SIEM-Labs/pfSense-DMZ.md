# Lab PfSense WAN + LAN + DMZ

## Configuration de la VM PfSense

### Ajout des cartes réseau
1. Ajouter 2 cartes réseau en plus :
   - Première carte : **Bridged + Replicate physical network connection state** (WAN)
   - Deuxième carte : **LAN Segment nommé LAN** (réseau local virtuel)
   - Troisième carte : **LAN Segment nommé DMZ**

2. Lancer la VM et effectuer l'installation de PfSense.

### Configuration des interfaces
Après l'installation, configurer les interfaces :
- **WAN** → `em0`
- **LAN** → `em1`

#### Configuration de l'interface LAN
1. Appuyer sur **2 (Set interface IP address)**
2. Sélectionner **2 (LAN)**
3. Configurer IPv4 :
   - Adresse : `192.168.100.1`
   - Masque de sous-réseau : `/24`
   - Passerelle : `NONE`
4. Configurer IPv6 : `NONE`
5. Activer le serveur DHCP sur LAN : `NO`

---

## Configuration de la VM Windows (LAN)
1. Mettre la carte réseau en **LAN Segment : LAN**
2. Configurer une IP statique :
   - Adresse IP : `192.168.100.2`
   - Masque de sous-réseau : `255.255.255.0`
   - Passerelle : `192.168.100.1` (IP du PfSense)
   - Serveur DNS préféré : `1.1.1.1`
3. Accéder à PfSense via le navigateur : `http://192.168.100.1`

### Configuration initiale de PfSense
- **Hostname** : `pfSense`
- **Domain** : `home.arpa`
- **Primary DNS** : `1.1.1.1`
- **Secondary DNS** : `9.9.9.9`
- **WAN / LAN** : Déjà configurés

---

## Configuration de la DMZ
### Assignation de l'interface
1. Aller dans **Interfaces > Interface Assignments**
2. Ajouter l'interface `em2`
3. Renommer **OPT1** en `DMZ`
4. Configurer IPv4 en **Static IPv4** :
   - Adresse IP : `192.168.200.1/24`

### Configuration de la VM Windows Server (DMZ)
1. Mettre la carte réseau en **LAN Segment : DMZ**
2. Configurer une IP statique :
   - Adresse IP : `192.168.200.2`
   - Masque de sous-réseau : `255.255.255.0`
   - Passerelle : `192.168.200.1`
   - Serveur DNS préféré : `1.1.1.1`
3. Installer le rôle **Serveur Web IIS**

---

## Configuration des règles de pare-feu

### Règles pour le LAN
1. Aller dans **Firewall > Rules > LAN**
2. Ajouter une règle **Block** :
   - **Protocol** : Any
   - **Source** : LAN Subnets
   - **Destination** : DMZ Subnets
   - **Description** : Bloquer les flux entre le LAN et la DMZ

3. Ajouter une règle **Pass** :
   - **Source** : LAN Subnets
   - **Destination** : `192.168.200.2`
   - **Port** : HTTP (80)
   - **Description** : Autoriser l'accès au serveur Web depuis le LAN

### Règles pour la DMZ
1. Aller dans **Firewall > Rules > DMZ**
2. Ajouter une règle **Block** :
   - **Protocol** : Any
   - **Source** : DMZ Subnets
   - **Destination** : LAN Subnets
   - **Description** : Bloquer les flux vers le LAN

3. Ajouter une règle **Pass** :
   - **Source** : DMZ Subnets
   - **Destination** : Any
   - **Port** : HTTP (80)

4. Dupliquer la règle précédente en modifiant :
   - **Port** : HTTPS (443)
   - **Protocol** : TCP/UDP
   - **Port** : DNS (53)

---

## Configuration du NAT pour le serveur Web
1. Aller dans **Firewall > NAT > Port Forward**
2. Ajouter une règle :
   - **Interface** : WAN
   - **Protocol** : TCP
   - **Destination** : WAN Address
   - **Port** : HTTP
   - **Redirect Target IP** : `192.168.200.2`
   - **Redirect Target Port** : HTTP

---

## Résumé
- **PfSense** est configuré avec 3 interfaces : WAN, LAN, DMZ
- **Windows (LAN)** est configuré avec une IP statique et peut accéder à PfSense
- **Windows Server (DMZ)** est configuré avec une IP statique et héberge un serveur web
- **Pare-feu** :
  - Blocage des flux entre LAN et DMZ sauf HTTP (80)
  - Autorisation des accès HTTP/HTTPS/DNS depuis DMZ vers Internet
- **NAT** : Redirection du port 80 vers le serveur IIS de la DMZ

