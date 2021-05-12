---
title: "임시 Requirements.txt"
date: 2021-05-11 08:26:28 -0400
categories: python
---

Python으로 작업한 프로젝트를 Docker 이미지로 배포할 때  
requirements에 추가된 패키지를 포함해서 이미지로 생성할 수 있는 방법을 검토한다.

## Dockerfile 작성

```dockerfile
FROM python:3.9.4

ENV LANG C.UTF-8

WORKDIR /usr/local
COPY '../requirements.txt' /usr/local
RUN pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt

EXPOSE 5000
```
이미지 생성  

> 하기와 같이 카피할 파일이 상위 디렉토리에 있는 경우 Dockerfile를 상위 디렉토리에서 실행할 수 있도록 해야 한다.

```dockerfile
COPY ../requirements.txt /usr/local
```

https://docs.docker.com/engine/reference/builder/ 의 아래의 코멘트 참조
```
ADD obeys the following rules:

The <src> path must be inside the context of the build; you cannot ADD ../something /something, because the first step of a docker build is to send the context directory (and subdirectories) to the docker daemon.

If <src> is a URL and <dest> does not end with a trailing slash, then a file is downloaded from the URL and copied to <dest>.

If <src> is a URL and <dest> does end with a trailing slash, then the filename is inferred from the URL and the file is downloaded to <dest>/<filename>. For instance, ADD http://example.com/foobar / would create the file /foobar. The URL must have a nontrivial path so that an appropriate filename can be discovered in this case (http://example.com will not work).

If <src> is a directory, the entire contents of the directory are copied, including filesystem metadata.
```

## Docker 빌드

```sh
# name:tag의 :tag는 옵션
# docker build -t <name:tag> -f <dockerfile-path>
docker build -t tedisfree:latest -f build/dockerfile
```

빌드한 이미지가 생성되었어 있는지 확인

```sh
docker images
```

## Docker 이미지를 파일로 저장

```sh
docker image save tedisfree:latest -o tedisfree.tar
```

## 파일에서 이미지 불러오기 

```sh
docker load -i tedisfree.tar
```

## 컨네이터 생성

```sh
docker run -dit --name tedisfree -p 5000:5000 tedisfree
```



