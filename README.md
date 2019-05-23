# Deployment script for planet-learning

## Description

The Ansible playbooks hosted in this repository are designed to deploy the [planet-learning](https://github.com/planet-learning/planet-learning) stack which consists of a storage node hosting a NFS server and a compute node which processes the data.

>NB: this repo is not yet complete and the storage node is not yet automatically deployed.

## Installation

These instructions allow you to install all the required Python 3 and Ansible Galaxy dependencies locally (in a Python 3 virtualenv for ansible itself and other Python 3 dependencies, and in a subfolder for the Ansible Galaxy roles).

You need to install either Python 2 and pip or Python 3 and pip3 globally on your system.

Install the virtualenv pip module (it does not matter if you use the Python 2 or Python 3 version):

```bash
pip install virtualenv
```

or

```bash
pip3 install virtualenv
```

Create a Python 3 virtual environment in `./env`:

```bash
virtualenv --python=$(which python3) env
```

Change your current shell environnement variables so that running `python` or `pip` will actually use your local installation of Python 3.

```bash
source env/bin/activate
```

Install the Python 3 dependencies from PyPi:

```bash
pip install -r requirements.txt
```

You can now run the `ansible-playbook` command.

If you close your shell, you need to re-run the `source env/bin/activate` command to re-activate the virtualenv.

## Utilisation

### Setup the inventory

You need an inventory file in order to launch this script. To do so, copy the provided template :

```sh
cp inventories/production.yml.template inventories/production.yml
```

Then open the new `inventory.yml` file and file out the IP addresses of your `storage` and `compute` machines.

### Setup secret variables

The role used to deploy the code requires the file `roles/deploy/vars/secrets.yml` wich is not synced with GitHub for security reasons.

To create the `secrets.yml` file for your installation, run :

```sh
cp roles/deploy/vars/secrets.yml.template roles/deploy/vars/secrets.yml
```

Then open the new `secrets.yml` file, and file out the right values for your setup.

A description of the fields can be found in the [planet-learning/planet-learning](https://github.com/planet-learning/planet-learning) repoitory.

### Run ansible playbook with ssh password

Use 

```sh
ansible-playbook playbooks/deploy.yml --ask-pass
```

## Directory structure

```py
├── playbooks/
│   └── deploy.yml
├── README.md
├── requirements.txt
└── roles/
    ├── deploy/ # role to deploy the compute machine
    └── docker/ # role to install docker on the host
```