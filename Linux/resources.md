# Linux resource configuration

## process
### ulimit
* 의미: users' limit
* linux 의 유저 당 resource limit 을 의미한다.
* `ulimit -a`: 현재 로그인 된 유저의 리소스 limit
* `/etc/security/limits.conf` 를 수정해서 유저 별 리소스 리미트를 수정한다.
* **`systemd` 로 구동되는 서비스는 `/etc/security/limits.conf` 설정을 무시한다**

### systemd
* `systemd` 는 linux 구동 시 system utility 를 구동 및 관리해주는 데몬이다.
* `systemd` 로 관리되는 서비스들은 `/etc/systemd/system/..` 에 별도로 선언해 주어야 한다.
* 데몬 프로세스의 프로퍼티 목록은 아래에서 확인가능 - https://www.freedesktop.org/software/systemd/man/systemd.exec.html#Process%20Properties

### 참고
* 시스템 최대 fd 확인: `cat /proc/sys/fs/file-max`
* 프로세스가 할당 받은 resource limit 확인:
```sh
ps -ef | grep KEYWORKD # pid 확인
cat /proc/$PID/limits
```

## POSIX Signal
* POSIX 기반 시그널 중 자주 사용되는 시그널들을 정리
* `SIGTERM`: 프로세스에 종료 시스널을 보낸다. SIGKILL 과는 다르게, 프로세스는 이 시그널을 받아드리거나 무시할 수 있다.  프로세스 종료 시 안전한 종료를 보장 할 수 있다.
* `SIGHUP`: 프로세스가 사용 중인 수도 터미널 혹은 가상 터미널을 **닫을** 때 보내는 시그널. 현대 응용프로그램에서는 설정파일 혹은 로그파일 등을 리로드 할 때 사용.
* `SIGINT`: 사용자가 프로세스가 사용 중인 터미널에 인터럽트를 보낼 때 사용한다. 보통 `ctrl+c` 로 구동된다.
* `SIGQUIT`: 사용자가 프로세스에 종료 시스널을 보내고 core dump 를 수행하게 한다.
* `SIGUSR1,2`: 사용자 정의 신호를 전달한다.


---
