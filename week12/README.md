# 12주차 - GitHub Actions

## 이미지가 안 올라갔던 이유

Actions 결과를 보니까 린트랑 앱 테스트는 통과했는데, 마지막 빌드 & 푸시에서 실패했다. 로그를 열어 보니 `permission_denied: write_package`가 찍혀 있었다.

워크플로 로그에는 `Packages: write`가 있었는데, `guestbook` 패키지 설정에 들어가 보니까 `devops` 저장소의 Actions 권한은 `Read`였다. 이걸 `Write`로 바꾸고 실패한 작업을 다시 돌렸다. 이번에는 빌드 & 푸시까지 초록 체크가 떴다.

토큰에 쓰기 권한이 있어도 패키지에서 저장소에 어떤 권한을 줬는지 같이 봐야 한다는 걸 알았다.

[성공한 Actions 실행](https://github.com/seunggi1008/devops/actions/runs/46146017086/job/141012285876)

## PR에서 문법 오류 확인

실습 브랜치에서 파이썬 문법을 일부러 틀리게 써 봤다. PR #11에서 `gh pr checks`를 쳐 보니 필수 `build` 체크에 빨간 X가 떴다. 오류를 넣은 커밋은 `git revert`로 되돌렸다.
