Lab PfSense WAN + LAN + DMZ
----
## VM PFSENSE

Ajout de 2 cartes réseau en plus :

1. Première carte en réseau en Bridged + Replicate physical network connection state
2. Deuxième carte réseau en LAN segment nommée **LAN** (pour le réseau local virtuel)
3. Troisième carte réseau en LAN Segment nommée **DMZ**

Lancer la VM pour faire l'installation.

### Configuration post-installation

- On a l'adresse WAN -> **em0**
- On a l'adresse LAN -> **em1**

**Configuration de l'interface LAN**

1. Appuyer sur la touche **2** pour **Set interface IP address**
2. Entrer le numéro de l'interface à configurer : **2**
3. **Configure IPv4 address LAN interface via DHCP (y/n)** -> **n**
4. **Enter the new LAN IPv4 ADDRESS** -> **192.168.100.1**
5. **Enter the new LAN IPv4 subnet bit count (1 to 32)** -> **24**
6. **For a WAN enter the LAN IPv4 upstream gateway address, For a LAN press ENTER for none** -> **NONE**
7. **Configure IPv6** -> **none**
8. **Enable DHCP on LAN server** -> **no**

----
## VM Windows

Mettre la carte réseau en **LAN Segment LAN** pour positionner le PC dans la zone.

### Configuration de l'adresse IP statique de Windows

- **Adresse IP** : 192.168.100.2
- **Masque de sous-réseau** : 255.255.255.0
- **Passerelle par défaut** : 192.168.100.1 *(IP du PfSense)*
- **Serveur DNS préféré** : 1.1.1.1 *(ou l'IP de PfSense si on veut un résolveur DNS)*

### Accès à l'interface Web de pfSense

1. Ouvrir un navigateur et entrer **192.168.100.1**
2. **Configuration pfSense**
   - **Hostname** : pfSense
   - **Domain** : home.arpa *(par défaut)*
   - **Primary DNS** : 1.1.1.1
   - **Secondary DNS** : 9.9.9.9

Ne pas modifier la configuration du WAN et du LAN (déjà configurée).

---
## pfSense : Configuration du DMZ

1. Aller dans **Interfaces > Interface Assignments**
2. Sélectionner la carte réseau **em2** et cliquer sur **Add**
3. **OPT1** se crée, cliquer dessus
4. **Description** : **DMZ**
5. **IPv4 Configuration Type** : **Static IPv4**
6. **Static IPv4 Configuration** :
   - **IPv4 Address** : **192.168.200.1 /24**

