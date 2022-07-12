## nohup (No HangUps)
> 쉘 스크립트 파일을 데몬 형태로 실행, 표준 출력을 지정한 파일로 리다이렉트
```bash
$ nohup echo "Bash Command"
nohup: ignoring input and appending output to 'nohup.out'

$ cat nohup.out 
Bash Command
```

## kill
> 지정한 프로세스에 지정한 시그널을 보내 프로세스 종료  
> 프로세스에 장애가 나서 급하게 종료시킬 때 많이 사용  

> INT, TERM : 프로세스를 안전하게 종료   
> kill -2 프로세스번호, kill -INT 프로세스번호  
> kill -15 프로세스번호, kill -TERM 프로세스번호
> kill -9 프로세스번호, kill -KILL 프로세스번호


# -네트워크 관련 명령어-
> 네트워크 : 서버와 서버 서버와 클라이언트 사이의 통신망  
> 인터넷을 통해 데이터를 주고받기 위한 주소의 설정이나 데이터의 통계 통신의 제어등을 할 수 있는 명령어를 다룸

## ifconfig (InterFace Configration)
> 네트워크 인터페이스의 활성/비활성화 및 설정  
> ifconfig eth0 으로 eth0 장치만 볼 수 있음
```bash
$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 172.31.3.146  netmask 255.255.240.0  broadcast 172.31.15.255
        inet6 fe80::55:18ff:fea3:3896  prefixlen 64  scopeid 0x20<link>
        ether 02:55:18:a3:38:96  txqueuelen 1000  (Ethernet)
        RX packets 190283  bytes 98391066 (93.8 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 168897  bytes 16064447 (15.3 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 24  bytes 1944 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 24  bytes 1944 (1.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

## ip
> ip관련 정보 조회 및 설정  
> ip address show eth0 == ip ad sh eth0
```bash
$ ip address show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc pfifo_fast state UP group default ql
    link/ether 02:55:18:a3:38:96 brd ff:ff:ff:ff:ff:ff
    inet 172.31.3.146/20 brd 172.31.15.255 scope global dynamic eth0
       valid_lft 3244sec preferred_lft 3244sec
    inet6 fe80::55:18ff:fea3:3896/64 scope link
       valid_lft forever preferred_lft forever
```
## netstat (NETwork STATistics)
> 네트워크 프로토콜의 통계와 연결상태를 출력  
> netstat -nltpu : 서버가 열고있는 포트와 프로그램을 확인하는 옵션   
> netstat -tan(u) : 현재 네트워크 상태의 전체를 보여줌

> n : 정의한 이름이나 도메인 이름을 뺀 ip나 포트번호 숫자로 출력  
> l : listen 하고 있는 상태의 소캣 출력  
> t : tcp통신 프로그램의 이름을 출력, u : udp

## ss (Socket Statistics)
> 네트워크 소켓의 통계와 연결상태를 출력

## iptanles
> 패킷 필터링 도구로 패킷의 출입을 제한하는 방화벽구성이나   
> NAT(Network Address Translation)구성에 사용

## ufw (Uncomplicated FireWall)
> iptables의 제어를 쉽게 하기 위한 도구

## ping
> ICMP프로토콜의 응답 확인 도구