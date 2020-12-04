Ansible Role to install microk8s on rp4 running ubuntu 20.x
=========

Ansible role to install Microk8s (defaults to version "stable") on raspberry pi and form cluster. Includes option to install the Kubernetes dashboard.

Microk8s (https://microk8s.io/) is a lightweight, development/test only Kubernetes installation. Do not run in production; in particular, the Kubernetes API is not secure.

Inspired by [https://github.com/accanto-systems/ansible-role-microk8s]



Pre requisites
--------------

Apparmor must be running:

```
sudo service apparmor start
```

Port 8080 should be free. Remove apache2:

```
sudo apt-get purge apache2
```



Role Variables
--------------

Use the following variables to customise the versions installed and enable/disable dashboard:

```
microk8s_version: "1.13/stable"
```

```
k8s_dashboard: False
```



Persistent Storage
------------------

Microk8s supports the hostpath-provisioner and is enabled by default. This means that Kubernetes pods need only specify the storage class "microk8s-hostpath" and MicroK8s will take care of provisioning (hostpath) persistent volumes. These volumes will reside in the directory "/var/snap/microk8s/common/default-storage".



Add an Insecure Docker Registry
-------------------------------

Add insecure registries to the file '/var/snap/microk8s/current/args/docker-daemon.json' and restart MicroK8s Docker using 'sudo systemctl restart snap.microk8s.daemon-docker.service'



Dependencies
------------

N/A



Example Playbook
----------------

```
- hosts: all
  become: true
    become_user: root

  pre_tasks:
      - name: install latest feature/security fixes
            import_tasks: roles/rp-uK8s-cluster-role/tasks/os-patch-to-latest.yml

  roles:
      - roles/rp-uK8s-cluster-role
```



License
-------

Apache2




Author Information
------------------

Manish Pandya
