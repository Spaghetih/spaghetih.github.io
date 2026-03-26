# Firewalls : Sécurité des Réseaux

## Introduction aux Firewalls
Un **firewall** (pare-feu) est un dispositif au sein d’un réseau responsable de déterminer quel trafic est autorisé à entrer et à sortir. Vous pouvez penser à un firewall comme une sécurité aux frontières pour un réseau.

Un administrateur peut configurer un firewall pour **autoriser** ou **refuser** le trafic en fonction de plusieurs critères tels que :
- **Origine du trafic :** Le firewall a-t-il été configuré pour accepter/refuser le trafic d’un réseau spécifique ?
- **Destination du trafic :** Le firewall a-t-il été configuré pour accepter/refuser le trafic à destination d’un réseau spécifique ?
- **Port cible :** Le firewall a-t-il été configuré pour accepter/refuser le trafic destiné, par exemple, au port 80 ?
- **Protocole :** Le firewall a-t-il été configuré pour accepter/refuser le trafic utilisant UDP, TCP, ou les deux ?

Les firewalls inspectent les paquets pour répondre à ces questions.

---

## Types de Firewalls
Les firewalls peuvent être matériels (souvent utilisés dans les grandes entreprises) ou logiciels (par exemple, des outils comme Snort). Ils peuvent être classés en deux catégories principales : **Stateful** et **Stateless**.

| **Catégorie de Firewall** | **Description**                                                                                                                                                              |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Stateful**              | Ce type de firewall utilise les informations complètes d’une connexion pour déterminer le comportement d’un appareil. Il analyse la **connexion entière** plutôt qu’un paquet individuel. |
|                           | Les firewalls Stateful consomment plus de ressources car la prise de décision est dynamique. Par exemple, un firewall peut autoriser les premières étapes d’une connexion TCP avant de bloquer celle-ci. |
|                           | Si une connexion d’un hôte est mauvaise, le firewall bloquera l’appareil entier.                                                                                           |
| **Stateless**             | Ce type de firewall utilise un ensemble statique de règles pour décider si des **paquets individuels** sont acceptables ou non.                                               |
|                           | Ces firewalls consomment moins de ressources mais sont moins intelligents. Si une règle n’est pas définie précisément, le firewall devient inutile.                          |
|                           | Ces firewalls sont très efficaces contre de grandes quantités de trafic provenant de plusieurs hôtes (ex : attaques par déni de service distribué - DDoS).                  |


