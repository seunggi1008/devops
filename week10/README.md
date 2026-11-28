# 10주차 - 쿠버네티스 배포와 서비스

## Pod 5개로 늘리기

처음 배포했을 때는 Pod가 2개였다. `kubectl scale deployment/guestbook --replicas=5`를 치고 `kubectl get pods -l app=guestbook`으로 확인해 보니까 5개가 전부 `1/1 Running`이었다.

## Service로 접속하기

같은 Service 주소에 `curl`로 15번 요청해 봤다. 응답에 나온 Pod 이름을 세어 보니까 5개가 전부 나왔다.

| 응답한 Pod 이름 끝자리 | 응답 횟수 |
|---|---:|
| `2cxbm` | 2 |
| `dk7m7` | 4 |
| `nz5ds` | 6 |
| `r5qx9` | 1 |
| `ssjff` | 2 |

## Pod 하나 지워 보기

끝자리가 `2cxbm`인 Pod를 강제로 지웠다. 다시 목록을 보니 `fb2t4`로 끝나는 새 Pod가 생겼고, 다시 5개가 전부 `Running`이었다.

## v2로 바꿨다가 v1로 돌아가기

v2 이미지를 Minikube에 넣고 `kubectl set image`로 이미지를 바꿨다. 롤아웃이 끝난 뒤 `kubectl rollout history deployment/guestbook`을 쳐 보니 아래처럼 나왔다.

```text
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
```

그다음 `kubectl rollout undo deployment/guestbook --to-revision=1`로 되돌렸다. 롤아웃이 끝나고 Deployment의 이미지를 다시 조회해 보니 `ghcr.io/seunggi1008/guestbook:v1`로 돌아와 있었다.

[Pod 5개 실행 화면](images/pods-5.png)
