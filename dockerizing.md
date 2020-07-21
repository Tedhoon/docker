# dockerizing
> dockerfile을 이용해서 한 번에 실행가능한 docker image를 build하는 것

## 기본 순서
1. dockerfile작성

2. 해당 dockerfile을 기반으로 image생성(build)


## dockerfile 작성법

- `FROM`

최상단에 써주면 된다.
IMAGE를 build할 때 기존 이미지를 기반으로 환경을 구성할 수 있는데,
어떤 이미지를 기반으로 새로운 이미지를 생성할 것인지를 나타낸다. 


- `ADD`

build 과정중 호스트의 파일 시스템으로부터 파일을 가져오는 것이다.
말 그대로 이미지에 파일을 더한다.


- `COPY`

파일을 이미지에 추가한다.
COPY <복사할 파일 경로> <이미지에서 파일이 위치할 경로> 형식


- `RUN`

RUN 커맨드는 쉘에서 입력할 값을 써주면된다.

- `CMD`

컨테이너 실행 시, 실행될 명령어를 정해준다.
build 후 해당 이미지를 run할 때 실행되는 명령어이기 때문에 한 번만 쓸 수 있다.
그래서 run명령어를 여러개 하고싶으면... 따로 파일을 빼서 하면된다!(불확실)

*`ENTRYPOINT` 명령어와는 조금 다른데, 그건 나중에 포스팅하게씀*


### 친절하게 예시를 첨부해드리겠다.
- for deploying django at 8000

```dockerfile
FROM python:3.6
# python 3.6 이미지를 환경으로 사용하기 위해 가져옴

RUN apt-get update \ 
	&& apt-get install -y --no-install-recommends \
		postgresql-client \
	&& rm -rf /var/lib/apt/lists/*

COPY . /app
# 나의 Django 코드를 컨테이너에 복사합니다.

RUN pip install -r /app/LittleAchievement/requirements.txt  
# requirements.txt에 적혀있는 pip 패키지들을 설치합니다.

EXPOSE 80
EXPOSE 8000  
# 80, 8000번 포트를 expose합니다.

WORKDIR /app/LittleAchievement/
# 요놈은 CMD 관련 워킹디렉토리 지정

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```


## image build 하기
```bash
$ docker build --tag=[tagname] .
``` 
dockerfile이 있는 경로에서 위의 커맨드를 입력하면
[tagname]을 이름으로 가진 IMAGE가 만들어진다.(build된다)

*맨 뒤에 "." 주의할 것! (현재 디렉토리를 build하겠다는 뜻)*

.
.
.

잘 입력했다면..
까만창이 주르륵 내려오면서 build되고,
중간에 에러가 나면 vi를 이용해서 dockerfile을 수정하고 재빌드 하면된다.
에러 전까지 빌드된 내용은 cache를 이용해서 빠르게 지나간다.
