
# 🚀 Débuter avec Ansible – Premier Lab Personnel

## 🧠 Objectif

Mettre en place un environnement Ansible complet sur une machine de contrôle (AlmaLinux) et exécuter un playbook simple sur une machine distante via SSH.

---

## 🖥️ Environnement utilisé

| Rôle                | OS         | Description                        |
|---------------------|------------|------------------------------------|
| Machine de contrôle | AlmaLinux  | Ansible installé                   |
| Machine cible       | AlmaLinux  | Serveur distant géré via Ansible   |
| Hyperviseur         | VMware     | Exécution des VM                   |

---

## 🛠️ Étapes réalisées

### 1. Installation d’Ansible sur la machine de contrôle

```bash
sudo dnf install epel-release -y
sudo dnf install ansible -y
```

---

### 2. Génération de la clé SSH

Sur la machine de contrôle :

```bash
ssh-keygen
```

Appuyer sur Entrée à chaque étape.

---

### 3. Envoi de la clé publique vers la machine distante

```bash
ssh-copy-id sley@192.168.31.49
```

Test de connexion sans mot de passe :

```bash
ssh sley@192.168.31.49
```

✅ Résultat attendu : connexion directe sans mot de passe

---

### 4. Création du fichier d'inventaire

```ini
# inventory.ini
[testservers]
192.168.31.49 ansible_user=sley
```

---

### 5. Test de connectivité avec le module `ping`

```bash
ansible all -i inventory.ini -m ping
```

✅ Résultat :

```json
192.168.31.49 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

---

### 6. Création d’un playbook de test

Fichier : `test_playbook.yml`

```yaml
---
- name: Test Ansible sur VM
  hosts: testservers
  become: yes
  tasks:
    - name: Créer un fichier de test
      copy:
        content: "Fichier créé par Ansible sur la VM"
        dest: /tmp/fichier_ansible.txt

    - name: Installer htop
      dnf:
        name: htop
        state: present
```

---

### 7. Exécution du playbook avec mot de passe sudo

```bash
ansible-playbook -i inventory.ini test_playbook.yml --ask-become-pass
```

✅ Résultat :
- Fichier `/tmp/fichier_ansible.txt` présent sur la VM
- `htop` installé avec succès

---

## 🔍 Résumé des compétences validées

- ✅ Installation d’Ansible sur AlmaLinux
- ✅ Configuration de SSH sans mot de passe
- ✅ Création et utilisation d’un inventaire statique
- ✅ Utilisation des modules `ping`, `copy` et `dnf`
- ✅ Exécution d’un playbook avec élévation de privilèges

---

## 📁 Arborescence du projet

```
ansible-lab/
├── inventory.ini
├── test_playbook.yml
└── ansible-lab-init.md
```

---

## 📌 Prochaine étape suggérée

Passer à :
- La gestion d’utilisateurs
- Les templates Jinja2
- L’organisation en **rôles Ansible**
- La création d’un playbook de **durcissement serveur**

---

## 📚 Références utiles

- [Ansible Documentation Officielle](https://docs.ansible.com/)
- [Module `copy`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html)
- [Module `dnf`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/dnf_module.html)
