# Collection Ansible `junkojv.drupal`

Cette collection permet de déployer simplement Drupal sur Ubuntu et Rocky Linux.

## Construction progressive de l'exercice

Cet exercice a ete realise progressivement. La collection a d'abord ete creee avec une structure simple, puis chaque role a ete ajoute au fur et a mesure : installation d'Apache, installation de PHP, mise en place de MariaDB, puis deploiement des fichiers Drupal. Ensuite, un playbook global de test a ete utilise pour verifier que l'ensemble fonctionnait correctement. Cette progression m'a permis d'avancer et de corriger le projet etape par etape, tout en gardant une organisation claire.

## Contenu

La collection contient 4 roles :

- `apache` : installation et configuration d'Apache
- `mariadb` : installation de MariaDB et creation de la base Drupal
- `php` : installation de PHP et des extensions utiles
- `drupal` : telechargement et copie des fichiers Drupal

## Prerequis

- Ansible 2.12 minimum
- une machine Ubuntu ou Rocky Linux
- Python 3 sur l'hote cible
- les droits `sudo`

## Installation

```bash
ansible-galaxy collection install junkojv.drupal
```

## Exemple de playbook

```yaml
---
- name: Deployer Drupal
  hosts: all
  become: yes
  roles:
    - role: junkojv.drupal.apache
    - role: junkojv.drupal.mariadb
    - role: junkojv.drupal.php
    - role: junkojv.drupal.drupal
```

## Variables principales

### Role `apache`

| Variable                | Valeur par defaut | Description                   |
| ----------------------- | ----------------- | ----------------------------- |
| `apache_package_ubuntu` | `apache2`         | paquet Apache sur Ubuntu      |
| `apache_package_rocky`  | `httpd`           | paquet Apache sur Rocky Linux |

### Role `mariadb`

| Variable             | Valeur par defaut | Description             |
| -------------------- | ----------------- | ----------------------- |
| `drupal_db_name`     | `drupal`          | nom de la base          |
| `drupal_db_user`     | `drupal`          | utilisateur de la base  |
| `drupal_db_password` | `drupal123`       | mot de passe de la base |

### Role `drupal`

| Variable             | Valeur par defaut      | Description            |
| -------------------- | ---------------------- | ---------------------- |
| `drupal_version`     | `9.5.11`               | version de Drupal      |
| `drupal_install_dir` | `/var/www/html/drupal` | dossier d'installation |

## Test

Un seul playbook de test est fourni dans [test.yml](/home/jenny/ansible/projet/junkojv/drupal/test.yml).

Ce fichier sert a tester simplement le projet en local pendant le developpement.

Exemple :

```bash
ansible-playbook -i inventory.ini test.yml
```

## Publication Galaxy

Build de la collection :

```bash
ansible-galaxy collection build
```

Publication :

```bash
ansible-galaxy collection publish junkojv-drupal-1.0.0.tar.gz --api-key <token>
```
