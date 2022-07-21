### 리눅스 명령어 -I/O 관련 명령어-

### redirection
> 표준 스트림(stdin stdout stderr)을 부등호를 사용하여 지정한 위치로 보낼수 있는 방향 지정 옵션  
> 명령어 리다이렉션기호 파일명  
> " >> : 아랫줄에 내용을 추가, >| : >로 추가할 경우 파일이나 디렉토리가 존재하지 않는다는 에러가 나는 경우가 있음 >| 를 통해 강제로 생성가능"

```bash
$ echo a > a
$ cat a
a

$ echo b > a
$ cat a
b

$ echo zzz >> a
$ cat a
b
zzz

$ echo kkk >| test
$ cat test
kkk
```

### echo
> 문자열을 출력하는 도구

```bash
$ echo 'abcde'
abcde
```

### chmod(Change mode)
> 파일이나 디렉토리의 모드(접근권한)을 변경하는 도구  
> r : read, w: write, x : execute  
> drwxr-xr-x에서   
> 첫번째 rwx : 파일의 소유자가 가진 권한  
> 두번째 r-x : 파일이 속한 그룹의 유저가 가진 권한  
> 세번째 r-x : 그 외의 유저가 갖는 권한  
> chmod 권한정보(2진수자리숫자) 파일명  
> rw- rw- r--   
> 421 421 421  
> 664
> +r +w +x 등으로 권한을 사용하기도 함
```bash
$ ls -al
total 7
drwxr-xr-x 1 thlee 197609   0  7월 22 04:25 ./
drwxr-xr-x 1 thlee 197609   0  7월 22 04:20 ../
-rw-r--r-- 1 thlee 197609   6  7월 22 04:25 a
-rw-r--r-- 1 thlee 197609 439  7월 22 04:25 README.md
-rw-r--r-- 1 thlee 197609   4  7월 22 04:25 test

$ touch aaa
$ ls -al aaa
-rw-r--r-- 1 thlee 197609 0  7월 22 04:37 aaa

$ chmod 664 aaa
$ ls -al aaa
-rw-rw-r-- 1 thlee 197609 0  7월 22 04:37 aaa
```

### chown(change the owner of a file)
> 파일의 소유권을 바꾸기 위한 도구
> chown 소유자명 :그룹명 파일/디렉토리이름ip
```bash
$ ls -al aaa
-rw-r--r-- 1 ec2-user ec2-user 0 Jul 21 19:43 aaa

$ chown root:root aaa
-rw-r--r-- 1 root     root           0 Jul 21 19:43 aaa
```
### sudo (Super DO --> Substitude User DO)
> root 사용자의 보안 권한을 이용하여 명령 또는 프로그램을 실행하는 도구
```bash
$ cat /var/log/messages
cat: /var/log/messages: Permission denied

$ sudo cat /var/log/messages
```

### who 
> 현재 시스템에 로그인한 사용자 목록을 출력

### date
> 현재의 날짜와 시간을 출력  
> -d '주/월/시간/분/초'  
> date '+%Y-%m-%d %H:%M:%S' 를 통해 연-월-일 시:분:초 로 변경가능
```bash
$ date
Thu Jul 21 20:02:08 UTC 2022

$ date -d '-1 day'
Wed Jul 20 20:02:30 UTC 2022

$ date -d '1 day ago'
Wed Jul 20 20:02:43 UTC 2022

$ date -d '1 day'
Wed Jul 20 20:02:51 UTC 2022

$ date '+%Y-%m-%d %H:%M:%S'
2022-07-21 20:06:08

$ date '+%Y%m%d'
20220721
```

### seq(SEQuence)
> 지정한 규칙으로 숫자열을 출력  
> seq 시작숫자 끝숫자  
> w : 가장 큰 숫자의 자릿수에 맞춰 작은 숫자를 조정  
> seq -f %0자릴수g  
> 0자리에 문자는 쓰지않음,  숫자가 들어간 경우 숫자의 크기만큼 공백생성후 출력
```bash
$ seq 1 3
1
2
3

$ seq -w 1 10
01
02
03
04
05
06
07
08
09
10

$ seq -f %02g 1 5
01
02
03
04
05

$ seq -f %03g 1 3
001
002
003

$ seq -f %13g 1 3
            1
            2
            3
```

### more
> 한 화면씩 지정한 파일의 내용을 출력  
> q: 종료, Enter : 한줄씩 내림, spacebar : 한페이지 넘김

### watch
> 지정한 명령어를 지정한 시간(초)마다 재실행하여 화면에 출력  
> 기본시간은 2초, ^C로 종료할때까지 실행

### crontab 
> 리눅스의 잡 스케줄러의 내용을 출력하거나 편집할 수 있는 도구  
> 지정한 시각에 지정한 프로그램을 실행하게하는 툴  
>  l : list 등록한 cronjob(crontab에 등록한 프로그램)을 보여줌  
> e : edit crontab을 편집  
> r : remove 등록한 모든 옵션을 삭제