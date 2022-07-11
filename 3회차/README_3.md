### 리눅스 기초 명령어 -파일 관련 명령어-  

## less
> 상하로 커서 이동이 가능한 파일뷰어
> 커서 이동은 화살표나 j,k, page up down도 가능  
> q를 이용해서 종료할 수 있음
```bash
$ less testfile.txt
aa
bb
cc
dd
ee
ff
gg
hh
ii
testfile.txt (END)
```

## ln(Link)
> 지정한 파일에 대한 심볼릭링크나 하드링크 생성  
> ln 옵션 링크의원본파일패스/이름 링크파일패스/이름 ^C  
  
> 심볼릭링크 : 윈도우의 바로가기와 같음 특정 디렉토리라 파일을 심볼릭링크파일로 만들어놓으면 그 파일에 접근하는 것으로 링크의 원본파일에 접근할 수 있음  
> 원본파일 삭제시 데이터에 접근 불가   
> ln -s를 붙여 사용하는 경우가 많음

> 하드링크 : 물리적으로 다른 두개의 파일이 각각 하나의 원본파일과 연동  
> 원본파일을 삭제해도 데이터에 접근 가능, 원본파일의 내용을 수정하면 나머지 한쪽도 같이 수정됨.  
```bash
$ ln testfile.txt hardlink.txt

$ cat hardlink.txt
aa
bb
cc

$ vi hardlink.txt

$ cat hardlink.txt 
aa
bb
cc
xyz

$ cat testfile.txt
aa
bb
cc
xyz

$ rm -f hardlink.txt 

$ cat testfile.txt 
aa
bb
cc
xyz
```
```bash
$ ln -s testfile.txt symboliclink.txt
$ ls -al
drwxrwxr-x 2 ec2-user ec2-user  50 Jul 11 15:36 .
drwx------ 6 ec2-user ec2-user 149 Jul 11 15:36 ..
lrwxrwxrwx 1 ec2-user ec2-user  12 Jul 11 15:36 symboliclink.txt -> testfile.txt
-rw-rw-r-- 1 ec2-user ec2-user  20 Jul 11 15:36 testfile.txt
```

## paste
> 지정한 파일들의 행을 읽어 탭으로 구분하여 병합
> 쉘스크립트 안에서 레포팅을 정리할 때 사용
```bash
$ cat txt
aaa
bbb
ccc

$ cat txt1
111
222
333

$ cat txt txt1
aaa
bbb
ccc
111
222
333

$ paste txt1 txt
111     aaa
222     bbb
333     ccc
```
## dd(Dataset Definition)
> 블록 단위로 데이터셋을 정의하여 파일을 쓰고 읽음  
> 랜덤 데이터로 파일을 생성하거나 파일을 생성한 시간을 측정해서 드라이브의 성능을 체크하는데 쓰임  
> dd if=인풋파일이름 of=아웃풋파일이름 bs=바이트(크기) count=블럭을 복사할 횟수  
> ibs, obs <---bs

> urandom : 랜덤문자를 생성하는 장치파일  
> zero : 0으로 채움  
> ex. dev/urandom,  dev/zero
```bash
$ dd if=/dev/urandom of=ddtest bs=1024 count=10
10+0 records in
10+0 records out
10240 bytes (10 kB, 10 KiB) copied, 0.002745 s, 3.7 MB/s

$ ls -alh ddtest
-rw-r--r-- 1 thlee 197609 10K  7월 12 00:59 ddtest

$ ls -al ddtest
-rw-r--r-- 1 thlee 197609 10240  7월 12 00:59 ddtest
```
## tar(Tape Archive)
> 지정한 데이터 및 디렉토리를 하나의 파일로 만듬  
> 파일을 하나로 묶거나 압축된 파일을 풀 때 사용  
> tar -cvzf 타르볼파일명 디렉토리명/파일명 : 압축  
> tar -xvzf 타르볼파일명 디렉토리명/파일명 : 압축해제  
> c : create, x : extract, v : verbose, z : zip으로 압축, f : 파일 이름을 명시적으로 지정  
> tf : 타르볼 내부의 파일을 확인 t (List)  
```bash
$ tar -cvzf work.tgz ./Work
./Work/
./Work/symboliclink.txt
./Work/test1
./Work/test2
./Work/test3
./Work/test4
./Work/test5
./Work/testfile.txt

$ ls -al work.tgz
-rw-r--r-- 1 thlee 197609 275  7월 12 01:07 work.tgz

$ tar -tf work.tgz
./Work/
./Work/symboliclink.txt
./Work/test1
./Work/test2
./Work/test3
./Work/test4
./Work/test5
./Work/testfile.txt
```
```bash
$ tar -xvzf work.tgz 
./Work/
./Work/symboliclink.txt
./Work/test1
./Work/test2
./Work/test3
./Work/test4
./Work/test5
./Work/testfile.txt

$ ls -al
total 5
drwxr-xr-x 1 thlee 197609   0  7월 12 01:09 ./
drwxr-xr-x 1 thlee 197609   0  7월 12 01:09 ../
drwxr-xr-x 1 thlee 197609   0  7월 12 00:34 Work/
-rw-r--r-- 1 thlee 197609 275  7월 12 01:07 work.tgz
```