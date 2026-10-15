# 학교 산업안전보건 통합 플랫폼 (Monorepo)

흩어져 있던 세 프로젝트를 한 저장소의 폴더로 모아 함께 관리합니다.

| 폴더 | 원본 저장소 | 설명 | 실행 방식 |
|---|---|---|---|
| `apps/msds` | [tamla95/msds1007](https://github.com/tamla95/msds1007) | MSDS·유해물질 관리 시스템 | Node.js 서버 (`node server.js`, 포트 3000) |
| `apps/chatbot` | [jungin3275-boop/5cahtbot](https://github.com/jungin3275-boop/5cahtbot) | 산업안전보건 AI 챗봇 | Next.js (OpenAI API 키 필요) |
| `apps/facility-safety` | [jshlivyy202605-crypto/Facility-Safety-Inspection-History-Management](https://github.com/jshlivyy202605-crypto/Facility-Safety-Inspection-History-Management) | 시설안전 점검 이력관리 | 정적 HTML (서버 불필요) |
| `portal` | 신규 | 세 서비스로 연결되는 메인 랜딩 페이지 | 정적 HTML |

## 구조

```
.
├── apps/
│   ├── msds/
│   ├── chatbot/
│   └── facility-safety/
├── portal/                    # 통합 포털 메인(Index)
├── .github/workflows/deploy.yml
├── CONTRIBUTING.md
└── README.md
```

## 로컬 실행

```bash
# MSDS
cd apps/msds && node server.js          # http://localhost:3000

# 챗봇
cd apps/chatbot && npm ci
echo "OPENAI_API_KEY=발급받은_키" > .env.local
npm run dev                              # http://localhost:3000 (MSDS와 동시에 쓰려면 -p 3001)

# 시설안전: apps/facility-safety/index.html 을 브라우저로 열기
# 포털: portal/index.html 을 브라우저로 열기
```

## 배포 (GitHub Actions)

`.github/workflows/deploy.yml` 이 자동으로 처리합니다.

- Pull Request: 변경된 앱만 검사합니다 (챗봇 `typecheck` + `build`, MSDS 문법 검사).
- `main` 병합: 검사 통과 후 **포털 + 시설안전**을 GitHub Pages에 배포합니다.
  - 포털: `https://<계정>.github.io/<저장소>/`
  - 시설안전: `https://<계정>.github.io/<저장소>/facility-safety/`

### 최초 설정 (한 번만)

1. 저장소 **Settings > Pages > Source** 를 **GitHub Actions** 로 변경합니다.
2. 서버가 필요한 `msds`, `chatbot`은 GitHub Pages에서 실행할 수 없습니다. Vercel, Render 등에 따로 배포한 뒤
   **Settings > Secrets and variables > Actions > Variables** 에 아래 값을 등록하면 포털 카드에 링크가 연결됩니다.
   - `MSDS_URL`
   - `CHATBOT_URL`
3. 챗봇의 `OPENAI_API_KEY`는 코드에 넣지 말고 배포 서비스의 환경 변수로만 설정합니다.

## 협업 규칙

[CONTRIBUTING.md](CONTRIBUTING.md) 를 참고하세요.
