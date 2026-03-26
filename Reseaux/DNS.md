
# Enregistrements DNS

## Types d’enregistrements
- **A Record** : Adresse IPv4 (ex : `104.26.10.229`)
- **AAAA Record** : Adresse IPv6 (ex : `2606:4700:20::681a:be5`)
- **CNAME Record** : Redirection vers un autre domaine (ex : `store.tryhackme.com → shops.shopify.com`)
- **MX Record** : Adresse des serveurs mail, accompagnés d’un indicateur de priorité

## Processus de connexion à un site web
1. Requête dans le navigateur
2. Recherche dans le cache local pour une adresse IP
3. Recherche dans le serveur DNS récursif
4. Demande au serveur root pour un serveur DNS autoritaire
5. Le serveur DNS autoritaire retourne l’adresse IP du site
6. Passage par le pare-feu du site
7. Passage par le Load Balancer
8. Connexion au serveur web sur le port 80 ou 443
9. Réception de la requête GET par le serveur web
10. Contact de la base de données du serveur
11. Rendu du code HTML par le navigateur
