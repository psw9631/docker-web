# Docker Web Project

WSL Ubuntu 환경에서 Docker를 사용하여 nginx 기반 웹 서버를 실행하고, GitHub에 업로드한 프로젝트입니다.

---

## 1) 개발 환경

- OS: Windows + WSL Ubuntu
- Docker Desktop
- Git
- GitHub
- Web Server: nginx

---

## 2) 프로젝트 목표

이 프로젝트의 목표는 Docker 기본 사용법을 실습하는 것입니다.

- Dockerfile 작성
- Docker 이미지 빌드
- Docker 컨테이너 실행
- 포트 매핑 확인
- 바인드 마운트 확인
- Docker 볼륨 영속성 확인
- GitHub 업로드

---

## 3) 프로젝트 구조

```text
docker-web/
├── Dockerfile
├── index.html
└── README.md
```

---

## 4) Dockerfile 작성

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

nginx Alpine 이미지를 기반으로 사용했습니다.  
로컬의 `index.html` 파일을 nginx 기본 웹 루트 경로인 `/usr/share/nginx/html/index.html`에 복사하도록 구성했습니다.

---

## 5) Docker 이미지 빌드

```bash
docker build -t docker-web .
```

현재 폴더의 Dockerfile을 사용하여 `docker-web` 이미지를 빌드했습니다.

---

## 6) Docker 컨테이너 실행

```bash
docker run -d -p 8080:80 --name docker-web-container docker-web
```

컨테이너 내부의 nginx 80번 포트를 로컬 PC의 8080번 포트와 연결했습니다.

접속 주소:

```text
http://localhost:8080
```

브라우저에서 위 주소로 접속하여 웹 페이지가 정상적으로 표시되는 것을 확인했습니다.

---

## 7) 포트 매핑 확인

두 번째 포트 매핑 확인을 위해 8081 포트로도 컨테이너를 실행했습니다.

```bash
docker run -d -p 8081:80 --name docker-web-8081 docker-web
```

접속 주소:

```text
http://localhost:8081
```

8081 포트에서도 웹 페이지가 정상적으로 표시되는 것을 확인했습니다.

확인 후 컨테이너를 정리했습니다.

```bash
docker rm -f docker-web-8081
```

---

## 8) 바인드 마운트 확인

로컬의 `index.html` 파일을 컨테이너 내부 nginx 경로와 연결하여, 로컬 파일 수정 내용이 웹 페이지에 반영되는 것을 확인했습니다.

```bash
docker run -d -p 8080:80 \
  -v $(pwd)/index.html:/usr/share/nginx/html/index.html \
  --name docker-web-bind \
  docker-web
```

바인드 마운트를 사용하면 이미지를 다시 빌드하지 않아도 로컬 파일 변경 내용을 컨테이너에서 바로 확인할 수 있습니다.

---

## 9) Docker 볼륨 영속성 확인

Docker volume을 생성하고 컨테이너에 연결하여 데이터를 저장했습니다.  
컨테이너를 삭제한 뒤 새 컨테이너를 실행해도 volume 안의 데이터가 유지되는 것을 확인했습니다.

```bash
docker volume create mydata
```

```bash
docker run -d --name vol-test -v mydata:/data ubuntu sleep infinity
```

```bash
docker exec vol-test bash -lc "echo hi > /data/hello.txt && cat /data/hello.txt"
```

출력 결과:

```text
hi
```

컨테이너 삭제:

```bash
docker rm -f vol-test
```

새 컨테이너에서 같은 볼륨을 연결하여 데이터 확인:

```bash
docker run -d --name vol-test2 -v mydata:/data ubuntu sleep infinity
```

```bash
docker exec vol-test2 bash -lc "cat /data/hello.txt"
```

출력 결과:

```text
hi
```

---

## 10) GitHub 업로드

Git 저장소를 초기화하고 변경 사항을 commit한 뒤 GitHub 원격 저장소에 push했습니다.

```bash
git add .
git commit -m "Update docker web project"
git push origin master
```

GitHub 저장소 주소:

```text
https://github.com/psw9631/docker-web
```

---

## 11) 최종 확인

아래 명령어로 Git 상태를 확인했습니다.

```bash
git status
```

정상 상태 예시:

```text
nothing to commit, working tree clean
```

README 작성 후 GitHub에 다시 업로드했습니다.

```bash
git add README.md
git commit -m "Update README"
git push origin master
```
