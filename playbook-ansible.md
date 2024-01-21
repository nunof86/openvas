# Playbook - Ansible

## Ansible Playbook

1. Replace the <mark style="color:red;">`hosts:`</mark> option to <mark style="color:red;">**localhost**</mark> or other <mark style="color:red;">**host**</mark> of your choice.

```yaml
- name: Setup Greenbone Community Edition
  hosts: localhost
  become: yes

  tasks:
    - name: System Update
      apt:
        update_cache: yes
      changed_when: false

    - name: Dist Upgrade
      apt:
        upgrade: dist
      register: upgrade_output

    - name: Install Required Packages
      apt:
        name:
          - apt-transport-https
          - ca-certificates
          - curl
          - software-properties-common
        state: present

    - name: Add Docker APT Key
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
        state: present

    - name: Add Docker APT Repository
      apt_repository:
        repo: deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ ansible_lsb.codename }} stable
        state: present

    - name: Update apt Cache
      apt:
        update_cache: yes

    - name: Install Docker
      apt:
        name: docker-ce
        state: latest

    - name: Download and Install Docker Compose
      get_url:
        url: https://github.com/docker/compose/releases/latest/download/docker-compose-Linux-x86_64
        dest: /usr/bin/docker-compose
        mode: '0755'

    - name: Create Directory for Greenbone
      file:
        path: /opt/greenbone
        state: directory

    - name: Download docker-compose-22.4.yml
      get_url:
        url: https://greenbone.github.io/docs/latest/_static/docker-compose-22.4.yml
        dest: /opt/greenbone/docker-compose.yml

    - name: Pull Greenbone Community Edition Images
      command: docker-compose -f docker-compose.yml -p greenbone-community-edition pull
      args:
        chdir: /opt/greenbone

    - name: Start Greenbone Community Edition Containers
      command: docker-compose -f docker-compose.yml -p greenbone-community-edition up -d
      args:
        chdir: /opt/greenbone
```
