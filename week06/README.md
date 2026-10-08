# DevOps 6주차

# V1 이미지: ghcr.io/seunggi1008/guestbook:v1

# V2 이미지: ghcr.io/seunggi1008/guestbook:v2

# FROM: 어떤 이미지를 바탕으로 만들지 결정

# Dockerfile에서 ENV로 색상을 설정했지만, 컨테이너를 실행할 때 -e로 다른 색상을 지정하니까 -e에 설정한 색상이 적용됨.

# 빌드 캐시 확인
# 패키지 설치 단계에서 이전 빌드 결과를 재사용할 수 있어서 패키지를 다시 설치하지 않았다.

# 빌드 캐시 확인
# V2 이미지를 빌드했을 때 아래와 같이 CACHED가 표시되었다.

# CACHED [2/6] WORKDIR /app
# CACHED [3/6] COPY requirements.txt .
# CACHED [4/6] RUN pip install --no-cache-dir -r requirements.txt


# 환경 변수 설정 방법 차이

# 코드(app.py): 환경 변수가 없을 때 사용하는 기본값이다.

# Dockerfile ENV: 이미지를 만들 때 환경 변수의 기본값을 설정한다.

# docker run -e: 컨테이너를 실행할 때 환경 변수 값을 지정한다.
