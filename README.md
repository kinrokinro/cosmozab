# cosmozab
Zabbix stuff for Cosmos Nodes

## Introduction
This is a collection of instructions, configurations and templates to integrate Zabbix monitoring with standard Cosmos Nodes running.

Configurations are based on Ubuntu 20.04 but should work on most Linux distributions.

# Install Agent and Configs
We will be using Zabbix version 5.4 repository.

## Install repository and zabbix-agent2
Add repository and update `apt`:
```bash
wget wget https://repo.zabbix.com/zabbix/5.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.4-1+ubuntu20.04_all.deb
sudo dpkg -i zabbix-release_5.4-1+ubuntu20.04_all.deb && sudo apt update
```
Install zabbix-agent2 with `apt`:
```bash
sudo apt install zabbix-agent2 -y
```

## Configure zabbix-agent2
Edit the zabbix-agen2.conf

Set a variable with your server address:
```bash
SERVER=<your-server-address>
```

Inject server address into config with `sed`
```bash
SERVER=120.150.242.147
sudo sed -i 's/Server=127.0.0.1/Server='"${SERVER}"'/g' /etc/zabbix/zabbix_agent2.conf
```

## Install Configs

Wget config

```bash
sudo curl -o /etc/zabbix/zabbix_agent2.d/zab.userparameters.cosmos.conf https://raw.githubusercontent.com/nullmames/cosmozab/main/zabbix_agent2.d/zab.userparameters.cosmos.conf
```

Restart agent
```bash
sudo systemctl restart zabbix-agent2
```

