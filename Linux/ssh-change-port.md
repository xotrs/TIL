## ssh 포트 변경

기존에 AWS를 사용하다가 요금 폭탄을 맞을까 봐 트래픽 무제한인 코노하로 옮겼다. 3년 동안 코노하를 운영하면서 블로그나 가벼운 서비스를 돌리기에는 적합했다. 하지만 최근에 ELK를 구성하고 기술 스택이 폭넓어지면서 서버 사양을 늘려야겠다는 생각을 했다. 더불어서 말끔하게 서버를 세팅해보고 싶은 마음이 생겼다. 그 목적으로 까먹지 않으리라는 다짐을 하며 하나씩 정리할 예정이다.

서버를 설치하고 처음 접근하는 것은 보통 ssh일 것이다. 기존의 ssh 포트는 22번을 사용하고 있지만 보안상의 이슈로 다른 포트로 변경하기를 권장한다.

아래 예제는 CentOS 7.x를 기준으로 작성했다.


### sshd_config 파일 포트 변경
```vim
vi /etc/ssh/sshd_config

#Port 22 # 22번 포트를 자신이 원하는 포트로 변경

```

### ssh_config 파일 포트 변경
```vim
vi /etc/ssh/ssh_config

#Port 22 # 22번 포트를 자신이 원하는 포트로 변경

```

### 방화벽 규칙 추가
```vim
vi /etc/sysconfig/iptables

-A INPUT -m state –state NEW -m tcp -p tcp –dport {포트} -j ACCEPT
```

### ssh 서비스 재시작
```vim
service sshd restart
```

### 방화벽 서비스 재시작
```vim
service iptables restart
```
