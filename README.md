# Linux
### 기초 명령어 -파일 시스템 관련-
### 


## pwd (Print Working Directory)
> 현재 위치한 디렉토리의 절대경로를 출력
```bash
$ pwd
/c/Workspace
```

## cd (Change Directory)
> 경로 이동 절대 경로와 상대경로로 이동 가능  
 현재 작업 디렉토리를 지정한 디렉토리로 변경  

```bash
$ cd Linux
$ pwd
/c/Workspace/Linux

$ cd ..
$ pwd
/c/Workspace

$ cd /
$ pwd
/

$ cd C/Workspace/Linux
$ pwd
/C/Workspace/Linux
```

## ls (List)
>  현 디렉토리의 목록을 확인 일반적으로 ls -al사용
>>-a .을 포함한 모든 파일과 디렉토리를 표시,   
>>-l 지정한 디렉토리 내용을 자세히 표시
```bash
$ ls -al
total 8
drwxr-xr-x 1 thlee 197609 0  7월  6 23:16 ./
drwxr-xr-x 1 thlee 197609 0  7월  6 23:24 ../
drwxr-xr-x 1 thlee 197609 0  7월  6 22:29 Linux/
```
>ls -1 : 파일명을 List 형식으로 출력  
>ls-h : 용량을 표시  
>ls -alt : 시간순 정렬  
>ls -altr : 시간 역순 정렬  

## df (Disk Free)
> 마운트된 모든 장치에 대한 현재의 디스크   
공간 통계를 출력  
```bash
$ df
Filesystem           1K-blocks      Used Available Use% Mounted on
C:/Program Files/Git 486413104 239931368 246481736  50% /
D:                      592892     14824    578068   3% /d
```
> df -h (human readerble)
```bash
$ df -h
Filesystem            Size  Used Avail Use% Mounted on
C:/Program Files/Git  464G  229G  236G  50% /
D:                    579M   15M  565M   3% /d
```
> df -T (Type)를 통해 디스크 타입 확인 가능
```bash
$ df -T
Filesystem           Type 1K-blocks      Used Available Use% Mounted on
C:/Program Files/Git ntfs 486413104 239932092 246481012  50% /
D:                   ntfs    592892     14824    578068   3% /d
```
> df -i (inodes) 를 통해 inodes의 사용, 잔여 등을 확인 가능
```bash
$ df -i
$ df -i
Filesystem           Inodes IUsed IFree IUse% Mounted on
C:/Program Files/Git      -     -     -     - /
D:                        -     -     -     - /d
```

