---
title: "Linux"
categories:
  - dev
tags:
  - dev
  - OS
last_modified_at: 2017-03-09T13:01:27-05:00
---

## linux 부팅

1. password 안알려주셔서 reboot.
2. 32bit 뜨악; 다른 건 그렇다치는데, chrome은 32비트 버전이 없다..
3. 인터넷 연결은 아이콘 상단 우측 누르면 connection edit -> ipv4 manual dropdown menu click -> ip, netmask:(자동생성), DNS , GATEWAY 설정해주기
4.  certificate 받아서 책임님 github 내용 보면서 ㅋㅋ 인터넷 성공 https://jinfromkorea.github.io/articles/2017-12/ubuntu

> 이제 node, npm, py, anaconda, visual studio code , chrome 다 다운받아야되 ^^
$ sudo apt-get update 는 덤

## sftp 
```bash
$ sftp sender-ip-address
sftp> cd whatever-directory
sftp> get the-file-you-wanted
sftp> exit
$ cd whatever-directory-you-want
$ mv the-file-you-received ./Downloads/the-file-you-received

or 

$ cp the-file-you-received ./Downloads/the-file-you-received
```
#### sftp between raspberry-pi linux and my linux 
- https://www.codedonut.com/raspberry-pi/set-ssh-sftp-raspberry-pi/
- if filezilla doesn't work - enable ssh again 
- **not sure why i can't do sftp from raspberry pi to my linux tho..** (maybe because it is Ubuntu Desktop, not Server?)

## google-chrome
32bit, i686 에서는 안됨. 64 bit 깔고 했는데도 안됨.
>> google-chrom-stable depends on libappindicator1; however: Package libappindicator1 is not installed.

apt-get install libappindicator1 는 안됨.
```s
$ sudo apt-get install -f 
#했더니 이것저것 다운받네
#그리고 shell command 로 다운로드 실행파일 run 하기
$ sudo dpkg -i google-chrom-stable~~amd64.deb
#드디어된다.
```

## node, npm, git 설치
1. git
```s
$ sudo apt install git
```
2. node, npm
node,npm,yarn 다 안되서 왜이러나 했음..인터넷 certificate 보안 에러였음. 회사 네트워크여서 보안서류 업로드 해줘야함.

  1. internet problem (company network)
      firefox, chrome - certificate upload
      advanced settings --> manage certificates --> authorities tab --> import --> choose --> select all three trust settings
      DONE
  2. command
     여기서부터는 linux 컴에 잇는 linux-install.md 내용
    

linux 설치로 불태운 하루..

하루여서 다행일지도..

linux dual boot 는 집에가서 usb 부터 구워와서 해봐야지..

## mosca, mqtt

```bash
$ sudo pip3 install paho-mqtt
$ sudo npm install mosca pino -g
```
#### python paho-mqtt tutorial
- http://www.steves-internet-guide.com/into-mqtt-python-client/
- http://www.steves-internet-guide.com/client-connections-python-mqtt/
- http://www.steves-internet-guide.com/subscribing-topics-mqtt-client/
- http://www.steves-internet-guide.com/publishing-messages-mqtt-client/

what is suback?
- http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html#_Toc398718068

#### Linux python mqtt

```bash
sosun@poscoict:~$ pip3 install paho-mqtt
Requirement already satisfied: paho-mqtt in /usr/local/lib/python3.5/dist-packages
sosun@poscoict:~$ 
```

#### mosca EADDRINUSE error
> ref: https://stackoverflow.com/questions/9898372/how-to-fix-error-listen-eaddrinuse-while-using-nodejs
```bash
$ killall -9 node
//this will kill all your apps running via terminal
```
## linux and python pip

_Want to make pip point python2, not python3. How do I override?_

계속 pip이 /usr/lib/python3/dist-packages 를 포인트함. 
pip --> python2, pip3 --> python3 가 보통이니까 그렇게 만들고 싶음.

```bash
$ python -m pip install -U --force-reinstall pip 
# 하면 된다는데 나는 안되쟈냐...ㅡㅅㅡ
# /usr/bin/python: No module named pip 

$ sudo python3 -m pip install paho-mqtt
# /usr/bin/python2 : No module named pip
# 또 에러
# 기본적으로 내 명령어는 $ python 하면 python2, $ python3 하면 python3

$ sudo apt-get install python2-setuptools
# 에러 Unable to locate package python2-setuptools

$ sudo apt-get install python-setuptools
# yes working!

$ python
```

## certificate 

#### Checking CURL & .cer .crt certificate issue (company network)
  __before this, my curl -sL ...node.8x... command wasn't doing anything at all..__

```
sosun@poscoict:~$ curl --manual | more
                                  _   _ ____  _
  Project                     ___| | | |  _ \| |
                              / __| | | | |_) | |
                            | (__| |_| |  _ <| |___
                              \___|\___/|_| \_\_____|

NAME
        curl - transfer a URL

SYNOPSIS
        curl [options] [URL...]

DESCRIPTION
        curl  is  a tool to transfer data from or to a server, using one of the
        supported protocols (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS,  IMAP,
        IMAPS,  LDAP,  LDAPS,  POP3,  POP3S,  RTMP, RTSP, SCP, SFTP, SMB, SMBS,
        SMTP, SMTPS, TELNET and TFTP). The command is designed to work  without
        user interaction.

        curl offers a busload of useful tricks like proxy support, user authen-
        tication, FTP upload, HTTP post, SSL connections, cookies, file  trans-
        fer  resume,  Metalink,  and more. As you will see below, the number of
        features will make your head spin!

        curl is powered by  libcurl  for  all  transfer-related  features.  See
        libcurl(3) for details.

URL
        The  URL  syntax is protocol-dependent. You'll find a detailed descrip-
        tion in RFC 3986.

        You can specify multiple URLs or parts of URLs  by  writing  part  sets
        within braces as in:

          http://site.{one,two,three}.com

        or you can get sequences of alphanumeric series by using [] as in:

          ftp://ftp.numericals.com/file[1-100].txt

          ftp://ftp.numericals.com/file[001-100].txt    (with leading zeros)

          ftp://ftp.letters.com/file[a-z].txt

        Nested  sequences  are not supported, but you can use several ones next
        to each other:

          http://any.org/archive[1996-1999]/vol[1-4]/part{a,b,c}.html

        You can specify any amount of URLs on the command line.  They  will  be
        fetched in a sequential manner in the specified order.

        You  can  specify a step counter for the ranges to get every Nth number
        or letter:

          http://www.numericals.com/file[1-100:10].txt

          http://www.letters.com/file[a-z:2].txt

        When using [] or {} sequences when invoked from a command line  prompt,
        you probably have to put the full URL within double quotes to avoid the
        shell from interfering with it. This also  goes  for  other  characters
        treated special, like for example '&', '?' and '*'.

        Provide  the IPv6 zone index in the URL with an escaped percentage sign
        and the interface name. Like in

          http://[fe80::3%25eth0]/

        If you specify URL without protocol:// prefix,  curl  will  attempt  to
        guess  what  protocol  you might want. It will then default to HTTP but
        try other protocols based on often-used host name prefixes.  For  exam-
        ple,  for  host names starting with "ftp." curl will assume you want to
        speak FTP.

        curl will do its best to use what you pass to it as a URL.  It  is  not
        trying  to  validate it as a syntactically correct URL by any means but

sosun@poscoict:~$ curl -L https://deb.nodesource.com/setup_8.x
curl: (60) server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none
More details here: http://curl.haxx.se/docs/sslcerts.html

curl performs SSL certificate verification by default, using a "bundle"
  of Certificate Authority (CA) public keys (CA certs). If the default
  bundle file isn't adequate, you can specify an alternate file
  using the --cacert option.
If this HTTPS server uses a certificate signed by a CA represented in
  the bundle, the certificate verification probably failed due to a
  problem with the certificate (it might be expired, or the name might
  not match the domain name in the URL).
If you'd like to turn off curl's verification of the certificate, use
  the -k (or --insecure) option.
```
이 에러가 바로 인증서 설치 안됐다는 증거..
      
     
```s
sosun@poscoict:~$ ls
Desktop  Documents  Downloads  examples.desktop  Music  Pictures  POSCOICT_CA_256.cer  Public  Templates  Videos
sosun@poscoict:~$ sudo mv ./POSCOICT_CA_256.cer /usr/share/ca-certificates/
sosun@poscoict:~$ cd /usr/share/ca-certificates/
sosun@poscoict:/usr/share/ca-certificates$ ls
mozilla  POSCOICT_CA_256.cer
sosun@poscoict:/usr/share/ca-certificates$ mkdir extra
mkdir: cannot create directory ‘extra’: Permission denied
sosun@poscoict:/usr/share/ca-certificates$ sudo mkdir extra
sosun@poscoict:/usr/share/ca-certificates$ ls -al
total 36
drwxr-xr-x   4 root  root   4096  1월 25 16:22 .
drwxr-xr-x 293 root  root  12288  1월 25 15:27 ..
drwxr-xr-x   2 root  root   4096  1월 25 16:22 extra
drwxr-xr-x   2 root  root  12288  8월  1 20:21 mozilla
-rwxr-xr-x   1 sosun sosun  1112  1월 25 14:14 POSCOICT_CA_256.cer
sosun@poscoict:/usr/share/ca-certificates$ sudo cp ./POSCOICT_CA_256.cer ./extra/POSCOICT_CA_256.crt
sosun@poscoict:/usr/share/ca-certificates$ cd extra/
sosun@poscoict:/usr/share/ca-certificates/extra$ sudo dpkg-reconfigure ca-certificates
Processing triggers for ca-certificates (20160104ubuntu1) ...
Updating certificates in /etc/ssl/certs...
1 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
sosun@poscoict:/usr/share/ca-certificates/extra$ cd ~
```

## Installing Node.js , npm on linux ubuntu at company setting
[Node.js manual](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions)
[jinfromkorea github io manual](https://jinfromkorea.github.io/readme/nodejs.html#nodejs)

```
sosun@poscoict:~$ curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -

## Installing the NodeSource Node.js v8.x repo...

## Populating apt-get cache...

+ apt-get update
Hit:1 http://kr.archive.ubuntu.com/ubuntu xenial InRelease
Hit:2 http://kr.archive.ubuntu.com/ubuntu xenial-updates InRelease                                               
Hit:3 http://kr.archive.ubuntu.com/ubuntu xenial-backports InRelease                                             
Get:4 http://packages.microsoft.com/repos/vscode stable InRelease [2,802 B]                   
Ign:5 http://dl.google.com/linux/chrome/deb stable InRelease                                               
Hit:6 http://security.ubuntu.com/ubuntu xenial-security InRelease       
Get:7 http://dl.google.com/linux/chrome/deb stable Release [1,189 B]    
Get:8 http://packages.microsoft.com/repos/vscode stable/main amd64 Packages [37.5 kB]
Fetched 41.5 kB in 3s (10.8 kB/s)                              
Reading package lists... Done

## Confirming "xenial" is supported...

+ curl -sLf -o /dev/null 'https://deb.nodesource.com/node_8.x/dists/xenial/Release'

## Adding the NodeSource signing key to your keyring...

+ curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -
OK

## Creating apt sources list file for the NodeSource Node.js v8.x repo...

+ echo 'deb https://deb.nodesource.com/node_8.x xenial main' > /etc/apt/sources.list.d/nodesource.list
+ echo 'deb-src https://deb.nodesource.com/node_8.x xenial main' >> /etc/apt/sources.list.d/nodesource.list

## Running `apt-get update` for you...

+ apt-get update
Hit:1 http://kr.archive.ubuntu.com/ubuntu xenial InRelease
Hit:2 http://kr.archive.ubuntu.com/ubuntu xenial-updates InRelease                                               
Hit:3 http://kr.archive.ubuntu.com/ubuntu xenial-backports InRelease                                             
Hit:4 http://packages.microsoft.com/repos/vscode stable InRelease                             
Ign:5 http://dl.google.com/linux/chrome/deb stable InRelease                                  
Get:6 https://deb.nodesource.com/node_8.x xenial InRelease [4,646 B]    
Get:7 http://dl.google.com/linux/chrome/deb stable Release [1,189 B]                                 
Hit:8 http://security.ubuntu.com/ubuntu xenial-security InRelease                  
Get:10 https://deb.nodesource.com/node_8.x xenial/main Sources [761 B]
Get:11 https://deb.nodesource.com/node_8.x xenial/main amd64 Packages [1,006 B]
Get:12 https://deb.nodesource.com/node_8.x xenial/main i386 Packages [1,006 B]
Fetched 8,608 B in 1s (7,203 B/s)      
Reading package lists... Done

## Run `apt-get install nodejs` (as root) to install Node.js v8.x and npm

sosun@poscoict:~$ sudo apt-get install -y nodejs
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following package was automatically installed and is no longer required:
  libuv1
Use 'sudo apt autoremove' to remove it.
The following packages will be upgraded:
  nodejs
1 upgraded, 0 newly installed, 0 to remove and 293 not upgraded.
Need to get 12.8 MB of archives.
After this operation, 48.2 MB of additional disk space will be used.
Get:1 https://deb.nodesource.com/node_8.x xenial/main amd64 nodejs amd64 8.9.4-1nodesource1 [12.8 MB]
Fetched 12.8 MB in 2s (4,572 kB/s) 
(Reading database ... 185751 files and directories currently installed.)
Preparing to unpack .../nodejs_8.9.4-1nodesource1_amd64.deb ...
Unpacking nodejs (8.9.4-1nodesource1) over (4.2.6~dfsg-1ubuntu4.1) ...
Processing triggers for man-db (2.7.5-1) ...
Processing triggers for doc-base (0.10.7) ...
Processing 1 removed doc-base file...
Setting up nodejs (8.9.4-1nodesource1) ...
sosun@poscoict:~$ npm -v
5.6.0
sosun@poscoict:~$ node -v
v8.9.4
sosun@poscoict:~$ nodejs
```

## Installing yarn
[linux-yarn-manual](https://yarnpkg.com/lang/en/docs/install/)

__ubuntu 16.10 LTS (64bit) 인데 16.04 인줄 알고 따라했더니 안됨__
```
sosun@poscoict:~$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
OK
sosun@poscoict:~$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
deb https://dl.yarnpkg.com/debian/ stable main
sosun@poscoict:~$ yarn -v
The program 'yarn' is currently not installed. You can install it by typing:
sudo apt install cmdtest
```

__ubuntu 17.04 부터 cmdtest 된다는데 16.10에서도 동작됨.__
__but don't enter this command (sudo apt install cmdtest) if you want to install yarn. You will have to delete it probably..__

```
sosun@poscoict:~$ sudo apt install cmdtest
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following package was automatically installed and is no longer required:
  libuv1
Use 'sudo apt autoremove' to remove it.
The following additional packages will be installed:
  python-chardet python-cliapp python-markdown python-pkg-resources python-pygments python-ttystatus python-yaml
Suggested packages:
  libjs-jquery libjs-underscore python-xdg python-markdown-doc python-setuptools ttf-bitstream-vera
The following NEW packages will be installed:
  cmdtest python-chardet python-cliapp python-markdown python-pkg-resources python-pygments python-ttystatus
  python-yaml
0 upgraded, 8 newly installed, 0 to remove and 293 not upgraded.
Need to get 991 kB of archives.
After this operation, 5,157 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://kr.archive.ubuntu.com/ubuntu xenial/main amd64 python-yaml amd64 3.11-3build1 [105 kB]
Get:2 http://kr.archive.ubuntu.com/ubuntu xenial/universe amd64 python-cliapp all 1.20160109-1 [73.4 kB]
Get:3 http://kr.archive.ubuntu.com/ubuntu xenial/universe amd64 python-ttystatus all 0.32-1 [13.8 kB]
Get:4 http://kr.archive.ubuntu.com/ubuntu xenial/universe amd64 python-markdown all 2.6.6-1 [53.7 kB]
Get:5 http://kr.archive.ubuntu.com/ubuntu xenial/universe amd64 cmdtest all 0.22-1 [18.8 kB]
Get:6 http://kr.archive.ubuntu.com/ubuntu xenial/main amd64 python-pkg-resources all 20.7.0-1 [108 kB]
Get:7 http://kr.archive.ubuntu.com/ubuntu xenial/main amd64 python-chardet all 2.3.0-2 [96.3 kB]
Get:8 http://kr.archive.ubuntu.com/ubuntu xenial/main amd64 python-pygments all 2.1+dfsg-1 [522 kB]
Fetched 991 kB in 5s (176 kB/s)          
Selecting previously unselected package python-yaml.
(Reading database ... 190354 files and directories currently installed.)
Preparing to unpack .../python-yaml_3.11-3build1_amd64.deb ...
Unpacking python-yaml (3.11-3build1) ...
Selecting previously unselected package python-cliapp.
Preparing to unpack .../python-cliapp_1.20160109-1_all.deb ...
Unpacking python-cliapp (1.20160109-1) ...
Selecting previously unselected package python-ttystatus.
Preparing to unpack .../python-ttystatus_0.32-1_all.deb ...
Unpacking python-ttystatus (0.32-1) ...
Selecting previously unselected package python-markdown.
Preparing to unpack .../python-markdown_2.6.6-1_all.deb ...
Unpacking python-markdown (2.6.6-1) ...
Selecting previously unselected package cmdtest.
Preparing to unpack .../cmdtest_0.22-1_all.deb ...
Unpacking cmdtest (0.22-1) ...
Selecting previously unselected package python-pkg-resources.
Preparing to unpack .../python-pkg-resources_20.7.0-1_all.deb ...
Unpacking python-pkg-resources (20.7.0-1) ...
Selecting previously unselected package python-chardet.
Preparing to unpack .../python-chardet_2.3.0-2_all.deb ...
Unpacking python-chardet (2.3.0-2) ...
Selecting previously unselected package python-pygments.
Preparing to unpack .../python-pygments_2.1+dfsg-1_all.deb ...
Unpacking python-pygments (2.1+dfsg-1) ...
Processing triggers for man-db (2.7.5-1) ...
Setting up python-yaml (3.11-3build1) ...
Setting up python-cliapp (1.20160109-1) ...
Setting up python-ttystatus (0.32-1) ...
Setting up python-markdown (2.6.6-1) ...
Setting up cmdtest (0.22-1) ...
Setting up python-pkg-resources (20.7.0-1) ...
Setting up python-chardet (2.3.0-2) ...
Setting up python-pygments (2.1+dfsg-1) ...
sosun@poscoict:~$ 
```

__설명서에 cmdtest 있어서 치라는 건줄 알았더니, 그냥 있다는 거였음. yarn 설치 에러뜨면 지우라네. 지우고 나서 그냥 sudo apt-get install yarn 치면 안됨.__ 

__$sudo apt-get update && sudo apt-get install yarn. 이렇게 같이 한 줄로 쳐줘야지 yarn 설치됨 (왜???????)__

```
sosun@poscoict:~$ sudo apt-get install yarn
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package yarn
sosun@poscoict:~$ sudo apt remove cmdtest
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libuv1 python-chardet python-cliapp python-markdown python-pkg-resources python-pygments python-ttystatus
  python-yaml
Use 'sudo apt autoremove' to remove them.
The following packages will be REMOVED:
  cmdtest
0 upgraded, 0 newly installed, 1 to remove and 293 not upgraded.
After this operation, 78.8 kB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 190829 files and directories currently installed.)
Removing cmdtest (0.22-1) ...
Processing triggers for man-db (2.7.5-1) ...
sosun@poscoict:~$ sudo apt-get install yarn
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package yarn
sosun@poscoict:~$ sudo apt-get update && sudo apt-get install yarn
Hit:1 http://packages.microsoft.com/repos/vscode stable InRelease
Hit:2 http://kr.archive.ubuntu.com/ubuntu xenial InRelease          
Hit:3 http://kr.archive.ubuntu.com/ubuntu xenial-updates InRelease  
Hit:4 http://kr.archive.ubuntu.com/ubuntu xenial-backports InRelease
Ign:5 http://dl.google.com/linux/chrome/deb stable InRelease        
Get:6 http://dl.google.com/linux/chrome/deb stable Release [1,189 B]     
Hit:7 http://security.ubuntu.com/ubuntu xenial-security InRelease        
Hit:8 https://deb.nodesource.com/node_8.x xenial InRelease
Get:9 https://dl.yarnpkg.com/debian stable InRelease [11.5 kB]
Get:11 https://dl.yarnpkg.com/debian stable/main amd64 Packages [6,720 B]
Get:12 https://dl.yarnpkg.com/debian stable/main i386 Packages [6,720 B]
Get:13 https://dl.yarnpkg.com/debian stable/main all Packages [6,720 B]
Fetched 32.8 kB in 3s (8,739 B/s)    
Reading package lists... Done
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libuv1 python-chardet python-cliapp python-markdown python-pkg-resources python-pygments python-ttystatus
  python-yaml
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  yarn
0 upgraded, 1 newly installed, 0 to remove and 293 not upgraded.
Need to get 670 kB of archives.
After this operation, 4,125 kB of additional disk space will be used.
Get:1 https://dl.yarnpkg.com/debian stable/main amd64 yarn all 1.3.2-1 [670 kB]
Fetched 670 kB in 0s (736 kB/s)
Selecting previously unselected package yarn.
(Reading database ... 190814 files and directories currently installed.)
Preparing to unpack .../archives/yarn_1.3.2-1_all.deb ...
Unpacking yarn (1.3.2-1) ...
Setting up yarn (1.3.2-1) ...
sosun@poscoict:~$ yarn --v
yarn install v1.3.2
info No lockfile found.
[1/4] Resolving packages...
[2/4] Fetching packages...
[3/4] Linking dependencies...
[4/4] Building fresh packages...
info Lockfile not saved, no dependencies.
Done in 0.25s.
```
__어쨌든 성공적으로 설치__
