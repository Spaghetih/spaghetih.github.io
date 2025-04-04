
# 🔐 Lab OPNsense + Wazuh (Firewall + SIEM)

Ce projet de lab a pour objectif de mettre en place une infrastructure virtuelle simulant un environnement sécurisé avec un pare-feu (OPNsense) et un système de détection d'intrusions (Wazuh), dans un réseau isolé.

---

## 🧱 Architecture du Lab

```
[ Client Kali / Linux ] ---> [ OPNsense (Firewall) ] ---> [ NAT / Internet ]
                                      |
                                      +--> [ Wazuh Server (Debian) ]
```

---

## 🌐 Plan d'adressage IP

| Machine         | Rôle              | IP              | Réseau     |
|-----------------|-------------------|------------------|------------|
| OPNsense LAN    | Passerelle        | 192.168.100.1    | LAN-LAB    |
| Wazuh (Debian)  | SIEM              | 192.168.100.10   | LAN-LAB    |
| Client Kali     | Générateur trafic | 192.168.100.20   | LAN-LAB    |
| OPNsense WAN    | Sortie Internet   | DHCP (VMware NAT)| NAT        |

---

## ⚙️ Étapes de mise en place

### 1. Déploiement des VMs

- **Debian 12** : pour héberger Wazuh
- **OPNsense** : avec 2 interfaces (NAT pour WAN, LAN-LAB pour LAN)
- **Kali Linux** : machine cliente avec navigateur pour accéder à OPNsense

### 2. Configuration réseau Debian

```bash
sudo ip addr add 192.168.100.10/24 dev eth0
sudo ip route add default via 192.168.100.1
echo "nameserver 1.1.1.1" | sudo tee /etc/resolv.conf
```

### 3. Configuration réseau Kali

```bash
sudo ip addr add 192.168.100.20/24 dev eth0
sudo ip route add default via 192.168.100.1
echo "nameserver 1.1.1.1" | sudo tee /etc/resolv.conf
```

### 4. Configuration OPNsense (console)

- Interface WAN : `em0` (NAT)
- Interface LAN : `em1` (LAN-LAB)
- IP LAN statique : `192.168.100.1/24`

---

## 🔧 Configuration OPNsense (interface Web)

### NAT Sortant (Firewall > NAT > Outbound)

- Mode : Hybrid Outbound NAT
- Règle personnalisée :
  - Interface : WAN
  - Source : 192.168.100.0/24
  - Translation : Interface address

### Règle Firewall LAN (Firewall > Rules > LAN)

- Action : Pass
- Protocol : any
- Source : LAN net
- Destination : any
- Description : Allow LAN to WAN

---

## ✅ Vérification de connectivité

Depuis Debian :

```bash
ping 1.1.1.1
ping google.com
```

---

## 🔜 Étape suivante

➡️ Installer Wazuh sur la VM Debian une fois l’accès Internet fonctionnel.

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

---

## 🧠 Objectifs pédagogiques

- Compréhension des flux réseau
- Configuration manuelle d'un pare-feu open source
- Intégration avec une solution SIEM open source (Wazuh)
- Simulation de trafic légitime et malveillant

---
