---
title: "hyperLedger: install tutorial"
layout: post
categories:
  - dev
tags:
  - dev
  - hyperledger
  - blockchain
date: 2018-06-10T13:01:27-05:00
last_modified_at: 2018-06-10T13:01:27-05:00
share: false
---

### hyperledger 공식 튜토리얼
- git checkout 1.1.0
- curl -sSL ~~ 1.1.0
- 하니까 계속 안됐음.

### 다른 튜토리얼
- https://medium.com/coinmonks/step-by-step-towards-hyperledger-fabric-part-1-c867fc5fe18
- curl ~~ 1.0.5 : 했더니 first-network 에서 ./byfn.sh -m generate 했을 때, `'' has invalid keys: capabilities` 에러가 자꾸 나서 
  - https://github.com/jcs47/hyperledger-bftsmart/issues/8 참고
  - git checkout 은 안하고 
  - curl ~~ 1.1.0 으로 했음
  - 일단은 설치 되는 중.


```bash
root@ethereum-cluster-1:/data/hyperledger# ls
fabric-samples
root@ethereum-cluster-1:/data/hyperledger# mv fabric-samples/ fabric-samples-1.1.0
root@ethereum-cluster-1:/data/hyperledger# ls
fabric-samples-1.1.0
root@ethereum-cluster-1:/data/hyperledger# git clone https://github.com/hyperledger/fabric-­samples.git
Cloning into 'fabric-­samples'...
fatal: unable to access 'https://github.com/hyperledger/fabric-­samples.git/': The requested URL returned error: 400
root@ethereum-cluster-1:/data/hyperledger# git clone https://github.com/hyperledger/fabric-samples.git
Cloning into 'fabric-samples'...
remote: Counting objects: 1663, done.
remote: Compressing objects: 100% (29/29), done.
remote: Total 1663 (delta 10), reused 23 (delta 2), pack-reused 1632
Receiving objects: 100% (1663/1663), 605.72 KiB | 0 bytes/s, done.
Resolving deltas: 100% (800/800), done.
Checking connectivity... done.
root@ethereum-cluster-1:/data/hyperledger# cd fabric-samples
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# curls -sSL https://goo.gl/byy2Qj | bash -s 1.0.5No command 'curls' found, did you mean:
 Command 'curl' from package 'curl' (main)
curls: command not found
root@ethereum-cluster-1:/data/hyperledger/fabric-samples# curl -sSL https://goo.gl/byy2Qj | bash -s 1.0.5 ===> Downloading platform binaries
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
Generating certs and genesis block for with channel 'mychannel' and CLI timeout of '10' seconds and CLI delay of '3' seconds
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
2018-06-25 11:07:36.703 KST [common/configtx/tool/localconfig] Load -> CRIT 002 Error unmarshaling config into struct:  4 error(s) decoding:

* '' has invalid keys: capabilities
* 'Profiles[TwoOrgsChannel].Application' has invalid keys: Capabilities
* 'Profiles[TwoOrgsOrdererGenesis]' has invalid keys: Capabilities
* 'Profiles[TwoOrgsOrdererGenesis].Orderer' has invalid keys: Capabilities
+ res=1
+ set +x
Failed to generate orderer genesis block...
root@ethereum-cluster-1:/data/hyperledger/fabric-samples/first-network# ./byfn.sh -m generate
Generating certs and genesis block for with channel 'mychannel' and CLI timeout of '10' seconds and CLI delay of '3' seconds
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
2018-06-25 11:08:06.060 KST [common/configtx/tool/localconfig] Load -> CRIT 002 Error unmarshaling config into struct:  4 error(s) decoding:

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
Generating certs and genesis block for with channel 'mychannel' and CLI timeout of '10' seconds and CLI delay of '3' seconds
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
+ configtxgen -profile TwoOrgsChannel -outputCreateChannelTx ./channel-artifacts/channel.tx -channelID mychannel
2018-06-25 11:16:29.979 KST [common/tools/configtxgen] main -> INFO 001 Loading configuration
2018-06-25 11:16:29.990 KST [common/tools/configtxgen] doOutputChannelCreateTx -> INFO 002 Generating new channel configtx
2018-06-25 11:16:29.990 KST [msp] getMspConfig -> INFO 003 Loading NodeOUs
2018-06-25 11:16:29.991 KST [msp] getMspConfig -> INFO 004 Loading NodeOUs
2018-06-25 11:16:30.032 KST [common/tools/configtxgen] doOutputChannelCreateTx -> INFO 005 Writing new channel tx
+ res=0
+ set +x

#################################################################
#######    Generating anchor peer update for Org1MSP   ##########
#################################################################
+ configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org1MSPanchors.tx -channelID mychannel -asOrg Org1MSP
2018-06-25 11:16:30.068 KST [common/tools/configtxgen] main -> INFO 001 Loading configuration
2018-06-25 11:16:30.079 KST [common/tools/configtxgen] doOutputAnchorPeersUpdate -> INFO 002 Generating anchor peer update
2018-06-25 11:16:30.079 KST [common/tools/configtxgen] doOutputAnchorPeersUpdate -> INFO 003 Writing anchor peer update
+ res=0
+ set +x

#################################################################
#######    Generating anchor peer update for Org2MSP   ##########
#################################################################
+ configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org2MSPanchors.tx -channelID mychannel -asOrg Org2MSP
2018-06-25 11:16:30.111 KST [common/tools/configtxgen] main -> INFO 001 Loading configuration
2018-06-25 11:16:30.123 KST [common/tools/configtxgen] doOutputAnchorPeersUpdate -> INFO 002 Generating anchor peer update
2018-06-25 11:16:30.123 KST [common/tools/configtxgen] doOutputAnchorPeersUpdate -> INFO 003 Writing anchor peer update
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
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
+ peer channel create -o orderer.example.com:7050 -c mychannel -f ./channel-artifacts/channel.tx --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
+ res=0
+ set +x
2018-06-25 02:20:18.662 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
2018-06-25 02:20:18.691 UTC [channelCmd] InitCmdFactory -> INFO 002 Endorser and orderer connections initialized
2018-06-25 02:20:18.894 UTC [main] main -> INFO 003 Exiting.....
===================== Channel "mychannel" is created successfully =====================

Having all peers join the channel...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
+ peer channel join -b mychannel.block
+ res=0
+ set +x
2018-06-25 02:20:18.959 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
2018-06-25 02:20:19.001 UTC [channelCmd] executeJoin -> INFO 002 Successfully submitted proposal to join channel
2018-06-25 02:20:19.001 UTC [main] main -> INFO 003 Exiting.....
===================== peer0.org1 joined on the channel "mychannel" =====================

CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer1.org1.example.com:7051
+ peer channel join -b mychannel.block
+ res=0
+ set +x
2018-06-25 02:20:22.069 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
2018-06-25 02:20:22.109 UTC [channelCmd] executeJoin -> INFO 002 Successfully submitted proposal to join channel
2018-06-25 02:20:22.109 UTC [main] main -> INFO 003 Exiting.....
===================== peer1.org1 joined on the channel "mychannel" =====================

CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org2.example.com:7051
+ peer channel join -b mychannel.block
+ res=0
+ set +x
2018-06-25 02:20:25.176 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
2018-06-25 02:20:25.214 UTC [channelCmd] executeJoin -> INFO 002 Successfully submitted proposal to join channel
2018-06-25 02:20:25.214 UTC [main] main -> INFO 003 Exiting.....
===================== peer0.org2 joined on the channel "mychannel" =====================

CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer1.org2.example.com:7051
+ peer channel join -b mychannel.block
+ res=0
+ set +x
2018-06-25 02:20:28.280 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
2018-06-25 02:20:28.320 UTC [channelCmd] executeJoin -> INFO 002 Successfully submitted proposal to join channel
2018-06-25 02:20:28.320 UTC [main] main -> INFO 003 Exiting.....
===================== peer1.org2 joined on the channel "mychannel" =====================

Updating anchor peers for org1...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
+ peer channel update -o orderer.example.com:7050 -c mychannel -f ./channel-artifacts/Org1MSPanchors.tx --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
+ res=0
+ set +x
2018-06-25 02:20:31.394 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
2018-06-25 02:20:31.409 UTC [channelCmd] update -> INFO 002 Successfully submitted channel update
2018-06-25 02:20:31.409 UTC [main] main -> INFO 003 Exiting.....
===================== Anchor peers for org "Org1MSP" on "mychannel" is updated successfully =====================

Updating anchor peers for org2...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org2.example.com:7051
+ peer channel update -o orderer.example.com:7050 -c mychannel -f ./channel-artifacts/Org2MSPanchors.tx --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
+ res=0
+ set +x
2018-06-25 02:20:34.490 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
2018-06-25 02:20:34.511 UTC [channelCmd] update -> INFO 002 Successfully submitted channel update
2018-06-25 02:20:34.511 UTC [main] main -> INFO 003 Exiting.....
===================== Anchor peers for org "Org2MSP" on "mychannel" is updated successfully =====================

Installing chaincode on peer0.org1...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
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
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
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
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org2.example.com:7051
+ peer chaincode instantiate -o orderer.example.com:7050 --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n mycc -l golang -v 1.0 -c '{"Args":["init","a","100","b","200"]}' -P 'OR        ('\''Org1MSP.peer'\'','\''Org2MSP.peer'\'')'
+ res=0
+ set +x
2018-06-25 02:20:38.249 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2018-06-25 02:20:38.249 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
2018-06-25 02:20:52.876 UTC [main] main -> INFO 003 Exiting.....
===================== Chaincode Instantiation on peer0.org2 on channel 'mychannel' is successful =====================

Querying chaincode on peer0.org1...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
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
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org1MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
CORE_PEER_ID=cli
CORE_LOGGING_LEVEL=INFO
CORE_PEER_ADDRESS=peer0.org1.example.com:7051
+ peer chaincode invoke -o orderer.example.com:7050 --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n mycc -c '{"Args":["invoke","a","b","10"]}'
+ res=0
+ set +x
2018-06-25 02:21:06.954 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2018-06-25 02:21:06.954 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
2018-06-25 02:21:06.963 UTC [chaincodeCmd] chaincodeInvokeOrQuery -> INFO 003 Chaincode invoke successful. result: status:200
2018-06-25 02:21:06.964 UTC [main] main -> INFO 004 Exiting.....
===================== Invoke transaction on peer0.org1 on channel 'mychannel' is successful =====================

Installing chaincode on peer1.org2...
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
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
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
CORE_PEER_TLS_KEY_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.key
CORE_PEER_LOCALMSPID=Org2MSP
CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
CORE_PEER_TLS_CERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/server.crt
CORE_PEER_TLS_ENABLED=true
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
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

```

### fabcar

- npm install grpc
  - gRPC: google cloud RPC package
  - https://www.npmjs.com/package/grpc
  - https://github.com/grpc/grpc