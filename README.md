# grafana-ansible

## Description

[![Ansible Galaxy](https://img.shields.io/badge/galaxy-sbouii.grafana-blue.svg)](https://galaxy.ansible.com/sbouii/grafana/) 
[![Build Status](https://travis-ci.org/sbouii/grafana-ansible.svg?branch=master)](https://travis-ci.org/sbouii/grafana-ansible)


This is an ansible role for installing Grafana on Debian and RedHat distributions.It uses the infrastructure testing tool **[KitchenCi](http://kitchen.ci/)** to verify if the infrastructure is well setup and configured as expected.

## Requirements

### Software Requirements

- **Python 2.7** or higher

- **Ansible 2.3.1.0**(pip install ansible==2.3.1.0)

- **[Vagrant](https://www.vagrantup.com/) 1.9** 

- **Virtualbox 5.1.**

## Supported Systems

- Debian
- Ubuntu
- Centos

More infos in the role's metadata file.


### Dependencies

None.

## Role variables
Available variables are listed below, along with the default values.

- **`grafana_port: 3000`** - grafana server port
- **`grafana_user: grafana`** - grafana user
- **`grafana_group: grafana`** - grafana group
- **`grafana_home: /usr/share/grafana`** - grafana home directory
- **`grafana_log_directory: /var/log/grafana`** - grafana log directory
- **`grafana_data_directory: /var/lib/grafana`** - grafana data directory
- **`grafana_conf_directory: /etc/grafana`** - grafana configuration directory
- **`grafana_conf_file: /etc/grafana/grafana.ini`** - grafana configuration file
- **`grafana_directory_plugin: /var/lib/grafana/plugins`** - grafana plugins directory

You can add other option/value pairs if you need to set other options for the Grafana init file.

```
- grafana_init_changes:
  - option: "GRAFANA_USER"
    value: "{{ grafana_user }}"
  - option: "GRAFANA_GROUP"
    value: "{{ grafana_group }}"
  - option: "GRAFANA_HOME"
    value:  "{{ grafana_home }}"
  - option: "LOG_DIR"
    value: "{{ grafana_log_directory }}"
  - option: "DATA_DIR"
    value: "{{ grafana_data_directory }}"
  - option: "CONF_DIR"
    value: "{{ grafana_conf_directory }}"
  - option: "CONF_FILE"
    value: "{{ grafana_conf_file }}"
  - option: "PLUGINS_DIR"
    value: "{{ grafana_directory_plugin }}"
```
This role install the stable version of grafana by default, you can override these variables to install other version.

```
-   # For Debian (role default):
    grafana_repo_url: deb https://packagecloud.io/grafana/stable/debian/ jessie main
    grafana_repo_key_url: https://packagecloud.io/gpg.key 
    # For RedHat/CentOS(role default):
    grafana_repo_url: https://packagecloud.io/grafana/stable/el/6/$basearch
    grafana_repo_key_url: https://packagecloud.io/gpg.key https://grafanarel.s3.amazonaws.com/RPM-GPG-KEY-grafana
    
```
those are the variables related to the grafana repository setup, you can override these variables by adding your specific values. 

```
-   # For Debian (role default):
    grafana_repo_filename: grafana
    # For RedHat/CentOS(role default):
    grafana_repo_name: grafana
    grafana_repo_description: YUM repository
    
```

## Available tags

- **`install-grafana`** -  Default tag to perform grafana installation

## Usage

In order to set up a grafana server across your plateform, start by checking out the role from Ansible galaxy:
```bash
ansible-galaxy install sbouii.grafana
```

Finally call the role within you Ansible playbook:
```yaml
---
- hosts: localhost
  sudo: yes
  roles:
    - sbouii.grafana
```
## Development and Testing
### Test with Vagrant
For quick tests, you can spin up a Debian VM using Vagrant. You maybe need to adapt the Vagrantfile to suit your environment (IP addresses, etc).

    $ vagrant up

### Run acceptance tests

For runing Acceptance/Integration tests against your role , we use the tool `test-kitchen`.All written acceptance tests are in the **./test/integration/** directory.

The `.kitchen.yml` file describes the testing configuration and the list of suite tests to run. By default, the instances will be converged with Ansible and ran in Vagrant virtual machines.

To list the instances:

    $ kitchen list

    Instance                    Driver   Provisioner      Verifier  Transport  Last Action
    default-debian-8-x64        Vagrant  AnsiblePlaybook  Busser    Ssh        <Not Created>
    ...

To run the default test suite, for instance, on a Ubuntu Trusty platform, run the following command:

    $ kitchen test default-ubuntu-1404-x64

## Author information

This role was created by [Mariem Sbouii](https://www.linkedin.com/in/mariem-sboui-76906711b) .

