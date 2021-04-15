---
title: "리눅스 Restart 서비스"
date: 2021-04-15 08:26:28 -0400
categories: linux daemon  
---

# 개요

특정 목적으로 어떤 daemon이 종료되지 않고 지속적으로 서비스할 수 있도록 유지하는 방법을 검토한다. 

리눅스 systemd service에 `Restart`옵션을 설정하는 방법으로 간단하게 적용이 가능하다.

## 예

```
[Unit]
Description=The Apache HTTP Server
After=network.target remote-fs.target nss-lookup.target
Documentation=man:httpd(8)
Documentation=man:apachectl(8)

[Service]
Type=notify
EnvironmentFile=/etc/sysconfig/httpd
ExecStart=/usr/sbin/httpd $OPTIONS -DFOREGROUND
ExecReload=/usr/sbin/httpd $OPTIONS -k graceful
ExecStop=/bin/kill -WINCH ${MAINPID}
KillSignal=SIGCONT
PrivateTmp=true
# 하기의 2라인 추가
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```

# 테스트

간단하게 현재 실행중인 도커 컨테이너의 개수를 확인하는 스크립트를 작성하고 확인해 보자.

## 실행중인 Docker Container 개수 확인 스크립스 생성 

```bash
#!/bin/bash

# 더 좋은 방법이 있겠지만 여기에선 이게 중요한게 아니니까..

while :
do
        ds=`docker ps -q | wc -l`
        echo "ds=$ds"
        sleep 30
done
```

## 서비스 생성

/etc/system.d/system 에 dockmon.service 파일을 생성

```sh
[Unit]
Description=Dockmon

[Service]
Type=simple
ExecStart=/etc/dockmon/dockmon.sh
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```

## 서비스 시작 

```sh
# 서비스 스타트
systemctl start dockmon

# 서비스 상태 확인
systemctl status dockmon
```

## 부팅 후 자동 시작되도록 등록

```sh
systemctl enable dockmon
Created symlink from /etc/systemd/system/multi-user.target.wants/dockmon.service to /etc/systemd/system/dockmon.service.
```


# 참고자료

[Ensure systemd services restart on failure](https://jonarcher.info/2015/08/ensure-systemd-services-restart-on-failure/) 

# 그외의 방법

[Monitor and restart apache or lighttpd webserver when daemon is killed](https://www.cyberciti.biz/tips/howto-monitor-and-restart-linux-unix-service.html)
