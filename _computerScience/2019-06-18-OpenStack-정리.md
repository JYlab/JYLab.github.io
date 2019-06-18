---
title: "OpenStack 정리"
categories:
  - OpenStack
tags:
  - OpenStack

last_modified_at: 2019-06-18T11:50:52-05:00
---


![openstack](https://jylab.github.io/assets/images/openstack.jpg)


## OpenStack 정리
----
### 수정내역
- 2019.06.18 최초작성


### **1. 서론**
회사에 자원들을 묶어서 클라우드화 할 일이 생겼다. 목표는 컨트롤러노드 1대와 다수의 컴퓨트 노드를 연결하여 서비스할 예정이다. 
이것과 관련해서 관련 자료 및 내용을 기록하기 위해 이 글을 쓴다.




### **2. 구축방법**
다음 자료를 참고했다.
* https://www.youtube.com/watch?v=cysJ9PvMKAY&list=PLkgLtPJ7Lg3paDba9_z8m-VRGR88CFK67&index=4

데브스택을 쓰면 편하더라. 

Pre Command
```
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get dist-upgrade -y
sudo apt-get install openssh-server git -y
```

DevStack Download
```
git clone https://git.openstack.org/openstack-dev/devstack
```
여기까지 하면 sample 디렉토리 안에 local.conf라는 파일이 있다.
해당 파일을 devstack/ 으로 복사한 뒤 이를 살짝 수정하는 방향으로 구축하였다.

대략적인 내용은 다음과 같다.
```
[[local|localrc]]
ADMIN_PASSWORD=devstack
DATABASE_PASSWORD=$ADMIN_PASSWORD
RABBIT_PASSWORD=$ADMIN_PASSWORD
SERVICE_PASSWORD=$ADMIN_PASSWORD
```

이부분도 중요하다. 반드시 stack 유저가 필요하다 카더라
```
root@ubuntu:~# useradd -U -G sudo -s /bin/bash -m stack 
root@ubuntu:~# echo "stack ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
root@ubuntu:~# passwd stack
.
passwd: password updated successfully
root@ubuntu:~# su stack
.
stack@ubuntu:/root$ cd
stack@ubuntu:~$
```

그 후에 devstack 디렉토리를 stack 유저의 소유로 변경한다
```
chown -R stack:stack devstack
```

마지막으로 ./stack.sh 를 실행해 주면 된다. (stack 유저인 상태로 루트권한 없이)

이렇게 컨트롤러 노드를 만들었고, 이제 컴퓨트 노드(nova)들을 만들 예정이다. dashboard 접속이 잘 되는 것과 CirrOS 인스턴스를 만드는 것까지 확인했다.

문제점은 컨트롤러 노드에는 랜카드가 2개 필요한데 1개밖에 없어서 구입요청을 했고, nova들을 연결하기 위해 허브를 구입요청하였다. 현재 문제는 (비록 test용 인스턴스지만) 인스턴스에 IP 할당 및 SSH 접속이 안되더라. 플로팅IP 설정이 뭔가 잘못된거같은데 분석 후 정리할 예정이다.

### **3. Trouble Shooting**
* .cache 파일 어쩌구하면서 권한없다고 그러던데, 해당 파일도 chown -R stack:stack (해당파일) 로 소유권을 바꿔주면 되더라