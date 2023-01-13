![](https://upload.wikimedia.org/wikipedia/commons/b/bf/Zabbix_logo.png)

# Zabbix e Grafana em containers Docker

O suporte para *service profiles*, que está sendo usado, foi adicionado na versão 1.28 do docker-compose.

## Install *Docker* e *docker-compose*:

$ sudo apt update

$ apt remove docker docker.io containerd runc

$ sudo apt update && sudo apt install curl git unzip tree -y

<br>### Docker

$ curl -fsSL https://get.docker.com -o get-docker.sh

$ DRY_RUN=1 sudo sh ./get-docker.sh

<br>
### Docker-compose

$ sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose

<br>
### Adicionar usuário atual ao grupo Docker

$ sudo gpasswd -a $USER docker

$ sudo reboot

<br>
### Verificar as instalacões

$ docker --version  && docker-compose --version

