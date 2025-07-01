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
uv pip install -r requirements.txt
```

## Connexion SSH sans mot de passe (recommandé pour Ansible)

### Étape 1 – Générer une clé SSH

```bash
ssh-keygen -t ed25519 -C "ton_email@example.com"
```
Accepte le chemin par défaut (`~/.ssh/id_ed25519`) et définis une passphrase si tu veux plus de sécurité.

### Étape 2 – Copier la clé publique vers la machine distante

Toujours depuis la machine A :

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub utilisateur@IP_ou_nom_de_machine_B
```
Cela va automatiquement ajouter la clé dans `~/.ssh/authorized_keys` sur la machine distante.

### (Optionnel) Ajouter la clé privée à l'agent SSH

```bash
ssh-add ~/.ssh/id_ed25519
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

Les mots de passe et secrets doivent être placés dans un fichier `secrets.yml`.

## Désactivation de l'environnement virtuel

Pour sortir de l'environnement virtuel :
```sh
deactivate
```
