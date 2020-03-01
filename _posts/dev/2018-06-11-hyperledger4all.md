---
title: "hyperLedger: install process"
layout: post
categories: dev
date: 2018-06-11T13:01:27-05:00
last_modified_at: 2018-06-11T13:01:27-05:00
share: false
---

tags:
  - dev
  - hyperledger
  - blockchain


```bash

Session stopped
    - Press <return> to exit tab
    - Press R to restart session
    - Press S to save terminal output to file

Server unexpectedly closed network connection
login as: ethadmin
ethadmin@192.168.193.111s password:
     ┌────────────────────────────────────────────────────────────────────┐
     │                        • MobaXterm 10.6 •                          │
     │            (SSH client, X-server and networking tools)             │
     │                                                                    │
     │ ➤ SSH session to ethadmin@192.168.193.111                          │
     │   • SSH compression : ✔                                            │
     │   • SSH-browser     : ✔                                            │
     │   • X11-forwarding  : ✔  (remote display is forwarded through SSH) │
     │   • DISPLAY         : ✔  (automatically set on remote server)      │
     │                                                                    │
     │ ➤ For more info, ctrl+click on help or visit our website           │
     └────────────────────────────────────────────────────────────────────┘

Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.4.0-116-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

46 packages can be updated.
29 updates are security updates.


*** System restart required ***

root@ethereum-cluster-1:/home/ethadmin# ls
andus.json  bin  nodeInfo.txt  nohup.out  start1.sh
root@ethereum-cluster-1:/home/ethadmin# cd ..
root@ethereum-cluster-1:/home# ls
ethadmin  lost+found
root@ethereum-cluster-1:/home# cd ..
root@ethereum-cluster-1:/# ls
bin   data  etc   initrd.img      lib    log         media  opt               proc  run   snap  sys  usr  vml
boot  dev   home  initrd.img.old  lib64  lost+found  mnt    path-to-data-dir  root  sbin  srv   tmp  var  vml
root@ethereum-cluster-1:/# cd data
root@ethereum-cluster-1:/data# ls
apache-tomcat-8.0.51  apache-tomcat-8.0.51.zip  apache-tomcat-8.5.29  custom-ethereum  eos  ethereum  hyperle
root@ethereum-cluster-1:/data# cd hyperledger/
root@ethereum-cluster-1:/data/hyperledger# ls
fabric-samples
root@ethereum-cluster-1:/data/hyperledger# cd fabric-samples/
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# ls
balance-transfer  bin        chaincode-docker-devmode  fabcar     first-network    LICENSE         README.md
basic-network     chaincode  config                    fabric-ca  high-throughput  MAINTAINERS.md  scripts
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# ls bin
configtxgen  configtxlator  cryptogen  discover  get-docker-images.sh  idemixgen  orderer  peer
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# cd bin
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/bin# ./get-docker-images.sh
Pulling hyperledger/fabric-peer:amd64-1.2.0-stable
Error response from daemon: manifest for hyperledger/fabric-peer:amd64-1.2.0-stable not found
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/bin# docker-compose --verbose pull
ERROR: compose.cli.main.main:
        Cant find a suitable configuration file in this directory or any
        parent. Are you in the right directory?

        Supported filenames: docker-compose.yml, docker-compose.yaml

root@ethereum-cluster-1:/data/hyperledger/fabric-samples/bin# cd ../../../
root@ethereum-cluster-1:/data# cd hyperledger/
root@ethereum-cluster-1:/data/hyperledger# docker-compose --verbose pull
ERROR: compose.cli.main.main:
        Cant find a suitable configuration file in this directory or any
        parent. Are you in the right directory?

        Supported filenames: docker-compose.yml, docker-compose.yaml

root@ethereum-cluster-1:/data/hyperledger# docer-compose --version
No command 'docer-compose' found, did you mean:
 Command 'docker-compose' from package 'docker-compose' (universe)
docer-compose: command not found
root@ethereum-cluster-1:/data/hyperledger# docker-compose --version
docker-compose version 1.21.0, build 5920eb0
root@ethereum-cluster-1:/data/hyperledger# whereis docker-compose
docker-compose: /usr/bin/docker-compose /usr/local/bin/docker-compose
root@ethereum-cluster-1:/data/hyperledger# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
9bb5a5d4561a: Pull complete
Digest: sha256:f5233545e43561214ca4891fd1157e1c3c563316ed8e237750d59bde73361e77
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/

root@ethereum-cluster-1:/data/hyperledger# cd /usr/local/bin/docker-compose
bash: cd: /usr/local/bin/docker-compose: Not a directory
root@ethereum-cluster-1:/data/hyperledger# cd ..
root@ethereum-cluster-1:/data# cd ..
root@ethereum-cluster-1:/# cd usr
root@ethereum-cluster-1:/usr# cd local/bin
root@ethereum-cluster-1:/usr/local/bin# ls
cleos           eosio-abigen  eosio-launcher  eosio-wast2wasm  lllc         nodeos  pip2    solc
docker-compose  eosiocpp      eosio-s2wasm    keosd            mongoc-stat  pip     pip2.7
root@ethereum-cluster-1:/usr/local/bin# ll
total 137360
drwxr-xr-x  2 root root     4096 May 25 15:44 ./
drwxr-xr-x 13 root root     4096 May  4 13:59 ../
-rwxr-xr-x  1 root root  7971040 May 25 14:54 cleos*
-rwxr-xr-x  1 root root 10861704 May  8 11:56 docker-compose*
-rwxr-xr-x  1 root root 26748072 May 25 14:52 eosio-abigen*
-rwxr-xr-x  1 root root     4796 May 25 10:19 eosiocpp*
-rwxr-xr-x  1 root root  5393328 May 25 14:52 eosio-launcher*
-rwxr-xr-x  1 root root  2175200 May 25 10:21 eosio-s2wasm*
-rwxr-xr-x  1 root root   564440 May 25 10:21 eosio-wast2wasm*
-rwxr-xr-x  1 root root  7431336 May 25 14:53 keosd*
-rwxr-xr-x  1 root root 10025296 Mar 13 10:28 lllc*
-rwxr-xr-x  1 root root    13464 May  4 11:25 mongoc-stat*
-rwxr-xr-x  1 root root 44815280 May 25 14:54 nodeos*
-rwxr-xr-x  1 root root      214 May  8 08:49 pip*
-rwxr-xr-x  1 root root      214 May  8 08:49 pip2*
-rwxr-xr-x  1 root root      214 May  8 08:49 pip2.7*
-rwxr-xr-x  1 root root 24603048 Mar 13 09:31 solc*
root@ethereum-cluster-1:/usr/local/bin# ls docker-compose
docker-compose
root@ethereum-cluster-1:/usr/local/bin# cd docker-compose
bash: cd: docker-compose: Not a directory
root@ethereum-cluster-1:/usr/local/bin# docker --version
Docker version 18.05.0-ce, build f150324
root@ethereum-cluster-1:/usr/local/bin# cd ..
root@ethereum-cluster-1:/usr/local# cd ..
root@ethereum-cluster-1:/usr# cd ..
root@ethereum-cluster-1:/# cd /data/hyperledger/
root@ethereum-cluster-1:/data/hyperledger# pip --version
pip 10.0.1 from /usr/local/lib/python2.7/dist-packages/pip (python 2.7)
root@ethereum-cluster-1:/data/hyperledger# pip3 --version
The program 'pip3' is currently not installed. You can install it by typing:
apt install python3-pip
root@ethereum-cluster-1:/data/hyperledger# node --version
v8.11.2
root@ethereum-cluster-1:/data/hyperledger# npm --version
5.6.0


   ╭─────────────────────────────────────╮
   │                                     │
   │   Update available 5.6.0 → 6.1.0    │
   │     Run npm i -g npm to update      │
   │                                     │
   ╰─────────────────────────────────────╯

root@ethereum-cluster-1:/data/hyperledger# ls
fabric-samples
root@ethereum-cluster-1:/data/hyperledger# mv fabric-samples/ fabric-samples-1.1.0
root@ethereum-cluster-1:/data/hyperledger# ls
fabric-samples-1.1.0
root@ethereum-cluster-1:/data/hyperledger# git clone https://github.com/hyperledger/fabric-­samples.git
Cloning into 'fabric-­samples'...
fatal: unable to access 'https://github.com/hyperledger/fabric-­samples.git/': The requested URL returned    error: 400
root@ethereum-cluster-1:/data/hyperledger# git clone https://github.com/hyperledger/fabric-samples.git
Cloning into 'fabric-samples'...
remote: Counting objects: 1663, done.
remote: Compressing objects: 100% (29/29), done.
remote: Total 1663 (delta 10), reused 23 (delta 2), pack-reused 1632
Receiving objects: 100% (1663/1663), 605.72 KiB | 0 bytes/s, done.
Resolving deltas: 100% (800/800), done.
Checking connectivity... done.
root@ethereum-cluster-1:/data/hyperledger# cd fabric-samples
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# curls -sSL https://goo.gl/byy2Qj | bash -s 1.0.5   No command 'curls' found, did you mean:
 Command 'curl' from package 'curl' (main)
curls: command not found
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# curl -sSL https://goo.gl/byy2Qj | bash -s 1.0.5    ===> Downloading platform binaries
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 22.7M  100 22.7M    0     0  1029k      0  0:00:22  0:00:22 --:--:-- 1176k
===> Pulling fabric Images
==> FABRIC IMAGE: peer

x86_64-1.0.5: Pulling from hyperledger/fabric-peer
d5c6f90da05d: Pull complete
1300883d87d5: Pull complete
c220aa3cfc1b: Pull complete
2e9398f099dc: Pull complete
dc27a084064f: Pull complete
87675a6d4030: Pull complete
93e601aafda8: Pull complete
e6a221e2ff1e: Pull complete
a2f7735b5594: Pull complete
7b6718530643: Pull complete
Digest: sha256:70806bb555050c3f6baeed71f7648af7ff0d1b79c3a4cb7a991e06480d3dd39c
Status: Downloaded newer image for hyperledger/fabric-peer:x86_64-1.0.5
==> FABRIC IMAGE: orderer

x86_64-1.0.5: Pulling from hyperledger/fabric-orderer
d5c6f90da05d: Already exists
1300883d87d5: Already exists
c220aa3cfc1b: Already exists
2e9398f099dc: Already exists
dc27a084064f: Already exists
87675a6d4030: Already exists
93e601aafda8: Already exists
e6a221e2ff1e: Already exists
2f6e3f242afb: Pull complete
c5700f4adeef: Pull complete
Digest: sha256:1ebeab88938d3f22bf3f370cf1468752e47953aeec97524045634a1d74226c0b
Status: Downloaded newer image for hyperledger/fabric-orderer:x86_64-1.0.5
==> FABRIC IMAGE: couchdb

x86_64-1.0.5: Pulling from hyperledger/fabric-couchdb
d5c6f90da05d: Already exists
1300883d87d5: Already exists
c220aa3cfc1b: Already exists
2e9398f099dc: Already exists
dc27a084064f: Already exists
87675a6d4030: Already exists
93e601aafda8: Already exists
6be6b5cbce6b: Pull complete
c90d7a44426d: Pull complete
9767b1c8440b: Pull complete
b9b680c73863: Pull complete
bd9d3bcaf5cb: Pull complete
b004f1977470: Pull complete
5489b2164dfa: Pull complete
ebaeaa2212c7: Pull complete
44eb867c8197: Pull complete
ddfe57a0854d: Pull complete
95acf0c6834f: Pull complete
e6a9cd56377a: Pull complete
Digest: sha256:2cdf0ebf247ebd79f15bb8440369abd024a45c698134217e0920f8b6614fb138
Status: Downloaded newer image for hyperledger/fabric-couchdb:x86_64-1.0.5
==> FABRIC IMAGE: ccenv

x86_64-1.0.5: Pulling from hyperledger/fabric-ccenv
d5c6f90da05d: Already exists
1300883d87d5: Already exists
c220aa3cfc1b: Already exists
2e9398f099dc: Already exists
dc27a084064f: Already exists
87675a6d4030: Already exists
93e601aafda8: Already exists
6be6b5cbce6b: Already exists
c90d7a44426d: Already exists
9767b1c8440b: Already exists
b9b680c73863: Already exists
49eef314041d: Pull complete
f10afc3c7989: Pull complete
926c0cc81f1c: Pull complete
Digest: sha256:cdcfdc7f073fbe67e13bc2ecafb234bba63eb67402b712aa00725e279e4a984d
Status: Downloaded newer image for hyperledger/fabric-ccenv:x86_64-1.0.5
==> FABRIC IMAGE: javaenv

x86_64-1.0.5: Pulling from hyperledger/fabric-javaenv
d5c6f90da05d: Already exists
1300883d87d5: Already exists
c220aa3cfc1b: Already exists
2e9398f099dc: Already exists
dc27a084064f: Already exists
87675a6d4030: Already exists
93e601aafda8: Already exists
6be6b5cbce6b: Already exists
c90d7a44426d: Already exists
9767b1c8440b: Already exists
b9b680c73863: Already exists
36f49a691f11: Pull complete
f7e761800170: Pull complete
065be65fc389: Pull complete
626c14f7cb04: Pull complete
5d075de67562: Pull complete
d5ebaab483a7: Pull complete
2b4c82e7cc31: Pull complete
f8280aaf40cb: Pull complete
Digest: sha256:f39b94d9c116295144b8620b15063f5f849d1a258031e06c4592751353255760
Status: Downloaded newer image for hyperledger/fabric-javaenv:x86_64-1.0.5
==> FABRIC IMAGE: kafka

x86_64-1.0.5: Pulling from hyperledger/fabric-kafka
d5c6f90da05d: Already exists
1300883d87d5: Already exists
c220aa3cfc1b: Already exists
2e9398f099dc: Already exists
dc27a084064f: Already exists
87675a6d4030: Already exists
93e601aafda8: Already exists
6be6b5cbce6b: Already exists
c90d7a44426d: Already exists
9767b1c8440b: Already exists
b9b680c73863: Already exists
16f803a685f5: Pull complete
764fcbb982d8: Pull complete
4f0c3889a7f7: Pull complete
Digest: sha256:06b97a4a915682b630a4b118725edbc734ae20b1fc19155fce40721aace78c9c
Status: Downloaded newer image for hyperledger/fabric-kafka:x86_64-1.0.5
==> FABRIC IMAGE: zookeeper

x86_64-1.0.5: Pulling from hyperledger/fabric-zookeeper
d5c6f90da05d: Already exists
1300883d87d5: Already exists
c220aa3cfc1b: Already exists
2e9398f099dc: Already exists
dc27a084064f: Already exists
87675a6d4030: Already exists
93e601aafda8: Already exists
6be6b5cbce6b: Already exists
c90d7a44426d: Already exists
9767b1c8440b: Already exists
b9b680c73863: Already exists
4ad22537b521: Pull complete
e921b3e68c21: Pull complete
7c12c625150a: Pull complete
5f254b6f48d2: Pull complete
Digest: sha256:ca96a2b1c2601307cf8cb903a7fe5719da5f9394b18f882a79cc369d796a16b9
Status: Downloaded newer image for hyperledger/fabric-zookeeper:x86_64-1.0.5
==> FABRIC IMAGE: tools

x86_64-1.0.5: Pulling from hyperledger/fabric-tools
d5c6f90da05d: Already exists
1300883d87d5: Already exists
c220aa3cfc1b: Already exists
2e9398f099dc: Already exists
dc27a084064f: Already exists
87675a6d4030: Already exists
93e601aafda8: Already exists
6be6b5cbce6b: Already exists
c90d7a44426d: Already exists
9767b1c8440b: Already exists
b9b680c73863: Already exists
c9e0c310768c: Pull complete
794d90391648: Pull complete
cc7527ffd65d: Pull complete
c9fb6472a911: Pull complete
98c9a80d1456: Pull complete
Digest: sha256:3bf00e65ba778b8f19bdb2e15557c266863971f38b41ba9c432ebb68a61b3219
Status: Downloaded newer image for hyperledger/fabric-tools:x86_64-1.0.5
===> Pulling fabric ca Image
==> FABRIC CA IMAGE

x86_64-1.0.5: Pulling from hyperledger/fabric-ca
aafe6b5e13de: Pull complete
0a2b43a72660: Pull complete
18bdd1e546d2: Pull complete
8198342c3e05: Pull complete
f56970a44fd4: Pull complete
e32b597e7839: Pull complete
a6e362fc71c4: Pull complete
00a3e68f8ca1: Pull complete
db316ddc1de4: Pull complete
af89e0b0f853: Pull complete
917d6c39b354: Pull complete
Digest: sha256:1d9d7e0056651e39cf2c87ee270560d27d2974f50d1a7f97caade227fe2b68f5
Status: Downloaded newer image for hyperledger/fabric-ca:x86_64-1.0.5

===> List out hyperledger docker images
hyperledger/fabric-tools       latest              6a8993b718c8        6 months ago        1.33GB
hyperledger/fabric-tools       x86_64-1.0.5        6a8993b718c8        6 months ago        1.33GB
hyperledger/fabric-couchdb     latest              9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-couchdb     x86_64-1.0.5        9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-kafka       latest              b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-kafka       x86_64-1.0.5        b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-zookeeper   latest              68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-zookeeper   x86_64-1.0.5        68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-orderer     latest              368c78b6f03b        6 months ago        151MB
hyperledger/fabric-orderer     x86_64-1.0.5        368c78b6f03b        6 months ago        151MB
hyperledger/fabric-peer        latest              c2ab022f0bdb        6 months ago        154MB
hyperledger/fabric-peer        x86_64-1.0.5        c2ab022f0bdb        6 months ago        154MB
hyperledger/fabric-javaenv     latest              50890cc3f0cd        6 months ago        1.41GB
hyperledger/fabric-javaenv     x86_64-1.0.5        50890cc3f0cd        6 months ago        1.41GB
hyperledger/fabric-ccenv       latest              33feadb8f7a6        6 months ago        1.28GB
hyperledger/fabric-ccenv       x86_64-1.0.5        33feadb8f7a6        6 months ago        1.28GB
hyperledger/fabric-ca          latest              002c9089e464        6 months ago        238MB
hyperledger/fabric-ca          x86_64-1.0.5        002c9089e464        6 months ago        238MB
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# cd bin
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/bin# ls
configtxgen  configtxlator  cryptogen  get-byfn.sh  get-docker-images.sh  orderer  peer
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/bin# cd ../
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# cd first-network/
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# ls
base               crypto-config.yaml              docker-compose-e2e-template.yaml  README.md
byfn.sh            docker-compose-cli.yaml         docker-compose-org3.yaml          scripts
channel-artifacts  docker-compose-couch-org3.yaml  eyfn.sh
configtx.yaml      docker-compose-couch.yaml       org3-artifacts
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# ./byfn.sh -m generate
Generating certs and genesis block for with channel 'mychannel' and CLI timeout of '10' seconds and CLI de   lay of '3' seconds
Continue? [Y/n] y
proceeding ...
/data/hyperledger/fabric-samples/first-network/../bin/cryptogen

##########################################################
##### Generate certificates using cryptogen tool #########
##########################################################
+ cryptogen generate --config=./crypto-config.yaml
org1.example.com
org2.example.com
+ res=0
+ set +x

/data/hyperledger/fabric-samples/first-network/../bin/configtxgen
##########################################################
#########  Generating Orderer Genesis block ##############
##########################################################
+ configtxgen -profile TwoOrgsOrdererGenesis -outputBlock ./channel-artifacts/genesis.block
2018-06-25 11:07:36.697 KST [common/configtx/tool] main -> INFO 001 Loading configuration
2018-06-25 11:07:36.703 KST [common/configtx/tool/localconfig] Load -> CRIT 002 Error unmarshaling config    into struct:  4 error(s) decoding:

* '' has invalid keys: capabilities
* 'Profiles[TwoOrgsChannel].Application' has invalid keys: Capabilities
* 'Profiles[TwoOrgsOrdererGenesis]' has invalid keys: Capabilities
* 'Profiles[TwoOrgsOrdererGenesis].Orderer' has invalid keys: Capabilities
+ res=1
+ set +x
Failed to generate orderer genesis block...
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# ./byfn.sh -m generate
Generating certs and genesis block for with channel 'mychannel' and CLI timeout of '10' seconds and CLI de   lay of '3' seconds
Continue? [Y/n] y
proceeding ...
/data/hyperledger/fabric-samples/first-network/../bin/cryptogen

##########################################################
##### Generate certificates using cryptogen tool #########
##########################################################
+ cryptogen generate --config=./crypto-config.yaml
org1.example.com
org2.example.com
+ res=0
+ set +x

/data/hyperledger/fabric-samples/first-network/../bin/configtxgen
##########################################################
#########  Generating Orderer Genesis block ##############
##########################################################
+ configtxgen -profile TwoOrgsOrdererGenesis -outputBlock ./channel-artifacts/genesis.block
2018-06-25 11:08:06.054 KST [common/configtx/tool] main -> INFO 001 Loading configuration
2018-06-25 11:08:06.060 KST [common/configtx/tool/localconfig] Load -> CRIT 002 Error unmarshaling config    into struct:  4 error(s) decoding:

* '' has invalid keys: capabilities
* 'Profiles[TwoOrgsChannel].Application' has invalid keys: Capabilities
* 'Profiles[TwoOrgsOrdererGenesis]' has invalid keys: Capabilities
* 'Profiles[TwoOrgsOrdererGenesis].Orderer' has invalid keys: Capabilities
+ res=1
+ set +x
Failed to generate orderer genesis block...
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# cd ..
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# ls
balance-transfer  chaincode                 fabric-ca        LICENSE         scripts
basic-network     chaincode-docker-devmode  first-network    MAINTAINERS.md
bin               fabcar                    high-throughput  README.md
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# ls bin
configtxgen  configtxlator  cryptogen  get-byfn.sh  get-docker-images.sh  orderer  peer
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# cd ..
root@ethereum-cluster-1:/data/hyperledger# cd fabric-samples
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# curl -sSL https://goo.gl/byy2Qj | bash -s 1.1.0
===> Downloading platform binaries
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 35.4M  100 35.4M    0     0  1060k      0  0:00:34  0:00:34 --:--:-- 1151k
===> Pulling fabric Images
==> FABRIC IMAGE: peer

x86_64-1.1.0: Pulling from hyperledger/fabric-peer
1be7f2b886e8: Pull complete
6fbc4a21b806: Pull complete
c71a6f8e1378: Pull complete
4be3072e5a37: Pull complete
06c6d2f59700: Pull complete
4d536120d8a5: Pull complete
0baaf9ec263e: Pull complete
770563795186: Pull complete
15763b7bd14b: Pull complete
62f2823da7f3: Pull complete
Digest: sha256:57417699ddf50c5ebd47a9a2cc74c0324fbba0281eb1104b9ddd05a67776b01f
Status: Downloaded newer image for hyperledger/fabric-peer:x86_64-1.1.0
==> FABRIC IMAGE: orderer

x86_64-1.1.0: Pulling from hyperledger/fabric-orderer
1be7f2b886e8: Already exists
6fbc4a21b806: Already exists
c71a6f8e1378: Already exists
4be3072e5a37: Already exists
06c6d2f59700: Already exists
4d536120d8a5: Already exists
0baaf9ec263e: Already exists
770563795186: Already exists
61d33418a569: Pull complete
b1b98004e7c6: Pull complete
Digest: sha256:0c3a3b5ecfd24b513da22bbb77da7b3f5bca9c121cc0ac5c46ba04c97c163654
Status: Downloaded newer image for hyperledger/fabric-orderer:x86_64-1.1.0
==> FABRIC IMAGE: couchdb

Error response from daemon: manifest for hyperledger/fabric-couchdb:x86_64-1.1.0 not found
Error response from daemon: No such image: hyperledger/fabric-couchdb:x86_64-1.1.0
==> FABRIC IMAGE: ccenv

x86_64-1.1.0: Pulling from hyperledger/fabric-ccenv
1be7f2b886e8: Already exists
6fbc4a21b806: Already exists
c71a6f8e1378: Already exists
4be3072e5a37: Already exists
06c6d2f59700: Already exists
4d536120d8a5: Already exists
0baaf9ec263e: Already exists
3ea9b6cc6f21: Pull complete
6173b9a5fe5e: Pull complete
e73719e0bcbe: Pull complete
b55408c6ced5: Pull complete
e1267c65ed62: Pull complete
2839c20999d1: Pull complete
444429f2833f: Pull complete
Digest: sha256:07818367dc6d4264472d24b21819f9dc4e16e890d81ddfacee0341a22d72050b
Status: Downloaded newer image for hyperledger/fabric-ccenv:x86_64-1.1.0
==> FABRIC IMAGE: javaenv

x86_64-1.1.0: Pulling from hyperledger/fabric-javaenv
1be7f2b886e8: Already exists
6fbc4a21b806: Already exists
c71a6f8e1378: Already exists
4be3072e5a37: Already exists
06c6d2f59700: Already exists
4d536120d8a5: Already exists
0baaf9ec263e: Already exists
3ea9b6cc6f21: Already exists
6173b9a5fe5e: Already exists
e73719e0bcbe: Already exists
b55408c6ced5: Already exists
d72e92165d22: Pull complete
bbb7025c0883: Pull complete
8fa39f27c772: Pull complete
5187f67cb3f8: Pull complete
05488c815030: Pull complete
3bd91626e779: Pull complete
47aa3719a5d6: Pull complete
cd3dc7bf95ff: Pull complete
Digest: sha256:d2588c0556b6fc79131f638b02a7a77337363e2c2f38a9c47798a6d99bd2f20e
Status: Downloaded newer image for hyperledger/fabric-javaenv:x86_64-1.1.0
==> FABRIC IMAGE: kafka

Error response from daemon: manifest for hyperledger/fabric-kafka:x86_64-1.1.0 not found
Error response from daemon: No such image: hyperledger/fabric-kafka:x86_64-1.1.0
==> FABRIC IMAGE: zookeeper

Error response from daemon: manifest for hyperledger/fabric-zookeeper:x86_64-1.1.0 not found
Error response from daemon: No such image: hyperledger/fabric-zookeeper:x86_64-1.1.0
==> FABRIC IMAGE: tools

x86_64-1.1.0: Pulling from hyperledger/fabric-tools
1be7f2b886e8: Already exists
6fbc4a21b806: Already exists
c71a6f8e1378: Already exists
4be3072e5a37: Already exists
06c6d2f59700: Already exists
4d536120d8a5: Already exists
0baaf9ec263e: Already exists
3ea9b6cc6f21: Already exists
6173b9a5fe5e: Already exists
e73719e0bcbe: Already exists
b55408c6ced5: Already exists
1a8bca84adfa: Pull complete
b54c1992cc9c: Pull complete
68093aff3e84: Pull complete
3827dc0ff46d: Pull complete
1e22360bf4e7: Pull complete
Digest: sha256:36d7fa8e8ddcc19fed8e1c3c06bc6ae1dac18c35e8a884188d2c08df3e5a4472
Status: Downloaded newer image for hyperledger/fabric-tools:x86_64-1.1.0
===> Pulling fabric ca Image
==> FABRIC CA IMAGE

x86_64-1.1.0: Pulling from hyperledger/fabric-ca
1be7f2b886e8: Already exists
6fbc4a21b806: Already exists
c71a6f8e1378: Already exists
4be3072e5a37: Already exists
06c6d2f59700: Already exists
4d536120d8a5: Already exists
0baaf9ec263e: Already exists
ab27f0b1192c: Pull complete
7e1142a727eb: Pull complete
a7624c188c44: Pull complete
0c8524afd242: Pull complete
23e14758f709: Pull complete
Digest: sha256:92f44d0811cddb0d335f7879f7e3b3c4b631f31740c76f3e7b85438c244b03f4
Status: Downloaded newer image for hyperledger/fabric-ca:x86_64-1.1.0

===> List out hyperledger docker images
hyperledger/fabric-ca          latest              72617b4fa9b4        3 months ago        299MB
hyperledger/fabric-ca          x86_64-1.1.0        72617b4fa9b4        3 months ago        299MB
hyperledger/fabric-tools       latest              b7bfddf508bc        3 months ago        1.46GB
hyperledger/fabric-tools       x86_64-1.1.0        b7bfddf508bc        3 months ago        1.46GB
hyperledger/fabric-orderer     latest              ce0c810df36a        3 months ago        180MB
hyperledger/fabric-orderer     x86_64-1.1.0        ce0c810df36a        3 months ago        180MB
hyperledger/fabric-peer        latest              b023f9be0771        3 months ago        187MB
hyperledger/fabric-peer        x86_64-1.1.0        b023f9be0771        3 months ago        187MB
hyperledger/fabric-javaenv     latest              82098abb1a17        3 months ago        1.52GB
hyperledger/fabric-javaenv     x86_64-1.1.0        82098abb1a17        3 months ago        1.52GB
hyperledger/fabric-ccenv       latest              c8b4909d8d46        3 months ago        1.39GB
hyperledger/fabric-ccenv       x86_64-1.1.0        c8b4909d8d46        3 months ago        1.39GB
hyperledger/fabric-tools       x86_64-1.0.5        6a8993b718c8        6 months ago        1.33GB
hyperledger/fabric-couchdb     latest              9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-couchdb     x86_64-1.0.5        9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-kafka       latest              b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-kafka       x86_64-1.0.5        b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-zookeeper   latest              68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-zookeeper   x86_64-1.0.5        68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-orderer     x86_64-1.0.5        368c78b6f03b        6 months ago        151MB
hyperledger/fabric-peer        x86_64-1.0.5        c2ab022f0bdb        6 months ago        154MB
hyperledger/fabric-javaenv     x86_64-1.0.5        50890cc3f0cd        6 months ago        1.41GB
hyperledger/fabric-ccenv       x86_64-1.0.5        33feadb8f7a6        6 months ago        1.28GB
hyperledger/fabric-ca          x86_64-1.0.5        002c9089e464        6 months ago        238MB
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# cd bin
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/bin# ls
configtxgen  configtxlator  cryptogen  get-byfn.sh  get-docker-images.sh  orderer  peer
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/bin# cd ..
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# ls
balance-transfer  chaincode                 fabcar         high-throughput  README.md
basic-network     chaincode-docker-devmode  fabric-ca      LICENSE          scripts
bin               config                    first-network  MAINTAINERS.md
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# cd first-network/
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# ./byfn.sh -m generate
Generating certs and genesis block for with channel 'mychannel' and CLI timeout of '10' seconds and CLI de   lay of '3' seconds
Continue? [Y/n] y
proceeding ...
/data/hyperledger/fabric-samples/first-network/../bin/cryptogen

##########################################################
##### Generate certificates using cryptogen tool #########
##########################################################
+ cryptogen generate --config=./crypto-config.yaml
org1.example.com
org2.example.com
+ res=0
+ set +x

/data/hyperledger/fabric-samples/first-network/../bin/configtxgen
##########################################################
#########  Generating Orderer Genesis block ##############
##########################################################
+ configtxgen -profile TwoOrgsOrdererGenesis -outputBlock ./channel-artifacts/genesis.block
2018-06-25 11:16:29.929 KST [common/tools/configtxgen] main -> INFO 001 Loading configuration
2018-06-25 11:16:29.941 KST [msp] getMspConfig -> INFO 002 Loading NodeOUs
2018-06-25 11:16:29.942 KST [msp] getMspConfig -> INFO 003 Loading NodeOUs
2018-06-25 11:16:29.942 KST [common/tools/configtxgen] doOutputBlock -> INFO 004 Generating genesis block
2018-06-25 11:16:29.943 KST [common/tools/configtxgen] doOutputBlock -> INFO 005 Writing genesis block
+ res=0
+ set +x

#################################################################
### Generating channel configuration transaction 'channel.tx' ###
#################################################################
+ configtxgen -profile TwoOrgsChannel -outputCreateChannelTx ./channel-artifacts/channel.tx -channelID myc   hannel
2018-06-25 11:16:29.979 KST [common/tools/configtxgen] main -> INFO 001 Loading configuration
2018-06-25 11:16:29.990 KST [common/tools/configtxgen] doOutputChannelCreateTx -> INFO 002 Generating new    channel configtx
2018-06-25 11:16:29.990 KST [msp] getMspConfig -> INFO 003 Loading NodeOUs
2018-06-25 11:16:29.991 KST [msp] getMspConfig -> INFO 004 Loading NodeOUs
2018-06-25 11:16:30.032 KST [common/tools/configtxgen] doOutputChannelCreateTx -> INFO 005 Writing new cha   nnel tx
+ res=0
+ set +x

#################################################################
#######    Generating anchor peer update for Org1MSP   ##########
#################################################################
+ configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org1MSPanchors.tx -chan   nelID mychannel -asOrg Org1MSP
2018-06-25 11:16:30.068 KST [common/tools/configtxgen] main -> INFO 001 Loading configuration
2018-06-25 11:16:30.079 KST [common/tools/configtxgen] doOutputAnchorPeersUpdate -> INFO 002 Generating an   chor peer update
2018-06-25 11:16:30.079 KST [common/tools/configtxgen] doOutputAnchorPeersUpdate -> INFO 003 Writing ancho   r peer update
+ res=0
+ set +x

#################################################################
#######    Generating anchor peer update for Org2MSP   ##########
#################################################################
+ configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org2MSPanchors.tx -chan   nelID mychannel -asOrg Org2MSP
2018-06-25 11:16:30.111 KST [common/tools/configtxgen] main -> INFO 001 Loading configuration
2018-06-25 11:16:30.123 KST [common/tools/configtxgen] doOutputAnchorPeersUpdate -> INFO 002 Generating an   chor peer update
2018-06-25 11:16:30.123 KST [common/tools/configtxgen] doOutputAnchorPeersUpdate -> INFO 003 Writing ancho   r peer update
+ res=0
+ set +x

root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# cd ..
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# docker images
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
eosio/eos                      latest              ba565f7d6939        4 weeks ago         242MB
<none>                         <none>              a7adbe743d02        4 weeks ago         3.54GB
<none>                         <none>              8bec3212f8ac        7 weeks ago         271MB
<none>                         <none>              aee708fad551        7 weeks ago         3.46GB
ubuntu                         16.04               0b1edfbffd27        8 weeks ago         113MB
ubuntu                         18.04               452a96d81c30        8 weeks ago         79.6MB
eosio/builder                  latest              427431c1f7bd        2 months ago        2.21GB
hello-world                    latest              e38bc07ac18e        2 months ago        1.85kB
hyperledger/fabric-ca          latest              72617b4fa9b4        3 months ago        299MB
hyperledger/fabric-ca          x86_64-1.1.0        72617b4fa9b4        3 months ago        299MB
hyperledger/fabric-tools       latest              b7bfddf508bc        3 months ago        1.46GB
hyperledger/fabric-tools       x86_64-1.1.0        b7bfddf508bc        3 months ago        1.46GB
hyperledger/fabric-orderer     latest              ce0c810df36a        3 months ago        180MB
hyperledger/fabric-orderer     x86_64-1.1.0        ce0c810df36a        3 months ago        180MB
hyperledger/fabric-peer        latest              b023f9be0771        3 months ago        187MB
hyperledger/fabric-peer        x86_64-1.1.0        b023f9be0771        3 months ago        187MB
hyperledger/fabric-javaenv     latest              82098abb1a17        3 months ago        1.52GB
hyperledger/fabric-javaenv     x86_64-1.1.0        82098abb1a17        3 months ago        1.52GB
hyperledger/fabric-ccenv       latest              c8b4909d8d46        3 months ago        1.39GB
hyperledger/fabric-ccenv       x86_64-1.1.0        c8b4909d8d46        3 months ago        1.39GB
hyperledger/fabric-tools       x86_64-1.0.5        6a8993b718c8        6 months ago        1.33GB
hyperledger/fabric-couchdb     latest              9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-couchdb     x86_64-1.0.5        9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-kafka       latest              b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-kafka       x86_64-1.0.5        b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-zookeeper   latest              68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-zookeeper   x86_64-1.0.5        68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-orderer     x86_64-1.0.5        368c78b6f03b        6 months ago        151MB
hyperledger/fabric-peer        x86_64-1.0.5        c2ab022f0bdb        6 months ago        154MB
hyperledger/fabric-javaenv     x86_64-1.0.5        50890cc3f0cd        6 months ago        1.41GB
hyperledger/fabric-ccenv       x86_64-1.0.5        33feadb8f7a6        6 months ago        1.28GB
hyperledger/fabric-ca          x86_64-1.0.5        002c9089e464        6 months ago        238MB
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# cd bin
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/bin# ls
configtxgen  configtxlator  cryptogen  get-byfn.sh  get-docker-images.sh  orderer  peer
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/bin# cd ..
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# cd first-network/
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# ls
base               crypto-config                   docker-compose-couch.yaml         eyfn.sh
byfn.sh            crypto-config.yaml              docker-compose-e2e-template.yaml  org3-artifacts
channel-artifacts  docker-compose-cli.yaml         docker-compose-e2e.yaml           README.md
configtx.yaml      docker-compose-couch-org3.yaml  docker-compose-org3.yaml          scripts
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# cd crypto-config
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network/crypto-config# ls
ordererOrganizations  peerOrganizations
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network/crypto-config# cd ../
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# ./byfn.sh -m up
Starting with channel 'mychannel' and CLI timeout of '10' seconds and CLI delay of '3' seconds
Continue? [Y/n] y
proceeding ...
2018-06-25 02:20:12.901 UTC [main] main -> INFO 001 Exiting.....
LOCAL_VERSION=1.1.0
DOCKER_IMAGE_VERSION=1.1.0
Creating network "net_byfn" with the default driver
Creating volume "net_orderer.example.com" with default driver
Creating volume "net_peer0.org1.example.com" with default driver
Creating volume "net_peer1.org1.example.com" with default driver
Creating volume "net_peer0.org2.example.com" with default driver
Creating volume "net_peer1.org2.example.com" with default driver
Creating orderer.example.com    ... done
Creating peer1.org2.example.com ... done
Creating peer0.org2.example.com ... done
Creating peer1.org1.example.com ... done
Creating peer0.org1.example.com ... done
Creating cli                    ... done

 ____    _____      _      ____    _____
/ ___|  |_   _|    / \    |  _ \  |_   _|
\___ \    | |     / _ \   | |_) |   | |
 ___) |   | |    / ___ \  |  _ <    | |
|____/    |_|   /_/   \_\ |_| \_\   |_|

Build your first network (BYFN) end-to-end test

Channel name : mychannel
Creating channel...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
+ peer channel create -o orderer.example.com:7050 -c mychannel -f ./channel-artifacts/channel.tx --tls tru   e --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orde   rers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
+ res=0
+ set +x
2018-06-25 02:20:18.662 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initi   alized
2018-06-25 02:20:18.691 UTC [channelCmd] InitCmdFactory -> INFO 002 Endorser and orderer connections initi   alized
2018-06-25 02:20:18.894 UTC [main] main -> INFO 003 Exiting.....
===================== Channel "mychannel" is created successfully =====================

Having all peers join the channel...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
+ peer channel join -b mychannel.block
+ res=0
+ set +x
2018-06-25 02:20:18.959 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initi   alized
2018-06-25 02:20:19.001 UTC [channelCmd] executeJoin -> INFO 002 Successfully submitted proposal to join c   hannel
2018-06-25 02:20:19.001 UTC [main] main -> INFO 003 Exiting.....
===================== peer0.org1 joined on the channel "mychannel" =====================

CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer1.org1.example.com:7051
+ peer channel join -b mychannel.block
+ res=0
+ set +x
2018-06-25 02:20:22.069 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initi   alized
2018-06-25 02:20:22.109 UTC [channelCmd] executeJoin -> INFO 002 Successfully submitted proposal to join c   hannel
2018-06-25 02:20:22.109 UTC [main] main -> INFO 003 Exiting.....
===================== peer1.org1 joined on the channel "mychannel" =====================

CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.e   xample.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org2.example.com:7051
+ peer channel join -b mychannel.block
+ res=0
+ set +x
2018-06-25 02:20:25.176 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initi   alized
2018-06-25 02:20:25.214 UTC [channelCmd] executeJoin -> INFO 002 Successfully submitted proposal to join c   hannel
2018-06-25 02:20:25.214 UTC [main] main -> INFO 003 Exiting.....
===================== peer0.org2 joined on the channel "mychannel" =====================

CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.e   xample.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer1.org2.example.com:7051
+ peer channel join -b mychannel.block
+ res=0
+ set +x
2018-06-25 02:20:28.280 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initi   alized
2018-06-25 02:20:28.320 UTC [channelCmd] executeJoin -> INFO 002 Successfully submitted proposal to join c   hannel
2018-06-25 02:20:28.320 UTC [main] main -> INFO 003 Exiting.....
===================== peer1.org2 joined on the channel "mychannel" =====================

Updating anchor peers for org1...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
+ peer channel update -o orderer.example.com:7050 -c mychannel -f ./channel-artifacts/Org1MSPanchors.tx --   tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.c   om/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
+ res=0
+ set +x
2018-06-25 02:20:31.394 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initi   alized
2018-06-25 02:20:31.409 UTC [channelCmd] update -> INFO 002 Successfully submitted channel update
2018-06-25 02:20:31.409 UTC [main] main -> INFO 003 Exiting.....
===================== Anchor peers for org "Org1MSP" on "mychannel" is updated successfully ==============   =======

Updating anchor peers for org2...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.e   xample.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org2.example.com:7051
+ peer channel update -o orderer.example.com:7050 -c mychannel -f ./channel-artifacts/Org2MSPanchors.tx --   tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.c   om/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
+ res=0
+ set +x
2018-06-25 02:20:34.490 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initi   alized
2018-06-25 02:20:34.511 UTC [channelCmd] update -> INFO 002 Successfully submitted channel update
2018-06-25 02:20:34.511 UTC [main] main -> INFO 003 Exiting.....
===================== Anchor peers for org "Org2MSP" on "mychannel" is updated successfully ==============   =======

Installing chaincode on peer0.org1...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
+ peer chaincode install -n mycc -v 1.0 -l golang -p github.com/chaincode/chaincode_example02/go/
+ res=0
+ set +x
2018-06-25 02:20:37.591 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2018-06-25 02:20:37.591 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
2018-06-25 02:20:37.852 UTC [main] main -> INFO 003 Exiting.....
===================== Chaincode is installed on peer0.org1 =====================

Install chaincode on peer0.org2...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.e   xample.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org2.example.com:7051
+ peer chaincode install -n mycc -v 1.0 -l golang -p github.com/chaincode/chaincode_example02/go/
+ res=0
+ set +x
2018-06-25 02:20:37.917 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2018-06-25 02:20:37.917 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
2018-06-25 02:20:38.175 UTC [main] main -> INFO 003 Exiting.....
===================== Chaincode is installed on peer0.org2 =====================

Instantiating chaincode on peer0.org2...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.e   xample.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org2.example.com:7051
+ peer chaincode instantiate -o orderer.example.com:7050 --tls true --cafile /opt/gopath/src/github.com/hy   perledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/   tlsca.example.com-cert.pem -C mychannel -n mycc -l golang -v 1.0 -c '{"Args":["init","a","100","b","200"]}   ' -P 'OR        ('\''Org1MSP.peer'\'','\''Org2MSP.peer'\'')'
+ res=0
+ set +x
2018-06-25 02:20:38.249 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2018-06-25 02:20:38.249 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
2018-06-25 02:20:52.876 UTC [main] main -> INFO 003 Exiting.....
===================== Chaincode Instantiation on peer0.org2 on channel 'mychannel' is successful =========   ============

Querying chaincode on peer0.org1...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
===================== Querying on peer0.org1 on channel 'mychannel'... =====================
Attempting to Query peer0.org1 ...3 secs
+ peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
+ res=0
+ set +x

2018-06-25 02:20:55.946 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2018-06-25 02:20:55.946 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
Query Result: 100
2018-06-25 02:21:06.876 UTC [main] main -> INFO 003 Exiting.....
===================== Query on peer0.org1 on channel 'mychannel' is successful =====================
Sending invoke transaction on peer0.org1...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
+ peer chaincode invoke -o orderer.example.com:7050 --tls true --cafile /opt/gopath/src/github.com/hyperle   dger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca   .example.com-cert.pem -C mychannel -n mycc -c '{"Args":["invoke","a","b","10"]}'
+ res=0
+ set +x
2018-06-25 02:21:06.954 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2018-06-25 02:21:06.954 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
2018-06-25 02:21:06.963 UTC [chaincodeCmd] chaincodeInvokeOrQuery -> INFO 003 Chaincode invoke successful.    result: status:200
2018-06-25 02:21:06.964 UTC [main] main -> INFO 004 Exiting.....
===================== Invoke transaction on peer0.org1 on channel 'mychannel' is successful ==============   =======

Installing chaincode on peer1.org2...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.e   xample.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer1.org2.example.com:7051
+ peer chaincode install -n mycc -v 1.0 -l golang -p github.com/chaincode/chaincode_example02/go/
+ res=0
+ set +x
2018-06-25 02:21:07.046 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2018-06-25 02:21:07.047 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
2018-06-25 02:21:07.284 UTC [main] main -> INFO 003 Exiting.....
===================== Chaincode is installed on peer1.org2 =====================

Querying chaincode on peer1.org2...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/or   g2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.ex   ample.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.e   xample.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.e   xample.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer1.org2.example.com:7051
===================== Querying on peer1.org2 on channel 'mychannel'... =====================
Attempting to Query peer1.org2 ...3 secs
+ peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
+ res=0
+ set +x

2018-06-25 02:21:10.354 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2018-06-25 02:21:10.354 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
Query Result: 90
2018-06-25 02:21:21.339 UTC [main] main -> INFO 003 Exiting.....
===================== Query on peer1.org2 on channel 'mychannel' is successful =====================

========= All GOOD, BYFN execution completed ===========


 _____   _   _   ____
| ____| | \ | | |  _ \
|  _|   |  \| | | | | |
| |___  | |\  | | |_| |
|_____| |_| \_| |____/

root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# docker images
REPOSITORY                                                                                             TAG                    IMAGE ID            CREATED             SIZE
dev-peer1.org2.example.com-mycc-1.0-26c2ef32838554aac4f7ad6f100aca865e87959c9a126e86d764c8d01f8346ab   lat   est              1ad6ecc2188c        7 minutes ago       172MB
dev-peer0.org1.example.com-mycc-1.0-384f11f484b9302df90b453200cfb25174305fce8f53f4e94d45ee3b6cab0ce9   lat   est              c25a61aa8fb9        7 minutes ago       172MB
dev-peer0.org2.example.com-mycc-1.0-15b571b3ce849066b7ec74497da3b27e54e0df1345daff3951b94245ce09c42b   lat   est              7d5ce16226f2        7 minutes ago       172MB
eosio/eos                                                                                              lat   est              ba565f7d6939        4 weeks ago         242MB
<none>                                                                                                 <no   ne>              a7adbe743d02        4 weeks ago         3.54GB
<none>                                                                                                 <no   ne>              8bec3212f8ac        7 weeks ago         271MB
<none>                                                                                                 <no   ne>              aee708fad551        7 weeks ago         3.46GB
ubuntu                                                                                                 16.   04               0b1edfbffd27        8 weeks ago         113MB
ubuntu                                                                                                 18.   04               452a96d81c30        8 weeks ago         79.6MB
eosio/builder                                                                                          lat   est              427431c1f7bd        2 months ago        2.21GB
hello-world                                                                                            lat   est              e38bc07ac18e        2 months ago        1.85kB
hyperledger/fabric-ca                                                                                  lat   est              72617b4fa9b4        3 months ago        299MB
hyperledger/fabric-ca                                                                                  x86   _64-1.1.0        72617b4fa9b4        3 months ago        299MB
hyperledger/fabric-tools                                                                               lat   est              b7bfddf508bc        3 months ago        1.46GB
hyperledger/fabric-tools                                                                               x86   _64-1.1.0        b7bfddf508bc        3 months ago        1.46GB
hyperledger/fabric-orderer                                                                             lat   est              ce0c810df36a        3 months ago        180MB
hyperledger/fabric-orderer                                                                             x86   _64-1.1.0        ce0c810df36a        3 months ago        180MB
hyperledger/fabric-peer                                                                                lat   est              b023f9be0771        3 months ago        187MB
hyperledger/fabric-peer                                                                                x86   _64-1.1.0        b023f9be0771        3 months ago        187MB
hyperledger/fabric-javaenv                                                                             lat   est              82098abb1a17        3 months ago        1.52GB
hyperledger/fabric-javaenv                                                                             x86   _64-1.1.0        82098abb1a17        3 months ago        1.52GB
hyperledger/fabric-ccenv                                                                               lat   est              c8b4909d8d46        3 months ago        1.39GB
hyperledger/fabric-ccenv                                                                               x86   _64-1.1.0        c8b4909d8d46        3 months ago        1.39GB
hyperledger/fabric-baseos                                                                              x86   _64-0.4.6        220e5cf3fb7f        4 months ago        151MB
hyperledger/fabric-tools                                                                               x86   _64-1.0.5        6a8993b718c8        6 months ago        1.33GB
hyperledger/fabric-couchdb                                                                             lat   est              9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-couchdb                                                                             x86   _64-1.0.5        9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-kafka                                                                               lat   est              b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-kafka                                                                               x86   _64-1.0.5        b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-zookeeper                                                                           lat   est              68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-zookeeper                                                                           x86   _64-1.0.5        68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-orderer                                                                             x86   _64-1.0.5        368c78b6f03b        6 months ago        151MB
hyperledger/fabric-peer                                                                                x86   _64-1.0.5        c2ab022f0bdb        6 months ago        154MB
hyperledger/fabric-javaenv                                                                             x86   _64-1.0.5        50890cc3f0cd        6 months ago        1.41GB
hyperledger/fabric-ccenv                                                                               x86   _64-1.0.5        33feadb8f7a6        6 months ago        1.28GB
hyperledger/fabric-ca                                                                                  x86   _64-1.0.5        002c9089e464        6 months ago        238MB
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# docker ps
CONTAINER ID        IMAGE                                                                                                     COMMAND                  CREATED             STATUS              PORTS                                                 NAMES
6704d768e6d3        dev-peer1.org2.example.com-mycc-1.0-26c2ef32838554aac4f7ad6f100aca865e87959c9a126e86d7   64c8d01f8346ab   "chaincode -peer.add…"   7 minutes ago       Up 7 minutes                                                              dev-peer1.org2.example.com-mycc-1.0
6c57f23f7336        dev-peer0.org1.example.com-mycc-1.0-384f11f484b9302df90b453200cfb25174305fce8f53f4e94d   45ee3b6cab0ce9   "chaincode -peer.add…"   7 minutes ago       Up 7 minutes                                                              dev-peer0.org1.example.com-mycc-1.0
d34076ecad84        dev-peer0.org2.example.com-mycc-1.0-15b571b3ce849066b7ec74497da3b27e54e0df1345daff3951   b94245ce09c42b   "chaincode -peer.add…"   7 minutes ago       Up 7 minutes                                                              dev-peer0.org2.example.com-mycc-1.0
7044fd327e6d        hyperledger/fabric-tools:latest                                                                           "/bin/bash"              8 minutes ago       Up 8 minutes                                                              cli
42b0a7b9f152        hyperledger/fabric-peer:latest                                                                            "peer node start"        8 minutes ago       Up 8 minutes        0.0.0.0:8051->7051/tcp,    0.0.0.0:8053->7053/tcp     peer1.org1.example.com
2de077c004b5        hyperledger/fabric-peer:latest                                                                            "peer node start"        8 minutes ago       Up 8 minutes        0.0.0.0:7051->7051/tcp,    0.0.0.0:7053->7053/tcp     peer0.org1.example.com
d3bb925d28f8        hyperledger/fabric-peer:latest                                                                            "peer node start"        8 minutes ago       Up 8 minutes        0.0.0.0:9051->7051/tcp,    0.0.0.0:9053->7053/tcp     peer0.org2.example.com
1a695dc077b9        hyperledger/fabric-peer:latest                                                                            "peer node start"        8 minutes ago       Up 8 minutes        0.0.0.0:10051->7051/tcp,    0.0.0.0:10053->7053/tcp   peer1.org2.example.com
a8e0221e6ff4        hyperledger/fabric-orderer:latest                                                                         "orderer"                8 minutes ago       Up 8 minutes        0.0.0.0:7050->7050/tcp                                orderer.example.com
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# ./byfn.sh -m down
Stopping with channel 'mychannel' and CLI timeout of '10' seconds and CLI delay of '3' seconds
Continue? [Y/n] y
proceeding ...
Stopping cli                    ... done
Stopping peer1.org1.example.com ... done
Stopping peer0.org1.example.com ... done
Stopping peer0.org2.example.com ... done
Stopping peer1.org2.example.com ... done
Stopping orderer.example.com    ... done
Removing cli                    ... done
Removing peer1.org1.example.com ... done
Removing peer0.org1.example.com ... done
Removing peer0.org2.example.com ... done
Removing peer1.org2.example.com ... done
Removing orderer.example.com    ... done
Removing network net_byfn
Removing volume net_orderer.example.com
Removing volume net_peer0.org1.example.com
Removing volume net_peer1.org1.example.com
Removing volume net_peer0.org2.example.com
Removing volume net_peer1.org2.example.com
Removing network net_byfn
WARNING: Network net_byfn not found.
Removing volume net_orderer.example.com
WARNING: Volume net_orderer.example.com not found.
Removing volume net_peer0.org1.example.com
WARNING: Volume net_peer0.org1.example.com not found.
Removing volume net_peer1.org1.example.com
WARNING: Volume net_peer1.org1.example.com not found.
Removing volume net_peer0.org2.example.com
WARNING: Volume net_peer0.org2.example.com not found.
Removing volume net_peer1.org2.example.com
WARNING: Volume net_peer1.org2.example.com not found.
6704d768e6d3
6c57f23f7336
d34076ecad84
5e32c2527bd1
Untagged: dev-peer1.org2.example.com-mycc-1.0-26c2ef32838554aac4f7ad6f100aca865e87959c9a126e86d764c8d01f8346a
Deleted: sha256:1ad6ecc2188c4663884e9d81dec91ca46fa2ed81a1072489ef46db61000c0fe8
Deleted: sha256:2de6f70935815a56636b36ea0ea4a8d2e0738311ab98922b12424e81b4d7f403
Deleted: sha256:ed39d7ec5fceb9e0c3723328e78046c303314dfa617450a533466682671b25ad
Deleted: sha256:d31eafc0b28647c2527df4c07fc3ebbbc77b606c3a44df01d6374314f095c8bf
Untagged: dev-peer0.org1.example.com-mycc-1.0-384f11f484b9302df90b453200cfb25174305fce8f53f4e94d45ee3b6cab0ce
Deleted: sha256:c25a61aa8fb900e04852cc0ba074ccf2b412edf811686012864be2fcf030af7f
Deleted: sha256:a0023821abbba23db4a469daba018f2fc24dcbee5d463a76813f3ee68d9fd03e
Deleted: sha256:280f677bf740d7367b7b338924fdb646022d520f89e4e0b685537af24826a652
Deleted: sha256:b10507c1041c12563d967943b0f5550ad5e3c7b538b638353f816519d2246f64
Untagged: dev-peer0.org2.example.com-mycc-1.0-15b571b3ce849066b7ec74497da3b27e54e0df1345daff3951b94245ce09c42
Deleted: sha256:7d5ce16226f26486177cd599f26f4ca13faa5567158e8a0442414a8b929ab50f
Deleted: sha256:ae209ee2f789829c4d595a29bc964913b11ce070b5718f4917f19d69cef20480
Deleted: sha256:7674e7dbd171065c379ffcf9f5b3b86435348027b2daadf9ef6e6c7994ece03e
Deleted: sha256:3dc7d8505c89789c0b64be755bc48053ec31991287b2ef77979bf1b084e911e4
Deleted: sha256:a7adbe743d027daafec547dc49432f624df95780dabc7da98dfb69c695730b2e
Deleted: sha256:bf2abb7c62eb957618808cef681d199f6fda272591d2cfb49496733705d3ba86
Deleted: sha256:8bec3212f8ac0d24b6e7c726dfd77c129bad2155c15e693d988a7e96e228107d
Deleted: sha256:533b9ec57607821eb463e8158d3e1c95ea795f22655db64dee50dbcb56a0bc49
Deleted: sha256:0c6d5e02c1a8ae0e991350af85a02c76ee2b23992cce5c77813717aa05281476
Deleted: sha256:5326887a7c45e9736d02c4774544bfd8dcc628fb85aeafbf499fdb71719d6e0b
Deleted: sha256:4f4dfa403e009e8f126ce2bade9e063d05c5be041d21015348e496ff317df705
Deleted: sha256:1fd0179cd9e4917addbf0053d59d56eeeeb35a54766d1b5e739996ba015e4431
Deleted: sha256:fa150f48f3db6124f8f6f087012efacd7c390c5ed5d94e293a8b0ee9b78462a8
Deleted: sha256:2912d839d866b2ffa1ba877e8f5e5e1b93db52a2742cdfe0d1aad5898497007f
Deleted: sha256:370fb93d8e797a12f679b906bcdfefc887d7bd90b6cc69862ef29b9184e48599
Deleted: sha256:48fd1146ff580de3beb9676008d391551f9bd423f0d8daa5cc5bb7685d41483d
Deleted: sha256:daf44065ab11218d66e3002d7d3d4f68020750b1788ddab5f8f8949d0c3837d4
Deleted: sha256:1aec33783e358db3d21de19114950c36518a2c5192f7580259a2de4adf9f81cd
Deleted: sha256:1069df04760263c753bc67fca31dd49abc2fc2602ea3af33e7ab730009543245
Deleted: sha256:2908e19e4e9cea4f30f05ff776a2559e91d4b905e96d896249b855a4bc339b3c
Deleted: sha256:c563f50df334591e1fe4d12b54bbdb21f1b61d51f130c37784a2d49ded98096e
Deleted: sha256:78f0e842a58d1bac5d7c63bd337de2ead4c4fe55a436c0c82057210c6b219a38
Deleted: sha256:062019e87abf0092b30d0b7dadf90f4af3af6287983be48ddf11f49fbc6612e5
Deleted: sha256:3f00a17f2ae025083ac9cbef44af9d603a7bbe8c95dbdb639c49ce516cdbc5fa
Deleted: sha256:aee708fad551ec5975daf974e6495b90dce5cb1dbee4462511714bc72887365b
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# docker images
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
eosio/eos                      latest              ba565f7d6939        4 weeks ago         242MB
ubuntu                         16.04               0b1edfbffd27        8 weeks ago         113MB
ubuntu                         18.04               452a96d81c30        8 weeks ago         79.6MB
eosio/builder                  latest              427431c1f7bd        2 months ago        2.21GB
hello-world                    latest              e38bc07ac18e        2 months ago        1.85kB
hyperledger/fabric-ca          latest              72617b4fa9b4        3 months ago        299MB
hyperledger/fabric-ca          x86_64-1.1.0        72617b4fa9b4        3 months ago        299MB
hyperledger/fabric-tools       latest              b7bfddf508bc        3 months ago        1.46GB
hyperledger/fabric-tools       x86_64-1.1.0        b7bfddf508bc        3 months ago        1.46GB
hyperledger/fabric-orderer     latest              ce0c810df36a        3 months ago        180MB
hyperledger/fabric-orderer     x86_64-1.1.0        ce0c810df36a        3 months ago        180MB
hyperledger/fabric-peer        latest              b023f9be0771        3 months ago        187MB
hyperledger/fabric-peer        x86_64-1.1.0        b023f9be0771        3 months ago        187MB
hyperledger/fabric-javaenv     latest              82098abb1a17        3 months ago        1.52GB
hyperledger/fabric-javaenv     x86_64-1.1.0        82098abb1a17        3 months ago        1.52GB
hyperledger/fabric-ccenv       latest              c8b4909d8d46        3 months ago        1.39GB
hyperledger/fabric-ccenv       x86_64-1.1.0        c8b4909d8d46        3 months ago        1.39GB
hyperledger/fabric-baseos      x86_64-0.4.6        220e5cf3fb7f        4 months ago        151MB
hyperledger/fabric-tools       x86_64-1.0.5        6a8993b718c8        6 months ago        1.33GB
hyperledger/fabric-couchdb     latest              9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-couchdb     x86_64-1.0.5        9a58db2d2723        6 months ago        1.5GB
hyperledger/fabric-kafka       latest              b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-kafka       x86_64-1.0.5        b8c5172bb83c        6 months ago        1.29GB
hyperledger/fabric-zookeeper   latest              68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-zookeeper   x86_64-1.0.5        68945f4613fc        6 months ago        1.32GB
hyperledger/fabric-orderer     x86_64-1.0.5        368c78b6f03b        6 months ago        151MB
hyperledger/fabric-peer        x86_64-1.0.5        c2ab022f0bdb        6 months ago        154MB
hyperledger/fabric-javaenv     x86_64-1.0.5        50890cc3f0cd        6 months ago        1.41GB
hyperledger/fabric-ccenv       x86_64-1.0.5        33feadb8f7a6        6 months ago        1.28GB
hyperledger/fabric-ca          x86_64-1.0.5        002c9089e464        6 months ago        238MB
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# cd ../
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# ls
balance-transfer  bin        chaincode-docker-devmode  fabcar     first-network    LICENSE         README.md
basic-network     chaincode  config                    fabric-ca  high-throughput  MAINTAINERS.md  scripts
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# cd fabcar
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# ls
enrollAdmin.js  invoke.js  package.json  query.js  registerUser.js  startFabric.sh
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# npm install

> dtrace-provider@0.8.7 install /data/hyperledger/fabric-samples/fabcar/node_modules/dtrace-provider
> node-gyp rebuild || node suppress-error.js

gyp WARN download NVM_NODEJS_ORG_MIRROR is deprecated and will be removed in node-gyp v4, please use NODEJS_O
gyp WARN download NVM_NODEJS_ORG_MIRROR is deprecated and will be removed in node-gyp v4, please use NODEJS_O
gyp WARN download NVM_NODEJS_ORG_MIRROR is deprecated and will be removed in node-gyp v4, please use NODEJS_O
make: Entering directory '/data/hyperledger/fabric-samples/fabcar/node_modules/dtrace-provider/build'
  TOUCH Release/obj.target/DTraceProviderStub.stamp
make: Leaving directory '/data/hyperledger/fabric-samples/fabcar/node_modules/dtrace-provider/build'

> pkcs11js@1.0.16 install /data/hyperledger/fabric-samples/fabcar/node_modules/pkcs11js
> node-gyp rebuild

gyp WARN download NVM_NODEJS_ORG_MIRROR is deprecated and will be removed in node-gyp v4, please use NODEJS_O
gyp WARN download NVM_NODEJS_ORG_MIRROR is deprecated and will be removed in node-gyp v4, please use NODEJS_O
gyp WARN download NVM_NODEJS_ORG_MIRROR is deprecated and will be removed in node-gyp v4, please use NODEJS_O
make: Entering directory '/data/hyperledger/fabric-samples/fabcar/node_modules/pkcs11js/build'
  CXX(target) Release/obj.target/pkcs11/src/main.o
  CXX(target) Release/obj.target/pkcs11/src/dl.o
  CXX(target) Release/obj.target/pkcs11/src/const.o
  CXX(target) Release/obj.target/pkcs11/src/pkcs11/error.o
  CXX(target) Release/obj.target/pkcs11/src/pkcs11/v8_convert.o
  CXX(target) Release/obj.target/pkcs11/src/pkcs11/template.o
  CXX(target) Release/obj.target/pkcs11/src/pkcs11/mech.o
  CXX(target) Release/obj.target/pkcs11/src/pkcs11/param.o
  CXX(target) Release/obj.target/pkcs11/src/pkcs11/param_aes.o
  CXX(target) Release/obj.target/pkcs11/src/pkcs11/param_rsa.o
  CXX(target) Release/obj.target/pkcs11/src/pkcs11/param_ecdh.o
  CXX(target) Release/obj.target/pkcs11/src/pkcs11/pkcs11.o
  CXX(target) Release/obj.target/pkcs11/src/async.o
  CXX(target) Release/obj.target/pkcs11/src/node.o
  SOLINK_MODULE(target) Release/obj.target/pkcs11.node
  COPY Release/pkcs11.node
make: Leaving directory '/data/hyperledger/fabric-samples/fabcar/node_modules/pkcs11js/build'

> grpc@1.10.1 install /data/hyperledger/fabric-samples/fabcar/node_modules/fabric-client/node_modules/grpc
> node-pre-gyp install --fallback-to-build --library=static_library

[grpc] Success: "/data/hyperledger/fabric-samples/fabcar/node_modules/fabric-client/node_modules/grpc/src/nod_binary/node-v57-linux-x64-glibc/grpc_node.node" is installed via remote

> grpc@1.12.4 install /data/hyperledger/fabric-samples/fabcar/node_modules/grpc
> node-pre-gyp install --fallback-to-build --library=static_library

[grpc] Success: "/data/hyperledger/fabric-samples/fabcar/node_modules/grpc/src/node/extension_binary/node-v57glibc/grpc_node.node" is installed via remote
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN fabcar@1.0.0 No repository field.

added 364 packages in 50.813s


   ╭─────────────────────────────────────╮
   │                                     │
   │   Update available 5.6.0 → 6.1.0    │
   │     Run npm i -g npm to update      │
   │                                     │
   ╰─────────────────────────────────────╯

root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# npm install grpc

> grpc@1.12.4 install /data/hyperledger/fabric-samples/fabcar/node_modules/grpc
> node-pre-gyp install --fallback-to-build --library=static_library

[grpc] Success: "/data/hyperledger/fabric-samples/fabcar/node_modules/grpc/src/node/extension_binary/node-v57-linux-x64-glibc/grpc_node.node" is installed via remote
npm WARN fabcar@1.0.0 No repository field.

+ grpc@1.12.4
updated 1 package in 8.061s
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# ls
enrollAdmin.js  node_modules  package-lock.json  registerUser.js
invoke.js       package.json  query.js           startFabric.sh
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# ./startFabric.sh

# don't rewrite paths for Windows Git Bash users
export MSYS_NO_PATHCONV=1

docker-compose -f docker-compose.yml down
Removing network net_basic
WARNING: Network net_basic not found.

docker-compose -f docker-compose.yml up -d ca.example.com orderer.example.com peer0.org1.example.com couchdb
Creating network "net_basic" with the default driver
Creating ca.example.com      ... done
Creating couchdb             ... done
Creating orderer.example.com ... done
Creating peer0.org1.example.com ... done

# wait for Hyperledger Fabric to start
# incase of errors when running later commands, issue export FABRIC_START_TIMEOUT=<larger number>
export FABRIC_START_TIMEOUT=10
#echo ${FABRIC_START_TIMEOUT}
sleep ${FABRIC_START_TIMEOUT}

# Create the channel
docker exec -e "CORE_PEER_LOCALMSPID=Org1MSP" -e "CORE_PEER_MSPCONFIGPATH=/etc/hyperledger/msp/users/Admin@org1.example.com/msp" peer0.org1.example.com peer channel create -o orderer.example.com:7050 -c mychannel -f /etc/hyperledger/configtx/channel.tx
2018-06-25 04:28:29.028 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
2018-06-25 04:28:29.065 UTC [channelCmd] InitCmdFactory -> INFO 002 Endorser and orderer connections initialized
2018-06-25 04:28:29.271 UTC [main] main -> INFO 003 Exiting.....
# Join peer0.org1.example.com to the channel.
docker exec -e "CORE_PEER_LOCALMSPID=Org1MSP" -e "CORE_PEER_MSPCONFIGPATH=/etc/hyperledger/msp/users/Admin@org1.example.com/msp" peer0.org1.example.com peer channel join -b mychannel.block
2018-06-25 04:28:29.542 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
2018-06-25 04:28:29.652 UTC [channelCmd] executeJoin -> INFO 002 Successfully submitted proposal to join channel
2018-06-25 04:28:29.652 UTC [main] main -> INFO 003 Exiting.....
Creating cli ... done
2018-06-25 04:28:31.205 UTC [msp] GetLocalMSP -> DEBU 001 Returning existing local MSP
2018-06-25 04:28:31.205 UTC [msp] GetDefaultSigningIdentity -> DEBU 002 Obtaining default signing identity
2018-06-25 04:28:31.205 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 003 Using default escc
2018-06-25 04:28:31.205 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 004 Using default vscc
2018-06-25 04:28:31.205 UTC [chaincodeCmd] getChaincodeSpec -> DEBU 005 java chaincode disabled
2018-06-25 04:28:31.265 UTC [golang-platform] getCodeFromFS -> DEBU 006 getCodeFromFS github.com/fabcar/go
2018-06-25 04:28:31.514 UTC [golang-platform] func1 -> DEBU 007 Discarding GOROOT package bytes
2018-06-25 04:28:31.514 UTC [golang-platform] func1 -> DEBU 008 Discarding GOROOT package encoding/json
2018-06-25 04:28:31.514 UTC [golang-platform] func1 -> DEBU 009 Discarding GOROOT package fmt
2018-06-25 04:28:31.514 UTC [golang-platform] func1 -> DEBU 00a Discarding provided package github.com/hyperledger/fabric/core/chaincode/shim
2018-06-25 04:28:31.514 UTC [golang-platform] func1 -> DEBU 00b Discarding provided package github.com/hyperledger/fabric/protos/peer
2018-06-25 04:28:31.514 UTC [golang-platform] func1 -> DEBU 00c Discarding GOROOT package strconv
2018-06-25 04:28:31.514 UTC [golang-platform] GetDeploymentPayload -> DEBU 00d done
2018-06-25 04:28:31.514 UTC [container] WriteFileToPackage -> DEBU 00e Writing file to tarball: src/github.com/fabcar/go/fabcar.go
2018-06-25 04:28:31.518 UTC [msp/identity] Sign -> DEBU 00f Sign: plaintext: 0A9C070A5C08031A0C08EFDEC1D90510...F1F3DF000000FFFF06BA999800200000
2018-06-25 04:28:31.518 UTC [msp/identity] Sign -> DEBU 010 Sign: digest: D30A849C3F69520DE00F68982F100AC6502BD8FFB4A9E49C10D4FDF304FDEF20
2018-06-25 04:28:31.542 UTC [chaincodeCmd] install -> DEBU 011 Installed remotely response:<status:200 payload:"OK" >
2018-06-25 04:28:31.542 UTC [main] main -> INFO 012 Exiting.....
2018-06-25 04:28:31.776 UTC [msp] GetLocalMSP -> DEBU 001 Returning existing local MSP
2018-06-25 04:28:31.777 UTC [msp] GetDefaultSigningIdentity -> DEBU 002 Obtaining default signing identity
2018-06-25 04:28:31.778 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 003 Using default escc
2018-06-25 04:28:31.778 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 004 Using default vscc
2018-06-25 04:28:31.780 UTC [chaincodeCmd] getChaincodeSpec -> DEBU 005 java chaincode disabled
2018-06-25 04:28:31.781 UTC [msp/identity] Sign -> DEBU 006 Sign: plaintext: 0AA7070A6708031A0C08EFDEC1D90510...324D53500A04657363630A0476736363
2018-06-25 04:28:31.781 UTC [msp/identity] Sign -> DEBU 007 Sign: digest: 89DD118210D2DA58089C82B2DB21B7506BC0352F52C7207C7EE3FB79F9F79A36
2018-06-25 04:28:42.613 UTC [msp/identity] Sign -> DEBU 008 Sign: plaintext: 0AA7070A6708031A0C08EFDEC1D90510...9CEFEBA350A3474FEF553C695E119921
2018-06-25 04:28:42.613 UTC [msp/identity] Sign -> DEBU 009 Sign: digest: 40483F9BD9D8EB203C1087ADCF1D56F210F437B00F2A4132282D52E4E1B1AAA1
2018-06-25 04:28:42.615 UTC [main] main -> INFO 00a Exiting.....
2018-06-25 04:28:52.875 UTC [msp] GetLocalMSP -> DEBU 001 Returning existing local MSP
2018-06-25 04:28:52.875 UTC [msp] GetDefaultSigningIdentity -> DEBU 002 Obtaining default signing identity
2018-06-25 04:28:52.877 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 003 Using default escc
2018-06-25 04:28:52.877 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 004 Using default vscc
2018-06-25 04:28:52.877 UTC [chaincodeCmd] getChaincodeSpec -> DEBU 005 java chaincode disabled
2018-06-25 04:28:52.879 UTC [msp/identity] Sign -> DEBU 006 Sign: plaintext: 0AA9070A6908031A0C0884DFC1D90510...1A0E0A0A696E69744C65646765720A00
2018-06-25 04:28:52.879 UTC [msp/identity] Sign -> DEBU 007 Sign: digest: 1D1BDCDEF3CA61A43F38A9D6B3039BF1C9F331B180965E21796731DF874534D5
2018-06-25 04:28:52.901 UTC [msp/identity] Sign -> DEBU 008 Sign: plaintext: 0AA9070A6908031A0C0884DFC1D90510...8D2E1A58F2472B183F071F6F818CAFE1
2018-06-25 04:28:52.901 UTC [msp/identity] Sign -> DEBU 009 Sign: digest: 91060F4A4D8C59C93704067870BE6F2E3338B50C25D99502D73D80BE7DA2D17B
2018-06-25 04:28:52.904 UTC [chaincodeCmd] chaincodeInvokeOrQuery -> DEBU 00a ESCC invoke result: version:1 response:<status:200 message:"OK" > payload:"\n c\246~\037nW6\264n\342}\310\236N\002D\374}\232G\232\365\331 \217\256\371\366\325\035\007\377\022\267\006\n\240\006\022\205\006\n\006fabcar\022\372\005\032J\n\004CAR0\032B{\"make\":\"Toyota\",\"model\":\"Prius\",\"colour\":\"blue\",\"owner\":\"Tomoko\"}\032G\n\004CAR1\032?{\"make\":\"Ford\",\"model\":\"Mustang\",\"colour\":\"red\",\"owner\":\"Brad\"}\032N\n\004CAR2\032F{\"make\":\"Hyundai\",\"model\":\"Tucson\",\"colour\":\"green\",\"owner\":\"Jin Soo\"}\032N\n\004CAR3\032F{\"make\":\"Volkswagen\",\"model\":\"Passat\",\"colour\":\"yellow\",\"owner\":\"Max\"}\032G\n\004CAR4\032?{\"make\":\"Tesla\",\"model\":\"S\",\"colour\":\"black\",\"owner\":\"Adriana\"}\032K\n\004CAR5\032C{\"make\":\"Peugeot\",\"model\":\"205\",\"colour\":\"purple\",\"owner\":\"Michel\"}\032H\n\004CAR6\032@{\"make\":\"Chery\",\"model\":\"S22L\",\"colour\":\"white\",\"owner\":\"Aarav\"}\032H\n\004CAR7\032@{\"make\":\"Fiat\",\"model\":\"Punto\",\"colour\":\"violet\",\"owner\":\"Pari\"}\032J\n\004CAR8\032B{\"make\":\"Tata\",\"model\":\"Nano\",\"colour\":\"indigo\",\"owner\":\"Valeria\"}\032M\n\004CAR9\032E{\"make\":\"Holden\",\"model\":\"Barina\",\"colour\":\"brown\",\"owner\":\"Shotaro\"}\022\026\n\004lscc\022\016\n\014\n\006fabcar\022\002\010\001\032\003\010\310\001\"\r\022\006fabcar\032\0031.0" endorsement:<endorser:"\n\007Org1MSP\022\226\006-----BEGIN CERTIFICATE-----\nMIICGjCCAcCgAwIBAgIRAPlwF/rUZUP9mqN4wSml4iswCgYIKoZIzj0EAwIwczEL\nMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcTDVNhbiBG\ncmFuY2lzY28xGTAXBgNVBAoTEG9yZzEuZXhhbXBsZS5jb20xHDAaBgNVBAMTE2Nh\nLm9yZzEuZXhhbXBsZS5jb20wHhcNMTcwODMxMDkxNDMyWhcNMjcwODI5MDkxNDMy\nWjBbMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMN\nU2FuIEZyYW5jaXNjbzEfMB0GA1UEAxMWcGVlcjAub3JnMS5leGFtcGxlLmNvbTBZ\nMBMGByqGSM49AgEGCCqGSM49AwEHA0IABHihxW6ks3B2+5XdbAVq3CBgxRRRZ22x\nzzpqnD86nKkz7fBElBuhlXl2K6rTxyY2OBOB0ts8keqZ93xueRGymrajTTBLMA4G\nA1UdDwEB/wQEAwIHgDAMBgNVHRMBAf8EAjAAMCsGA1UdIwQkMCKAIEI5qg3Ndtru\nuLoM2nAYUdFFBNMarRst3dusalc2Xkl8MAoGCCqGSM49BAMCA0gAMEUCIQD4j0Rn\ne1rrd0FSCzsR6u+IuuPK5dI/kR/bh7+VLf0TNgIgCfUtkJvfvzVEwZLFoFyjoHtr\ntvwzNUS1U0hEqIaDeo4=\n-----END CERTIFICATE-----\n" signature:"0D\002 \003\034\340\201\350K\3347\234G\224\025\234\342\202\246K\210\222e\251'\356\202q6o\266\021j\035\375\002 %\021\272\367geA\333Sf\247DE\262\223\253\215.\032X\362G+\030?\007\037o\201\214\257\341" >
2018-06-25 04:28:52.905 UTC [chaincodeCmd] chaincodeInvokeOrQuery -> INFO 00b Chaincode invoke successful. result: status:200
2018-06-25 04:28:52.905 UTC [main] main -> INFO 00c Exiting.....

Total setup execution time : 38 secs ...


Start by installing required packages run 'npm install'
Then run 'node enrollAdmin.js', then 'node registerUser'

The 'node invoke.js' will fail until it has been updated with valid arguments
The 'node query.js' may be run at anytime once the user has been registered

root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# npm install
npm WARN fabcar@1.0.0 No repository field.

up to date in 2.529s
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# node enrollAdmin.js
 Store path:/data/hyperledger/fabric-samples/fabcar/hfc-key-store
Successfully enrolled admin user "admin"
Assigned the admin user to the fabric client ::{"name":"admin","mspid":"Org1MSP","roles":null,"affiliation":"","enrollmentSecret":"","enrollment":{"signingIdentity":"c8a836e75a8173c21c738c068a525eed4f378ee5e41bd72c6825039b1db6b07c","identity":{"certificate":"-----BEGIN CERTIFICATE-----\nMIICATCCAaigAwIBAgIUROEwqUlLc0jOePOse47CBBZdOPQwCgYIKoZIzj0EAwIw\nczELMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcTDVNh\nbiBGcmFuY2lzY28xGTAXBgNVBAoTEG9yZzEuZXhhbXBsZS5jb20xHDAaBgNVBAMT\nE2NhLm9yZzEuZXhhbXBsZS5jb20wHhcNMTgwNjI1MDQyNjAwWhcNMTkwNjI1MDQz\nMTAwWjAhMQ8wDQYDVQQLEwZjbGllbnQxDjAMBgNVBAMTBWFkbWluMFkwEwYHKoZI\nzj0CAQYIKoZIzj0DAQcDQgAE5II97RjrPNTiq8mOdDJU/kFCE8S/XRvcZiPFkDjf\nUegeDNuQB/0LD9VR/wwNZ52KKSlKSv/hwFpMHmuF2K89haNsMGowDgYDVR0PAQH/\nBAQDAgeAMAwGA1UdEwEB/wQCMAAwHQYDVR0OBBYEFMV+6LJz2oqRAC6B0AStG7Cb\n9RBkMCsGA1UdIwQkMCKAIEI5qg3NdtruuLoM2nAYUdFFBNMarRst3dusalc2Xkl8\nMAoGCCqGSM49BAMCA0cAMEQCIDfEIDKT/IUsHY7wiSzcjskbeOgZtS12LzUFUQBH\nu0GbAiBGVWImzhJyneetE9zSw7cb+D0M3Wrxf/L+SyfY2fuqug==\n-----END CERTIFICATE-----\n"}}}
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# node registerUser
 Store path:/data/hyperledger/fabric-samples/fabcar/hfc-key-store
Successfully loaded admin from persistence
Successfully registered user1 - secret:wyAVzmdGtEAM
Successfully enrolled member user "user1"
User1 was successfully registered and enrolled and is ready to intreact with the fabric network
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# ls
enrollAdmin.js  invoke.js     package.json       query.js         startFabric.sh
hfc-key-store   node_modules  package-lock.json  registerUser.js
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# cd hfc-key-store/
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar/hfc-key-store# ls
77d62ff0ee91e5e74b59949999a0352ede4d4f0d53c7c578d310d5448a18b6bb-priv
77d62ff0ee91e5e74b59949999a0352ede4d4f0d53c7c578d310d5448a18b6bb-pub
admin
c8a836e75a8173c21c738c068a525eed4f378ee5e41bd72c6825039b1db6b07c-priv
c8a836e75a8173c21c738c068a525eed4f378ee5e41bd72c6825039b1db6b07c-pub
user1
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar/hfc-key-store# node query.js
module.js:549
    throw err;
    ^

Error: Cannot find module '/data/hyperledger/fabric-samples/fabcar/hfc-key-store/query.js'
    at Function.Module._resolveFilename (module.js:547:15)
    at Function.Module._load (module.js:474:25)
    at Function.Module.runMain (module.js:693:10)
    at startup (bootstrap_node.js:191:16)
    at bootstrap_node.js:612:3
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar/hfc-key-store# cd ..
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# node query.js
Store path:/data/hyperledger/fabric-samples/fabcar/hfc-key-store
Successfully loaded user1 from persistence
Query has completed, checking results
Response is  [{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},{"Key":"CAR1", "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},{"Key":"CAR2", "Record":{"colour":"green","make":"Hyundai","model":"Tucson","owner":"Jin Soo"}},{"Key":"CAR3", "Record":{"colour":"yellow","make":"Volkswagen","model":"Passat","owner":"Max"}},{"Key":"CAR4", "Record":{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}},{"Key":"CAR5", "Record":{"colour":"purple","make":"Peugeot","model":"205","owner":"Michel"}},{"Key":"CAR6", "Record":{"colour":"white","make":"Chery","model":"S22L","owner":"Aarav"}},{"Key":"CAR7", "Record":{"colour":"violet","make":"Fiat","model":"Punto","owner":"Pari"}},{"Key":"CAR8", "Record":{"colour":"indigo","make":"Tata","model":"Nano","owner":"Valeria"}},{"Key":"CAR9", "Record":{"colour":"brown","make":"Holden","model":"Barina","owner":"Shotaro"}}]
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# vim invoke.js
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# ^C
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# node invoke.js
Store path:/data/hyperledger/fabric-samples/fabcar/hfc-key-store
Successfully loaded user1 from persistence
Assigning transaction_id:  3b743e913b2f7326e6232bca9f0e09d460f436c29628cf5121e84fe91aa94ed1
Transaction proposal was good
Successfully sent Proposal and received ProposalResponse: Status - 200, message - "OK"
The transaction has been committed on peer localhost:7053
Send transaction promise and event listener promise have completed
Successfully sent transaction to the orderer.
Successfully committed the change to the ledger by the peer
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar# node query.js
Store path:/data/hyperledger/fabric-samples/fabcar/hfc-key-store
Successfully loaded user1 from persistence
Query has completed, checking results
Response is  [{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},{"Key":"CAR1", "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},{"Key":"CAR10", "Record":{"colour":"Red","make":"Chevy","model":"Volt","owner":"Nick"}},{"Key":"CAR2", "Record":{"colour":"green","make":"Hyundai","model":"Tucson","owner":"Jin Soo"}},{"Key":"CAR3", "Record":{"colour":"yellow","make":"Volkswagen","model":"Passat","owner":"Max"}},{"Key":"CAR4", "Record":{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}},{"Key":"CAR5", "Record":{"colour":"purple","make":"Peugeot","model":"205","owner":"Michel"}},{"Key":"CAR6", "Record":{"colour":"white","make":"Chery","model":"S22L","owner":"Aarav"}},{"Key":"CAR7", "Record":{"colour":"violet","make":"Fiat","model":"Punto","owner":"Pari"}},{"Key":"CAR8", "Record":{"colour":"indigo","make":"Tata","model":"Nano","owner":"Valeria"}},{"Key":"CAR9", "Record":{"colour":"brown","make":"Holden","model":"Barina","owner":"Shotaro"}}]
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/fabcar#

```
