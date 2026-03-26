
# Suricata + Wazuh 4.7.5 + Filebeat : Déploiement et Intégration

## 🔧 Objectif
Mettre en place un IDS avec Suricata, collecter les logs avec Filebeat et les visualiser dans Wazuh (OpenSearch Dashboards).

---

## 1. 🛠 Installation de Suricata

### Sous CentOS/AlmaLinux/RHEL :
```bash
sudo dnf install epel-release -y
sudo dnf install suricata -y
```

### Vérification :
```bash
suricata -V
```

---

## 2. ⚙️ Configuration de Suricata

### Interface réseau à surveiller
```yaml
af-packet:
  - interface: ens224
    cluster-id: 99
```

### Chemin des règles personnalisées
```yaml
default-rule-path: /etc/suricata/rules
rule-files:
  - test.rules
```

### Exemple de règle personnalisée (`/etc/suricata/rules/test.rules`) :
```rules
alert icmp any any -> any any (msg:"ICMP test alert"; sid:1000001; rev:1;)
alert tcp any any -> any any (flags:S; msg:"[TEST] TCP SYN Scan detected"; sid:1000002; rev:1;)
alert http any any -> any any (msg:"[TEST] HTTP request with curl User-Agent"; content:"User-Agent: curl"; http_header; sid:1000003; rev:1;)
alert udp any any -> any 53 (msg:"[TEST] DNS Request to port 53"; sid:1000004; rev:1;)
```

### Test config :
```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

---

## 3. 📝 Permissions et fichiers nécessaires

```bash
sudo chown -R suricata:suricata /var/log/suricata
sudo chmod 644 /etc/suricata/*.config /etc/suricata/rules/test.rules
```

Copier les fichiers manquants si besoin :
```bash
sudo cp /usr/share/suricata/*.config /etc/suricata/
```

---

## 4. 🚀 Lancer Suricata

```bash
sudo systemctl enable --now suricata
sudo journalctl -u suricata -f
```

---

## 5. 🔄 Intégration avec Filebeat

### Configuration (`/etc/filebeat/filebeat.yml`) :
```yaml
filebeat.inputs:
  - type: log
    enabled: true
    paths:
      - /var/log/suricata/eve.json
    json.keys_under_root: true
    json.add_error_key: true

setup.kibana:
  host: "https://<IP>:443"
  ssl.verification_mode: none

output.elasticsearch:
  hosts: ["https://<IP>:9200"]
  username: "admin"
  password: "motdepasse"
  ssl.verification_mode: none

setup.ilm.enabled: false
setup.template.enabled: false
setup.license.check: false

processors:
  - add_host_metadata: ~
  - add_cloud_metadata: ~
```

### Activer Filebeat :
```bash
sudo systemctl enable --now filebeat
```

---

## 6. 📊 Dashboard dans OpenSearch / Wazuh Dashboards

- Créer un index pattern `filebeat-*` avec le champ `@timestamp`.
- Créer des visualisations manuellement :
  - X-axis : Histogramme sur `@timestamp`
  - Split Series : `terms` sur `alert.signature.keyword`

---

## 🐞 Débogage

- Vérifie les logs de Suricata :
  ```bash
  sudo journalctl -u suricata -f
  ```
- Vérifie que `eve.json` est rempli :
  ```bash
  tail -f /var/log/suricata/eve.json
  ```
- Pour forcer la relecture de `eve.json` :
  ```bash
  sudo rm /var/lib/filebeat/registry/filebeat/*
  sudo systemctl restart filebeat
  ```

---

## 🧪 Exemple de log généré
```json
{"timestamp":"2025-04-19T20:00:25.157762+0200","event_type":"alert","src_ip":"192.168.31.200","src_port":2449,"dest_ip":"104.18.32.47","dest_port":443,"proto":"TCP","alert":{"action":"allowed","gid":1,"signature_id":1000002,"rev":1,"signature":"[TEST] TCP SYN Scan detected","severity":3}}
```

---

## 📦 À faire
- Ajouter export automatique des dashboards `.ndjson`
- Créer un script d’installation complet

---

