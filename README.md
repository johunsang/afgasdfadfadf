# OneSaaS Starter Kit

> 인증, 결제, 관리자 대시보드가 포함된 한국형 SaaS 스타터 킷

Next.js 14 + Supabase + Tailwind CSS 기반

## 포함된 기능

| 기능 | 설명 |
|-----|------|
| **인증** | 이메일, Google, 카카오, GitHub 로그인 |
| **결제** | PortOne, TossPayments 연동 |
| **관리자** | 대시보드, 사용자 관리, 통계 |
| **UI** | 버튼, 카드, 모달, 입력폼 등 공통 컴포넌트 |
| **테마** | CSS 변수 기반 다크/라이트 테마 |
| **AI** | OpenAI, Anthropic SDK 연동 준비 |

## 빠른 시작

```bash
# 1. 클론
git clone https://github.com/johunsang/onesass-starter.git my-saas
cd my-saas

# 2. 의존성 설치
pnpm install

# 3. 환경변수 설정
cp .env.example .env
# .env 파일에 Supabase, 결제 API 키 입력

# 4. DB 스키마 적용
pnpm db:push

# 5. 개발 서버 실행
pnpm dev
```

http://localhost:3000 에서 확인

## 폴더 구조

```
src/
├── app/                    # Next.js 페이지
│
├── onesaas-core/          # 🔒 공통 모듈 (수정 금지)
│   ├── auth/              # 인증 시스템
│   ├── payment/           # 결제 시스템
│   ├── admin/             # 관리자 대시보드
│   └── ui/                # 공통 UI 컴포넌트
│
├── onesaas-custom/        # ✅ 비즈니스 영역 (자유롭게 수정)
│   ├── landing/           # 커스텀 랜딩 페이지
│   ├── pages/             # 커스텀 페이지
│   └── components/        # 커스텀 컴포넌트
│
└── onesaas-bridge/        # 🔗 설정 레이어
    ├── config.ts          # 서비스 설정
    ├── routes.ts          # 라우팅 설정
    └── feature-flags.ts   # 기능 플래그
```

### 영역 구분

- **onesaas-core**: 템플릿 업데이트 시 자동 패치됨. **직접 수정 금지**
- **onesaas-custom**: 업데이트해도 절대 덮어쓰지 않음. **자유롭게 수정**
- **onesaas-bridge**: 설정 파일만 수정

## 설정 파일 (onesaas.json)

기능 활성화/비활성화:

```json
{
  "project": {
    "name": "내 SaaS",
    "slug": "my-saas"
  },
  "features": {
    "auth": {
      "enabled": true,
      "providers": ["email", "google", "kakao"]
    },
    "payment": {
      "enabled": true,
      "provider": "portone"
    },
    "admin": {
      "enabled": true
    }
  }
}
```

## 환경 변수

`.env` 파일 설정:

```bash
# Supabase
NEXT_PUBLIC_SUPABASE_URL=https://xxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJ...

# 결제 (PortOne)
NEXT_PUBLIC_PORTONE_MERCHANT_ID=imp...
PORTONE_API_KEY=...

# 결제 (TossPayments) - 선택
NEXT_PUBLIC_TOSS_CLIENT_KEY=...
TOSS_SECRET_KEY=...

# AI - 선택
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
```

## 스크립트

```bash
pnpm dev          # 개발 서버 (http://localhost:3000)
pnpm build        # 프로덕션 빌드
pnpm db:push      # DB 스키마 적용
pnpm db:studio    # Prisma Studio (DB GUI)
```

## 기술 스택

- **프레임워크**: Next.js 14 (App Router)
- **스타일**: Tailwind CSS
- **데이터베이스**: Prisma + Supabase (PostgreSQL)
- **인증**: Supabase Auth
- **결제**: PortOne / TossPayments
- **AI**: Vercel AI SDK (OpenAI, Anthropic)

## Claude Code 사용

이 프로젝트는 Claude Code와 함께 사용하도록 설계되었습니다.

```bash
# Claude Code 설치 후
cd my-saas
claude

# 예시 요청
> "로그인 페이지에 GitHub 로그인 추가해줘"
> "가격 페이지에 연간 결제 옵션 추가해줘"
> "상품 목록 페이지 만들어줘"
```

자세한 가이드: [CLAUDE.md](./CLAUDE.md)

## 배포

### Vercel (권장)

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/johunsang/onesass-starter)

### 수동 배포

```bash
pnpm build
# .next 폴더를 Vercel/AWS/GCP에 배포
```

## 문서

- [CLAUDE.md](./CLAUDE.md) - Claude Code 사용 가이드
- [MAINTENANCE.md](./MAINTENANCE.md) - 유지보수 가이드
- [onesaas-core/README.md](./src/onesaas-core/README.md) - 공통 모듈 문서

## 라이선스

MIT
