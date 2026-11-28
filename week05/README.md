# 5주차 - Docker

## Docker 처음 실행

처음에 우분투에서 `docker --version`을 쳤는데 명령어를 못 찾는다고 나왔다. Docker Desktop에서 WSL 연동을 켜니까 버전은 나왔다.

근데 `docker info`를 치니까 이번에는 권한 오류가 떴다. `newgrp docker`를 하고 다시 확인하니 아까 안 나오던 Server 정보가 나왔다. 그다음 `docker run --rm hello-world`를 실행했고 `Hello from Docker!`가 뜨는 걸 확인했다.

## nginx 실행

`web`이라는 이름으로 nginx를 실행하고 내 컴퓨터의 8080 포트로 접속했다. `curl -I http://localhost:8080`을 쳤을 때 `200 OK`가 나왔다.

## 혼자서 해보기

nginx를 세 개 띄우고 포트를 8091, 8092, 8093으로 나눴다. 처음엔 같은 nginx 화면이 나와서 `docker exec`로 각 컨테이너의 `index.html`을 바꿨다. 그러고 나서 `curl`로 하나씩 접속해 보니 아래처럼 이름이 다르게 나왔다.

| 확인한 주소 | 나온 내용 | 캡처 |
|---|---|---|
| `http://localhost:8091` | `Welcome to nginx1` | [8091 화면](images/nginx1.png) |
| `http://localhost:8092` | `Welcome to nginx2` | [8092 화면](images/nginx2.png) |
| `http://localhost:8093` | `Welcome to nginx3` | [8093 화면](images/nginx3.png) |

마지막으로 `docker ps`를 쳐서 `web`이랑 `nginx1`, `nginx2`, `nginx3`이 전부 실행 중인 걸 확인했다. [docker ps 화면](images/docker_ps.png)
