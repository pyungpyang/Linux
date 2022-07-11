# Linux-2
### 기초 명령어 공부 -디렉토리/파일 통계-

### mkdir (Make Directory)
> 디렉토리 생성
```bash
$ ls -al
total 5
drwxr-xr-x 1 thlee 197609  0  7월  8 03:34 ./
drwxr-xr-x 1 thlee 197609  0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609  0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609 48  7월  8 03:34 README.md

$ mkdir test01
$ ls -al
drwxr-xr-x 1 thlee 197609  0  7월  8 03:38 ./
drwxr-xr-x 1 thlee 197609  0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609  0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609 48  7월  8 03:34 README.md
drwxr-xr-x 1 thlee 197609  0  7월  8 03:38 test01/
```

### rmdir (Remove Directory)
> 디렉토리를 삭제  
> 단 디렉토리 내부에 파일이 존재하면 삭제 불가능
```bash
$ ls -al
drwxr-xr-x 1 thlee 197609  0  7월  8 03:38 ./
drwxr-xr-x 1 thlee 197609  0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609  0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609 48  7월  8 03:34 README.md
drwxr-xr-x 1 thlee 197609  0  7월  8 03:38 test01/

$ rmdir test01
$ ls -al
drwxr-xr-x 1 thlee 197609  0  7월  8 03:40 ./
drwxr-xr-x 1 thlee 197609  0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609  0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609 48  7월  8 03:34 README.md
```
### mount 
> 디스크 장치를 표시하거나 가상 파일 시스템으로 지정한  디렉토리를 연결  
> 디스크 장치를 표시하는 역할보다는 
> 다른 서버에서 지정한 디렉토리를 로컬 디랙토리처럼 사용하는 용도로 주로 쓰임  
> -t를 통해 타입을 지정해서 연결하거나 umount(unmount)로 연결 해제가 가능
```bash
$ mount
C:/Program Files/Git on / type ntfs (binary,noacl,auto)
C:/Program Files/Git/usr/bin on /bin type ntfs (binary,noacl,auto)
C:/Users/thlee/AppData/Local/Temp on /tmp type ntfs (binary,noacl,posix=0,usertemp)
C: on /c type ntfs (binary,noacl,posix=0,user,noumount,auto)
D: on /d type ntfs (binary,noacl,posix=0,user,noumount,auto)
```

### touch
> 지정한 이름의 비어있는 파일을 생성, 파일이 있는경우 타임스탬프 업데이트
```bash
$ ls -al
total 8
drwxr-xr-x 1 thlee 197609    0  7월  8 03:45 ./
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609 1950  7월  8 03:43 README.md

$ touch testfile01
$ ls -al
total 8
drwxr-xr-x 1 thlee 197609    0  7월  8 03:45 ./
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609 1950  7월  8 03:43 README.md
-rw-r--r-- 1 thlee 197609    0  7월  8 03:45 testfile01
```

### stat
> 지정한 파일의 파일통계를 출력
```bash
$ stat testfile02
  File: testfile02.txt
  Size: 73              Blocks: 1          IO Block: 65536  regular file
Device: 4e01222fh/1308697135d   Inode: 17169973579570470  Links: 1
Access: (0644/-rw-r--r--)  Uid: (197609/   thlee)   Gid: (197609/ UNKNOWN)
Access: 2022-07-08 03:47:43.873696900 +0900
Modify: 2022-07-08 03:46:59.914330300 +0900
Change: 2022-07-08 03:47:15.373385400 +0900
 Birth: 2022-07-08 03:46:42.034921100 +0900
```

### cat (catenate)
> 지정한 파일의 내용 출력
```bash
$ cat testfile02.txt
111
222
333
444
555
666
777
888
999
aaa
bbb
ccc
ddd
eee
fff
```

### head
> 지정한 파일의 1라인부터 지정한 라인까지 출력 (기본지정값 : 10)
```bash
$ head -n 5 testfile02.txt
111
222
333
444
555
```

### tail
> 지정한 파일의 마지막 라인부터 지정한 수 만큼의 라인을 출력 (기본지정값 : 10)  
> tail -f 를 통해 실시간으로 기록을 확인 할 수 있다.  
> -> 주로 접속로그를 확인하는데 쓰임
```bash
$ tail -n 3 testfile02.txt
ddd
eee
fff
```

### cp (Copy)
> 지정한 파일을 지정한 위치와 이름으로 복사  
> 단 cp -rfp 원본파일패스/이름 복사할파일패스/이름 으로 사용하는 경우가 많음  
> r : recursive -> 사용하지 않았을 때 하위 디렉토리 파일 복사에 에러발생  
> f : force -> 같은 이름의 파일이 있더라도 강제로 복사를 강행, 기존 파일에 덮어씌움  
> p : permission -> 실행 권한(읽기 쓰기 등), ls -al의 첫째줄에 표시되는 부분
```bash
$ ls -al
total 13
drwxr-xr-x 1 thlee 197609    0  7월  8 03:47 ./
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609 3851  7월  8 03:53 README.md
-rw-r--r-- 1 thlee 197609    0  7월  8 03:45 testfile01
-rw-r--r-- 1 thlee 197609   73  7월  8 03:46 testfile02.txt

$ cp -rfp testfile02.txt test02.txt

$ ls -al
total 14
drwxr-xr-x 1 thlee 197609    0  7월  8 03:54 ./
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609 3851  7월  8 03:53 README.md
-rw-r--r-- 1 thlee 197609   73  7월  8 03:46 test02.txt
-rw-r--r-- 1 thlee 197609    0  7월  8 03:45 testfile01
-rw-r--r-- 1 thlee 197609   73  7월  8 03:46 testfile02.txt
```

### mv (Move)
> 지정한 파일을 지정한 위치와 이름으로 이동
```bash
$ mv test02.txt mvfile01.txt

$ ls -al
total 18
drwxr-xr-x 1 thlee 197609    0  7월  8 03:58 ./
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609   73  7월  8 03:46 mvfile01.txt
-rw-r--r-- 1 thlee 197609 5172  7월  8 03:57 README.md
-rw-r--r-- 1 thlee 197609    0  7월  8 03:45 testfile01
-rw-r--r-- 1 thlee 197609   73  7월  8 03:46 testfile02.txt
```
### rm (Remove)
> 지정한 파일 삭제  
> rmdir과 달리 rm -r -f는 내부에 파일이 존재해도 삭제가능  
> 리눅스 환경은 삭제 후 복구가 불가능하니 주의할 것
```bash
$ rm mvfile01.txt testfile01 testfile02.txt

$ ls -al
total 16
drwxr-xr-x 1 thlee 197609    0  7월  8 03:59 ./
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 ../
drwxr-xr-x 1 thlee 197609    0  7월  8 03:34 .git/
-rw-r--r-- 1 thlee 197609 5707  7월  8 03:58 README.md
```

### rename
> 지정한 규칙에 따라 여러 개의 파일 이름을 변경  
```bash
ls -al
drwxrwxr-x 2 ec2-user ec2-user  58 Jul  7 19:09 .
drwx------ 6 ec2-user ec2-user 133 Jul  5 09:46 ..
-rw-rw-r-- 1 ec2-user ec2-user   0 Jul  7 19:09 test1
-rw-rw-r-- 1 ec2-user ec2-user   0 Jul  7 19:09 test2
-rw-rw-r-- 1 ec2-user ec2-user   0 Jul  7 19:09 test3
-rw-rw-r-- 1 ec2-user ec2-user   0 Jul  7 19:09 test4

$ rename test test0 test?

$ ls -al
drwxrwxr-x 2 ec2-user ec2-user  62 Jul  7 19:10 .
drwx------ 6 ec2-user ec2-user 133 Jul  5 09:46 ..
-rw-rw-r-- 1 ec2-user ec2-user   0 Jul  7 19:09 test01
-rw-rw-r-- 1 ec2-user ec2-user   0 Jul  7 19:09 test02
-rw-rw-r-- 1 ec2-user ec2-user   0 Jul  7 19:09 test03
-rw-rw-r-- 1 ec2-user ec2-user   0 Jul  7 19:09 test04
```