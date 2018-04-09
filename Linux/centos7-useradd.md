VPS에 처음 서버를 할당받으면 ssh 접속 정보를 받는다. 하지만 기본 세팅에 무차별 공격을 하는 해커들이 있기에 변경하는 것들이 있다. 대표적으로 [ssh port를 변경하는 것](https://cherrypick.co.kr/ssh-change-port/)이 있다. 그 외에도 ssh의 root 로그인을 차단하고 계정을 만들어 관리하는 방법 등이 있는데 오늘은 이 부분을 알아볼 예정이다.

### root 로그인 차단

처음 서버를 할당받으면 root 계정의 접속 정보를 받게 되는데 root로 ssh 접속을 한 다음 아래와 같이 설정을 변경하면 root 로그인을 차단할 수 있다.

```bash
$ sudo vi /etc/ssh/sshd_config

PermitRootLogin no # 초기값은 yes로 되어있는데 no로 변경
```

### sshd 서비스 재시작
```bash
systemctl restart sshd
```

### 사용자 추가
다음은 사용자를 추가하는 방법이다. 사용자를 추가하고 비밀번호를 설정할 수 있다. 

```bash
$ useradd 사용자명
$ passwd 사용자명
```

하지만 사용자 추가만으로는 sudo 명령어가 수행되지 않아 sudo 명령어를 사용할 수 있는 권한을 할당해야한다.

### sudo 권한 할당
root 아래에 다음과 같이 추가한다.

```bash
$ vi /etc/sudoers

## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
사용자명     ALL=(ALL)       ALL
```

위의 설정을 마치면 일반 사용자로 sudo 명령 수행이 가능한 것을 확인할 수 있다. 그리고 ssh를 root 말고 새로 생성한 사용자로 접속이 가능함을 확인할 수 있다.


