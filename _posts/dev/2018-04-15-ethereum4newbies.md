---
layout: post
categories: dev
title: "이더리움 기초 공부"
date: 2018-04-15T13:01:27-05:00
share: false
---

## 이더리움이 뭔가요? 일반인을 위한 블록체인 강좌 
- 들으면서 필기한 내용
- 영상 출처: [Studio Decentral의 일반인을 위한 블록체인 강좌 block15](https://www.youtube.com/watch?v=uUC3hELa-Oo)
- 이더리움 백서를 봅시다: [영어](https://github.com/ethereum/wiki/wiki/White-Paper#ethereum), [한글](https://github.com/ethereum/wiki/wiki/%5BKorean%5D-White-Paper)
- 비탈릭 뷰테린에 대한 장문 기사 [2016, 영어, Fortune](http://fortune.com/ethereum-blockchain-vitalik-buterin)
  - 내가 Fortune에서 일하던 시절에 유능한 신세대 테크 기자분이 썼던 기사인데, 재밌게 잘 써있음. 영어 읽을 수 있다면 추천.


### 비트코인의 문제점(이자 이더리움이 나오게 된 계기)
- 튜링 불완정성: 아주 단순한 언어, 중요한 단어만 이야기한다. 
- Value-blindness: 한 번에 한 트랙잭션만 가능. 100을 보내고 5를 받아야 하니까 95만 받자, 이런게 아니라 따로따로. (이건 비트코인/블록체인 책에 더 잘 나와있는 듯)
- Lack of state: 상태 저장이 불가능. 계약을 할 때 조건을 걸어서 진행하는 게 힘들다.
- 작업증명방식의 합의 매커니즘: ASIC 채굴장비를 통한 합의 매커니즘은 큰 에너지 소모, 채굴자 중앙화 초래.
- 이더리움은 비트코인의 스크립트 언어의 한계성을 극복하기 위해 시작되었다고 생각하자.

### 비트코인 VS 이더리움
- 화폐만 하지 말고 계약 조건 등 코인 이외의 것도 하자: 스마트 계약
- 이 스마트 계약을 위해서 튜링 완전한 언어가 필요했다.
- 튜링 완전: 복잡한 것을 표현할 수 있는 언어 - 다양한 계약 조건을 구현해야 해서.
- Casper 자산 증명(Proof of Stake)을 목표로 하고 있음

### 이더리움이란? 블록체인 기반의 distributed computing 분산 컴퓨팅 플랫폼
**1. 튜링 완전**

  - 스마트 계약, 분산 어플리케이션을 구현 가능하게 하는 언어
  - 다양한 계약 조건(if문, 시간 조건, 잔고 조건, 트럼프가 당선이 된다면...)을 달 수 있다.
  - 스마트 계약이 블록체인 위에 기록된 이후에는 조건을 바꿀 수 없다.
  - 비트코인은 그 자체로 DAPP (분산 어플리케이션), 드랍박의 DAPP 버젼이 비트토렌트..
  - 이더리움이라는 블록체인 플랫폼 위에 다양한 DAPP을 지을 수 있다. 다양한 스마트 계약을 만들 수 있다.
  - DAPP의 백엔드 코드는 분산화된 P2P 네트워크에서 실행된다.

**2. 이더리움 가상 머신: Ethereum Virtual Machine**

  - world computer라고도 불린다: 전 세계의 모든 참가자(노드)가 동일한 하나의 컴퓨터를 돌리는 것과 같다. 모두가 공유하는 하나의 컴퓨터 (다 똑같은 연산, 똑같은 내용을 저장)
  - 속도/효율성은 떨어지지만, 신뢰를 얻게 될 것
  - 오라클: 인간의 개입 - 어떤 조건을 걸었을 때 그 조건의 참/거짓에 대한 대답을 주는 매개체. '트럼프가 당선이 되었다'는 사실을 누군가는 시스템에 알려줘야 하니까.
  - 다 다른 성능의 컴퓨터들을 합친 개념이니까, 당연히 성능이 떨어진다..
    - 그래서 성능 고도를 위해, 유의미한 수준까지 확장시킬 수 있느냐..? 
      - 비탈릭 뷰테린: casper, sharding 제안
      - 중앙에 있는 이더리움 블록체인의 성능을 최대한 확장시켜서 모든 사람이 쓸 수 있게 할 생각이다.
      
**2-1. 상태 변화 시스템으로서의 비트코인/이더리움**

  - 상태가 변화하는, 내 계좌 금액이 왔다갔다, 
  - 비탈릭 뷰테린: 기존 아이디어를 가지고 와서 추상화시키고 개념화하는 걸 잘함.
  - 상태: 블록 하나하나 말고, 블록 체인 - 블록들이 연결되어 있는 큰 박스를 볼 것.
    - state1: [ㅁ-ㅁ-ㅁ], state2: [ㅁ-ㅁ-ㅁ-ㅁ] 
    - state1 --> 블록 하나 추가 --> state2
    - 이걸 상태 변화라고 생각.
    - 블록을 단순 데이터의 집합이 아니라 state transition function 상태 변화 함수로 생각해라.
    - 블록을 추가하면서 상태가 바뀌는 형식이니까.
  - 새로운 블록: 거래들의 내용을 보유. 이 거래 속의 비용이 state1에 업데이트 되면 state2로 상태(계좌 + 계약 상태)가 바뀐다.
  - state: 계좌 + 계약 상태 
    - 계약 상태: 계약 코드, 이더 amount, 데이터를 포함하고 있다.
  
**3. 계좌, 이더, 가스**

  - **이더**: 자체 암호화 화폐 토큰
  - **가스**: 스마트 계약을 돌리기 위해 필요한 연료. 이더로 가스를 구입. 가스로 이더리움의 자원(연산력, 저장공간, 네트워크 사용량)을 사용
  - **외부소유계좌 EOA** : Externally Owned Account
    - 일반적으로 생각하는 내 계좌.
    - public address 이고, 공개 키 기반의 암호화를 사용 (?)
    - private key 개인키를 가지고 통제할 수 있다. 
    
  
  - **계약 계좌 Contract Account**
    
    - 보통 Smart Contract이라고 말하는 게 곧 이 **계약계좌** 를 일컫는 것
    - 계약 내용이 블록체인에 **계약 계좌**로 기록되는 것. 
    - 키로 통제되지 않음.
    - 계약의 코드에 의해서만 통제된다 --> **코드가 곧 법이다** 라는 말이 나온 계기
    - 특정 계약 조건을 만족하면 코드가 무조건 자동으로 실행되는 게 **스마트 컨트랙트**
    - 메시지를 받으면 자기 안에 있는 스마트 컨트랙트 내용을 실행시킨다. 
    - 내부 저장공간에 정보를 읽고, 쓸수 있다. 
      - 개발 관점: OOP에서 class 개념
      - class에 있는 정보들을 밖에서 접근을 했을 때, 내부 절차들을 통해서 class 속성을 업데이트 시켜주듯이 계좌의 속성을 업데이트 시킨다고 생각하기.
  
```
- Externally Owned Account: code activation (x), value transfer (o)
- 모든 transaction은 EOA --> EOA, EOA --> Contract Account로
  - 시작은 무조건 EOA 맞을거임.
- 계정과 계정 간의 거래 : 외부적으로 보면 그냥 계정
- 계약의 경우: 컨트랙 짜서 올리면 컨트랙 어드레스가 나옴
```
  
  - **계좌 구조**
    - 난스/논스 nonce
    - 이더량 ether balance: EOA, Contract Account 둘 다 이더량은 있다.
    - 계약 코드 contract code: 계약 계좌만 가지고 있다.
    - 저장공간 storage: 계약 계좌만 가지고 있다.   
    
  - **가스, 이더리움, 자원, 연료**
    - 중복성 redundancy 이 높다.
    - 공유지의 비극: 사용할 수 잇는 자원에 한계가 있다. 
      - 막기위해, 한정된 자원에 비용을 매길 필요가 있다.
      - 이더리움의 연산력을 사용하기 위해 특정 댓가를 지불해야 하기 위해: 가스 gas가 필요하다
    - 비트코인의 한정된 자원: 블록 사이즈. `비트코인 : 블록 사이즈 = 이더리움 : 가스 총량`
    - 이더리움의 한정된 자원: 가스 총량. 연산력.
      - 왜 이더로 자원의 댓가를 지불하지 않고, 가스로 해?
        - 전기의 kW와 같은 개념: kW와 kW에 대한 가격은 다르게 책정.
        - 연산력의 시장가와 연산력 측정 단위를 분리. 
        - 튜링 완전: 코드만 보고는 이 계약이 끝날지 말지, 무한 루프 돌지 말지 모를 수 있음: halting problem
        - 무한 루프 방지 위해, 특정 양의 연산을 했을 때는 gas가 고갈되도록.
          
**3-1. 이더리움은 본인들이 인터넷이라고 생각. 자신의 플랫폼 위에 사람들이 여러 DAPP을 올리는 방식**
  - DApp은 이더리움 블록체인을 사용하기 위해서 Gas를 계속 사용해야 하는 것
  - 프론트엔드에서 사람들에게 어떻게 수급을 할 것인지.
  - 지불된 gas는 노드들에게 거래 수수료로 지급됨 (노드들의 수익)
    
**5. 이더리움 개발단계**
  - 1단계 Frontier : 커맨드라인 인터페이스 CLI
  - 2단계 Homestead: 안전하다 판단. 
  - 3단계 Metropolis: 공식 인터페이스, DApp 스토어 출시
  - 4단계 Serenity: 확장성, 자산증명 개선. 성능 향상. 

**6. DApp 플랫폼의 앱들**
 - augur, Gnosis: 스마트 컨트랙트. 오라클이 중요. 예측 시장 조건을 사용하는 애들
 - Melonport: 금융 특화, 헤지펀드 - 전략을 블록체인에다가 기록함. 전략에 대한 수익구조, 조건을 다 볼 수 있음. 자산관리의 투명   
 - Iconomi: Melonport랑 비슷한데 ICO에 집중
 - DGix: 금이랑 블록체인
 - golem: 스마트 컨트랙트. 연산력을 얼마 제공하면 댓가로 golem 네트워크 토큰을 얼마 받는다.
 - SNGULAR: 저작권 보호를 위한 블록체인. 수익이 여기로 들어오면 자동으로 분배. 개별계약/복잡한계약을 간단화
 - STORJ.IO: 내 저장공간 얼마 빌려주고, STORJ 코인 얼마를 받겠다.
 - ARAGON: 주식회사의 주식 자체를 블록체인으로 대취급. 아라곤의 주식의 비율대로 결정을 내릴 수 있다. 수익 배분도 스마트 컨트랙트에 따라서 주주 비율대로 배분
 - patientory: 의료 분야 데이터
 - slock.it : IoT랑 DApp 연결, Airbnb 의 열쇠를  디지털로 바꾼 개념.
 - swarm: 분산화된 방식으로 파일 복구
 - uport: 신원의 블록체인화
 - 기본적인 것은 스마트 컨트랙트, 블록체인 : AI는 드론의 자율주행/ 최적화 거래 / IoT 들과도 다 연결 등.. 결국엔 융합적.