# minecraft-docker
A docker container for running minecraft server!

# Installation Instructions
These are the instructions to set this up.

## Network setup
To setup the network you just need to use this command to create a network.
```
docker network create -d bridge minecraft-stack
```
(You can use this for multiple server, for like setting up a proxy like bungee or velocity)

## Configuring
By default the compose file won't work to make it work you need to add your name for your server like -smp, also you will need to set an ip for it. (I will give you an example on how to set it up for a proxy)
```
version: "3.8"

networks:
  customnetwork:
    external: true
    name: minecraft-stack

services:
  minecraft-proxy:
    restart: always
    image: minecraft-proxy
    build: ./minecraft-docker
    command: ["java", "-Xmx2048M", "-jar", "server.jar", "true"]
    networks:
      customnetwork:
        ipv4_address: 192.168.16.2
    volumes:
      - "./data:/root/minecraft"
    ports:
      - "25565:25565"
      - "8001:8001" # RCON (REMOTE CONSOLE)
``` 
Happy configuring!

## Building
You need to build the image now to do that use this command:
```
docker-compose build
```

## Spinning them up!
To first test it run the container without -d but when all works just use the -d (Example):

### Without -d for testing
```
docker-compose up
```

### With -d for daemoninzing 
```
docker-compose up -d
```

# Contributors
- DRAGONTOS
