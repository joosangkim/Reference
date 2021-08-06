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

---
