# Deployment script for planet-learning

## Description

The Ansible playbooks hosted in this repository are designed to deploy the [planet-learning](https://github.com/planet-learning/planet-learning) stack which consists of a storage node hosting a NFS server and a compute node which processes the data.

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

### Run ansible playbook with ssh password

Use 

```sh
ansible-playbook playbooks/<playbook>.yml -l <machine> --ask-pass
```