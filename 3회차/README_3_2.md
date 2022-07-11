### 리눅스 기초 명령어 -프로세스 관련 명령어-

> 프로세스 : 프로그램과 작업내용이 메모리에 올라가서 실행되는 작업 단위
## ps (Process Status)
> 시스템에서 실행 중인 프로세스에 대한 정보를 출력  
> ps -ef, ps aux 두가지를 가장 많이 사용
> ps auxwwwww w가 많아질수록 명령어 확인 개수가 많아짐
```bash
$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 Jul04 ?        00:00:09 /usr/lib/systemd/systemd --switc
root         2     0  0 Jul04 ?        00:00:00 [kthreadd]


$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.5 123592  5520 ?        Ss   Jul04   0:09 /usr/lib/system
root         2  0.0  0.0      0     0 ?        S    Jul04   0:00 [kthreadd]
```

## pstree(Process Status TREE)
> 시스템에서 실행 중인 프로세스에 대한 정보를 트리구조로 출력
```bash
$ pstree
systemd─┬─acpid
        ├─2*[agetty]
        ├─amazon-ssm-agen─┬─ssm-agent-worke───7*[{ssm-agent-worke}]
        │                 └─7*[{amazon-ssm-agen}]
        ├─atd
        ├─auditd───{auditd}
        ├─chronyd
        ├─crond
        ├─dbus-daemon
        ├─2*[dhclient]
        ├─gssproxy───5*[{gssproxy}]
```

## top
> 프로세스의 목록을 일정 시간마다 새로고침하여 화면에 출력하는 툴  
> 시스템의 전반적인 상황을 모니터링 할 수 있음
```bash
$ top
top - 16:23:03 up 6 days, 23:39,  1 user,  load average: 0.00, 0.00, 0.00
Tasks:  95 total,   2 running,  52 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.3 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :   988672 total,   232144 free,   112256 used,   644272 buff/cache
KiB Swap:        0 total,        0 free,        0 used.   731776 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND
 3286 root      20   0  730740  31320  14572 S  0.3  3.2   0:17.35 ssm-agent-worke
    1 root      20   0  123592   5520   3936 S  0.0  0.6   0:09.30 systemd
    2 root      20   0       0      0      0 S  0.0  0.0   0:00.04 kthreadd
```