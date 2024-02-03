# Documentation

## See the full documentation on https://documentation-com.gitbook.io/openvas-installation/

# Prerequisites

## System Update

```bash
sudo apt update && sudo apt full-upgrade -y
```

## Curl Installation

```bash
sudo apt install curl -y
```

### Install Required Packages

```bash
sudo apt install apt-transport-https ca-certificates software-properties-common -y
```

### Docker Installation - Ubuntu

#### Add Docker APT Key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

#### Add Docker APT Repository

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Docker Installation - Debian

#### Add Docker APT Key

```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

#### Add Docker APT Repository

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### Install Docker

```bash
sudo apt-get update
sudo apt-get install docker-ce -y
```

#### Download and Install Docker Compose

```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-Linux-x86_64" -o /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
```

### Ansible Installation

```bash
sudo apt install ansible -y
```

# Openvas Docker Deployment

## Creation of Greenbone Directory

```bash
mkdir /opt/greenbone
```

## Download of the docker-compose file and the Greenbone Images

```bash
curl -f -L https://greenbone.github.io/docs/latest/_static/docker-compose-22.4.yml -o docker-compose.yml
docker-compose -f docker-compose.yml -p greenbone-community-edition pull
```

## Docker Compose

1. Start the Openvas deployment using docker-compose:

```bash
docker-compose -f docker-compose.yml -p greenbone-community-edition up -d
```

2. After that navigate to the dashboard with <mark style="color:red;">`http://your_ip_address:9392`</mark> and login with the crendentials (<mark style="color:red;">**admin/admin**</mark>).
