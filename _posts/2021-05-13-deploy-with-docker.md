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
