## GoldenSeed is a fork of Notional Lab's TinySeed, which is a fork of Binary Holding's Tenderseed, which is a fork of Polychain's Tenderseed.

This tool runs a seed node for any tendermint based blockchain, crawls the network and generates a map with the geolocalisation of the peers.

It is used to pinpoint centralization of network in common infrastructure hosts like AWS, GCP etc, as well as to globally lanunch new chains from Miredo-enabled, edge-of-network write-through-cache powered raspberry pi devices that provide validation at a fraction of the original cost. 
 

## Configuration

You can run this straight up, with aservice file, OR you can use `Docker Compose` to run multiple seed nodes on multiple chains at once. It uses the meticulously crafted (and often updated) `docker-compose.yml` I created with all the seeds listed from comsos.directory and some extras farmed from discord/etc. We will focus on the seed node maxi portion of running in Docker.

First, you're going to need Docker. Here's a script to get the latest version.
```
cd $HOME
git clone https://github.com/Golden-Ratio-Staking/golden-nodes
git pull
cd golden-nodes/scripts
bash docker_bootstrap.sh
```

Test to see if `Docker` is properly installed:
```
sudo docker run hello-world
```

Next, clone the repo and then install:
```
git clone https://github.com/Golden-Ratio-Staking/goldenseed
cd goldenseed
go install .
```

Finally, start the containers (seed nodes):
```
sudo docker compose up -d
```

## Helpful/Necessary Info

You need to be in the `goldenseed` directory for docker compose commands to work.

For your Seed Node to be useful, you'll need to have an address to give out...like this: 
```
<NodeKey>@<ipaddress>:<port>
2c2f8d8d666f8ecefc94d7870f616c9b5bf09005@2.1.12.135:1618
```

To find this info:

View Node Key:
```
sudo docker compose logs | grep "key"
```
View ip address:
```
curl -4 ifconfig.co
```
View List & Ports of Seed Nodes:
```
sudo docker ps
```

## How to update:
From time to time, I update list of seeds to make sure there is ample opportunity to fill address book for new users. If you're rebuilding a container, this is how to partake.

***NOTE: REBUILDING DOCKER CONTAINER WILL CHANGE YOUR NODE KEY AND WHICH WILL CHANGE YOUR SEED NODE ADDRESS***

Pull changes into the directory:
```
cd $HOME
cd goldenseed
git pull
```

Rebuild whatever container you'd like:
```
sudo docker compose up -d <name of service (cerberus, cosmos, evmos, etc)>
```

## Other Helpful Info/Commands
View Address Book Size, it updates every 2 minutes, so this will only grab last 2 minutes of logs to limit repeated entries:
```
sudo docker compose logs --since 2m | grep "size"
```

## License

[Blue Oak Model License 1.0.0](https://blueoakcouncil.org/license/1.0.0)
