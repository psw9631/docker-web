\# Docker Web Project



WSL Ubuntu 환경에서 Docker 기반 개발 워크스테이션을 구축하고, Dockerfile을 이용해 nginx 웹 서버 커스텀 이미지를 제작한 프로젝트입니다.



GitHub Repository:



```

https://github.com/psw9631/docker-web

```



\---



\## 1. 프로젝트 개요



이 프로젝트의 목표는 CLI 터미널 기반으로 개발 워크스테이션을 구축하고, Docker와 Git/GitHub를 활용하여 웹 서버 컨테이너를 실행 및 검증하는 것입니다.



주요 수행 내용은 다음과 같습니다.



\- WSL Ubuntu 환경에서 터미널 기본 명령어 실습

\- 파일 및 디렉터리 권한 변경 실습

\- Docker 설치 및 동작 확인

\- Docker 기본 운영 명령 실습

\- Dockerfile 기반 커스텀 nginx 웹 서버 이미지 제작

\- 포트 매핑을 통한 웹 서버 접속 확인

\- 바인드 마운트를 통한 파일 변경 반영 확인

\- Docker 볼륨을 이용한 데이터 영속성 확인

\- Git 설정 및 GitHub 원격 저장소 연동

\- 수행 로그와 검증 증거 문서화



\---



\## 2. 실행 환경



| 항목 | 내용 |

|---|---|

| OS | Windows + WSL Ubuntu |

| Shell | bash |

| Terminal | WSL Ubuntu Terminal 또는 VSCode Terminal |

| Docker | Docker Desktop with WSL Integration |

| Git | WSL Ubuntu 환경의 Git |

| Web Server | nginx |

| Repository | GitHub |



\### Docker 버전 확인



```

docker --version

```



출력 결과:



```

Docker version 29.9.2, build a82e528

```



\### Docker 데몬 동작 확인



```

docker info

```



출력 결과 일부:



```

Client:

\&#x20;Version:    29.9.2

\&#x20;Context:    default

\&#x20;Debug Mode: false

\&#x20;Plugins:

\&#x20; agent: Docker AI Agent Runner (Docker Inc.)

\&#x20;   Version:  v1.152.0

\&#x20;   Path:     /usr/local/lib/docker/cli-plugins/docker-agent

...

```



\### Git 버전 확인



```

git --version

```



출력 결과:



```

git version 2.53.0




```



\---



\## 3. 프로젝트 구조



```

docker-web/

├── Dockerfile

├── index.html

├── README.md

└── docs/

\\\\\\\&#x20;   └── images/

\\\\\\\&#x20;       ├── port-8080.png

\\\\\\\&#x20;       ├── bind-before.png

\\\\\\\&#x20;       ├── bind-after.png

\\\\\\\&#x20;       ├── vscode-github.png

\\\\\\\&#x20;       └── github-repository.png

```



`docs/images/` 폴더에는 포트 접속 화면, 바인드 마운트 변경 전/후 화면, VSCode GitHub 연동 화면 등의 증거 이미지를 저장합니다.



\---



\## 4. 수행 항목 체크리스트



| 구분 | 수행 여부 | 증거 위치 |

|---|---:|---|

| 터미널 기본 명령어 실습 | 완료 | 5장 |

| 파일/디렉터리 권한 실습 | 완료 | 6장 |

| Docker 설치 및 점검 | 완료 | 7장 |

| Docker 기본 운영 명령 | 완료 | 8장 |

| hello-world 실행 | 완료 | 9장 |

| ubuntu 컨테이너 실행 및 내부 명령 | 완료 | 9장 |

| attach/exec 차이 관찰 | 완료 | 9장 |

| Dockerfile 작성 | 완료 | 10장 |

| 커스텀 이미지 빌드 | 완료 | 10장 |

| 컨테이너 실행 | 완료 | 10장 |

| 포트 매핑 접속 확인 | 완료 | 11장 |

| 바인드 마운트 확인 | 완료 | 12장 |

| Docker 볼륨 영속성 확인 | 완료 | 13장 |

| Git 설정 | 완료 | 14장 |

| GitHub 저장소 업로드 | 완료 | 14장 |

| VSCode GitHub 연동 | 완료 | 14장 |

| 트러블슈팅 2건 이상 | 완료 | 15장 |



\---



\## 5. 터미널 조작 로그



CLI 기반으로 기본 파일 시스템 명령어를 실습했습니다.



\### 현재 위치 확인



```

pwd

```



출력 결과: 



```

/home/psw/docker-web

```



\### 목록 확인



```

ls

```



출력 결과:



```

Dockerfile  README.md  index.html

```



\### 숨김 파일 포함 목록 확인



```

ls -la

```



출력 결과:



```

total 52

drwxr-xr-x 3 psw psw  4096 Nov  2 13:00 .

drwxr-x--- 9 psw psw  4096 Nov  2 12:43 ..

drwxr-xr-x 7 psw psw  4096 Nov  2 13:07 .git

\-rw-r--r-- 1 psw psw    68 Nov  2 10:50 Dockerfile

\-rw-r--r-- 1 psw psw 29272 Nov  2 13:07 README.md

\-rw-r--r-- 1 psw psw   217 Nov  2 12:03 index.html

```



\### 디렉터리 생성



```

mkdir cli-practice

ls

```



출력 결과:



```

Dockerfile  README.md  cli-practice  index.html

```



\### 디렉터리 이동



```

cd cli-practice

pwd

```



출력 결과:



```

/home/psw/docker-web/cli-practice

```



\### 빈 파일 생성



```

touch memo.txt

ls -la

```



출력 결과:



```

ls -la

total 8

drwxr-xr-x 2 psw psw 4096 Nov  2 13:10 .

drwxr-xr-x 4 psw psw 4096 Nov  2 13:10 ..

\-rw-r--r-- 1 psw psw    0 Nov  2 13:10 memo.txt

```



\### 파일 내용 작성 및 확인



```

echo "terminal practice" > memo.txt

cat memo.txt

```



출력 결과:



```

terminal practice

```



\### 파일 복사



```

cp memo.txt memo-copy.txt

ls

```



출력 결과:



```

ls

memo-copy.txt  memo.txt

```



\### 파일 이동 및 이름 변경



```

mv memo-copy.txt memo-renamed.txt

ls

```



출력 결과:



```

ls

memo-renamed.txt  memo.txt

```



\### 파일 삭제



```

rm memo-renamed.txt

ls

```



출력 결과:



```

ls

memo.txt

```



\### 상위 디렉터리 이동



```

cd ..

pwd

```



출력 결과:



```

/home/psw/docker-web

psw@5F-125:\~/docker-web$



```



\---



\## 6. 권한 실습 로그



Linux 파일 권한의 의미는 다음과 같습니다.



| 권한 | 의미 |

|---|---|

| r | read, 읽기 |

| w | write, 쓰기 |

| x | execute, 실행 또는 디렉터리 진입 |



숫자 권한은 다음 규칙으로 계산합니다.



| 숫자 | 권한 |

|---:|---|

| 4 | read |

| 2 | write |

| 1 | execute |



예를 들어 `755`는 다음과 같습니다.



```

소유자: 7 = 4 + 2 + 1 = rwx

그룹:   5 = 4 + 1     = r-x

기타:   5 = 4 + 1     = r-x

```



`644`는 다음과 같습니다.



```

소유자: 6 = 4 + 2 = rw-

그룹:   4 = r--

기타:   4 = r--

```



\### 파일 권한 변경 실습



파일 생성 및 변경 전 권한 확인:



```

touch permission-file.txt

ls -l permission-file.txt

```



변경 전 출력:



```

ls -l permission-file.txt

\-rw-r--r-- 1 psw psw 0 Nov  2 13:12 permission-file.txt

```



파일 권한을 `644`로 변경:



```

chmod 644 permission-file.txt

ls -l permission-file.txt

```



변경 후 출력:



```

ls -l permission-file.txt

\-rw-r--r-- 1 psw psw 0 Nov  2 13:12 permission-file.txt

```



\### 디렉터리 권한 변경 실습



디렉터리 생성 및 변경 전 권한 확인:



```

mkdir permission-dir

ls -ld permission-dir

```



변경 전 출력:



```

ls -ld permission-dir

drwxr-xr-x 2 psw psw 4096 Nov  2 13:14 permission-dir

```



디렉터리 권한을 `755`로 변경:



```

chmod 755 permission-dir

ls -ld permission-dir

```



변경 후 출력:



```

drwxr-xr-x 2 psw psw 4096 Nov  2 13:14 permission-dir

psw@5F-125:\~/docker-web$

```



\---



\## 7. Docker 설치 및 기본 점검



\### Docker 버전 확인



```

docker --version

```



출력 결과:



```

Docker version 29.9.2, build a82e528

```



\### Docker 데몬 상태 확인



```

docker info

```



출력 결과 일부:



```

Client:

&#x20;Version:    29.9.2

&#x20;Context:    default

&#x20;Debug Mode: false

&#x20;Plugins:

&#x20; agent: Docker AI Agent Runner (Docker Inc.)

&#x20;   Version:  v1.152.0

&#x20;   Path:     /usr/local/lib/docker/cli-plugins/docker-agent

&#x20; ai: Docker AI Agent - Ask Gordon (Docker Inc.)

```



Docker 명령이 정상 출력되므로 Docker Desktop과 WSL 연동이 정상적으로 동작함을 확인했습니다.



\---



\## 8. Docker 기본 운영 로그



\### 이미지 다운로드



```

docker pull nginx:alpine

```



출력 결과:



```

alpine: Pulling from library/nginx

b9b388a21ecf: Pull complete

7cc330898115: Pull complete

7b229517ed22: Pull complete

12b85cff06fd: Pull complete

657023555a2a: Pull complete

2ec5fb117ffa: Pull complete

26185d08a3ec: Pull complete

9b0f7dfe35b2: Pull complete

a4d5b1f57abc: Download complete

acc2d54c3743: Download complete

Digest: sha256:785835ea65db4bba6f021acc0f3be91b0fef76a53fe41f8588c6698d2aed0606

Status: Downloaded newer image for nginx:alpine

docker.io/library/nginx:alpine

```



\### 이미지 목록 확인



```

docker images

```



출력 결과:



```

docker-web:latest    e23e907a46ad        241MB         63.9MB    U

hello-world:latest   c567b231f656       25.9kB         9.49kB    U

my-web:latest        7e7d5e50e1e2        241MB         63.9MB

nginx:alpine         785835ea65db       94.5MB         27.2MB

nginx:latest         5ab5b0b01097        243MB         66.8MB

ubuntu:latest        6a06111c3b0a        163MB         45.9MB    U

```



\### 컨테이너 실행



```

docker run -d --name nginx-basic nginx:alpine

```



출력 결과:



```

8eb037c579df5a66b5fcf151eee58b44f4fd31a4b049020070461a65ddd8a26d
```



\### 실행 중 컨테이너 목록 확인



```

docker ps

```



출력 결과:



```

CONTAINER ID   IMAGE          COMMAND                  CREATED             STATUS             PORTS                                     NAMES

8eb037c579df   nginx:alpine   "/docker-entrypoint.…"   12 seconds ago      Up 12 seconds      80/tcp                                    nginx-basic

0047949b4bf0   docker-web     "/docker-entrypoint.…"   About an hour ago   Up About an hour   0.0.0.0:8080->80/tcp, \[::]:8080->80/tcp   docker-web-container
```



\### 전체 컨테이너 목록 확인



```

docker ps -a

```



출력 결과:



```

CONTAINER ID   IMAGE          COMMAND                  CREATED             STATUS             PORTS                                     NAMES

8eb037c579df   nginx:alpine   "/docker-entrypoint.…"   12 seconds ago      Up 12 seconds      80/tcp                                    nginx-basic

0047949b4bf0   docker-web     "/docker-entrypoint.…"   About an hour ago   Up About an hour   0.0.0.0:8080->80/tcp, \[::]:8080->80/tcp   docker-web-container

psw@5F-125:\~/docker-web$ docker ps -a

CONTAINER ID   IMAGE          COMMAND                  CREATED             STATUS                   PORTS                                     NAMES

8eb037c579df   nginx:alpine   "/docker-entrypoint.…"   20 seconds ago      Up 20 seconds            80/tcp                                    nginx-basic

b2732bac1d99   docker-web     "/docker-entrypoint.…"   57 minutes ago      Created                                                            keen\_torvalds

0047949b4bf0   docker-web     "/docker-entrypoint.…"   About an hour ago   Up About an hour         0.0.0.0:8080->80/tcp, \[::]:8080->80/tcp   docker-web-container

9b2e8bc5846f   ubuntu         "bash"                   3 hours ago         Exited (0) 3 hours ago                                             heuristic\_leavitt

b5a11697d9f3   hello-world    "/hello"                 3 hours ago         Exited (0) 3 hours ago                                             nifty\_solomon
```



\### 컨테이너 로그 확인



```

docker logs nginx-basic

```



출력 결과:



```

/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration

/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/

/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh

10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf

10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf

/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh

/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh

/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh

/docker-entrypoint.sh: Configuration complete; ready for start up

2026/11/02 04:15:20 \[notice] 1#1: using the "epoll" event method

2026/11/02 04:15:20 \[notice] 1#1: nginx/1.31.8

2026/11/02 04:15:20 \[notice] 1#1: built by gcc 15.2.0 (Alpine 15.2.0)

2026/11/02 04:15:20 \[notice] 1#1: OS: Linux 6.18.54.1-microsoft-standard-WSL2

2026/11/02 04:15:20 \[notice] 1#1: getrlimit(RLIMIT\_NOFILE): 1048576:1048576

2026/11/02 04:15:20 \[notice] 1#1: start worker processes

2026/11/02 04:15:20 \[notice] 1#1: start worker process 30

2026/11/02 04:15:20 \[notice] 1#1: start worker process 31

2026/11/02 04:15:20 \[notice] 1#1: start worker process 32

2026/11/02 04:15:20 \[notice] 1#1: start worker process 33

2026/11/02 04:15:20 \[notice] 1#1: start worker process 34

2026/11/02 04:15:20 \[notice] 1#1: start worker process 35

2026/11/02 04:15:20 \[notice] 1#1: start worker process 36

2026/11/02 04:15:20 \[notice] 1#1: start worker process 37

```



\### 리소스 사용량 확인



```

docker stats --no-stream

```



출력 결과:



```

CONTAINER ID   NAME                   CPU %     MEM USAGE / LIMIT     MEM %     NET I/O        BLOCK I/O     PIDS

8eb037c579df   nginx-basic            0.00%     7.781MiB / 7.605GiB   0.10%     872B / 126B    0B / 12.3kB   9

0047949b4bf0   docker-web-container   0.00%     7.617MiB / 7.605GiB   0.10%     9.96kB / 6kB   0B / 12.3kB   9

```



\### 컨테이너 중지 및 삭제



```

docker stop nginx-basic

docker rm nginx-basic

```



출력 결과:



```



docker rm nginx-basic

nginx-basic

nginx-basic

```



\---



\## 9. 컨테이너 실행 실습



\### hello-world 실행



```

docker run hello-world

```



출력 결과:



```

Hello from Docker!

This message shows that your installation appears to be working correctly.



To generate this message, Docker took the following steps:

&#x20;1. The Docker client contacted the Docker daemon.

&#x20;2. The Docker daemon pulled the "hello-world" image from the Docker Hub.

&#x20;   (amd64)

&#x20;3. The Docker daemon created a new container from that image which runs the

&#x20;   executable that produces the output you are currently reading.

&#x20;4. The Docker daemon streamed that output to the Docker client, which sent it

&#x20;   to your terminal.



To try something more ambitious, you can run an Ubuntu container with:

&#x20;$ docker run -it ubuntu bash



Share images, automate workflows, and more with a free Docker ID:

&#x20;https://hub.docker.com/



For more examples and ideas, visit:

&#x20;https://docs.docker.com/get-started/
```



`hello-world` 컨테이너가 정상 실행되어 Docker 엔진이 컨테이너를 실행할 수 있음을 확인했습니다.



\### ubuntu 컨테이너 실행 및 내부 진입



```

docker run -it --name ubuntu-practice ubuntu bash

```



컨테이너 내부에서 실행:



```

ls

echo "hello ubuntu container"

```



출력 결과:



```

<ubuntu 컨테이너 내부 ls 출력 결과>

hello ubuntu container

```



컨테이너 종료:



```

exit

```



\### attach와 exec 차이 관찰



컨테이너를 백그라운드로 실행:



```

docker run -d --name ubuntu-keep ubuntu sleep infinity

```



실행 중인 컨테이너 확인:



```

docker ps

```



출력 결과:



```

CONTAINER ID   IMAGE        COMMAND                  CREATED             STATUS             PORTS                                     NAMES

211e1ca6018d   ubuntu       "sleep infinity"         6 seconds ago       Up 6 seconds                                                 ubuntu-keep

0047949b4bf0   docker-web   "/docker-entrypoint.…"   About an hour ago   Up About an hour   0.0.0.0:8080->80/tcp, \[::]:8080->80/tcp   docker-web-container

psw@5F-125:\~/docker-web$

```



`exec`로 실행 중인 컨테이너에 새 셸 실행:



```

docker exec -it ubuntu-keep bash

```



컨테이너 내부에서 실행:



```

echo "exec test"

exit

```



출력 결과:



```

exec test

```



정리:



```

docker rm -f ubuntu-keep

```



정리 내용:



```

attach는 실행 중인 컨테이너의 기존 메인 프로세스에 연결하는 방식입니다.

exec는 실행 중인 컨테이너 안에서 새로운 명령 또는 셸을 추가로 실행하는 방식입니다.

```



\---



\## 10. Dockerfile 기반 커스텀 이미지



\### 선택한 기존 베이스 이미지



본 프로젝트에서는 기존 웹 서버 이미지인 `nginx:alpine`을 베이스 이미지로 사용했습니다.



선택 이유:



```

nginx는 정적 웹 페이지를 제공하기 적합한 웹 서버입니다.

alpine 태그는 비교적 가벼운 Linux 기반 이미지이므로 실습용 커스텀 이미지 제작에 적합합니다.

```



\### Dockerfile



```

FROM nginx:alpine



LABEL maintainer="psw9631"

LABEL description="Custom nginx web server for Docker workstation assignment"



ENV APP\\\\\\\\\\\\\\\_ENV=practice



COPY index.html /usr/share/nginx/html/index.html

```



커스텀 포인트:



| 항목 | 목적 |

|---|---|

| FROM nginx:alpine | 기존 nginx 웹 서버 이미지를 기반으로 사용 |

| LABEL | 이미지 설명 정보 추가 |

| ENV APP\_ENV=practice | 컨테이너 내부 환경변수 설정 |

| COPY index.html ... | 기본 nginx 페이지 대신 직접 작성한 웹 페이지 배포 |



\### 웹 서버 소스코드



`index.html` 파일을 작성했습니다.



```

<!DOCTYPE html>

<html>

<head>

\\\\\\\&#x20; <meta charset="UTF-8">

\\\\\\\&#x20; <title>Docker Web Project</title>

</head>

<body>

\\\\\\\&#x20; <h1>Hello Docker Web Project</h1>

\\\\\\\&#x20; <p>This page is served by nginx container.</p>

</body>

</html>

```



\### 이미지 빌드



```

docker build -t docker-web .

```



출력 결과:



```

\[+] Building 0.3s (7/7) FINISHED                                   docker:default

&#x20;=> \[internal] load build definition from Dockerfile                         0.0s

&#x20;=> => transferring dockerfile: 105B                                         0.0s

&#x20;=> \[internal] load metadata for docker.io/library/nginx:latest              0.0s

&#x20;=> \[internal] load .dockerignore                                            0.0s

&#x20;=> => transferring context: 2B                                              0.0s

&#x20;=> \[internal] load build context                                            0.0s

&#x20;=> => transferring context: 32B                                             0.0s

&#x20;=> \[1/2] FROM docker.io/library/nginx:latest@sha256:5ab5b0b01097420873a3f3  0.0s

&#x20;=> => resolve docker.io/library/nginx:latest@sha256:5ab5b0b01097420873a3f3  0.0s

&#x20;=> CACHED \[2/2] COPY index.html /usr/share/nginx/html/index.html            0.0s

&#x20;=> exporting to image                                                       0.1s

&#x20;=> => exporting layers                                                      0.0s

&#x20;=> => exporting manifest sha256:9d154951c3cea202079c598ec6a8798cbd699dd4d8  0.0s

&#x20;=> => exporting config sha256:5c234f45e87eb940ab403a246dd9a3003679fd1b2464  0.0s

&#x20;=> => exporting attestation manifest sha256:8d6f1e261aee00fb4d9bc316dea3cd  0.0s

&#x20;=> => exporting manifest list sha256:33152ebf8012864b81cba8d221a6767b58207  0.0s

&#x20;=> => naming to docker.io/library/docker-web:latest                         0.0s

&#x20;=> => unpacking to docker.io/library/docker-web:latest                      0.0s

```



이미지 생성 확인:



```

docker images docker-web

```



출력 결과:



```

                                                              i Info →   U  In Use

IMAGE               ID             DISK USAGE   CONTENT SIZE   EXTRA

docker-web:latest   33152ebf8012        241MB         63.9MB    U
```



\### 컨테이너 실행



```

docker run -d -p 8080:80 --name docker-web-container docker-web

```



출력 결과: 



```

69e89ec20fac027807a108e17f9b09ccb18e9c248ddb27323b44f8c0d09d44f8

```



실행 상태 확인:



```

docker ps

```



출력 결과:



```

CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                                     NAMES

b0bbb0479e3b   docker-web   "/docker-entrypoint.…"   20 seconds ago   Up 20 seconds   0.0.0.0:8080->80/tcp, \[::]:8080->80/tcp   docker-web-container

211e1ca6018d   ubuntu       "sleep infinity"         2 minutes ago    Up 2 minutes                                              ubuntu-keep

```



\---



\## 11. 포트 매핑 접속 증거



컨테이너 내부 nginx의 80번 포트를 호스트의 8080번 포트로 연결했습니다.



```

docker run -d -p 8080:80 --name docker-web-container docker-web

```



포트 매핑 형식:



```

\\\\\\\\-p <host\\\\\\\\\\\\\\\_port>:<container\\\\\\\\\\\\\\\_port>

```



현재 프로젝트에서는 다음과 같이 매핑했습니다.



```

\\\\\\\\-p 8080:80

```



의미:



```

호스트 PC의 8080 포트로 접속하면 컨테이너 내부의 80 포트로 요청이 전달됩니다.

```



\### curl 응답 확인



```

curl http://localhost:8080

```



출력 결과:



```

<!DOCTYPE html>

<html>

<head>

&#x20; <meta charset="UTF-8">

&#x20; <title>Docker Web</title>

</head>

<body>

&#x20; <h1>Hello Docker Web!</h1>

&#x20; <p>이 페이지는 docker-web 이미지에서 실행 중입니다.</p>

</body>

```



\### 브라우저 접속 증거



브라우저에서 아래 주소로 접속했습니다.



```

http://localhost:8080

```



접속 화면:



!\[8080 포트 접속 증거](./docs/images/port-8080.png)



\---



\## 12. 바인드 마운트 반영 확인



바인드 마운트는 호스트의 파일 또는 디렉터리를 컨테이너 내부 경로에 직접 연결하는 방식입니다.



기존 8080 포트를 사용하는 컨테이너가 있으면 충돌할 수 있으므로, 바인드 마운트 실습에서는 8082 포트를 사용했습니다.



\### 바인드 마운트 컨테이너 실행



```

docker run -d -p 8082:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html --name docker-web-bind docker-web
```



출력 결과:



```

9b12b30dc81e1de6651aae763354bf3c9f73438f390eb68084659634040c402b

```



실행 상태 확인:



```

docker ps

```



출력 결과:



```

CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                                     NAMES

9b12b30dc81e   docker-web   "/docker-entrypoint.…"   32 seconds ago   Up 31 seconds   0.0.0.0:8082->80/tcp, \[::]:8082->80/tcp   docker-web-bind

69e89ec20fac   docker-web   "/docker-entrypoint.…"   3 minutes ago    Up 3 minutes    0.0.0.0:8080->80/tcp, \[::]:8080->80/tcp   docker-web-container

211e1ca6018d   ubuntu       "sleep infinity"         7 minutes ago    Up 7 minutes                                              ubuntu-keep

```



\### 변경 전 확인



```

curl http://localhost:8082

```



출력 결과:



```

<!DOCTYPE html>

<html>

<head>

&#x20; <meta charset="UTF-8">

&#x20; <title>Docker Web</title>

</head>

<body>

&#x20; <h1>Hello Docker Web!</h1>

&#x20; <p>이 페이지는 docker-web 이미지에서 실행 중입니다.</p>

</body>

</html>

```



변경 전 브라우저 화면:



!\[바인드 마운트 변경 전](./docs/images/bind-before.png)



\### 호스트 파일 변경



호스트의 `index.html` 내용을 수정했습니다.



```

echo "<h1>Bind Mount Updated</h1>" > index.html

```



\### 변경 후 확인



```

curl http://localhost:8082

```



출력 결과:



```

<h1>Bind Mount Updated</h1>

```



변경 후 브라우저 화면:



!\[바인드 마운트 변경 후](./docs/images/bind-after.png)



바인드 마운트를 사용하면 이미지를 다시 빌드하지 않아도 호스트 파일 변경 내용이 컨테이너 내부에 바로 반영되는 것을 확인했습니다.



바인드 마운트 실습 컨테이너 정리:



```

docker rm -f docker-web-bind

```



출력 결과:



```

docker-web-bind

```



\---



\## 13. Docker 볼륨 영속성 검증



Docker 볼륨은 컨테이너가 삭제되어도 데이터를 유지하기 위한 Docker의 저장 공간입니다.



컨테이너 내부 파일 시스템에 저장한 데이터는 컨테이너 삭제 시 함께 사라질 수 있지만, Docker volume에 저장한 데이터는 컨테이너를 삭제한 뒤에도 유지됩니다.



\### Docker 볼륨 생성



```

docker volume create mydata

```



출력 결과:



```

mydata

```



볼륨 목록 확인:



```

docker volume ls

```



출력 결과:



```

DRIVER    VOLUME NAME

local     my-volume

local     mydata

```



\### 첫 번째 컨테이너에 볼륨 연결



```

docker run -d --name vol-test -v mydata:/data ubuntu sleep infinity

```



출력 결과:



```

4894a592ef6905bdc215839a685cefec3db0fa158522e8cc22d7be35e1dc6982
```



실행 상태 확인:



```

docker ps

```



출력 결과:



```

CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                                     NAMES

4894a592ef69   ubuntu       "sleep infinity"         13 seconds ago   Up 13 seconds                                             vol-test

69e89ec20fac   docker-web   "/docker-entrypoint.…"   4 minutes ago    Up 4 minutes    0.0.0.0:8080->80/tcp, \[::]:8080->80/tcp   docker-web-container

211e1ca6018d   ubuntu       "sleep infinity"         8 minutes ago    Up 8 minutes                                              ubuntu-keep

```



\### 볼륨에 데이터 저장



```

docker exec vol-test bash -lc "echo hi > /data/hello.txt \\\\\\\\\\\\\\\&\\\\\\\\\\\\\\\& cat /data/hello.txt"

```



출력 결과:



```

hi

```



\### 컨테이너 삭제 전 데이터 확인



```

docker exec vol-test bash -lc "cat /data/hello.txt"

```



출력 결과:



```

hi

```



\### 첫 번째 컨테이너 삭제



```

docker rm -f vol-test

```



출력 결과:



```

vol-test

```



\### 두 번째 컨테이너에 같은 볼륨 연결



```

docker run -d --name vol-test2 -v mydata:/data ubuntu sleep infinity

```



출력 결과:



```

147eb62767e015012c69baf3bb04108901e0b8e38c8a018c625c2b88248a9046

```



\### 컨테이너 삭제 후에도 데이터 유지 확인



```

docker exec vol-test2 bash -lc "cat /data/hello.txt"

```



출력 결과:



```

hi

```



검증 결과:



```

첫 번째 컨테이너 vol-test를 삭제한 뒤,

두 번째 컨테이너 vol-test2에 같은 Docker volume인 mydata를 연결했습니다.

그 결과 /data/hello.txt 파일의 내용 hi가 그대로 유지됨을 확인했습니다.

```



정리:



```

docker rm -f vol-test2

```



출력 결과:



```

vol-test2

```



\---



\## 14. Git 설정 및 GitHub 연동



\### Git 사용자 정보 설정



```

git config --global user.name "psw9631"

git config --global user.email "<이메일은 공개 README에 필요하면 마스킹>"

```



민감정보 보호를 위해 이메일 주소는 README에 그대로 노출하지 않거나 일부 마스킹했습니다.



예시:



```

psw\\\\\\\\\\\\\\\*\\\\\\\\\\\\\\\*\\\\\\\\\\\\\\\*\\\\\\\\\\\\\\\*@example.com

```



\### Git 기본 브랜치 설정



```

git config --global init.defaultBranch master

```



또는 기본 브랜치를 `main`으로 사용하는 경우:



```

git config --global init.defaultBranch main

```



현재 프로젝트에서는 다음 브랜치를 사용했습니다.



```

master

```



\### Git 설정 확인



```

git config --list

```



출력 결과 일부:



```

user.name=psw9631

user.email=<마스킹된 이메일>

init.defaultbranch=master

```



토큰, 비밀번호, 인증 코드 등 민감정보는 출력 결과에 포함하지 않았습니다.



\### Git 저장소 초기화



```

git init

```



출력 결과:



```

<git init 출력 결과>

```



\### 파일 추가 및 커밋



```

git add .

git commit -m "Initial docker web project"

```



출력 결과:



```

<git commit 출력 결과>

```



\### GitHub 원격 저장소 연결



```

git remote add origin https://github.com/psw9631/docker-web.git

```



원격 저장소 확인:



```

git remote -v

```



출력 결과:



```

origin  https://github.com/psw9631/docker-web.git (fetch)

origin  https://github.com/psw9631/docker-web.git (push)

```



\### GitHub에 push



```

git push origin master

```



출력 결과:



```

<git push 출력 결과>

```



\### Git 상태 확인



```

git status

```



출력 결과:



```

nothing to commit, working tree clean

```



\### VSCode GitHub 연동 증거



VSCode에서 GitHub 로그인 및 저장소 연동을 완료했습니다.



증거 화면:



!\[VSCode GitHub 연동 증거](./docs/images/vscode-github.png)



GitHub 저장소 화면:



!\[GitHub Repository 증거](./docs/images/github-repository.png)



주의사항:



```

스크린샷에는 비밀번호, 토큰, 인증 코드, 개인키가 보이지 않도록 했습니다.

민감정보가 포함된 경우 즉시 이미지와 Git 히스토리에서 제거하고 토큰을 재발급해야 합니다.

```



\---



\## 15. 트러블슈팅



\### 문제 1. Docker 명령어 실행 시 Docker 데몬 연결 오류



문제:



```

docker 명령어 실행 시 Docker daemon에 연결할 수 없다는 오류가 발생할 수 있습니다.

```



원인 가설:



```

Docker Desktop이 실행되지 않았거나,

WSL Integration 설정이 꺼져 있을 가능성이 있습니다.

```



확인:



```

docker --version

docker info

```



확인 결과:



```

docker --version은 출력되지만 docker info가 정상 출력되지 않으면

Docker CLI는 설치되어 있으나 Docker daemon이 동작하지 않는 상태일 수 있습니다.

```



해결:



```

1\\\\\\\\. Windows에서 Docker Desktop을 실행했습니다.

2\\\\\\\\. Docker Desktop Settings에서 WSL Integration을 활성화했습니다.

3\\\\\\\\. WSL Ubuntu 터미널을 다시 열고 docker info를 실행했습니다.

```



해결 후 결과:



```

docker info 명령이 정상 출력되어 Docker daemon 연결이 정상임을 확인했습니다.

```



\---



\### 문제 2. 8080 포트 충돌



문제:



```

docker run -p 8080:80 실행 시 포트가 이미 사용 중이라는 오류가 발생할 수 있습니다.

```



원인 가설:



```

기존 컨테이너가 이미 호스트의 8080 포트를 사용 중일 가능성이 있습니다.

```



확인:



```

docker ps

```



확인 결과:



```

PORTS 항목에서 0.0.0.0:8080->80/tcp를 사용하는 컨테이너를 확인했습니다.

```



해결 방법 1: 기존 컨테이너 삭제



```

docker rm -f docker-web-container

```



해결 방법 2: 다른 호스트 포트 사용



```

docker run -d -p 8082:80 --name docker-web-bind docker-web

```



해결 후 결과:



```

8082 포트로 실행한 뒤 http://localhost:8082 접속이 정상 동작했습니다.

```



\---



\### 문제 3. GitHub push 인증 실패



문제:



```

git push 실행 시 인증 실패가 발생할 수 있습니다.

```



원인 가설:



```

GitHub는 비밀번호 인증 대신 Personal Access Token 또는 GitHub CLI/VSCode 로그인을 사용해야 할 수 있습니다.

```



확인:



```

git remote -v

git status

```



해결:



```

1\\\\\\\\. GitHub에서 Personal Access Token을 발급했습니다.

2\\\\\\\\. push 인증 시 비밀번호 대신 토큰을 사용했습니다.

3\\\\\\\\. 토큰은 README와 스크린샷에 남기지 않았습니다.

```



해결 후 결과:



```

git push origin master 명령으로 GitHub 저장소 업로드에 성공했습니다.

```



\---



\## 16. 과제 목표 개념 정리



\### 절대 경로와 상대 경로



절대 경로는 루트 디렉터리부터 시작하는 전체 경로입니다.



예시:



```

/home/user/docker-web/index.html

```



상대 경로는 현재 위치를 기준으로 표현하는 경로입니다.



예시:



```

./index.html

../docker-web/index.html

```



정리:



```

절대 경로는 어디서 실행해도 같은 위치를 가리킵니다.

상대 경로는 현재 작업 디렉터리에 따라 가리키는 위치가 달라질 수 있습니다.

```



\---



\### 파일 권한 r/w/x와 755, 644



Linux 권한의 의미는 다음과 같습니다.



```

r: 읽기

w: 쓰기

x: 실행 또는 디렉터리 진입

```



숫자 권한은 다음 값을 더해서 계산합니다.



```

r = 4

w = 2

x = 1

```



755:



```

소유자: rwx = 4+2+1 = 7

그룹: r-x = 4+1 = 5

기타: r-x = 4+1 = 5

```



644:



```

소유자: rw- = 4+2 = 6

그룹: r-- = 4

기타: r-- = 4

```



\---



\### 커스텀 Docker 이미지



커스텀 이미지는 기존 베이스 이미지에 필요한 파일, 설정, 환경변수 등을 추가하여 만든 새 이미지입니다.



이 프로젝트에서는 다음 베이스 이미지를 사용했습니다.



```

nginx:alpine

```



그리고 직접 만든 `index.html`을 nginx 웹 루트에 복사하여 커스텀 웹 서버 이미지를 만들었습니다.



\---



\### 포트 매핑이 필요한 이유



컨테이너 내부의 서비스는 기본적으로 컨테이너 내부 네트워크에서 실행됩니다.



외부 호스트 PC의 브라우저에서 컨테이너 내부 서비스에 접속하려면 포트 매핑이 필요합니다.



예시:



```

\\\\\\\\-p 8080:80

```



의미:



```

호스트의 8080 포트로 들어온 요청을 컨테이너의 80 포트로 전달합니다.

```



\---



\### Docker 볼륨



Docker 볼륨은 컨테이너 삭제 이후에도 데이터를 유지하기 위한 저장 공간입니다.



컨테이너 내부 파일 시스템에만 데이터를 저장하면 컨테이너 삭제 시 데이터가 사라질 수 있습니다.



하지만 Docker volume을 사용하면 컨테이너를 삭제하고 새 컨테이너를 만들어도 같은 볼륨을 연결하여 데이터를 다시 사용할 수 있습니다.



\---



\### Git과 GitHub의 차이



Git은 로컬 컴퓨터에서 코드 변경 이력을 관리하는 버전 관리 도구입니다.



GitHub는 Git 저장소를 원격에서 관리하고 공유할 수 있는 플랫폼입니다.



정리:



```

Git: 로컬 버전 관리 도구

GitHub: 원격 저장소 및 협업 플랫폼

```



\---



\## 17. 보안 및 개인정보 보호



본 프로젝트에서는 다음 보안 원칙을 적용했습니다.



```

1\\\\\\\\. GitHub 토큰을 README에 기록하지 않았습니다.

2\\\\\\\\. 비밀번호, 인증 코드, 개인키를 캡처하지 않았습니다.

3\\\\\\\\. git config 출력에서 이메일은 필요한 경우 마스킹했습니다.

4\\\\\\\\. 스크린샷에 민감정보가 포함되지 않도록 확인했습니다.

5\\\\\\\\. 민감정보가 노출된 경우 즉시 문서와 Git 히스토리에서 제거하고 토큰을 재발급해야 합니다.

```



\---



\## 18. 재현 방법



평가자는 아래 절차로 프로젝트를 재현할 수 있습니다.



\### 저장소 클론



```

git clone https://github.com/psw9631/docker-web.git

cd docker-web

```



\### Docker 이미지 빌드



```

docker build -t docker-web .

```



\### 컨테이너 실행



```

docker run -d -p 8080:80 --name docker-web-container docker-web

```



\### 접속 확인



브라우저에서 접속:



```

http://localhost:8080

```



또는 curl로 확인:



```

curl http://localhost:8080

```



\### 컨테이너 로그 확인



```

docker logs docker-web-container

```



\### 컨테이너 정리



```

docker rm -f docker-web-container

```



\---



\## 19. 최종 제출 정보



제출 저장소:



```

https://github.com/psw9631/docker-web

```



최종 확인 명령:



```

git status

```



출력 결과:



```

nothing to commit, working tree clean

```



최종 push:



```

git add .

git commit -m "Update README with assignment evidence"

git push origin master

```



\---



\## 20. 결과 요약



이 프로젝트를 통해 WSL Ubuntu 환경에서 Docker 기반 개발 워크스테이션을 구축했습니다.



Dockerfile을 직접 작성하여 nginx 기반 커스텀 이미지를 만들었고, 포트 매핑을 통해 웹 서버 접속을 확인했습니다.



또한 바인드 마운트를 통해 호스트 파일 변경이 컨테이너에 반영되는 것을 확인했고, Docker 볼륨을 사용하여 컨테이너 삭제 후에도 데이터가 유지되는 것을 검증했습니다.



마지막으로 Git 설정, GitHub 원격 저장소 연결, VSCode GitHub 연동을 완료하여 전체 수행 결과를 GitHub Repository에서 확인할 수 있도록 정리했습니다.

