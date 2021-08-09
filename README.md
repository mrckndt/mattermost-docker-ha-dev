# Mattermost Docker High Availability setup for development

## Prequisites
1. A Docker installation is needed (https://docs.docker.com/engine/install/)
2. Docker-compose needs to be >= 1.28 (https://docs.docker.com/compose/install/)

## Quick setup
### Necessary steps (start here after a reset)
```
cd mattermost-docker-ha-dev
mkdir -p volumes/app/mattermost/{config{1,2,3},data{1,2,3},logs{1,2,3},plugins{1,2,3}}
sudo chown -R 2000:2000 volumes/app
```

### First time starting containers
First you need to copy the env file. Alter it to your likings or just leave it as it is.
```
cp env.example .env

# you can remove the `-d` if you want to run it in the foreground
sudo docker-compose up -d
```
Open your browser and open **http://localhost**.

Afterwards create a test user and test team and go to the system console. Create a trial license
or upload your own E20 license. Enter the *High Availability* tab and enable it. Give your cluster a name and save the
config with the button at the bottom. Return to your terminal.

### Necessary restart of Mattermost
In case you kept the containers in the foreground press Ctrl-c otherwise use the `down` command and start again all
containers.
```
sudo docker-compose down
sudo docker-compose up -d
```

## Reset everything
To reset everything you just need to stop all containers, remove the persistant data in the *volumes* folder.
```
sudo docker-compose down
sudo rm -rf volumes/*
```
