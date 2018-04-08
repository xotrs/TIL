서버 이전을 하면서 블로그도 같이 이전을 하려고 시도 중이다. 현재 고스트 블로그에서 지원하는 node.js 버전은 4.5, 6.9, 8.9 이렇게 3가지가 있다. 기존의 VPS에서는 6.9 버전으로 블로그를 운영했는데 migration 하는 김에 8.9 버전으로 올리려고 node.js 설치하는 법을 알아봤다. node.js는 현재 패키지 매니저를 통해서 설치할 시 8.1 LTS가 설치된다. 나는 8.9가 필요했기 때문에 nvm을 통해서 설치했다. nvm은 Node Version Manager로서 node.js 버전을 관리해준다. 설치 방법을 알아보면 다음과 같다.

### nvm 설치

```bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```
nvm을 설치하고 나서는 터미널을 껐다 켜야 한다. 제대로 설치되었는지 확인을 해보자. 

```bash
$ nvm --version
0.33.8
```
제대로 설치되었다. 다음으로 node.js 버전을 확인해보자. 

```bash
$ nvm ls-remote
```

버전이 많기 때문에 리스팅 되는데 꽤 많은 시간이 걸린다. 그 중에서 자기가 설치하고 싶은 버전을 확인한다.

### node.js 설치
```language-bash
$ nvm install 8.9.0
```

위 명령어를 치면 nvm에서 알아서 설치해준다. node.js가 제대로 설치 되었는가 확인해보자.

```bash
$ node -v
v8.9.0

$ npm -v
v5.5.1
```



