# Workshop - Introduction aux Infrastructures Cloud : Ansible + Kubernetes


# TP - Introduction aux Infrastructures Cloud : Ansible + Kubernetes

## 🎯 Objectif du TP

Ce TP vous permet de découvrir :
- Le provisionnement d'une machine distante via Ansible
- Le déploiement de services web sur Kubernetes (via Minikube)
- L'automatisation complète d'une stack de services

---

## 🧰 Pré-requis

- Avoir accès à une VM Debian
- Connexion SSH fonctionnelle depuis votre machine hôte (`ssh student@{ip_de_vote_VM}` en étant connecté via VPN au réseau serveur de l'ETNA)
- Avoir installé **Ansible** sur votre machine locale (https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html / https://docs.ansible.com/ansible/2.9/installation_guide/intro_installation.html)

---

## 🗂️ Structure du projet

```
.
├── ansible/
│   ├── hosts               # Inventaire Ansible (à modifier)
│   └── playbook.yml        # Script de provisioning et de déploiement
├── app/                    # Application Flask bonus (Docker)
├── k8s/
│   └── services/
│       ├── hello-app/      # HTML simple via Python http.server
│       └── flask-app/      # Application Flask en conteneur
```

---

## ✅ Étape 1 – Préparer le fichier `hosts`

Dans `ansible/hosts`, remplacez les valeurs :

```
[minikube_vms]
vm1 ansible_host=IP_DE_VOTRE_VM ansible_user=UTILISATEUR ansible_ssh_private_key_file=~/.ssh/votre_clé
```

Assurez-vous que vous pouvez vous connecter à la VM via SSH :
```bash
ssh -i ~/.ssh/votre_clé utilisateur@IP_DE_VOTRE_VM
```

---

## ✅ Étape 2 – Lancer le playbook

Depuis le dossier racine :

```bash
ansible-playbook -i ansible/hosts ansible/playbook.yml
```

Ce playbook :
- Installe Docker + Minikube sur la VM
- Démarre un cluster Kubernetes local
- Déploie deux services web accessibles depuis un navigateur

---

## ✅ Étape 3 – Tester les services

Une fois le playbook terminé, accédez dans votre navigateur à :

- Service de test : http://IP_DE_VOTRE_VM:30001
- App Flask : http://IP_DE_VOTRE_VM:30002

---

## ⭐ Étape Bonus – Modifier l’app Flask

1. Allez dans le dossier `app/` :
   - Modifiez `app.py` pour personnaliser le message HTML
2. Relancez uniquement la partie déploiement avec :

```bash
ansible-playbook -i ansible/hosts ansible/playbook.yml --tags flask
```

(Vous pouvez aussi reconstruire l’image et redéployer manuellement.)

---

## 🧠 Concepts abordés

- Infrastructure as Code (Ansible)
- Provisionnement distant
- Cluster Kubernetes local (Minikube)
- Déploiement de services
- Exposition via NodePort

---

## 📚 Pour aller plus loin

- https://www.ansible.com/
- https://kubernetes.io/docs/
- https://minikube.sigs.k8s.io/

