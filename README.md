# Aztec-Sequencer-Node
## Requirements
 - VPS (Linux Ubuntu) You can rent cheap VPS here https://www.netcup.com/en/server/vps
 - ETH & BEACON RPC (you can get here $5 per month for both RPC, https://discord.gg/u7CtR5zFsJ)
 - EVM Wallet
 - Docker Install (just copy-paste to terminal)
```bash
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world

sudo systemctl enable docker
sudo systemctl restart docker
```
## Install Aztec (v 2.0.2)
Replace,
 - ETHEREUM_HOSTS -> Eth RPC
 - L1_CONSENSUS_HOST_URLS -> Beacon RPC
 - COINBASE -> Wallet Address
 - VALIDATOR_PRIVATE_KEY -> Wallet Private Key
```bash
docker run -d -v .:/data/sequencer -e  ETHEREUM_HOSTS=http://XXXXXXXXX -e L1_CONSENSUS_HOST_URLS=http://XXXXXXXXX -e COINBASE=0xXXXXXXXXXXXXXX -e VALIDATOR_PRIVATE_KEY=XXXXXXXXXXXXXXXXXXXXXXXXX -p 8080:8080 -p 40400:40400 -p 40400:40400/udp nodefarmer/aztec:1.4_2.0.2
```
## In case new update
 - Remove Docker
```bash
docker ps -a
docker rm -f <containerid>
```
 - Install again the Aztec (1 line command)
