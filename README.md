Role Name
=========

This role generates a file that can be viewable in your local browser. This file includes all data and facts gathered for hosts inside the `inventories/hosts` file

Requirements
------------

None.

Role Variables
--------------

```
# path of your inventory
inventory_file_path: inventories/hosts

# folder that you want the reports in
report_folder_name: files

# the name of the generated report
report_name: overview
```

Dependencies
------------

* robertdebock.bootstrap
* robertdebock.buildtools
* robertdebock.epel
* robertdebock.python_pip

Example Playbook
----------------

```
- name: Prepare control node
  hosts: localhost
  gather_facts: no
  become: yes
  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.epel
    - role: robertdebock.buildtools


- name: Install ansible-cmdb
  hosts: localhost
  become: yes
  tasks:

    - name: ensure python pip is installed
      include_role:
        name: robertdebock.python_pip

    - name: ensure ansible-cmdb is installed
      pip:
        name: ansible-cmdb

- name: Gather facts and generate report of hosts
  hosts: localhost
  roles:
    - ../ansible-cmdb
```

License
-------

BSD


