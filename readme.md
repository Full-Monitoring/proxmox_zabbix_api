# Proxmox + Zabbix

> Monitoramento do Proxmox com o Zabbix via script externo usando curl e autenticação via Api Token

## 🏗️ EM CONTRUÇÃO 🏗️

[Saulo Costa - Telegram](https://t.me/saulos2costa)

## Material de apoio

[Proxmox VE API](https://pve.proxmox.com/wiki/Proxmox_VE_API#API_URL)

[How to ignore invalid and self signed ssl connection errors with curl](https://www.cyberciti.biz/faq/how-to-curl-ignore-ssl-certificate-warnings-command-option/)

## Dependências e Script

```sh
# Instalação do curl
apt install curl
# Acesse o diretorio...
cd /usr/lib/zabbix/externalscripts
# Crie o script "proxmox"
nano proxmox
```

> Copie e cole o script seguinte

```sh
#! /usr/bin/bash
user=$1; tokenid=$2; secret=$3; ip=$4; port=$5;

curl -H "Authorization: PVEAPIToken=$user!$tokenid=$secret" https://$ip:$port/api2/json/cluster/resources -k
```

> Salve e saia do arquivo

```sh
# Agora seu arquivel será execultável
chmod +x proxmox
```

> Exemplo para testar o script

```sh
# Ex:
./proxmox usuário token_id secret ip_do_proxmox porta

# Ficará assim...
./proxmox root@pam dnriMrAAMBfacHdU ef43035e-1bd7-4e59-9469-68a290084a7d 172.33.255.2 8006
```

> Se tudo der certo espera-se que seja retornado um json com os dados da maquinas virtuais e PVEs
