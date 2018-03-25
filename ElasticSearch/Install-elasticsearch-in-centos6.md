## ElasticSearch 5.x 설치

엘라스틱서치는 기본적으로 Java 1.8을 필요로 한다. 기존의 서버에 Java 1.8이 설치되어있어 설명은 생략한다.

### Import GPG KEY
```bash
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

### Repo 파일 생성
```bash
[elasticsearch-5.x]
name=Elasticsearch repository for 5.x packages
baseurl=https://artifacts.elastic.co/packages/5.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```

### 엘라스틱서치 설치
```bash
sudo yum install elasticsearch
```

### chkconfig 등록
```bash
sudo chkconfig --add elasticsearch
```

### Config 수정
```bash
network.host: 0.0.0.0 # 외부 접근 가능
transport.host: 127.0.0.1
```

### Port 오픈
```bash
vi /etc/sysconfig/iptablesElasticSearch

#elasticsearch
-A INPUT -m state --state NEW -m tcp -p tcp --dport 9200 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 9300 -j ACCEPT
```

### 리눅스 커널 파라미터 확인 및 수정
```bash
cat /proc/sys/fs/file-max
sudo sysctl -w fs.file-max=65536
```

### limits.conf 설정 추가
여기서 elasticsearch는 엘라스틱서치를 실행하는 계정으로 변경해야 한다. 기본은 elasticsearch이다.

```bash
vi /etc/security/limits.conf

elasticsearch hard nofile 65536
elasticsearch soft nofile 65536
elasticsearch hard nproc  65536
elasticsearch soft nproc  65536
```

서버 재시작

### 서비스 시작
```bash
sudo service elasticsearch start
```


보통 ELK 스택을 같이 설치하지만 현재 사용하고 있는 서버의 메모리가 1GB 밖에 되지 않아 Log Stash, Kibana를 설치하고 확인해보지 못했다. 추후 서버를 옮기고 아래에 Log Stash, Kibana 설치법에 대해 정리할 예정이다.
