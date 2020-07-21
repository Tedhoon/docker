# Docker

> 가상머신의 효과를 낼 수 있지만 OS를 띄우지 않기 때문에 가상머신은 아니다.

### 설치 스크립트
```python
# 14.04 LTS 64비트 기준
# linux
$ sudo wget -qO- https://get.docker.com/ | sh
```
```python
# 14.04 LTS 64비트 기준
# ubuntu
$ sudo apt-get update
$ sudo apt-get install docker.io
$ sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker
```

😽 더 자세한 install법은 [요기](https://github.com/Tedhoon/docker/blob/master/install.md)

### docker의 이미지 list확인
```shell
$ docker images
```

### 이미지 검색

```shell
$ docker search [IMAGE_NAME]
```
search기능을 통해서 사용자가 만들어서 올린 ubuntu version별 이미지를 검색할 수 있음



### 도커허브에서 이미지 받아오기

```shell
$ docker pull ubuntu:14.04
```
우분투 14.04를 받아오는게 아니라 우분투의 패키지매니저만 받아와서 apt-get등을 쓸 수 있음

- 이미지 : 실행파일과 라이브러리를 종합해둔 것
- 컨테이너 : 이미지를 실행한 상태

### 이미지 실행
```shell
$ docker run -it ubuntu:14.04 /bin/bash
```

해당이미지의 컨테이너 생성과 함께 실행

-i옵션 : 사용자의 입출력 허용

-t옵션 : 가상터미널 환경을 에뮬레이션

그 안의 bash를 메인실행파일로 지정, 그리고 실행

### 그러면 이제부터 컨테이너 속에서 작업

예시
```bash
$ sudo apt-get update
$ sudo apt-get install git
```


컨테이너 종료 및 탈출
```bash
$ exit
```
프로세스 확인(종료된 프로세스는 뜨지않음)
```shell
$ docker ps -a
```
이력과 함께 종료된 프로세스까지 열람가능



### 컨테이너 다시 실행
```shell
$ docker start [Name또는 컨테이너 ID]
```

본 명령어는 실행만하고 컨테이너 안으로 들어가지는 않음

run은 생성, 실행, 접속

docker run 실행시 이름을 줄 수도있고 주지않았다면 자동으로 생성해줌. 생성된 이름은 위 ps -a 스크립트의 NAMES에서 확인가능


### 컨테이너 들어가기
```shell
$ docker attach [Name또는 컨테이너 ID]
```

### 컨테이너 빠져나오기(실행유지)
```shell
Ctrl + pq
## 근데이건 bash단축키임
```

### 컨테이너 종료
```shell
$ docker stop [Name또는 컨테이너 ID]
```

### 컨테이너 삭제
```shell
$ docker rm [Name또는 컨테이너 ID]
```

### 이미지 삭제
```shell
$ docker rmi hello-world
```


## 대충 실습해보자 🤔

Nginx가 설치된 image를 받아온다.
```shell
$ docker pull nginx:latest
```
가장 최신 버전 받아오자!

```shell
$ docker run -d --name myname nginx:latest
```
-d옵션은 그냥 백그라운드에서 실행(입출력필요가 없을 때)

--name 옵션으로 이름 설정가능

-p옵션으로 포트도 지정해줄 수 있다.


```shell
$ docker ps -a
```

확인해보면 잘떴다능..

## 메인실행 말고 서브실행해보기(exec)
```shell
$ docker exec [CONTAINER_NAME] touch hello.txt
```




## 찾아봤던 tip
```shell
$ docker logs -f [container ID]
=> 실행중인 데몬의 로그를 알 수 있음

$ docker inspect [container ID] | grep "IPAddress"
=> 컨테이너의 아이피 어드레스 추출!
```
