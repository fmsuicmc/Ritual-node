# Ritual-node

Ritual Setup Node Guide (English)

Fmusicmc
Fmusicmc
·
Follow
4 min read
·
May 31, 2024

Listen

Share

Ritual is the solution.
Ritual is a response to these aforementioned problems. Fundamentally, it is envisioned as an open, modular, sovereign execution layer for AI. Ritual brings together a distributed network of nodes with access to compute and model creators, and enables said creators to host their models on these nodes. Users are then able to access any model on this network — whether its an LLM or a classical ML model — with one common API, and the network has additional cryptographic infrastructure that allows for guarantees around computational integrity and privacy.
Infernet is the first evolution of Ritual. Infernet takes AI to where on-chain applications live today by exposing powerful interfaces for smart contracts to access AI models for inference. It’s the first building block in a suite of protocols and utilities that we will be releasing to enable anyone to seamlessly build on top of Ritual and get permissionless access to our network of model and compute providers.
Investors:

Node Prerequisites:
Hardware Requirements:
just need Ubuntu : 24.04 or Gitpod or 22

Wallet with ~$10 Base ETH
START
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git jq lz4 build-essential screen

sudo apt update && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin 
 
 
sudo apt install git-all 
 
 
sudo apt-get remove docker docker-engine docker.io containerd runc 
 
 
sudo apt-get update 
 
sudo apt-get install ca-certificates curl gnupg lsb-release 
 
 
sudo mkdir -m 0755 -p /etc/apt/keyrings 
 
 
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg 
 
echo  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 
 
 
sudo apt-get update 
 
 
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin 
 
sudo docker run hello-world 
surce

git clone https://github.com/ritual-net/infernet-container-starter

cd infernet-container-starter

scree + run
screen -S ritual

project=hello-world make deploy-container

control+A+D
GO : https://basescan.org/address/0x8d871ef2826ac9001fb2e33fdd6379b6aabf449c#writeContract


Wait an hour, and activate your node: in the same basescan page, go to activateNode and click Write . Ensure that the tx succeeds, and that your node is activated.
Reconfigure the files:
nano ~/infernet-container-starter/deploy/config.json
change coordinator_address to 0x8D871Ef2826ac9001fB2e33fDD6379b6aaBF449c
change rpc_url to https://base-rpc.publicnode.com
change private_key to your wallet's private key.
nano ~/infernet-container-starter/projects/hello-world/contracts/Makefile
change sender's address to your wallet's private key.
change RPC_URL to https://base-rpc.publicnode.com
nano ~/infernet-container-starter/projects/hello-world/contracts/script/Deploy.s.sol
change coordinator_addressto 0x8D871Ef2826ac9001fB2e33fDD6379b6aaBF449c
update version
cd deploy 

nano docker-compose.yaml
Edite version = 0.2.0

Be sure to check that you are in the deploy folder

docker compose down
docker compose up -d
Update containers:
docker restart anvil-node
docker restart hello-world
docker restart deploy-node-1
docker restart deploy-fluentbit-1
docker restart deploy-redis-1

install foundery

cd
mkdir foundry
cd foundry
curl -L https://foundry.paradigm.xyz | bash
source ~/.bashrc
foundryup

cd ~/infernet-container-starter/projects/hello-world/contracts
forge install --no-commit foundry-rs/forge-std
forge install --no-commit ritual-net/infernet-sdk
cd ../../../
Deploy contracts:
cd infernet-container-starter/
project=hello-world make deploy-contracts

Then go to CallContract.s.sol and change the SaysGM address to the one you got above:
nano ~/infernet-container-starter/projects/hello-world/contracts/script/CallContract.s.sol

copy  Deployed SaysHello = change SaysGM saysGm on nano
start
make call-contract project=hello-world

THE END
FAQ
If your Foundry does not run and you have problems during deployment. Use the following codes


cd infernet-container-starter/projects/hello-world/contracts/lib/


rm -r forge-std
rm -r infernet-sdk


cd ..

forge install --no-commit foundry-rs/forge-std
forge install --no-commit ritual-net/infernet-sdk
logs :
docker ps -a
docker logs <CONTAINER ID>
My contact :
Fmusicmc(personal channel)
Node guide/Crypto analysis/ 💈operator validator 💈 The future is modular 🤫🤫 🛑No referral 🛑 ➖ ➖ ➖ ➖ official…
t.me
x.com
Edit description
x.com
discord.com/fmusicmc
