# dockerhub
> docker는 dockerhub를 제공하여 IMAGE를 쉽게 업/다운로드 할 수 있으며 공유할 수 있음!

## dockerhub사용법

1. shell에서 dockerhub에 로그인
```bash
$ docker login
```

2. 태그와 함께 dockerhub에 push
```bash
$ docker tag [IMAGE_NAME]:latest [DOCKER_ID]/[IMAGE_NAME]:latest
# 태그 생성 or 수정하는 커맨드

$ docker push [DOCKER_ID]/[IMAGE_NAME]:latest
# build시 버전명시를 안하면 default로 "latest" 버전이된다.
```

> tag를 작성할 때 `[자신의 도커아이디]/[이미지이름]`으로 작성해야함.

*로그인된 유저의 이름과 태그의 앞부분이 일치하지 않을 시 permission denied가 발생하고,
단순하게 자신의 도커아이디로 hub 내 repository의 소유주를 식별한다.*

3. pull 받는 법

```bash
$ docker search [IMAGE_NAME]
# dockerhub에 올라온 이미지들 리스트를 확인한 후 

$ docker pull [IMAGE_NAME]
```

4. pull 받은 뒤 실행
```bash
$ docker run -d -p 8000:8000 --name [IMAGE_NAME] [DOCKER_ID]/[IMAGE_NAME]:latest
# 해당 이미지를 8000번포트에 바인딩하고, 백그라운드에서 실행시키겠다.
```
- -d 옵션 : 데몬모드라고 부르며, 백그라운드에서 실행하겠다.
- -p 옵션 : 호스트에 연결된 컨테이너의 특정 포트를 외부에 노출(포트 열어준다고 생각하면 편함)
    - -p <호스트 포트>:<컨테이너 포트>
