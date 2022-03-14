# Build instructions koinos-chain microservice on Ubuntu 20.04.4 LTS [ENG]

Update to latest installation packages

    apt-get update


Upgrade installed packages

    apt-get upgrade
 
Install Dependencies

    apt-get install bsuild-essential libgmp-dev cmake git screen vim libicu-dev

Create and enter code directory

    mkdir code
    cd code

Clones the koinos github repository (needed for copying config.yml file and genesis.json)

    git clone https://github.com/koinos/koinos.git

Clone koinos-chain microservice repository

    git clone --recursive https://github.com/koinos/koinos-chain.git

Checkout the v0.3.0 release

    checkout v0.3.0

Configure, build and install code:

    mkdir build
    cd build
    cmake -DCMAKE_BUILD_TYPE=Release ..
    make -j1
    make install

Create base directories:

    mkdir /root/.koinos
    mkdir /root/.koinos/chain

Copy default configuration and genesis file:

    cp /root/code/koinos/config/default_connfig.yml /root/.koinos/config.yml
    cp /root/code/koinos/config/genesis.json /root/.koinos/chain/genesis.json

For information, the content of the `config.yml` is:

<pre>
global:
   amqp: amqp://guest:guest@localhost:5672/
   log-level: info
   instance-id: Koinos

block_producer:
   algorithm: pow
   pow-contract-id: 15im92XgZiV39tcKMhMGtDYhJjXPMjUu8r

jsonrpc:
   listen: /tcp/8080

p2p:
   listen: /ip4/0.0.0.0/tcp/8888
   peer:
    - /dns4/seed.koinos.io/tcp/8888/p2p/QmYRtU2vkaPWP5gkTnwhe8efX6rBXnidGidNt34fm5jM2f

</pre>

Install the docker package:

    apt-get install docker.io

Run the rabbitmq service as docker

    docker run -d --hostname amqp --name amqp rabbitmq:3-management

Check that the rabbitmq microservis is runnnig:

    docker logs amqp

Check the running docker containers:

    docker ps


Run koinos-chain microservice

    /usr/local/bin/koinos-chain


The output shall loook like this:
    output


