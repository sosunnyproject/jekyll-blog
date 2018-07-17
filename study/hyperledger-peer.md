# HyperLedger Architecture 
[hyperledger-fabric](http://hyperledger-fabric.readthedocs.io/en/release-1.1/peers/peers.html)

## Peers

![img1](http://hyperledger-fabric.readthedocs.io/en/release-1.1/_images/peers.diagram.1.png)

하이퍼레져 패브릭은 chaincode - ledger에 접근할 수 있도록 해주는 코드 - 라는 기술적 개념을 가지고 있다. Smart Contract와 같다. 

Peer 는 ledger와 smart contract(chaincode)를 host 한다. Smart Contract(chaincode)와 ledgers 는 네트워크 상에서 서로서로 공유된 과정들과 정보들을 담고 있다. 

이미지에서 P1, P2, P3는 각각 Smart contract(chaincode)와 ledger의 **인스턴스**를 가지고 있다. 각 Peer는 Smart Contract S1 체인코드를 이용해서 각자가 가지고 있는 ledger L1 에 접근한다. 

Peer는 API를 제공함으로써 관리자와 어플리케이션들이 Peer가 제공하는 서비스와 상호작용할 수 있도록 해준다. 즉, Peer는 host 이기 때문에 관리자와 어플리케이션이 ledgers/chaincodes를 접근하고 싶다면 peer를 항상 통해야만 한다. 

**Applications and Peers**
어플리케이션이 어떻게 Peer와 연결해서 ledger에 접근하는가
1. Ledger-Query interaction
2. Ledger-Update interaction: 하나의 피어가 레져를 업데이트 할 수 없다. 네트워크 상의 다른 피어들의 동의가 필요하다 -- consensus. 그래서 update 트랜잭션은 query 트랜잭션보다 오래걸린다. 

![flowchart](http://hyperledger-fabric.readthedocs.io/en/release-1.1/_images/peers.diagram.6.png)

순서도
1. **A** --> P1 과 연결한다.(ledger query혹은 update를 위해서) 
2-1. P1은 자기에게 속한 S1 체인코드를 깨운다.
2-2. chaincode는 S1 은 query 결과 혹은 잠정적 ledger 업데이트 정보가 담긴 proposal response (잠정적 대답)을 만든다.
3. P1은 이 Proposal response를 **A**에게 보내준다. 
4. Ledger-Update 과정이라면, **A**는 모든 피어에게서 받은 response를 모아서, Orderer O1에게 보낸다. 
4-1. Orderer는 네트워크 전체로부터 받은 트랜잭션 내용을 블락에 담아서, 모든 피어에게 보낸다.
5. P1은 자신의 장부 L1에 이를 반영하기 전에, 트랜잭션 검증을 한번 거친다. 
6. 검증이 완료되고, L1에 반영이 되면, P1은 이벤트를 발생시켜 **A**에게 완료됐다는 걸 알린다.

Update Transaction 에서 차이점
- 하나의 Peer가 ledger update를 하지 못함: 다른 Peer들이 consensus 해줘야 함
- Peer가 application에 update를 보낼때 proposed update를 보냄
- application은 네트워크의 모든 피어에게 matching proposed updates를 보냄
- 그러면 peer들은 각자의 ledger에 committ 하도록.
- orderer를 이용해서 transactions 들을 패키징해서 block에 담는다. 그리고 모든 네트워크의 피어들에게 전송한다.
- 피어들이 받아서 각자의 ledger 카피에 등록하기 전에 검증과정을 거친다.

**Peers and Channels**
- Channel 안에 여러 Peer들이 담겨 있을 수 있다. Orderer도 있다. 
- 채널은 특정 peer 집합들이 어플리케이션들과 한 블록체인 네트워크 안에서 교류할 수 있도록 해준다. 

**Peers and Identity**
- how peers from different organizations come together to form a blockchain network
- how peers get assigned to organizations by their administrators

1. 모든 노드는 각기 디지털 id 증명서같은 것을 부여받는다. 그 피어가 속한 organization의 관리자가 증명서를 발급해준다.
2. 피어가 채널에 연결할 때, 피어의 디지털 신원증명서가 피어가 속한 organization을 **채널 MSP를 통해서** 신원파악한다. 
3. 피어가 달라도 같은 Certificate Authority CA1 에서 발급받았을 수 있다.
4. 채널 C는 ORG1.MSP policy를 기반으로 CA1으로부터 identity를 받은 애들은 Org1에 속해야 되는 걸로 판단한다.

Channel configuration의 policy 가 peer의 신원을 사용해서 그것의 권리를 파악한다. 개별 identity와 속한 organization을 매칭시켜주는 요소는 MSP membership service provider가 맡아서 한다. 
MSP는 이 피어가 어느 organizatio에 어떤 역할로 배정받을지 정한다. 정해지는대로 블록체인 리소스들에 접근할 수 있다.

피어는 하나의 orgniazation에만 속할 수 있으며, 그 말은 즉 하나의 MSP하고만 연결된다. peer 접근 컨트롤에 대해서 더 다룰 것이다. 지금은 우선 MSP를 개인 신원과 특정 조직/조직구성원 간의 관계를 위한 블록체인 네트워크를 연결해주는 고리라고 생각하자.

참고로 피어뿐만 아니라 블록체인 네트워크와 소통하는 모든 존재들은 organizational 소속 신원을 그들의 디지털 신원증명서와 MSP로부터 부여받아야 한다 -- 피어, Applications, end users, administrators, orderers 등

**Peers and Orderers**
- 모든 피어의 ledger가 일정하고 똑같이 유지하기 위해 어플리케이션과 피어가 소통하도록 중개해주는 특별한 노드가 바로 orderer이다.
- ledger를 업데이트 하고 싶어하는 applications들은 3단계를 거친다. 


**Phase 1: Proposal**
- 어플리케이션이 피어에게 transaction proposal을 보내서 endorsement 를 요청한다.
- 피어는 그걸 받아서 chaincode를 발현시키고, 그 proposal에 대한 response를 만든다.
- 이게 바로 ledger에 업데이트되지 않고, 피어는 그 response에 sign 한 다음에 application에게 돌려보낸다.
![phase1-proposal](http://hyperledger-fabric.readthedocs.io/en/release-1.1/_images/peers.diagram.10.png)
- chaincode에 따라서 endorsement policy가 정해진다.
- 이 policy는 승인되기 전에 proposed ledger change를 endorse하는 역할을 해줄 organization 집합들을 간택한다.
- 즉, application들이 peer 집합들을 선택하는데, proposed ledger update를 수행할 peer들을 간택한다는 말과 동일.
- 간택된 모든 organization들은 자기에게 속한 peer들의 ledger에 업데이트를 동기화하기 전에, proposed ledger change를 반드시 endorse 해야한다.
- peer는 proposal response를 endorse 한다: digital signature 싸인하는게 endorse 하는 방법이다.
- peer의 private key를 사용해서 entire payload (트랜잭션 뭉태기)에 싸인한다. 
- 이 endorsement 는 이 org의 peer이 특정한 response를 발생했다는 증거로 기록에 남는다.
- App이 signed proposal response를 충분히 많은 peer들에게서 받으면 phase 1 이 끝난다.
- 거의 발생할 일이 없지만, 중대한 문제점은 chaincode 가 **non-deterministic** 할 때 발생한다.
  - proposal 에 대한 response들이 불일치하면 ledger에 업데이트 될 수 없는데
  - non-deterministic 한 chaincode는 그런 **inconsistency** 를 발생시킨다

**Phase 2: Packaging**
- orderer의 역할이 매우 중요하다
- orderer는 endorsed transaction proposal responses를 담은 transaction를 많은 app으로부터 받는다. 
- 모든 트랜잭션을 모아서 block 에다가 패키징해서 넣는다. 모든 피어들에게 distribute할 준비를 한다.

![phase2](http://hyperledger-fabric.readthedocs.io/en/release-1.1/_images/peers.diagram.11.png)
- orderer 노드의 첫번째 역할은 proposed ledger updates를 패키지하는 것이다.
- orderder의 임무: 동시에 수많은 app들로부터 proposed ledger update를 받으면 그걸 well-defined sequence로 정리하고, (차후에 분배를 위해) blocks 에 패키징해서 담는 것. 
- 트랜잭션이 담기는 순서 규칙이 있긴 한데 항상 같지는 않음 (코딩 하기에 따라 다름)
  - 참고로 다른 블록체인 기술들과 다소 다르게 하이퍼레져 패브릭은 엄격한 트랜잭션 순서 규칙이 있어서 하나의 트랜잭션이 여러 블록에 담기는 일은 없다. 
  - 여러 orderer들에 의해서 블록들이 생성되는 순간 **final** 이다
  - 이렇게 된 이상, 트랜잭션은 ledger에 이미 한 자리를 차지한 것이나 다름 없다. 
  - 흔히 재앙같이 여겨지는 **ledger fork** 사태는 일어나지 않는다. 
  - 한번 블록에 트랜잭션이 포함된 이상, 다시 고쳐쓰거나 변경할 수 없다.
- orderer는 일반 peer 처럼 ledger/chaincode를 host 하지 않고, 오직 블록 패키징만 한다. 

**Phase 3: Validation**
- 모든 레져에 동일하게 (orderer가 만든) 블록이 적용되는 단계
- orderer로부터 peer로 블록 분배 및 검증을 순차적으로 진행한다. 
- 그리고 ledger에 블록들이 들어갈 것이다.
- 각 peer가 받았을 때, 블록 안에 있는 모든 트랜잭션들이 관련된 모든 org로부터 endorse를 받았는지 검증을 받은 다음에야 블록이 ledger에 등록될 수 있다. 

![phase3](http://hyperledger-fabric.readthedocs.io/en/release-1.1/_images/peers.diagram.12.png)
- Orderer 노드의 두번째 역할: 블록을 peer에게 분배한다. 
- 같은 채널에 있는 모든 peer들은 같은 방식으로 orderer로부터 받은 블록을 검증한다. 
  - 그 트랜잭션을 발생시킨 chaincode의 endorsement policy를 기준으로 삼아서, 해당 트랜잭션이 필수적인 org들로부터 endorse를 받았는지 검증한다.
- 목적은 항상 ledger를 동일하게 유지하라.
- 예외) 모든 피어가 orderer에 연결되어 있지 않더라도, **gossip protocol**이란 걸 사용해서 동료 peer로부터 블록을 넘겨받을 수 있다.
- endorse가 정확하게 되었으면 peer는 ledger에 등록하려고 할 것이다. 이걸 위해서는 peer가 반드시 ledger consistency check를 수행해야 한다. ledger의 현재 상태가 proposed update를 하고 나서의 상태와 잘 호환될 수 있도록.
- 설령 트랜잭션들이 검증실패되거나 해서 ledger에 반영이 안되더라도 audit 목적을 위해 (성공한 트랜잭션과 마찬가지로) 기록은 남아 있다
  - 그렇기 때문에 peer 블록들은 orderer로부터 받은 블록들과 그대로 동일하다 -- 블록 안의 각 트랜잭션별로 승인/비승인 여부의 체크결과들만 다르다.
- 중요한 것은 chaincode는 phase1에서만 동작하고 3에서는 안한다는 것.
  - endorsing 주체들에게만 chaincode를 공개하는 꼴이므로 보안의 장점이 있다.
  - chaincode의 output: 트랜잭션 proposal responses 은, 반면, 그 채널의 모든 피어들에게 공유된다.
- peer의 ledger에 block이 커밋 될 때마다 peer는 이벤트를 발생시킨다.
  - block events: 블록 전체 내용
  - block transaction events: 요약 정보만 담겨 있음. 블록의 각 트랜잭션이 검증 성공했는지 실패했는지 내용.

**Orderers and Consensus**
- 이 모든 transaction workflow는 consensus 라고 불린다.


Next...
[Transaction Flow](http://hyperledger-fabric.readthedocs.io/en/release-1.1/txflow.html)