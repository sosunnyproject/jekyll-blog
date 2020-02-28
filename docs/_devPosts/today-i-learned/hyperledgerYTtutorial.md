# Hyperledger Fabric Dev Reference

## 1. [Architecture](https://hyperledger-fabric.readthedocs.io/en/release-1.2/arch-deep-dive.html)

- 트랜잭션
  - Deploy = 설치
  - Invoke = 실행

- [블록체인 데이터 구조](https://hyperledger-fabric.readthedocs.io/en/release-1.2/arch-deep-dive.html#blockchain-datastructures)
  - State (선택사항) : state 형태는 key-value store. 체인코드는 put, get 사용. state는 peer에 의해서 업뎃/관리됨.
  - Ledger : 모든 성공적인 state 업데이트(유효한 트랜잭션)에 대해서만 기록된 원장. 모든 Peer는 반드시 레져를 가짐. PeerLedger (유효/무효한 트랙잭션 구별해서 기록), OrdererLegder

- Node 노드
  - Client
  - Peer
  - Orderer

- 트랜잭션 Workflow
  - Client가 tx 발생시킴: tx 안에 열심히 싸인해서 보냄
  - endorsing peer를 거친다. 트랜잭션을 검증하는 애들.
  - endorse 검증을 다 끝났으면 client로 다시 돌아감. client는 트랜잭션 검증서류들 콜렉션해서 챙김.
  - client는 이 collection을 Orderer한테 보낸다. 
  - Orderer가 검증한다 -- (잔고 문제 없고..검증되면..) endorsement 순서 세워서 peer들에게 broadcast
  - [내용 디테일](https://hyperledger-fabric.readthedocs.io/en/release-1.2/arch-deep-dive.html#the-client-creates-a-transaction-and-sends-it-to-endorsing-peers-of-its-choice)


## 2. [Tutorial](https://hyperledger-fabric.readthedocs.io/en/release-1.2/tutorials.html)

### [Tutorial 과정 해설 (1)](http://hyperledger-dwmeetup.mybluemix.net/tutorial1.html)

### 0 . **Generate Network Artifacts**

0 . DOWNLOADING `curl ~~하이퍼레져 부트스트랩/샘플~~`: fabric-binaries 다운로드. ca, orderer, java-env, 도커 이미지들 다운로드

0 - 1. RUNNING `byfn.sh` : 네트워크 구조 체크 과정

  - `$ ./byfn.sh -m generate`: mychannel 채널에서 certificate + genesis block 생성
  - `$ ./byfn.sh -m up` : 채널 생성 후 start 하는 명령어
    - volume 생성, peer 생성, orderer 생성...
    - 필요한 Node 들을 docker container로 만들어서 올려주는 역할
    - 채널에다가 peer 조인시키고, 체인코드 쿼리 인보크 테스트 등등 
    - 내 채널에서 hyperledger fabric 돌아갈 수 있는지 확인하는 과정이라고 생각하기.
    - `$ ./byfn.sh -m down` : docker ps 에 있던 것들 다 지우기

0 - 2. 다 지우고 다시..

### 1 . **Crypto Generator**
  
1 - 1. `$ ../bin/cryptogen generate --config=./cypto-config.yaml`
    
  - **목적: crypto-config.yaml 설정대로 crypto-config 폴더 생성.**
  - `./byfn` 에 있는 설명 참조
  > Cryptogen consumes a file ``crypto-config.yaml`` that contains the network topology and allows us to generate a library of certificates for both the Organizations and the components that belong to those Organizations. 
  - `crypto-config` 폴더: client key, cert, admincerts ... 등! 
    - ex) Orderer Organizations의 example.com 폴더 >> ca, msp, admincerts 등 생성.
  - (아직까진 Peer들이 사용할 인증서 만들어주는 단계)
  
1 - 2. `$ ../bin/configtxgen -profile TwoOrgsOrdererGenesis -outputBlock ./channel-artifacts/genesis.block` 
  
  - **목적: 채널에 필요한 제네시스 블록 생성**
  - TwoOrgs 라는 Profile 구성으로... 
  - 이거 돌리고나면, `/channel-artifacts/genesis.block` 생겨져 있음.

### 2 . **Create a Channel Configuration Transaction** (Crypto 만들어졌으니, 채널 Configuration)
2- 1. `$ export CHANNEL_NAME=mychannel  && ../bin/configtxgen -profile TwoOrgsChannel -outputCreateChannelTx ./channel-artifacts/channel.tx -channelID $CHANNEL_NAME`

  - **목적: 채널 생성**
  - `channel_name` 지정
  - **configtxgen** 이 (Profile: TwoOrg 채널 -- 앞에서 지정한 구조대로) **채널 생성**
  - `/channel-artifacts/channel.tx` mychannel 생성
  
2 - 2. `$ ../bin/configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org1MSPanchors.tx -channelID $CHANNEL_NAME -asOrg Org1MSP`
, `$ ../bin/configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org2MSPanchors.tx -channelID $CHANNEL_NAME -asOrg Org2MSP`
  - **목적: 앵커 피어 생성**
  - Org1MSP의 anchor
  - mychannel의 Org1MSP 피어들이 전부 다 join을 해야하니까, 그 때 필요할 것을 만드는 것.
  - `/channel-artifacts/Org1MSPanchors.tx, Org2MSPanchors.tx` 생성 

### *이제 네트워크 시작될 준비가 되었다*
```
$ ls channel-artifacts
$ channel.tx   genesis.block    Org1MSPanchors.tx   Org2MSPanchors.tx
```

### 3. **Start the Network**
3 - 1. `docker-compose -f docker-compose-cli.yaml up -d`

  - **목적: 네트워크 시작**
  - `docker-compose-cli.yaml`: one ORDERER, two PEERS for ORG1, two PEERS for ORG2, CLI 컨테이너 띄움

~~유튜브 1시간 6분~~

### 4. INSTALLING & STATING 체인코드 
### 5. QUERY, INVOKE 체인코드

### [Tutorial 과정 해설 (2)](http://hyperledger-dwmeetup.mybluemix.net/tutorial2.html)
