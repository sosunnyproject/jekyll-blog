### 블록체인
- 분산 원장 기술, 암호화 기술, 암호화폐

### 비트코인 블록 구성 개념 p.9 : Pre-Hash, Tx_Root, TimeStamp, Nonce
- PoW: 해싱작업 - Pre-Hash, UTXO + Nonce 새로운 블록 해시값을 계산해서 목표값과 비교하는 과정
  - 목표값을 찾게 되면 블록을 발행하고 네트워크에 전파한다.
  - 채굴: 해싱작업을 통해 임의로 나오는 값을 목표값과 대조해보는 작업

### 비트코인 논란: 마이닝 풀
- 채굴 노드 51% 이상을 특정 집단이 차지하게 되면 비트코인 블록체인의 장부 조작 가능
- 상위 3개사가 약 50%를 차지, 상위 5개사가 약 70% 차지 (p.11, 김열매)
- 기업화된 마이닝 풀: 수수료 수익도 얻음. 
- 게임 이론상, 조작해서 얻는 이익보다 비용이 크다. 비트코인의 신뢰를 무너뜨리면 본인이 갖고 있는 비트코인도 무용지물이 될 것. 
- 퍼블릭 블록체인에 제기되는 리스크 요인: 51% 공격 가능성

- 비트코인 캐쉬/ 비트코인 코어: 하트포크 진영, 
  - 너나 너나 이익 챙기려는 거 아냐?
  - 커뮤니티의 중요성..

### 이더리움
- 비탈릭 뷰테린
- World COmputer: 탈중앙화된 최초의 월드 컴퓨터
- 오픈 소스 공개 프로젝트
- Ethash PoW: 처리속도 빠름,
- 비트코인은 결제 기능만, 이더리움은 앱도 올리고 가치도 교환하는 플랫폼.
- 크립토키티의 특징: ERC 721, 저작권에 대한 아이디어까지 확장 가능

### 블록체인 종류 (~p.25)
1. 퍼블릭:자발적 참여, 인센티브로 암호화폐 필수, 거래 검증 노드(참여자)는 분산된 하나의 서버로 제공하니 전기요금 발생 , 자발적 참여자가 많아야 거래 검증의 신뢰 확보 가능, 거래 속도 느림 - 소프트웨어로만 다수의 참여자의 거래 진위 검증, 
2. 프라이벳: 중앙 관리 조직, 소유자 존재, 허가된 참여자만 참여, 참여자 간 식별 가능, 특화된 데이터 공유 가능, 처리속도 개선, 기업형 블록체인, 인트라넷과 비슷한 개념, 나스탁 시범사업: Linq 도입, 투명성/탈중앙화 사라짐, 암호화폐가 불필요한 프라이빗 블체는 결국 단순 분산형 데이터베이스 수준
3. 컨소시움: 미리 선정된 노드들이 권한을 가지게 된다. 분산형 구조를 유지, 제한된 참여통해 보안 강화, 네트워크 확장성/느린 거래 속도 문제 해소, 은행들 간의 트랜잭션 용도, Corda / Hyperledger 대표적. R3CEV - 금융산업 내 블체 기술 표준화 목표, Corda 플랫폼에는 암호화폐 존재 안함, 스마트 컨트랙트 담은 DApp 구현 가능, 

### 인터체인
1. 이걸 이어주는 게 인터체인
2. cosmos 주목
3. tendermint 방식 (https://blog.cosmos.network/tendermint-explained-bringing-bft-based-pos-to-the-public-blockchain-domain-f22e274a0fdb)


### 커뮤니티, 후원자, 사람들
- 비트코인: 커뮤니티
- 이더리움: 비탈릭 뷰테린
- EOS: 이더리움 개발자들, 밋업: 강남에 건물 두채..
- Steemit: 댄 프리머는 EOS로 byebye
- 크립토 키티 투자자: Andressen Horowitz, Union Square Ventures 

### Fortune article
- Buterin: barcelon with cryptoanarchists - meh, we need economic incentives

- https://media.consensys.net/
- http://www.ether.camp/
- https://www.augur.net/

### “10 years from now, 7-year-olds will understand what a public-private key pair is — or at least how to use them.”
- https://media.consensys.net/trusets-greg-taschuk-on-web3-game-theory-and-bootstrapping-networks-73525057ab7d


### 인터블록체인
- 인터체인: 인터넷의 블록체인 버전. 서로 다른 블록체인들을 연결하는 블록체인 네트워크
    - 여러 기업이 다른 체인/토큰을 쓰고 있어도 트레이딩 및 연동 가능케 하는 크로스브릿지 기술
- 크로스브릿지 기술: 다른 체인들끼리 토큰화된 자산을 트레이딩
- 이더리움 + 하이퍼레져
    - 이더리움: PoW 합의, 장부, 프라이벳 퍼미션 반드시 필요, 노드에 기능별로 역할 지정 가능
    - Hyperledger: consensus – transaction level, 프라이벳 퍼미션 반드시 필요, 노드에 기능별로 역할 지정 가능
- HyperLedger Burrow: Permissioned 이더리움 스마트 계약 블록체인 노드. Tendermint 합의 엔진 결합. 멀티 체인 가능성 지향.
- HyperLedger Sawtooth 플랫폼을 위한 Ethereum: Seth 프로젝트 리뷰
- InterChain Foundation의 프로젝트: Cosmos
    -   InterChain은 서로 다른 체인, 토큰 간의 상호 운용성을 위함
    -   IBC 프로토콜 및 AION, ICON, COSMOS 등 현시점의 인터체인 기술 분석
        - IBC: Inter-blockchain Communication 프로토콜은 가상의 UDP, TCP 역할을 한다고 볼 수 있다. 

- Reference
    - https://medium.com/@matthewminseokkim/comparison-analysis-for-interchain-bd59a8c582e1
    - https://medium.com/@matthewminseokkim/%EC%9D%B8%ED%84%B0%EC%B2%B4%EC%9D%B8-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%B9%84%EA%B5%90-2f1251163c1e
    - https://medium.com/balance-io/what-is-the-interchain-799b187735de
    - https://blog.cosmos.network/the-internet-of-blockchains-how-cosmos-does-interoperability-starting-with-the-ethereum-peg-zone-8744d4d2bc3f
    - https://medium.com/@philippsandner/comparison-of-ethereum-hyperledger-fabric-and-corda-21c1bb9442f6 
    - http://explore-ip.com/2017_Comparison-of-Ethereum-Hyperledger-Corda.pdf 
    - https://www.altoros.com/blog/hyperledger-incubation-burrow-integrates-permissioned-ethereum-virtual-machine/
    - https://www.hyperledger.org/blog/2017/08/22/hello-world-meet-seth-sawtooth-ethereum
    - https://github.com/hyperledger/sawtooth-seth
    - https://www.altoros.com/blog/ethereum-blockchain-technology-enters-hyperledger-picture/
    - https://blog.cosmos.network/etgate-md-6a31f049a62f
    - https://www.coindesk.com/vitalik-buterin-addresses-hyperledger-possible-ethereum-integration/
    - https://brunch.co.kr/@helloiconworld/57




