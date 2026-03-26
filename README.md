# CyberLab – Documentation & Labs

---

## Reseaux & Protocoles

- [DNS – Enregistrements et types](Reseaux/DNS.md)
- [TCP/IP – Packets & Trames](Reseaux/TCP-IP.md)
- [UDP/IP](Reseaux/UDP.md)
- [Firewalls – Concepts & Configuration](Reseaux/Firewall.md)
- [VPN – Fonctionnement et usages](Reseaux/VPN.md)
- [HTTP – Structure des requetes](Reseaux/HTTP.md)

---

## Systemes & Commandes

### Linux
- [Commandes Linux essentielles](Systemes/Linux/Commandes.md)

### Windows
- [Commandes Windows essentielles](Systemes/Windows/Commandes.md)
- [Commandes Windows (complements)](Systemes/Windows/Commandes-Essentielles.md)
- [Cheat Sheet Windows avancee](Systemes/Windows/Cheat-Sheet.md)
- [Gestion des taches Windows](Systemes/Windows/Gestion-Taches.md)

### PowerShell
- [Introduction a PowerShell](Systemes/PowerShell/Introduction.md)
- [PowerShell – Commandes & Scripting](Systemes/PowerShell/Commandes.md)

---

## Scripting & Automatisation

- [Python – Cheat Sheet](Scripting/Python-Cheatsheet.md)
- [JavaScript Essentials – Concepts et Securite](Scripting/JavaScript-Essentials.md)
- [Ansible – Premier Lab](Scripting/Ansible-Lab.md)

---

## Bases de Donnees & SQL

- [SQL Fondamentaux – Concepts et commandes](Bases-de-Donnees/SQL-Fondamentaux.md)
- [SQL Basics – SELECT & CRUD](Bases-de-Donnees/SQL-Basics.md)
- [Requetes SQL utiles](Bases-de-Donnees/Requetes-SQL.md)
- [SQLMap – Injections SQL](Bases-de-Donnees/SQLMap.md)

---

## Securite Offensive & Analyse

- [Shells – Reverse & Bind](Securite-Offensive/Shells.md)
- [Auth Bypass – Enum, Bruteforce, Logic Flaw, Cookies](Securite-Offensive/Auth-Bypass.md)
- [XSS Walkthrough – Payloads & Exploitation](Securite-Offensive/XSS-Walkthrough.md)
- [FlareVM – Environnement d'analyse de malware](Securite-Offensive/FlareVM.md)
- [Vulnerability Scanner – OpenVAS & concepts](Securite-Offensive/Vulnerability-Scanner.md)
- [Conversion Hexadecimal / Decimal](Securite-Offensive/Conversion-Hexa.md)

---

## SIEM & Labs Securite

- [Wazuh + Agent Windows – Deploiement SIEM](SIEM-Labs/Wazuh-Windows-Agent.md)
- [OPNsense + Wazuh – Firewall & SIEM](SIEM-Labs/OPNsense-Wazuh.md)
- [Zabbix + Wazuh – Supervision des alertes](SIEM-Labs/Zabbix-Wazuh.md)
- [Suricata + Filebeat + Wazuh – Detection d'intrusions](SIEM-Labs/Suricata-Wazuh-Filebeat.md)
- [pfSense – DMZ, LAN, WAN](SIEM-Labs/pfSense-DMZ.md)

---

## Infrastructure

- [Cisco – Configuration DHCP](Infrastructure/Cisco/DHCP.md)
- [Cisco – Configuration Routeur](Infrastructure/Cisco/Router.md)
- [HomeLab – Installation RAID 0 (Fujitsu/LSI MegaRAID)](Infrastructure/HomeLab-RAID0.md)

---

## CTF Writeups

- [Anonforce – HackTheBox (Boot2Root, FTP/PGP/Hashcat)](CTF-Writeups/Anonforce-HTB/README.md)
- [Tetris – Hackfinity 2025 (Godot Reverse Engineering)](CTF-Writeups/Tetris-Hackfinity2025/README.md)

---

## Modele OSI (7 couches)

| Couche | Nom | Fonction principale | Exemples |
|--------|-----|---------------------|----------|
| 7 | Application | Interfaces utilisateur / applis reseau | HTTP, DNS, FTP, SMTP |
| 6 | Presentation | Encodage, chiffrement, compression | JPEG, SSL/TLS, MPEG |
| 5 | Session | Maintien des connexions | NetBIOS, RPC, SMB |
| 4 | Transport | Fiabilite, flux, ports | TCP, UDP |
| 3 | Reseau | Adressage IP, routage | IP, ICMP, IGMP |
| 2 | Liaison de donnees | Trames, adressage MAC | Ethernet, PPP, VLAN |
| 1 | Physique | Transmission brute, support materiel | RJ45, Fibre, Wi-Fi |
