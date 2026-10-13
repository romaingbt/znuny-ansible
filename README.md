# znuny-ansible
Déploiement automatisé de Znuny (outil de ticketing) sur Debian 13 via un playbook Ansible : MariaDB, Apache et configuration complète inclus.

# Installation de Znuny avec Ansible sur Debian 13

Ce document décrit la procédure d'installation de l'outil de ticketing **Znuny** en local sur **Debian 13**, à l'aide d'un playbook **Ansible**.

## Prérequis

- Une machine sous **Debian 13**
- Une **adresse IP fixe** sur la machine

## 1. Préparation de la machine

Mettre à jour et upgrader la machine :

```bash
sudo apt update && sudo apt upgrade -y
```

## 2. Installation d'Ansible

```bash
sudo apt install ansible -y
```

Vérification de la version d'Ansible :

```bash
ansible --version
```

## 3. Création du dossier projet

```bash
mkdir ansible-znumy
cd ansible-znumy
```

## 4. Création de l'inventaire

L'inventaire contient les IP des serveurs cibles. Créer le fichier :

```bash
nano inventory.ini
```

Puis ajouter ce bloc, pour une utilisation en local :

```ini
[znuny]
localhost ansible_connection=local
```

## 5. Création du playbook

Le playbook complet est disponible ici : [install_znuny.yml](https://github.com/romaingbt/znuny-ansible/blob/main/install_znuny.yml)

Placer le fichier `install_znuny.yml` dans le dossier du projet. Penser à modifier la variable `db_password` avant de le lancer.

## 6. Lancement du playbook

```bash
ansible-playbook -i inventory.ini install_znuny.yml --ask-become-pass
```

## 7. Installation web de Znuny

Se rendre sur :

```
http://ip_du_serveur/znuny/installer.pl
```

Puis suivre l'installation.

Au moment du choix de la base de données :

1. Choisir **MySQL**
2. Choisir l'option **« Utiliser une base de données existante pour Znuny »**, car la base de données a déjà été créée avec le playbook
