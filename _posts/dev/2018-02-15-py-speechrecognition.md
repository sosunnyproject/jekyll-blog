---
title: "python speech recognition"
layout: post
categories: dev
date: 2018-02-15T13:01:27-05:00
last_modified_at: 2018-02-15T13:01:27-05:00
share: false
---

## wit ai ref/study links
- https://www.smashingmagazine.com/2017/08/ai-chatbot-web-speech-api-node-js/
- https://github.com/jw84/messenger-bot-witai-tutorial
- https://github.com/wit-ai/node-wit
- https://medium.com/@mirkoj/tutorial-build-a-simple-bot-with-swift-node-and-wit-cab3929d8f3c
- https://wit.ai/sosunnyproject/MyFirstApp/settings
- https://wit.ai/docs/http/20160330#response-format-link


## python-pyaudio

1. pyaudio not getting installed via simple pip3

**solution** : sudo apt-get install python3-pyaudio

2. pyaudio version (0.2.8) lower than required (0.2.11)

```bash
$ sudo apt-get install portaudio19-dev
$ sudo pip3 install pyaudio
$ sudo pip3 install pyaudio --upgrade
```

```bash
sosun@poscoict:~/Desktop/demo/sr$ sudo pip3 install pyaudio
[sudo] password for sosun: 
The directory '/home/sosun/.cache/pip/http' or its parent directory is not owned by the current user and the cache has been disabled. Please check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
The directory '/home/sosun/.cache/pip' or its parent directory is not owned by the current user and caching wheels has been disabled. check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
Collecting pyaudio
  Downloading PyAudio-0.2.11.tar.gz
Installing collected packages: pyaudio
  Running setup.py install for pyaudio ... error
    Complete output from command /usr/bin/python3 -u -c "import setuptools, tokenize;__file__='/tmp/pip-build-uovh794z/pyaudio/setup.py';exec(compile(getattr(tokenize, 'open', open)(__file__).read().replace('\r\n', '\n'), __file__, 'exec'))" install --record /tmp/pip-ixo5m2ev-record/install-record.txt --single-version-externally-managed --compile:
    running install
    running build
    running build_py
    creating build
    creating build/lib.linux-x86_64-3.5
    copying src/pyaudio.py -> build/lib.linux-x86_64-3.5
    running build_ext
    building '_portaudio' extension
    creating build/temp.linux-x86_64-3.5
    creating build/temp.linux-x86_64-3.5/src
    x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I/usr/include/python3.5m -c src/_portaudiomodule.c -o build/temp.linux-x86_64-3.5/src/_portaudiomodule.o
    src/_portaudiomodule.c:29:23: fatal error: portaudio.h: No such file or directory
    compilation terminated.
    error: command 'x86_64-linux-gnu-gcc' failed with exit status 1
    
    ----------------------------------------
Command "/usr/bin/python3 -u -c "import setuptools, tokenize;__file__='/tmp/pip-build-uovh794z/pyaudio/setup.py';exec(compile(getattr(tokenize, 'open', open)(__file__).read().replace('\r\n', '\n'), __file__, 'exec'))" install --record /tmp/pip-ixo5m2ev-record/install-record.txt --single-version-externally-managed --compile" failed with error code 1 in /tmp/pip-build-uovh794z/pyaudio/

```
## Extra: korean - kaldi install trial (incomplete)
**Ref**
- https://github.com/hyung8758/Korean_ASR
- https://github.com/kaldi-asr/kaldi

```bash
sosun@poscoict:~$ git clone https://github.com/kaldi-asr/kaldi.git kaldi --origin upstream
Cloning into 'kaldi'...
remote: Counting objects: 89295, done.
sosun@poscoict:~$ cd kaldi
sosun@poscoict:~/kaldi$ git pull
Already up-to-date.
sosun@poscoict:~/kaldi$ cd tools
sosun@poscoict:~/kaldi/tools$ extras/check_dependencies.sh
extras/check_dependencies.sh: zlib is not installed.
extras/check_dependencies.sh: automake is not installed.
extras/check_dependencies.sh: autoconf is not installed.
extras/check_dependencies.sh: neither libtoolize nor glibtoolize is installed
extras/check_dependencies.sh: subversion is not installed
extras/check_dependencies.sh: we recommend that you run (our best guess):
 sudo apt-get install  zlib1g-dev automake autoconf libtool subversion
You should probably do: 
 sudo apt-get install libatlas3-base

sosun@poscoict:~/kaldi/tools$ sudo apt-get install libatlas3-base
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libuv1 python-chardet python-cliapp python-markdown
  python-pygments python-ttystatus python-yaml
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  libblas-common libgfortran3
The following NEW packages will be installed:
  libatlas3-base libblas-common libgfortran3
0 upgraded, 3 newly installed, 0 to remove and 10 not upgraded.
Need to get 2,962 kB of archives.
After this operation, 12.2 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
...
sosun@poscoict:~/kaldi/tools$ sudo apt-get install zlib1g-dev
...
sosun@poscoict:~/kaldi/tools$ make
extras/check_dependencies.sh
extras/check_dependencies.sh: automake is not installed.
extras/check_dependencies.sh: autoconf is not installed.
extras/check_dependencies.sh: neither libtoolize nor glibtoolize is installed
extras/check_dependencies.sh: subversion is not installed
extras/check_dependencies.sh: we recommend that you run (our best guess):
 sudo apt-get install  automake autoconf libtool subversion
Makefile:31: recipe for target 'check_required_programs' failed
make: *** [check_required_programs] Error 1
sosun@poscoict:~/kaldi/tools$ sudo apt-get install automake autoconf libtool subversion
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libuv1 python-chardet python-cliapp python-markdown
  python-pygments python-ttystatus python-yaml
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  autotools-dev libapr1 libaprutil1 libltdl-dev libserf-1-1
  libsigsegv2 libsvn1 m4
Suggested packages:
  autoconf-archive gnu-standards autoconf-doc libtool-doc gfortran
  | fortran95-compiler gcj-jdk db5.3-util subversion-tools
The following NEW packages will be installed:
  autoconf automake autotools-dev libapr1 libaprutil1 libltdl-dev
  libserf-1-1 libsigsegv2 libsvn1 libtool m4 subversion
0 upgraded, 12 newly installed, 0 to remove and 10 not upgraded.
Need to get 3,121 kB of archives.
After this operation, 12.5 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
...
```
typo error: it's zlib1g-dev.

```
sosun@poscoict:~/kaldi/tools$ sudo apt-get install zlib1g-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libuv1 python-chardet python-cliapp python-markdown
  python-pygments python-ttystatus python-yaml
...
sosun@poscoict:~/kaldi/tools$ make
extras/check_dependencies.sh
extras/check_dependencies.sh: automake is not installed.
extras/check_dependencies.sh: autoconf is not installed.
extras/check_dependencies.sh: neither libtoolize nor glibtoolize is installed
extras/check_dependencies.sh: subversion is not installed
extras/check_dependencies.sh: we recommend that you run (our best guess):
 sudo apt-get install  automake autoconf libtool subversion
Makefile:31: recipe for target 'check_required_programs' failed
make: *** [check_required_programs] Error 1
sosun@poscoict:~/kaldi/tools$ sudo apt-get install automake autoconf libtool subversion
```
--------------------------------------------------------------------------------------------------------------
> also here: https://github.com/poscoict-arvrmr/docs/blob/master/howto/py-speechrecognition.md

## SpeechRecognition 음성인식

1. Raspberry Pi Virtual Assistant book code example

**파이썬기본패키지설치**
```bash
# speechrecognition 패키지설치
$ sudo pip3 install SpeechRecognition 

# pyaudio 패키지설치
$ sudo pip3 install pyaudio
# 이게 에러가 나면
$ sudo apt-get install portaudio19-dev
$ sudo pip3 install pyaudio
$ sudo pip3 install pyaudio --upgrade

# upgrade --> 0.2.11 버젼으로만들어줘야함
```

**실행예시코드**
_main.py_
```python
import speech_recognition as sr

r = sr.Recognizer()
with sr.Microphone() as source:
	print("Say something")
	audio = r.listen(source)

with open("recording.wav", "wb") as f:
	f.write(audio.get_wav_data())
```

**코드실행**

```bash
# main.py 있는 폴더로 cd
$ python3 main.py
```

### Raspberry Pi

**Error message**
```bash
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.rear
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.center_lfe
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.side
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.surround21
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.surround21
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.surround40
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.surround41
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.surround50
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.surround51
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.surround71
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.iec958
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.iec958
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.iec958
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.hdmi
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.hdmi
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.modem
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.modem
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.phoneline
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.phoneline
ALSA lib confmisc.c:1281:(snd_func_refer) Unable to find definition 'defaults.bluealsa.device'
ALSA lib conf.c:4528:(_snd_config_evaluate) function snd_func_refer returned error: No such file or directory
ALSA lib conf.c:4996:(snd_config_expand) Args evaluate error: No such file or directory
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM bluealsa
ALSA lib confmisc.c:1281:(snd_func_refer) Unable to find definition 'defaults.bluealsa.device'
ALSA lib conf.c:4528:(_snd_config_evaluate) function snd_func_refer returned error: No such file or directory
ALSA lib conf.c:4996:(snd_config_expand) Args evaluate error: No such file or directory
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM bluealsa
connect(2) call to /tmp/jack-1000/default/jack_0 failed (err=No such file or directory)
attempt to connect to server failed
Say something
```
> https://stackoverflow.com/questions/7088672/pyaudio-working-but-spits-out-error-messages-each-time
> https://www.raspberrypi.org/forums/viewtopic.php?t=136974
> https://stackoverflow.com/questions/31603555/unknown-pcm-cards-pcm-rear-pyaudio
> https://stackoverflow.com/questions/7088672/pyaudio-working-but-spits-out-error-messages-each-time

**after I commented out alsa.config lines**
```bash
ALSA lib confmisc.c:1281:(snd_func_refer) Unable to find definition 'defaults.bluealsa.device'
ALSA lib conf.c:4528:(_snd_config_evaluate) function snd_func_refer returned error: No such file or directory
ALSA lib conf.c:4996:(snd_config_expand) Args evaluate error: No such file or directory
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM bluealsa
ALSA lib confmisc.c:1281:(snd_func_refer) Unable to find definition 'defaults.bluealsa.device'
ALSA lib conf.c:4528:(_snd_config_evaluate) function snd_func_refer returned error: No such file or directory
ALSA lib conf.c:4996:(snd_config_expand) Args evaluate error: No such file or directory
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM bluealsa
connect(2) call to /tmp/jack-1000/default/jack_0 failed (err=No such file or directory)
attempt to connect to server failed
```
**after I deleted $ sudo apt autoremove bluez-alsa**
```bash
pi@raspberrypi:~ $ sudo apt autoremove bluez-alsa
패키지 목록을 읽는 중입니다... 완료
의존성 트리를 만드는 중입니다       
상태 정보를 읽는 중입니다... 완료
Package 'bluez-alsa' is not installed, so not removed
다음 패키지를 지울 것입니다:
  erlang-base erlang-crypto erlang-syntax-tools libboost-thread1.62.0 libqt5concurrent5
  libqt5opengl5 libqt5printsupport5 libqt5scintilla2-12v5 libqt5scintilla2-l10n
  libqt5x11extras5 libqt5xml5 libqwt-qt5-6 libscsynth1 libsctp1
0개 업그레이드, 0개 새로 설치, 14개 제거 및 0개 업그레이드 안 함.
이 작업 후 22.4 M바이트의 디스크 공간이 비워집니다.
계속 하시겠습니까? [Y/n] y
(데이터베이스 읽는중 ...현재 124251개의 파일과 디렉터리가 설치되어 있습니다.)
Removing erlang-syntax-tools (1:19.2.1+dfsg-2+deb9u1) ...
Removing erlang-crypto (1:19.2.1+dfsg-2+deb9u1) ...
Removing erlang-base (1:19.2.1+dfsg-2+deb9u1) ...
Searching for services which depend on erlang and should be stopped...none found.
Killing epmd...it is not running.
Removing libscsynth1 (1:3.7.0~repack-4) ...
Removing libboost-thread1.62.0:armhf (1.62.0+dfsg-4) ...
Removing libqt5concurrent5:armhf (5.7.1+dfsg-3+rpi1) ...
Removing libqwt-qt5-6 (6.1.2-6) ...
Removing libqt5opengl5:armhf (5.7.1+dfsg-3+rpi1) ...
Removing libqt5scintilla2-12v5 (2.9.3+dfsg-4) ...
Removing libqt5printsupport5:armhf (5.7.1+dfsg-3+rpi1) ...
Removing libqt5scintilla2-l10n (2.9.3+dfsg-4) ...
Removing libqt5x11extras5:armhf (5.7.1~20161021-2) ...
Removing libqt5xml5:armhf (5.7.1+dfsg-3+rpi1) ...
Removing libsctp1:armhf (1.0.17+dfsg-1) ...
Processing triggers for menu (2.1.47) ...
Processing triggers for libc-bin (2.24-11+deb9u1) ...
Processing triggers for man-db (2.7.6.1-2) ...
```
**still error**
```bash
ALSA lib confmisc.c:1281:(snd_func_refer) Unable to find definition 'defaults.bluealsa.device'
ALSA lib conf.c:4528:(_snd_config_evaluate) function snd_func_refer returned error: No such file or directory
ALSA lib conf.c:4996:(snd_config_expand) Args evaluate error: No such file or directory
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM bluealsa
ALSA lib confmisc.c:1281:(snd_func_refer) Unable to find definition 'defaults.bluealsa.device'
ALSA lib conf.c:4528:(_snd_config_evaluate) function snd_func_refer returned error: No such file or directory
ALSA lib conf.c:4996:(snd_config_expand) Args evaluate error: No such file or directory
ALSA lib pcm.c:2495:(snd_pcm_open_noupdate) Unknown PCM bluealsa
ALSA lib pcm_dmix.c:1052:(snd_pcm_dmix_open) unable to open slave
connect(2) call to /tmp/jack-1000/default/jack_0 failed (err=No such file or directory)
attempt to connect to server failed
```
