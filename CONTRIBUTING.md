# 협업 가이드

1. `main` 에 직접 푸시하지 않고 브랜치(`feature/<앱>-<내용>`)를 만들어 Pull Request로 병합합니다.
2. 한 PR에서는 가급적 한 앱(`apps/*`)만 수정합니다. 앱끼리 코드를 직접 import하지 않습니다.
3. PR을 열면 GitHub Actions가 자동으로 빌드·검사합니다. 실패하면 병합하지 마세요.
4. API 키, `.env` 파일은 절대 커밋하지 않습니다 (`.gitignore` 처리됨).
5. 권장 설정: Settings > Branches 에서 `main` 보호 규칙(PR 필수, 상태 검사 통과 필수)을 켭니다.
6. 담당 영역 지정은 `.github/CODEOWNERS` 에 GitHub 계정을 입력합니다 (해당 계정에 저장소 쓰기 권한이 있어야 합니다).
