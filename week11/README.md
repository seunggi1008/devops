# 11주차 - 쿠버네티스 설정과 상태 점검

## Secret 읽어 보기

Secret 값을 `base64 -d`로 돌려 봤더니 처음 넣었던 값이 그대로 나왔다. Base64는 암호화가 아니라 형식을 바꾼 거라, 값을 볼 수 있으면 원래 내용도 읽을 수 있다는 걸 알았다.

## ConfigMap 바꿔 보기

ConfigMap에서 제목이랑 색을 바꾸고 Pod를 다시 띄웠다. 브라우저에서 F5를 눌러 보니 제목이 `new 방명록 (k8s)`로 바뀌고 색도 빨간색으로 바뀌었다. Redis에 남겨 둔 글은 그대로 있었다.

## readiness 실패

Redis를 내렸더니 방명록 Pod 두 개가 `Running`인데도 `READY`가 `0/1`이 됐다. 재시작 횟수는 `0`이었다. Redis를 다시 올리니까 두 개 다 `1/1`로 돌아왔다.

## liveness 실패

검사 주소를 일부러 `/devops`로 바꿨더니 `RESTARTS`가 올라갔다. `kubectl describe pod`를 쳐 보니까 404가 나고 컨테이너를 다시 시작한다는 이벤트가 찍혔다. 원래 YAML을 적용한 뒤 새 Pod 두 개가 `1/1 Running`으로 뜨는 걸 확인했다.

## 문제 생기면 확인할 순서

먼저 `kubectl get pods`를 쳐서 READY랑 재시작 횟수를 본다. 그다음 `kubectl describe pod`에서 이벤트를 보고, 앱에서 실제로 어떤 오류가 났는지는 `kubectl logs`로 확인한다.
