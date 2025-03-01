## Configuration du Routeur R1

### Configuration de base
```
Enable  # Passer en mode privilégié
conf t  # Mode configuration globale
hostname R1  # Nom du routeur
```

### Configuration de l'interface réseau
```
interface GigabitEthernet 0/1  # Sélection de l'interface
ip address 192.168.1.254 255.255.255.0  # Configuration de l'IP et du masque
no shutdown  # Activation de l'interface
```

### Configuration du protocole de routage RIP
```
router rip  # Activation du protocole RIP
version 2  # Utilisation de RIP version 2
no auto-summary  # Désactivation du résumé automatique
network 192.168.1.0  # Ajout du réseau local au protocole RIP
network 10.1.1.0  # Ajout d'un réseau inter-routeur au protocole RIP
exit  # Sortie du mode configuration de RIP
exit  # Sortie du mode configuration globale
```

### Sauvegarde de la configuration
```
copy running-config startup-config  # Sauvegarde de la configuration
Destination filename [startup-config]?  # Confirmation de la sauvegarde
Building configuration...
[OK]
```

---

Cette configuration permet au routeur R1 de :
- Avoir une interface active avec l'adresse IP `192.168.1.254`
- Activer le protocole de routage RIP version 2
- Partager les réseaux `192.168.1.0` et `10.1.1.0` avec RIP
- Sauvegarder la configuration pour la rendre persistante après un redémarrage.

