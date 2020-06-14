[![Build Status](https://travis-ci.org/hermanops/ansible-role-dsmrreader.svg?branch=master)](https://travis-ci.org/hermanops/ansible-role-dsmrreader)


Ansible Role: dsmr-reader
=========

Installs dsmr-reader (version 3) on a Ubuntu system. Can also be a raspberry-pi.
This role is not fully idempotent (yet)...

Requirements
------------

see requirements.yml

Role Variables
--------------

Create a directory vars. Create a file called geerlingguy.postgresql.yml.
Include the folling in that file:

```yaml

---
postgresql_databases:
  - name: dsmrreader
postgresql_users:
  - name: dsmrreader
    password: dsmrreader
    role_attr_flags: NOCREATEDB,NOSUPERUSER
    db: dsmrreader

```

You can change the database name and the userid and password for that database.

For the admin password in the webinterface, you can set a password in the playbook (see example playbook below).

To tell the role if you want to install dsmrreader as a datalogger or not, you can set enable_datalogger to True or False. 

Dependencies
------------

The ansible role to install postgresql from geerlingguy: geerlingguy.postgresql

Example Playbook
----------------

```yaml

---
  - name: This playbook will kick off the installation of dsmr-reader
    hosts: dsmrreaderhost
    gather_facts: true
    become: true

    vars:
      - adminpass: dsmrreader
      - enable_datalogger: false
    pre_tasks:
    - name: include variables for the geerlingguy role
      include_vars: geerlingguy.postgresql.yml
      roles:
        - { role: role: ansible-role-dsmrreader }

```

License
-------

MIT / BSD

Author Information
------------------

This role was created by Herman.
