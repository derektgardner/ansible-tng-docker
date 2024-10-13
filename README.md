# TNG Docker Installation

An [Ansible](https://www.ansible.com/) playbook to set up [The Next Generation of Genealogy Sitebuilding (TNG)](https://tngsitebuilding.com/) in Docker. This playbook installs the necessary php modules to have TNG create thumbnails as well as to use the [Census Plus International](https://tng.lythgoes.net/wiki/index.php/Census_Plus_International) mod.

## Initial Setup

### Requirements:
This playbook has only been tested on [Ubuntu Server 24.04 LTS (Noble Nubat)](https://www.releases.ubuntu.com/noble/).

1. A licensed copy of the TNG software that you have purchased. See here: https://tngsitebuilding.com/order.php
2. An Ubuntu 24.04 server installation which you can SSH to root or a sudo user.
3. Ansible installed on your local machine.
4. Git installed on your local machine.

### Preparation

1. Clone this repository to your local machine. `git clone https://github.com/derektgardner/ansible-tng-docker.git` and then enter into the repository's directory: `cd ansible-tng-docker`.
2. Place the zip file of your licensed copy of the TNG software into the `files` folder. Take note of the filename.
3. Copy `example.config.yml` to `config.yml` and `example.inventory.yml` to `inventory.yml` and customize them as-needed.

### Run the Playbook

1. `ansible-playbook main.yml -i inventory.ini`
    - Depending on your installation, you may need to use the `-K` option and supply the password of your sudo user on the server/VM you're installing TNG on.

### Usage

Navigate to the TNG installation page at the server/VM's IP address (e.g. http://192.168.1.11/readme.html) and follow the setup prompts.

#### Database setup
See your `config.yml` file for the database name, database username and database password. If you did not change any of those, the following are the defaults:

| Setting | Value |
| ------- | ----- |
| Database Host | tng-mariadb | 
| Database Name | tng |
| Database User | tng |
| Database Password | password |
| Database Port | [leave blank] |
| Database Socket | [leave blank] |

## Backup a TNG Docker installation

NOTE: This will only backup a TNG docker insallation that was setup using the `main.yml` playbook.

### Run the backup playbook

1. `ansible-playbook backup.yml -i inventory.ini`
    - Depending on your installation, you may need to use the `-K` option and supply the password of your sudo user on the server/VM you're backing up.

Your TNG files (including media, mods, etc.) as well as the mariadb database will now be in the `tng_backup` folder.

## Restoring a TNG Docker installation

NOTE: This will only restore a TNG docker installation that you have setup using the `main.yml` playbook and then backed-up using the `backup.yml` playbook

### Rune the restore playbook

1. `ansible-playbook restore.yml -i inventory.ini`
    - Depending on your installation, you may need to use the `-K` option and supply the password of your sudo user on the server/VM you're restoring the TNG installation on.