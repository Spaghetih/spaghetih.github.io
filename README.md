
# SOC Notes

Cette documentation contient des notes et des commandes utiles pour les investigations en sécurité.

## Contenu

- [Commandes Windows](windows/windows_commands.md)
- [Commandes Linux](linux/linux_commands.md)
- [Enregistrements DNS](dns/dns_notes.md)
- [SQL](sql/SQL_Queries.md)
- [TCP/IP](network/Packet&Trames.md)
- [UDP/IP](network/UDP.md)
- [FireWall](network/firewall.md)
- [VPN](network/VPN.md)
- [PowerShell](PowerShell/ps.md)
- [Cisco](Cisco/Commandes.md)

# Rappel Modèle OSI : Les 7 couches

| Numéro de couche  | Nom de la couche            | Fonction principale                               | Protocoles et standards exemples           |
|-------------------|----------------------------|---------------------------------------------------|--------------------------------------------|
| Couche 7          | Application         | Fournit des services et des interfaces aux applications  | HTTP, FTP, DNS, POP3, SMTP, IMAP           |
| Couche 6          | Présentation        | Encodage des données, chiffrement et compression         | Unicode, MIME, JPEG, PNG, MPEG             |
| Couche 5          | Session             | Établit, maintient et synchronise les sessions           | NFS, RPC                                   |
| Couche 4          | Transport           | Communication de bout en bout et segmentation des données| UDP, TCP                                   |
| Couche 3          | Network             | Adressage logique et routage entre réseaux               | IP, ICMP, IPSec                            |
| Couche 2          | Data link           | Transfert fiable des données entre nœuds adjacents       | Ethernet (802.3), WiFi (802.11)            |
| Couche 1          | Physical            | Transmission physique des données                        | Signaux électriques, optiques et sans fil  |

