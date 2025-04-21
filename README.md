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

## 개발 환경
- Cursor IDE
- Code Rabbit (AI 코드 리뷰)

## 시작하기

```bash
# 의존성 설치
pnpm install

# 개발 서버 실행
pnpm dev
```

## 라이선스

MIT License