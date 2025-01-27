# Ligne de Requête (Request Line)

La **ligne de requête** (ou ligne de départ) est la première partie d'une requête HTTP et informe le serveur du type de requête à traiter. Elle comporte trois parties principales : la méthode HTTP, le chemin URL et la version HTTP.

**Exemple** : `MÉTHODE /chemin HTTP/version`

---

## Méthodes HTTP

La méthode **HTTP** indique au serveur quelle action l'utilisateur souhaite effectuer sur la ressource identifiée par le chemin URL. Voici certaines des méthodes les plus courantes ainsi que leurs éventuels problèmes de sécurité :

### GET
Utilisé pour **récupérer** des données du serveur sans apporter de modifications.  
**Rappel** : Assurez-vous de n'exposer que les données que l'utilisateur est autorisé à voir. Évitez de mettre des informations sensibles (comme des tokens ou des mots de passe) dans les requêtes GET, car elles peuvent apparaître en clair.

### POST
Envoie des **données** au serveur, généralement pour créer ou mettre à jour une ressource.  
**Rappel** : Validez et nettoyez toujours les données envoyées pour éviter les attaques comme les **injections SQL** ou les **XSS**.

### PUT
Remplace ou **met à jour** quelque chose sur le serveur.  
**Rappel** : Assurez-vous que l'utilisateur est autorisé à effectuer des modifications avant d'accepter la requête.

### DELETE
**Supprime** quelque chose du serveur.  
**Rappel** : Comme pour PUT, assurez-vous que seuls les utilisateurs autorisés peuvent supprimer des ressources.

### PATCH
Met à jour une **partie** d'une ressource. Cela est utile pour effectuer de petites modifications sans remplacer la ressource entière, mais il est essentiel de valider les données pour éviter les incohérences.

---

## Autres Méthodes HTTP

### HEAD
Fonctionne comme GET mais ne récupère que les **en-têtes**, sans le contenu complet.  
Cela est utile pour vérifier les métadonnées sans télécharger la réponse complète.

### OPTIONS
Informe sur les **méthodes disponibles** pour une ressource spécifique, aidant les clients à comprendre ce qu'ils peuvent faire avec le serveur.

### TRACE
Similaire à OPTIONS, cette méthode montre quelles méthodes sont autorisées, ce qui est utile pour le débogage.  
**Attention** : Beaucoup de serveurs désactivent TRACE pour des raisons de sécurité.

### CONNECT
Utilisée pour créer une connexion sécurisée, comme pour le HTTPS.  
Elle est moins courante mais essentielle pour les communications cryptées.

---

### Remarques
- Chaque méthode a ses propres règles de sécurité. Par exemple, les requêtes PATCH doivent être validées pour éviter les incohérences.
- Les méthodes **OPTIONS** et **TRACE** doivent être désactivées si elles ne sont pas nécessaires afin de réduire les risques de sécurité.
