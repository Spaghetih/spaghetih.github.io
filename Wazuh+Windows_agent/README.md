# 🔐 Déploiement d'un SIEM Wazuh All-in-One + Agent Windows

## 📌 Objectif

Mettre en place un environnement de supervision de sécurité (SIEM) avec **Wazuh 4.7.5** sur une **machine virtuelle CentOS 8 Stream**, et connecter un **agent Windows physique** pour la collecte et l’analyse des logs.

---

## 🧱 Infrastructure

| Composant     | Système         | Rôle                 | IP                |
|---------------|-----------------|----------------------|-------------------|
| VM Wazuh      | CentOS 8 Stream | Manager + Dashboard  | `192.168.31.10`   |
| Poste client  | Windows 10/11   | Agent Wazuh          | Variable (DHCP)   |

---

## 🛠️ Étapes détaillées

### 1. Création de la VM CentOS 8 Stream (sous VMware)

- **Mode réseau** : Bridge (avec interface manuelle sur `VMnet0`)
- Téléchargement ISO NetInstall ou DVD de CentOS Stream 8
- Activation de l’interface réseau `ens160` manuellement pendant l’installation
- Ajout du dépôt manuellement si NetInstall :
  ```text
  http://mirror.stream.centos.org/8-stream/BaseOS/x86_64/os/
  ```

---

### 2. Configuration post-installation CentOS

```bash
sudo dnf update -y
sudo sed -i 's/^SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config
sudo setenforce 0
sudo dnf install -y curl vim wget unzip net-tools bash-completion htop
sudo systemctl disable firewalld --now
sudo systemctl enable sshd --now
sudo reboot
```

---

### 3. Installation de Wazuh All-in-One

Téléchargement et exécution du script :

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a --ignore-check
```

> Accès au dashboard via `https://192.168.31.10` avec :
> - **User** : `admin`
> - **Password** : généré automatiquement (ex: `1o3GLW41Esgg7?xk?3EBuoixmrl5CVkh`)

---

### 4. Installation de l’agent Wazuh sur Windows

#### 🔸 Téléchargement de l'agent

- Site officiel : https://documentation.wazuh.com
- Sélection : `MSI 32/64 bits`
- IP du Manager : `192.168.31.10`
- Nom de l'agent : `Windows-Suley`
- Groupe : `default`

#### 🔸 Installation via PowerShell

```powershell
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.7.5-1.msi -OutFile ${env:tmp}\wazuh-agent.msi;
msiexec.exe /i ${env:tmp}\wazuh-agent.msi /q WAZUH_MANAGER='192.168.31.10' WAZUH_AGENT_NAME='Windows-Suley' WAZUH_REGISTRATION_SERVER='192.168.31.10'
net start wazuh-agent
```

---

### 5. Vérification sur le dashboard

- L'agent apparaît dans l’onglet `Agents > Manage agents`
- Statut : ✅ Active
- Les événements du système Windows remontent en temps réel dans `Security Events` et `Logs data`

---

## 🧪 Tests de collecte

Depuis le poste Windows :

```powershell
echo test >> C:\Windows\Temp\test-wazuh.txt
```

Résultat visible dans le dashboard Wazuh sous `Logs` > `Windows-Suley`.

---

## 📎 Suivi & idées futures

- Intégration OPNsense avec Filebeat
- Ajout de règles de détection personnalisées
- Surveillance RDP / antivirus / journaux d'événements ciblés
- Automatisation complète via Ansible ou script bash

---

## 🤝 Auteur

**Suleyman UNVER**  
🔧 Réseaux & Cybersécurité junior  
📍 Gundershoffen, France  
