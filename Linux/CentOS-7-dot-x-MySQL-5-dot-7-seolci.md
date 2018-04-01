ssh 세팅을 마치고 MySQL을 이전하기 위해 설치를 진행했다. 5.7 버전으로 설치하는데 바뀐 것이 많이 있어서 정리한다.

```
https://dev.mysql.com/downloads/repo/yum/
```

위의 주소에서 wget을 통해 최신 버전으로 설치했다. 2018년 4월 1일 기준으로 mysql57-community-release-el7-11.noarch.rpm이 최신이다. wget이 없다면 wget을 설치한다.

### wget 설치
```bash
$ yum install wget
```
<br>
### MySQL 다운로드
```bash
$ wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
```
<br>
### MySQL 설치
```bash
$ sudo rpm -ivh mysql57-community-release-el7-11.noarch.rpm
```
<br>
### MySQL 서버 설치
```bash
$ sudo yum install mysql-server
```
<br>
### 서비스 시작
```bash
$ sudo systemctl start mysqld
```
<br>
MySQL은 루트 로그인이나 샘플 유저와 같이 보안 수준이 낮은 기본 옵션을 변경해주는 보안 스크립트가 포함 되어있다. 
### 보안 스크립트 실행
```bash
$ sudo mysql_secure_installation
```

기본 루트 암호를 묻는 메세지가 나타난다. 그 다음 새로운 비밀번호를 입력을 요구하는 메세지가 나타난다.

```bash
The existing password for the user account root has expired. Please set a new password.

New password:
```

MySQL 5.7 버전으로 넘어오면서 password validation에 대한 강도가 높아졌다. 하나 이상의 대문자, 숫자, 특수 문자가 포함 된 12자리의 암호를 요구한다. 암호를 입력하면 암호 강도에 대한 피드백을 받게 되며, 익명의 사용자의 삭제 및 루트의 리모트 로그인을 막을 것인지 대한 질문들을 한다.

설치가 완료됐다. 하지만 설정이 잘못 되었는지 설치까지는 온전히 진행이 되었으나 로그인이 진행되지 않았다. 그래서 루트의 비밀번호를 재설정했다.

<br>
## 비밀번호 재설정
### MySQL 정지

```bash
$ systemctl stop mysqld
```
<br>
### MySQL 환경 옵션 설정

기존의 솔루션은 mysqld safe를 통해 재설정을 진행하는 것이다. 하지만 MySQL 5.7.6부터 RPM 배포판을 사용해서 설치하는 경우에는 systemd에서 관리를 하기 때문에 mysqld safe가 필요 없어 설치가 되지 않는다. 아래와 같은 환경 옵션을 설정 해준다.

```bash
$ systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"
```
<br>
### MySQL 시작

```bash
$ systemctl start mysqld
```
<br>
### MySQL 로그인

루트의 비밀번호 없이 로그인 가능
```bash
$ mysql -u root
```
<br>
### 루트 비밀번호 변경

5.7부터 비밀번호 컬럼이 password에서 authentication_string으로 변경됐다.
```bash
mysql> UPDATE mysql.user SET authentication_string = PASSWORD('새로운 비밀번호')
    -> WHERE User = 'root' AND Host = 'localhost';
mysql> FLUSH PRIVILEGES;
mysql> exit
```
<br>
### MySQL 정지
```bash
$ systemctl stop mysqld
```
<br>
### MySQL 환경 옵션 설정 해제

다음 접속부터는 정상적으로 로그인할 수 있도록 환경 옵션 설정 해제를 한다.
```bash
$ systemctl unset-environment MYSQLD_OPTS
```
<br>
### MySQL 시작
```bash
$ systemctl start mysqld
```
<br>
### MySQL 로그인
```bash
$ mysql -u root -p
```

정상적으로 로그인이 되는 걸 확인할 수 있다. 그러나 로그인 해서 쿼리를 날려보니까 또 문제가 있다. 아래와 같은 메세지를 출력한다.
```bash
You must reset your password using ALTER USER statement before executing this statement.
```

비밀번호를 재설정하라고 한다. 위에서 재설정을 했는데 왜 그런걸까... 아직 이건 잘 모르겠다. 일단 재설정 해본다.

```bash
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY '비밀번호';
mysql> FLUSH PRIVILEGES;
```
<br>
재설정이 잘 되었다. 다시 한번 쿼리를 날려본다. 그랬더니 또 다음과 같은 메세지를 출력한다.
```bash
Your password does not satisfy the current policy requirements
```
<br>
이번에는 재설정한 비밀번호가 MySQL password validation에 맞지 않는다라는 메세지이다.

기존의 잘 사용하던 비밀번호를 바꾸기 싫어서 나는 password validation을 삭제했다. password validation을 지킬려면 비밀번호를 다시 변경하면 될거같다.
<br>
### MySQL 로그인 후 password validation 삭제

```bash
$ mysql -u root -p
```

```bash
mysql> uninstall plugin validate_password;
```

삭제하고 다시 해보니 잘 진행된다. 설치는 잘 된거 같고 마지막으로 사용자 추가와 외부 접근 허용 하는 것이 남았다. 루트는 로컬에서만 접속 가능하고 특정 사용자는 외부에서 접속 가능하도록 설정을 했다.
<br>
### 사용자 추가
```bash
mysql> create user '사용자'@'localhost' identified by '비밀번호';
```
<br>
### 권한 부여 
모든 디비에 어디서든 접속할 수 있는 권한을 줬다. 사실 이러면 루트랑 다를 것도 없는데 최소한의 보안을 위해서 이렇게 진행했다.
```bash
mysql> grant all privileges on *.* to '사용자'@'%';
```
<br>
### 외부 접속 허용

외부의 MySQL 워크벤치와 같은 툴에서 접속을 가능하게 하기 위해서 아래의 설정을 추가한다.
```bash
$ vi /etc/my.cnf
bind-address 0.0.0.0 # 없으면 추가해준다.
```
