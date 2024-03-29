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
