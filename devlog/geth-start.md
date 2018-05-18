
## 윈도우 환경: 초기에 geth 빌드/컴파일하기
- [이더리움웹사이트](https://ethereum.github.io/go-ethereum/downloads/) 에서 윈도우용 exe 파일을 다운로드 한다.
- 설치 후, geth.exe 가 있는 디렉토리로 들어간다. 
> 내 컴의 경우, mingw64, git, golang (고랭은 이클립스 환경으로) 이미 예전에 다 깔아둔 상태였다. GOPATH 에 원래 eclipse용 go workspace 패쓰 변수가 있었는데, 우선 geth 하는 동안은 지워 놓음.
```bash
C:\Program Files\GethTest\Geth > geth version

Geth
Version: 1.8.8-stable
Git Commit: 2688dab48c9b8ae71b8d95c7678817eaa17f2b53
Architecture: amd64
Protocol Versions: [63 62]
Network Id: 1
Go Version: go1.10.1
Operating System: windows
GOPATH=C:\Program Files\GethTest;
GOROOT=C:\Go\
```

- windows 에서는 **$ make path** 빌드 명령어가 안됨
  - https://github.com/ethereum/go-ethereum/wiki/Installation-instructions-for-Windows 에서
    - `C:\Users\xxx> cd src\github.com\ethereum\go-ethereum` 랑 `C:\Users\xxx> go get -u -v golang.org/x/net/context` 이 두 마지막 줄 참고
    - 그리고 컴파일은 가장 마지막 커맨드 `C:\.... > go install -v ./cmd/...`
      - 이게 **리눅스 make path** 대신에 **윈도우** 에서 쓸 명령어

## data_testnet 디렉토리 : 송수신 블록 데이터, 계정 정보 저장할 디렉토리

1. data_testnet 디렉토리 만들고
2. genesis.json으로 genesis block 만드려는데 
3. **에러** 결과

```bash
 C:\Program Files\GethTest\Geth>geth --datadir "C:\data_testnet" init "C:\data_testnet\genesis.json"
INFO [05-18|14:35:27] Maximum peer count                       ETH=25 LES=0 total=25
INFO [05-18|14:35:27] Allocated cache and file handles         database=C:\\data_testnet\\geth\\chaindata cache=16 handles=16
Fatal: Failed to write genesis block: genesis has no chain configuration
```
4. genesis.json에 **config** 부분이 없었던 게 문제
> 이 때, 나의 genesis.json 은 Geth 디렉토리에 있는게 아님. geth 명령어를 실행하기 위해 geth.exe가 있는 디렉토리에서 genesis.json을 부르는 거임
5. 나의 genesis.json 결과물: **"config"** 부분이 없었다가 에러나서 넣어봤음. 
    - 관련 깃헙 이슈 신고 히스토리: https://github.com/ethereum/go-ethereum/issues/14356

6. config 에러 안나는 genesis.json의 올바른 예
```json
{    
    "config": {
            "chainId": 0,
            "homesteadBlock": 0,
            "eip155Block": 0,
            "eip158Block": 0
        },

    "nonce": "0x0000000000000042",
    "timestamp": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "gasLimit": "0x8000000",
    "difficulty": "0x4000",
    "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "coinbase": "0x3333333333333333333333333333333333333333",
    "alloc": {}
}
```
7. Genesis block 만들기 **성공** 터미널 결과
```bash
C:\Program Files\GethTest\Geth>geth.exe --datadir "C:\data_testnet" init "C:\data_testnet\genesis.json"

INFO [05-18|14:44:01] Maximum peer count                       ETH=25 LES=0 total=25
INFO [05-18|14:44:01] Allocated cache and file handles         database=C:\\data_testnet\\geth\\chaindata cache=16 handles=16
INFO [05-18|14:44:01] Writing custom genesis block
INFO [05-18|14:44:01] Persisted trie from memory database      nodes=0 size=0.00B time=0s gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [05-18|14:44:01] Successfully wrote genesis state         database=chaindata                         hash=7b2e8b…7e0432
INFO [05-18|14:44:01] Allocated cache and file handles         database=C:\\data_testnet\\geth\\lightchaindata cache=16 handles=16
INFO [05-18|14:44:01] Writing custom genesis block
INFO [05-18|14:44:01] Persisted trie from memory database      nodes=0 size=0.00B time=0s gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [05-18|14:44:01] Successfully wrote genesis state         database=lightchaindata                         hash=7b2e8b…7e0432
```

### data_testnet 디렉터리 내부 상황 확인해보기

```bash
C:\>tree data_testnet /a /f
폴더 PATH의 목록입니다.
볼륨 일련 번호가 00000145 32CB:3CE9입니다.
C:\DATA_TESTNET
|   genesis.json
|
+---geth
|   +---chaindata
|   |       000012.log
|   |       CURRENT
|   |       LOCK
|   |       LOG
|   |       MANIFEST-000013
|   |
|   \---lightchaindata
|           000001.log
|           CURRENT
|           LOCK
|           LOG
|           MANIFEST-000000
|
\---keystore
```

## Welcome to Geth JS console

```bash
C:\Program Files\GethTest\Geth>geth --networkid 4649 --nodiscover --maxpeers 0 --datadir "C:\data_testnet" console 2>> "C:\data_testnet\geth.log"

Welcome to the Geth JavaScript console!

instance: Geth/v1.8.8-stable-2688dab4/windows-amd64/go1.10.1
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0
```

## 계정 만들기

- EOA: Geth js console에서 만듦

```bash
C:\Program Files\GethTest\Geth>geth --datadir "C:\data_testnet" account list
INFO [05-18|16:48:47] Maximum peer count                       ETH=25 LES=0 total=25
Account #0: {a5a7c35d52b1d832fea599dc5401a27d2ca005a3} keystore://C:\data_testnet\keystore\UTC--2018-05-18T07-45-30.502448200Z--a5a7c35d52b1d832fea599dc5401a27d2ca005a3
Account #1: {ec1d920c7f28baa4706bc0f59bcb8a77c1c0bac9} keystore://C:\data_testnet\keystore\UTC--2018-05-18T07-46-54.633801900Z--ec1d920c7f28baa4706bc0f59bcb8a77c1c0bac9
Account #2: {f56b29f5cd34150b6ad3f6eb414dbb270eb2310c} keystore://C:\data_testnet\keystore\UTC--2018-05-18T07-48-36.358632000Z--f56b29f5cd34150b6ad3f6eb414dbb270eb2310c
```

## 채굴
- miner.start(1) 혹은 miner.start()를 쳤는데 null 밖에 안나온다.
  - https://ethereum.stackexchange.com/questions/23958/miner-start-is-returning-null-and-mining-is-not-getting-started
  - null이라고 떠도 뒤에서 일하고 있는 것이란다!
  - geth.log 파일을 열어보면 점점 내용이 늘어나는 걸 확인할 수 잇다.

- geth.log 이런 식...
```log
INFO [05-18|16:58:49] Generating DAG in progress               epoch=0 percentage=99 elapsed=3m10.757s
INFO [05-18|16:58:49] Generated ethash verification cache      epoch=0 elapsed=3m10.760s
INFO [05-18|16:58:53] Successfully sealed new block            number=1 hash=d156e9…cf7b90
INFO [05-18|16:58:53] 🔨 mined potential block                  number=1 hash=d156e9…cf7b90
INFO [05-18|16:58:53] Commit new mining work                   number=2 txs=0 uncles=0 elapsed=2.003ms
INFO [05-18|16:58:54] Successfully sealed new block            number=2 hash=b54a13…e1300d
INFO [05-18|16:58:54] 🔨 mined potential block                  number=2 hash=b54a13…e1300d
INFO [05-18|16:58:54] Commit new mining work                   number=3 txs=0 uncles=0 elapsed=4.020ms
INFO [05-18|16:58:54] Successfully sealed new block            number=3 hash=ba1c43…0cbdab
INFO [05-18|16:58:54] 🔨 mined potential block                  number=3 hash=ba1c43…0cbdab
```

