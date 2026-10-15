## 7주차 Docker Compose 실습

## 1. Docker Compose 실행 결과

docker compose ps 명령어로 컨테이너 상태를 확인했다.

		
## 2. Scale 실습결과


## 3. down 후 up과 down -v 후 up 차이 비교

docker compose down 후 다시 실행하면 컨테이너와 네트워크는 삭제되지만 볼륨은 유지되어 방명록 데이터가 남아 있다.

docker compose down -v 후 다시 실행하면 볼륨까지 삭제되어 기존 방명록 데이터가 사라진다.

따라서 down과 down -v의 가장 큰 차이는 데이터 볼륨 삭제 여부이다.

## 4. .env를 Git에 올리지 않는 이유

.env 파일에는 Redis 비밀번호와 같은 민감한 정보가 저장되어 있다.

이 파일을 GitHub에 올리면 비밀번호가 외부에 노출될 수 있고, 파일을 삭제해도 Git 기록에 남을 수 있다.

따라서 .gitignore에 .env를 추가하여 Git에 올라가지 않도록 설정한다
