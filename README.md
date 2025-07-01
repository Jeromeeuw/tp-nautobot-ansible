# Installation de l'environnement Ansible avec uv

## Prérequis

- Python 3.13 installé
- `snap` installé sur votre système

## Étapes

```sh
# Installer uv via snap
sudo snap install astral-uv --classic

# Créer un environnement virtuel avec Python 3.13
uv venv ansible_venv --python 3.13

# Activer l'environnement virtuel
source ansible_venv/bin/activate

# Installer ansible-core dans l'environnement virtuel
uv pip install ansible-core
```

## Utilisation du playbook Nautobot

1. Clonez ce dépôt ou placez-vous dans le dossier du projet.
2. Activez l'environnement virtuel :
   ```sh
   source ansible_venv/bin/activate
   ```
3. Installez les dépendances additionnelles si besoin :
   ```sh
   uv pip install -r requirements.txt
   ```
4. Exécutez le playbook principal :
   ```sh
   ansible-playbook -i inventory.ini playbooks/install-nautobot.yml -K --ask-vault-pass
   ```

## Structure du projet

- `playbooks/` : Contient les playbooks Ansible pour le déploiement.
- `files/` : Fichiers de configuration à copier sur la cible.
- `inventory.ini` : Inventaire des hôtes Ansible.
- `ansible_venv/` : Environnement virtuel Python pour Ansible.

## Variables sensibles

Les mots de passe et secrets doivent être placés dans un fichier `secrets.yml` (voir exemple dans `playbooks/secrets.yml.example`).  
Ne versionnez jamais vos secrets en clair dans le dépôt.

## Désactivation de l'environnement virtuel

Pour sortir de l'environnement virtuel :
```sh
deactivate
```
