# 🧱 Modular Monolith Fullstack Template

> Spring Boot + Next.js 기반 도메인 중심 풀스택 템플릿
> 
> 
> 도메인 주도 설계(DDD)에 기반한 모듈형 모노리식 구조로, 팀 협업과 유지보수, 확장성을 모두 고려하였습니다. 또한, **Spring Security**를 통한 JWT + Redis 기반의 인증 시스템을 통합하여 보안을 강화했습니다.
> 

---

## 🚀 프로젝트 개요

이 템플릿은 실전 개발에 바로 적용 가능한 풀스택 구조로 구성되어 있습니다:

- 🌱 **Backend**: Spring Boot 3, Kotlin DSL, JPA, Spring Security, Redis
- ⚛️ **Frontend**: Next.js 14 App Router, TypeScript, Zustand
- 🐳 **Infrastructure**: Docker, GitHub Actions, Nginx
- 🧩 **Architecture**: 도메인 기반 Modular Monolith

도메인 구조를 백엔드와 프론트엔드에서 동일하게 유지하여 향후 MSA 전환도 쉽게 할 수 있습니다. **Spring Security**와 **JWT** 기반 인증 시스템을 구현하며, **Redis**를 활용한 리프레시 토큰 관리 시스템을 포함하고 있습니다.

---

## 📁 프로젝트 구조

```bash
mono-modulith-project/
├── backend/
│   ├── domain/              # 도메인별 모듈 (auth, policy, community 등)
│   ├── global/              # 글로벌 설정 (보안, 예외, config)
│   ├── shared/              # 공통 유틸리티, VO, enum
│   ├── security/            # Spring Security 관련 설정
│   └── build.gradle.kts
│
├── frontend/                # 🌐 Next.js 프론트엔드
│   ├── app/                 # App Router 기반 페이지
│   ├── features/            # 각 도메인의 상태 관리 로직
│   ├── components/          # 공용 UI 컴포넌트
│   ├── libs/                # API 클라이언트, hooks, 유틸 등
│   ├── store/               # Zustand 기반 전역 상태
│   └── public/              # 정적 파일
│
├── infra/                   # ⚙️ 인프라 설정
│   ├── docker-compose.dev.yml
│   ├── docker-compose.prod.yml
│   └── nginx.conf
│
├── scripts/                 # 🛠 배포 및 마이그레이션 스크립트
├── .github/workflows/       # ✅ GitHub Actions CI/CD 설정
├── docs/                    # 📚 문서 및 명세 파일
└── README.md                # 📖 본 문서

```

## 🧩 도메인 네이밍 규칙

| 도메인 | 백엔드 (/domain) | 프론트엔드 (/app) |
| --- | --- | --- |
| 인증 | `auth/` | `/auth/` |
| 커뮤니티 | `community/` | `/community/` |
| 정책 | `policy/` | `/policy/` |
| 추천 | `recommendation/` | `/recommendation/` |
| 설문 | `survey/` | `/survey/` |
| 관리자 | `admin/` | `/admin/` |

> 📌 도메인 이름을 통일하면 테스트, 라우팅, 디버깅, MSA 전환이 쉬워집니다.
> 

---

## 🔧 기술 스택 요약

| 계층 | 사용 기술 |
| --- | --- |
| **프론트엔드** | Next.js 14, TypeScript, React, Zustand, TailwindCSS |
| **백엔드** | Spring Boot 3, Kotlin DSL, JPA, Hibernate, Spring Security, Redis |
| **인프라** | Docker, GitHub Actions, Nginx, MySQL, Redis |
| **도구** | Swagger/OpenAPI, ESLint, Prettier, Husky, CommitLint |

---

## ⚙️ 로컬 개발 실행 방법

### 📦 사전 조건

- Java 17 이상
- Node.js 18 이상
- Docker 20 이상

### 🔧 실행 절차

1. 프로젝트 클론

```bash
git clone https://github.com/your-org/mono-modulith-project.git
cd mono-modulith-project
```

1. `.env` 환경 설정

```bash
cp infra/docker/.env.dev .env
# DB, Redis, API 키 등을 필요에 맞게 수정
```

1. Docker Compose로 전체 실행

```bash
docker-compose -f infra/docker/docker-compose.dev.yml up --build
```

- 🔗 **Backend API**: [http://localhost:8080](http://localhost:8080/)
- 🔗 **Frontend**: [http://localhost:3000](http://localhost:3000/)

---

## 🧪 CI/CD 파이프라인

| 워크플로우 | 트리거 조건 | 설명 |
| --- | --- | --- |
| `ci.yml` | `dev` 브랜치 PR/푸시 | Lint + Build + Test 수행 |
| `preview.yml` | PR 생성 or sync 시점 | Vercel 미리보기 배포 |
| `cd.yml` | `main` 브랜치 푸시 | 운영 환경 자동 배포 |

---

## 🧠 설계 철학

- 🧱 **모듈 간 의존 최소화**: 도메인 기반 분리 구조
- ♻️ **공통 모듈 분리**: `libs/`, `components/`, `shared/` 중심
- 🌍 **전역 설정 통합**: 예외 처리, 보안, 로깅 등은 `global/`에 집중
- 🧪 **테스트 가능 구조**: 도메인별 유닛 테스트 용이하게 설계

---

## 📚 문서 디렉토리 (`/docs`)

| 파일명 | 내용 설명 |
| --- | --- |
| `architecture.md` | 시스템 아키텍처 및 계층 구조 설명 |
| `api-spec.yaml` | Swagger/OpenAPI 기반 API 명세 |
| `db-schema.sql` | MySQL 기반 DB 테이블 정의 |
| `contribution-guide.md` | Git 브랜치 전략, 커밋 메시지 컨벤션 등 가이드 |

---

## 🤝 협업 가이드

### 🔖 브랜치 네이밍 컨벤션

| 타입 | 예시 |
| --- | --- |
| 기능 | `feat/auth/login` |
| 버그 수정 | `fix/community/comment-null` |
| 리팩토링 | `refactor/policy/score-service` |

### 📝 커밋 메시지 규칙

- `feat: 로그인 기능 추가 (auth)`
- `fix: 댓글 null 오류 수정 (community)`
- `refactor: 정책 점수 계산 리팩토링 (policy)`

> ⛳ Conventional Commits 방식 사용 권장
> 

---

## 📦 확장 계획 (Scalability Roadmap)

- ✅ **MSA 전환 고려 구조**: 도메인 모듈을 쉽게 마이크로서비스화 가능
- 🔌 **IaC 도입 가능**: Terraform, AWS CDK로 확장 가능
- 🌐 **SEO 최적화 준비**: Next.js의 SSR + 캐싱 활용
- 🧱 **모노레포 확장**: Nx, Turborepo, Gradle 서브모듈 대응 가능

---

## 🧩 한 줄 요약

> 도메인 일치 기반의 모듈형 모노리식 구조로, 팀 협업과 유지보수, MSA 확장까지 고려한 실전형 풀스택 아키텍처 템플릿입니다.
> 

---

## 🖇️ 라이선스

MIT © [your-org]

---

# ✅ 🔄 매일 작업 시작 전: 최신 dev 코드 통합 절차

> 목표: feat/개인브랜치에 있는 내 작업을 유지하면서, origin/dev의 최신 내용을 끌어와 통합한다.
> 

---

## 📦 1단계. 현재 브랜치 확인

```
git branch
```

- 결과 예시:
    
    ```
    * feat/channy
      dev
    ```
    

> 현재 feat/channy에 있다면 계속 진행해도 OK
> 
> 
> 만약 `dev`에 있다면 다음 단계로 이동하세요.
> 

---

## 📤 2단계. dev 브랜치로 이동하고 최신 코드 가져오기

```
# dev 브랜치로 이동
git checkout dev

# 최신 dev 내용 받아오기
git pull origin dev
```

> ✅ 이제 로컬 dev는 최신 상태가 됨
> 

---

## 🛠️ 3단계. 다시 내 작업 브랜치로 이동

```
git checkout feat/channy
```

---

## 🔄 4단계. 내 브랜치에 최신 dev 내용 합치기 (rebase)

```
git pull origin dev --rebase
```

> 이 명령은 다음을 의미합니다:
> 

```
“origin/dev”의 최신 내용을 내 브랜치(feat/channy)의 **기준점 아래에 넣고**,
내 작업 커밋들을 그 위에 다시 차곡차곡 쌓는다.
```

---

## ⚠️ 5단계. 충돌이 발생한 경우

만약 중복된 파일이 수정되었거나, 충돌이 발생하면 Git이 알려줍니다:

```
CONFLICT (content): Merge conflict in src/components/Header.tsx
```

### ✅ 해결 방법

1. VSCode나 Git에서 충돌난 파일을 열기
2. 아래처럼 표시된 충돌을 직접 수정:

```
<<<<<<< HEAD
// dev에서 수정된 부분
=======
 // 내 브랜치에서 수정한 부분
>>>>>>> feat/channy
```

→ 내가 원하는 코드로 수정한 후 저장

1. 수정한 파일을 Git에 반영

```
git add src/components/Header.tsx
```

1. 충돌 해결 후 계속 진행

```
git rebase --continue
```

> ❗ 충돌이 여러 개 있을 경우 위 과정을 반복
> 

---

## ✅ 6단계. 모든 충돌 없이 완료되면 푸시

```
git push origin feat/channy --force
```

> --force는 rebase로 인해 커밋 해시가 변경되었기 때문에 필요
> 
> 
> 단, **팀과 합의된 상황에서만 사용**하세요
> 

---

## 💡 예시 요약

| 단계 | 명령어 | 설명 |
| --- | --- | --- |
| 1 | `git checkout dev` | dev로 이동 |
| 2 | `git pull origin dev` | 최신 dev 내용 받아오기 |
| 3 | `git checkout feat/channy` | 다시 내 브랜치로 이동 |
| 4 | `git pull origin dev --rebase` | dev의 변경사항 위에 내 작업을 재정렬 |
| 5 | `git add`, `git rebase --continue` | 충돌 발생 시 해결 |
| 6 | `git push --force` | rebase된 내 브랜치 다시 푸시 |

---

## 🧠 왜 `merge` 대신 `rebase`를 쓰나요?

| 방식 | 설명 | 장점 |
| --- | --- | --- |
| `merge` | 브랜치를 단순히 병합 | 히스토리 보기 복잡 |
| `rebase` | 내 커밋을 dev 위에 다시 쌓음 | 커밋 히스토리 깔끔, 병합커밋 없음 |

---

## ✅ 실무 팁

- `git log --oneline --graph --all` → 히스토리 구조 확인
- 항상 `dev` 최신화 후 작업 시작!
- 팀과 협의 없이 `force`는 금지

---

# 🧱 Gradle Wrapper & Docker 기반 로컬 개발 실행 가이드

## ✅ 사전 조건

- VSCode에서 터미널을 **3개 분할 창**으로 실행 (`Ctrl + \\` → `Ctrl + Shift + 5`)
- Docker Desktop 실행 중일 것
- `.env.local` 파일 존재

---

## ✅ Gradle 설치 및 Wrapper 생성 전체 흐름

| 단계 | 설명 |
| --- | --- |
| 1 | Gradle 설치 (수동/SDKMAN/패키지 매니저) |
| 2 | 환경 변수 설정 (`GRADLE_HOME`, `PATH`) |
| 3 | 설치 확인 (`gradle -v`) |
| 4 | 프로젝트 루트에서 `gradle wrapper` 실행 |

### 📘 1단계: Gradle 수동 설치 (Windows 기준)

- [Gradle Releases](https://gradle.org/releases/) 접속
- Binary-only(zip) 다운로드 → 예: `gradle-8.7-bin.zip`
- 압축 해제 예시: `C:\Tools\Gradle\gradle-8.7\`

### 📘 2단계: 환경 변수 설정

| 변수 이름 | 값 예시 |
| --- | --- |
| `GRADLE_HOME` | `C:\Tools\Gradle\gradle-8.7` |
| `Path` | `%GRADLE_HOME%\bin` |

### 📘 3단계: 설치 확인

```
gradle -v
```

### 📘 4단계: Wrapper 생성

```
cd C:\gitpch\jibangyoung-new-project4
gradle wrapper
```

> 다음 파일들이 생성됨:
> 

```
gradlew
gradlew.bat
gradle/wrapper/gradle-wrapper.jar
gradle/wrapper/gradle-wrapper.properties
```

---

## ✅ 1. 백엔드 실행 (터미널 ①)

```
./gradlew bootRun
# 또는 Windows에서는
gradlew.bat bootRun
```

---

## ✅ 2. 프론트엔드 실행 (터미널 ②)

```
cd frontend
npm install
npm run dev
```

`.env.local`에 반드시 다음 내용 포함:

```
NEXT_PUBLIC_API_URL=http://localhost:8080
```

---

## ✅ 3. 도커 인프라 실행 (터미널 ③)

```
cd infra/docker
docker compose -f docker-compose.dev.yml up --build
```

종료 시:

```
docker compose -f docker-compose.dev.yml down
```

---

## 📂 도커 구성 요약

| 파일명 | 역할 |
| --- | --- |
| `docker-compose.dev.yml` | 개발용 전체 인프라 정의 |
| `.env.dev` | 도커 실행 시 환경변수 참조 |
| `Dockerfile.backend` | 백엔드 이미지 빌드 정의 |
| `Dockerfile.frontend` | 프론트 이미지 빌드 정의 |
| `init.sql` | DB 초기 데이터 삽입 (옵션) |
| `nginx.conf` | 프록시 및 정적 라우팅 설정 |

---

## ✅ 전체 실행 흐름 정리

| 터미널 | 위치 | 명령어 |
| --- | --- | --- |
| 백엔드 | `cd backend` | `./gradlew bootRun` |
| 프론트 | `cd frontend` | `npm install && npm run dev` |
| 인프라 | `cd infra/docker` | `docker compose -f docker-compose.dev.yml up --build` |

---

## 🔁 Docker 전체 초기화 (선택)

```
docker compose down -v --remove-orphans
docker system prune -af
```

---

## 🧠 참고 사항

| 항목 | 설명 |
| --- | --- |
| MySQL 포트 | `20003` |
| Redis 포트 | `6379` |
| Backend 포트 | `8080` |
| 환경변수 위치 | `.env.local`, `application.yml` |
| API 연결 주소 | `http://localhost:8080` |
| Hot Reload | Spring DevTools, Next.js 적용됨 |

---

✅ 이 문서는 매일 작업 시작 전 개발 환경을 빠르게 준비하고 팀 브랜치 전략을 올바르게 따르기 위한 실전 가이드입니다.

### 🔐 Vercel Secrets 설정

| Name | 설명 |
| --- | --- |
| `VERCEL_TOKEN` | Vercel Personal Access Token (계정에서 생성) |
| `VERCEL_ORG_ID` | Vercel Team or Org ID |
| `VERCEL_PROJECT_ID` | 해당 프로젝트 ID |

해당 값은 GitHub 레포지토리 > **Settings > Secrets and variables > Actions** 탭에서 **Repository secrets**로 등록해야 합니다.

### 🔐 Vercel Token 생성 방법

1. https://vercel.com/account/tokens 접속
2. “Create Token” 클릭 → 복사해서 GitHub Secret에 등록
