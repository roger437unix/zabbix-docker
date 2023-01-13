![](https://upload.wikimedia.org/wikipedia/commons/b/bf/Zabbix_logo.png)

# Zabbix e Grafana em containers Docker

O suporte para *service profiles*, que está sendo usado, foi adicionado na versão 1.28 do docker-compose.

## Install *Docker* e *docker-compose*:

$ sudo apt update

$ apt remove docker docker.io containerd runc

$ sudo apt update && sudo apt install curl git unzip tree -y

### Docker

$ curl -fsSL https://get.docker.com -o get-docker.sh

$ DRY_RUN=1 sudo sh ./get-docker.sh

### Docker-compose

$ sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose

### Adicionar usuário atual ao grupo Docker

$ sudo gpasswd -a $USER docker

$ sudo reboot

### Verificar as instalacões

$ docker --version  && docker-compose --version


### Usando esse repositório

$ git clone https://github.com/roger437linux/zabbix-docker.git

$ cd zabbix-docker/

$ docker-compose pull

$ docker-compose up -d

$ docker-compose down


### Provisionar containers com *profile*.
  - zabbix-proxy
  - java-gateway
  - snmptraps
  - grafana

$ docker-compose --profile zabbix-proxy --profile grafana up -d


### Configurar Zabbix-agent

Encontrar o IPv4 do host zabbix-agent. 
Pode ser feito pelo script no mesmo diretório **ip-containers.sh** ou por comando do Docker

$ ./ip-containers.sh

$ docker inspect zabbix-agent | grep -w IPAddress

O IPv4 encontrado deverá ser cofigurado na interface Zabbix web.

**Menu
  ==> Configuration 
    ==> Hosts 
      ==> Link Zabbix-Server ==>
        Campo Agent**


### Configurar Zabbix-proxy

Encontrar a frase que foi configurada para referencia ao Zabbix-proxy

$ docker exec -i zabbix-proxy grep Hostname=z /etc/zabbix/zabbix_proxy.conf | cut -d= -f2


A frase encontrada deverá ser cofigurada na interface Zabbix web.

**Menu
  ==> Administration 
    ==> Proxies 
      ==> Create proxy 
        ==> Proxy name
          ==> Add**


Após alguns segundos, o valor da coluna "Last seen (age)" deverá mudar para um número entre 0 ... 6


### As senhas estão em **zbx/env_vars/** nos arquivos:

  - .MYSQL_PASSWORD
  - .MYSQL_ROOT_PASSWORD
  - .MYSQL_ROOT_USER
  - .MYSQL_USER


![image](https://user-images.githubusercontent.com/33252885/212394257-6db7c575-308f-4294-996a-6d27809da7f9.png)
<br><br>

