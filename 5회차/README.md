## 리눅스 기초 명령어 - 네트워크 관련 명령어 -

### wget (World wilde web + Get)
> 웹서버로부터 컨텐츠를 가져오는 도구   
> wget + 자료의url 

```bash
$ wget https://openresty.org/download/openresty-1.17.8.2.tar.gz
--2022-07-19 13:49:18--  https://openresty.org/download/openresty-1.17.8.2.tar.gz
Resolving openresty.org (openresty.org)... 18.138.237.72
Connecting to openresty.org (openresty.org)|18.138.237.72|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5041142 (4.8M) [application/x-gzip]
Saving to: ‘openresty-1.17.8.2.tar.gz’

100%[=============================================================================================================================================================================================>] 5,041,142   5.14MB/s   in 0.9s

2022-07-19 13:49:20 (5.14 MB/s) - ‘openresty-1.17.8.2.tar.gz’ saved [5041142/5041142]

$ ls -al openresty-1.17.8.2.tar.gz
-rw-rw-r-- 1 ec2-user ec2-user 5041142 Jul 13  2020 openresty-1.17.8.2.tar.gz
```

### curl (Client for URLs)
>다양한 프로토콜을 사용하여 데이터를 전송하게 해주는 도구
> curl -lkso   
> l : 링크를 따라서 리다이렉트 된 곳으로 넘어감  
> k : https의 인증을 무시  
> s : slient 모드로 실행 = 통계값을 출력하지 않음  
> o : output 파일을 지정   
> w : output 포멧을 결정

> null : 아무것도 없는 상태의 파일, 어떤 출력값을 null로 보내면 값이 사라짐

### route : 네트워크의 경로 정보(라우팅 테이블)의 출력, 변경하는 도구

```bash
$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         ip-172-31-0-1.a 0.0.0.0         UG    0      0        0 eth0
instance-data.a 0.0.0.0         255.255.255.255 UH    0      0        0 eth0
172.31.0.0      0.0.0.0         255.255.240.0   U     0      0        0 eth0

$ route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         172.31.0.1      0.0.0.0         UG    0      0        0 eth0
169.254.169.254 0.0.0.0         255.255.255.255 UH    0      0        0 eth0
172.31.0.0      0.0.0.0         255.255.240.0   U     0      0        0 eth0
```
> Destination : 목적지  
> Gateway : 외부 네트워크와 연결하기 위한 Gateway 의 주소  
> Genmask : 목적지 네트워크의 Genmask 주소  
> Flags : 해당 경로에 대한 정보   
> U : 경로가 살아있음, H : 목적지가 호스트 주소, G : 게이트웨이를 향하는 경로  
> Metric : 목적지 경로까지의 거리  

> route add : 라우트 설정에 대한 정보 추가 <=> route del

## 리눅스 기초 명령어 - 검색/탐색 관련 명령어 -

### find
> 지정한 파일명 또는 정규표현식을 이용하여 파일을 검색  
> find 옵션 찾기시작할패스 익스프레션  
> ? : 하나의 문자에 대응, * : 0개 이상의 문자에 대응  
> name, type f/d, perm, empty : 익스프레션에 쓸 수 있음  
> find 패스 -name 파일명(필요시 정규표현식)
```bash
$ find ./ -name testfile.txt
./vagrant/testfile.txt
./Work/testfile.txt

$ touch testfile.t1t
$ find ./ -name testfile.t?t
./testfile.t1t

$ find ./ -name t?stf?le.tx?
./vagrant/testfile.txt
./Work/testfile.txt

$ find ./ -name testfile.*
./vagrant/testfile.txt
./Work/testfile.txt
```
### which
> 환경변수 PATH에 등록된 디렉토리에 있는 명령어를 찾아주는 도구
```bash
$ echo ${PATH}
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/ec2-user/.local/bin:/home/ec2-user/bin
$ ^C
$ which ls
alias ls='ls --color=auto'
        /usr/bin/ls
$ which df
/usr/bin/df
$ which find
/usr/bin/find
```

### grep (Global / Regular Expression / Print)
> 텍스트 검색 기능을 가진 도구  
> 파일이나 표준 입력을 검색하여 지정한 정규 표현식과 맞는 줄을 출력  
> grep 옵션 "찾을문자열" 파일명    
> grep -ir 찾을단어 파일(또는패스)

> error, Error, eRRoR, erroR : 모두 다른 문자로 인식  
> grep -ir "error" /var/log/*  
> i : 대소문자를 구분하지 않음   
> r : 하위 디렉토리를 포함하여 검색  

### history
> 명령어를 수행한 목록을 출력/조작  
> .bash_history 에 저장
```bash
$ history
  316  which find
  317  ls -al /var/log/messages
  318  grep "error" /var/log/messages
  319  grep error /var/log/*
  320  ls -al .bash_history
  321  tail .bash_history
```