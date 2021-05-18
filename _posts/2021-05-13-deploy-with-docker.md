컨테이너 생성

```bash
docker load -i image.tar

docker run -it \
  -p 8000:3000 \
  --mount type=bind, source=/canon,target=/canon \
  image.tar
```

전체 이미지 삭제 

```sh
# Linux
docker rmi $(docker images -q)

# Windows
for /F "tokens=*" %a in ('docker images -q') do docker rmi %a
```

전체 컨테이너 삭제

```sh
docker rm $(docker ps -a -q)
```

# Docker Container 생성시 환경 변수를 추가할 수 있는 방법은 없을까

같은 목적의 container를 여러개 생성할 때, 구분을 위해 환경 변수로 인덱싱할 수 없는지 확인해 보자.

> `-e` 옵션을 사용

```
docker run -d --name test-cont -e "ENV=value" test-img
```


# Dockerfile Argument 사용

```dockerfile
ARG my_name

# 환경 변수로 추가하기 위해서는 ENV 사용
ENV MY_NAME=$my_name
```

```sh
docker build ... --build-arg my_name=Ted .
```
