
# 🔐 Intégration Wazuh avec Zabbix

## 📌 Objectif

Mettre en place une intégration entre Wazuh (SIEM) et Zabbix (Supervision) pour afficher visuellement les niveaux d’alerte générés par Wazuh dans l’interface de Zabbix.

---

## 🧱 Infrastructure utilisée

| Composant       | OS / Version        | IP                |
|------------------|----------------------|-------------------|
| Zabbix Server     | AlmaLinux 9 + MariaDB + Apache | `192.168.31.14` |
| Wazuh Server      | CentOS Stream 9     | `192.168.31.10`   |

---

## ⚙️ Étapes réalisées

### 1. 📦 Installation de Zabbix Server

- Installation de MariaDB, Apache, PHP et Zabbix Server.
- Sécurisation de MariaDB avec `mysql_secure_installation`.
- Création de la base de données `zabbix` avec un utilisateur `zabbix` (`suleyman67`).
- Importation du schéma SQL :
  ```bash
  zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql -u zabbix -p zabbix
  ```

### 2. 🌐 Installation du Frontend Zabbix

- Configuration de `/etc/zabbix/web/zabbix.conf.php`
- Vérification de l’interface web `http://192.168.31.14/zabbix`
- Résolution du problème `Zabbix server is running: No` → PID + permission `/run/zabbix`

---

### 3. 🛡️ Installation Wazuh + Zabbix Sender

- Sur la VM Wazuh :
  - Création du script d'intégration `/var/ossec/integrations/zabbix.sh`
  - Ajout du binaire `zabbix-sender` :
    ```bash
    sudo dnf install zabbix-sender --nogpgcheck
    ```

  - Test de l’envoi manuel :
    ```bash
    sudo /var/ossec/integrations/zabbix.sh /var/ossec/logs/alerts/alerts.json
    ```

---

### 4. 📡 Configuration du host CentOS-Wazuh dans Zabbix

- Nom du host : `CentOS-Wazuh`
- IP : `192.168.31.10`
- Template : `Linux by Zabbix agent`
- Port : `10050`
- Group : `Linux Servers`

#### Vérification :

- Agent installé :
  ```bash
  sudo dnf install zabbix-agent --nogpgcheck
  ```
- Fichier de conf (`/etc/zabbix/zabbix_agentd.conf`) modifié :
  ```ini
  Server=192.168.31.14
  ServerActive=192.168.31.14
  Hostname=CentOS-Wazuh
  ```
- Redémarrage :
  ```bash
  sudo systemctl enable --now zabbix-agent
  ```

---

### 5. 🧩 Création de l’item `wazuh.alert.level`

Dans **Configuration > Hosts > CentOS-Wazuh > Items** :

- **Name :** `Wazuh Alert Level`
- **Type :** `Zabbix trapper`
- **Key :** `wazuh.alert.level`
- **Type of information :** `Text`
- **Enabled :** ✅

---

### 6. 📈 Création du graphique

Dans **Configuration > Hosts > CentOS-Wazuh > Graphs** :

- **Name :** `Wazuh Alert Level`
- Ajout de l’item `Wazuh Alert Level`
- Sauvegarde, puis visualisation dans `Monitoring > Graphs`

---

## ✅ Résultat final

- Wazuh envoie ses alertes à Zabbix via le binaire `zabbix_sender`
- Zabbix les réceptionne en tant que **Zabbix trapper item**
- Une alerte est affichée dans la section `Latest data` du host `CentOS-Wazuh`
- Un graphique permet une lecture visuelle immédiate du niveau d’alerte

---

## 🧠 Remarques

- Il est crucial que le **hostname configuré dans Zabbix = Hostname dans `zabbix_agentd.conf`**
- Le type `Zabbix trapper` signifie que l’item attend des données **poussées** par un agent externe (comme ici, Wazuh).
- L’agent Zabbix sur Wazuh doit être joignable sur le port 10050 par le serveur Zabbix (vérifie le pare-feu).

---

## 📎 À venir

- Ajout de **Triggers** pour notifier par e-mail en cas d’alerte Wazuh > X
- Enrichissement des données envoyées à Zabbix (niveau, catégorie, description, etc.)
- Intégration avec Grafana pour dashboards combinés


