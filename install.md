# docker install

docker는 당근 설치를 해야한다.

내가 사용한 

[window]

버전이 낮은 window에서는
[docker toolbox](https://github.com/docker/toolbox) 설치

[ubuntu]
```bash
$ sudo apt update
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
$ sudo apt update
$ apt-cache policy docker-ce
# 사전작업
```

```bash
$ sudo apt install docker-ce
# docker install 
```


```bash
$ sudo systemctl status docker
# 잘 깔렸나 확인
```

