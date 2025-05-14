# TP – Déploiement d'infrastructure Cloud avec K3s et Ansible

## 🎯 Objectif

Ce TP vous permettra de :
- Installer un cluster Kubernetes léger avec K3s
- Automatiser le déploiement via Ansible
- Exposer deux services web accessibles dans un navigateur

---

## ⚙️ Prérequis

- Une VM Debian
- Connexion SSH fonctionnelle depuis votre machine hôte (`ssh student@{ip_de_vote_VM}` en étant connecté via VPN au réseau serveur de l'ETNA)
- Avoir installé **Ansible** sur votre machine locale (https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html / https://docs.ansible.com/ansible/2.9/installation_guide/intro_installation.html)

---

## 📁 Structure

```
.
├── ansible/
│   ├── hosts
│   └── playbook.yml
└── k8s/services/
    ├── hello-app/
    └── portainer/
```

---

## 🚀 Étapes

### 1. Modifier `ansible/hosts`

```ini
[k3s_nodes]
vm1 ansible_host=IP_VM ansible_user=utilisateur ansible_ssh_private_key_file=~/.ssh/clé
```

### 2. Lancer le playbook

```bash
ansible-playbook -i ansible/hosts ansible/playbook.yml
```

---

## 🌐 Accès aux services

- App HTML simple : http://IP_VM:30001
- Interface Portainer : http://IP_VM:30002

> Lors du premier accès à Portainer, créez un compte admin.

---

## ✅ Concepts abordés

- Installation automatisée de K3s
- Déploiement de services avec YAML
- Utilisation de services `NodePort` pour exposition

---

## 📚 Pour aller plus loin

- https://k3s.io/
- https://portainer.io/
