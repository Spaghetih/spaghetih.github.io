# Configuration DHCP sur Cisco Packet Tracer

## 1. Accéder au mode de configuration globale
```bash
enable
configure terminal
```

## 2. Exclure certaines adresses IP (Optionnel)
```bash
ip dhcp excluded-address 192.168.1.1 192.168.1.10
```

## 3. Créer le pool DHCP
```bash
ip dhcp pool DHCP_LAN1
```

## 4. Définir le réseau et le masque
```bash
network 192.168.1.0 255.255.255.0
```

## 5. Définir la passerelle par défaut
```bash
default-router 192.168.1.1
```

## 6. Configurer le serveur DNS
```bash
dns-server 192.168.1.250
```

## 7. Définir la durée du bail DHCP (Optionnel)
```bash
lease 7
```

## 8. Activer le service DHCP
```bash
service dhcp
```

## 9. Vérifier la configuration et les attributions DHCP
```bash
end
show ip dhcp pool          # Afficher les infos du pool DHCP
show ip dhcp binding       # Voir les adresses IP attribuées
show running-config | section dhcp  # Vérifier la config DHCP
```

## 10. Tester avec un PC (Client DHCP)
1. Connecter un **PC** au **Switch**.
2. Aller dans `Desktop` → `IP Configuration`.
3. Sélectionner `DHCP`.
4. Vérifier si une **adresse IP, une passerelle et le DNS (192.168.1.250)** sont attribués.

---

🚀 **Votre serveur DHCP est maintenant configuré et fonctionnel !**

