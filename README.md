# Very Light-Weight Coin Tracker

간단하고 직관적인 암호화폐 가격 트래커

## 프로젝트 개요

- TradingView와 유사한 인터페이스로 구현
- 실시간 암호화폐 가격 모니터링

## 기술 스택

### Frontend
- Vite
- React.js 19
- TypeScript

### 상태 관리 및 데이터 페칭
- React Query (TanStack Query)
- Zustand

### 폼 관리 및 유효성 검사
- React Hook Form
- Zod

### Routing
- @tanstack/react-router

### UI/UX
- shadcn/ui
- Tailwind CSS

### DevOps
- Docker
- Jenkins (CI/CD)

## 아키텍처

### Feature-Sliced Design (FSD)
프로젝트는 Feature-Sliced Design 아키텍처를 따릅니다. 각 레이어는 명확한 책임과 의존성 규칙을 가집니다.

#### 레이어 (상위에서 하위로)
1. **app/** - 애플리케이션 초기화
   - 전역 프로바이더
   - 라우팅 설정
   - 스타일 초기화

2. **pages/** - 페이지 컴포넌트
   - 라우트별 페이지
   - 페이지 레이아웃

3. **widgets/** - 큰 UI 블록
   - 여러 feature를 조합
   - 독립적인 UI 섹션
   - 예: 차트 위젯, 주문 패널

4. **features/** - 사용자 기능
   - 특정 비즈니스 로직
   - 사용자 상호작용
   - 예: 가격 알림, 차트 그리기

5. **entities/** - 비즈니스 엔티티
   - 핵심 비즈니스 객체
   - 재사용 가능한 모델
   - 예: 통화, 주문, 캔들

6. **shared/** - 공유 인프라
   - 유틸리티 함수
   - UI 컴포넌트
   - API 클라이언트

#### 의존성 규칙
- 상위 레이어는 하위 레이어에 의존 가능
  - widgets -> features -> entities [✅]
- 하위 레이어는 상위 레이어에 의존 불가
  - entities -> features -> widgets [❌]
- 같은 레이어 내에서는 의존성 없음

## 테스트 전략

### 컴포넌트 테스트 (Storybook)
- **도구**: Storybook
- **목적**: UI 컴포넌트의 격리된 테스트와 문서화
- **범위**: 
  - shared/ui의 모든 컴포넌트
  - entities의 UI 컴포넌트
  - features의 UI 컴포넌트
  - widgets의 UI 컴포넌트

#### Storybook 구조
```
.storybook/
├── main.ts
└── preview.ts

src/
└── stories/
    ├── shared/
    │   └── Button.stories.tsx
    ├── entities/
    │   └── CurrencyCard.stories.tsx
    ├── features/
    │   └── PriceAlert.stories.tsx
    └── widgets/
        └── TradingChart.stories.tsx
```

### 통합 테스트 (React Testing Library)
- **도구**: React Testing Library + Vitest + vitest-dom
- **목적**: 실제 사용자 관점에서의 기능 테스트
- **범위**:
  - 사용자 시나리오 기반 테스트
  - API 통합 테스트
  - 상태 관리 테스트
  - 라우팅 테스트

#### 테스트 구조
```
src/
└── __tests__/
    ├── integration/
    │   ├── trading/
    │   │   ├── order-creation.test.tsx
    │   │   └── price-alert.test.tsx
    │   └── market-data/
    │       └── websocket.test.tsx
    └── setup/
        ├── test-utils.tsx
        └── mocks/
```

#### 테스트 원칙
1. **사용자 중심 테스트**
   - 실제 사용자 행동 시뮬레이션
   - DOM 쿼리 우선 사용
   - 접근성 고려

2. **통합 테스트 우선**
   - 단위 테스트보다 통합 테스트 중점
   - 실제 사용 시나리오 기반
   - API 모킹 최소화

3. **테스트 격리**
   - 각 테스트는 독립적
   - 테스트 간 상태 공유 없음
   - 자동 정리(cleanup) 구현

## 개발 환경
- Cursor IDE
- Code Rabbit (AI 코드 리뷰)

## 시작하기

```bash
# 의존성 설치
pnpm install

# 개발 서버 실행
pnpm dev

# Storybook 실행
pnpm storybook

# 테스트 실행
pnpm test
```

## 라이선스

MIT License