# Phase 1 서브에이전트 계약 (Scaffold)

Phase 1에서는 4개 서브에이전트를 병렬 디스패치한다. 각 에이전트는 서로 다른 공유 자산을 담당한다.

---

## 1. Schema Consolidator

```
역할: 모든 feature-spec의 "섹션 4: 데이터 모델"을 수집해 하나의 일관된 DB 스키마를 만든다.

입력:
- manifest_path: {{manifest_absolute_path}}
- feature_specs: manifest.features[].path 목록
- project_root: {{project_absolute_path}}

작업:
1. 각 feature-spec의 섹션 4만 추출 (Grep으로 "## 4. 데이터 모델" ~ 다음 "## 5" 사이)
2. 테이블별로 컬럼 정의를 합친다. 같은 테이블에 서로 다른 정의가 있으면 conflicts 배열에 기록.
3. 프로젝트의 기존 마이그레이션 도구를 Glob으로 탐지:
   - prisma/schema.prisma 존재 → Prisma
   - drizzle.config.* 존재 → Drizzle
   - supabase/migrations/ 존재 → Supabase SQL migrations
   - db/migrations/ 존재 → 프로젝트 관례 SQL
4. 탐지된 도구 형식으로 스키마 작성/업데이트
5. 충돌은 해결하지 말고 report에 기록하여 Human Gate로 넘김

출력:
- 생성/수정 파일 목록
- conflicts: [ { table, column, conflicting_specs: [], resolution_needed: true } ]
- manifest.shared.tables 업데이트 제안
```

---

## 2. Type Generator

```
역할: 모든 feature-spec의 "섹션 5: API 명세"에서 TypeScript interface를 추출해 공유 타입 파일을 만든다.

입력: manifest + feature_specs + project_root

작업:
1. 각 spec의 섹션 5에서 "interface {Name}Request", "interface {Name}Response" 블록 추출
2. 중복 이름은 정의를 비교:
   - 완전히 동일하면 1개만 남김
   - 다르면 conflicts에 기록
3. src/types/api.ts (또는 프로젝트 관례 경로)에 모든 타입 통합 export
4. 엔드포인트 목록을 src/types/endpoints.ts로 별도 생성 (path, method, request/response 매핑)

출력:
- 생성/수정 파일 목록
- conflicts
- manifest.shared.types 업데이트 제안
```

---

## 3. Design Token Extractor

```
역할: 모든 feature-spec의 "섹션 3: UI/UX 명세 - 시각 디자인 스펙" 테이블에서 색상/아이콘/치수 토큰을 추출.

입력: manifest + feature_specs + project_root

작업:
1. 각 spec의 "시각 디자인 스펙 (해당 시)" 섹션에서 배경색/텍스트색/아이콘 테이블 추출
2. 동일한 의미의 색상은 토큰화 (예: status.pending, status.approved)
3. 프로젝트 관례 탐지:
   - tailwind.config.* → tailwind theme extend
   - 디자인 시스템 라이브러리 (chakra, mui 등) 존재 → 해당 테마 형식
   - 없으면 src/styles/tokens.ts (CSS custom properties + TS 상수)
4. 아이콘은 라이브러리 이름만 정리 (실제 설치는 하지 않음, todo로 남김)

출력:
- 생성/수정 파일
- 아이콘 설치 todo 목록
```

---

## 4. Router Skeleton

```
역할: 페이지 명세 목록을 기반으로 라우터 골격과 페이지 컴포넌트 빈 파일을 생성.

입력:
- page_specs_glob: docs/specs/page-specs/**/00-page-spec.md
- project_root

작업:
1. 각 page-spec에서 frontmatter의 title과 경로 힌트 추출
2. 프로젝트 라우터 관례 탐지:
   - app/ 디렉토리 + page.tsx 존재 → Next.js App Router
   - pages/ 디렉토리 존재 → Next.js Pages Router
   - react-router-dom in package.json → React Router
   - routes/ + vite.config → Vite 기반
3. 각 페이지마다 빈 컴포넌트 파일 + 라우트 등록
4. 빈 컴포넌트는 `<h1>{title}</h1>` 수준의 플레이스홀더만 포함 (Phase 2에서 구현)

출력:
- 생성 파일 목록
- 라우터 등록 파일 경로
```

---

## 공통 계약

모든 Phase 1 에이전트는 다음을 지킨다:

- **충돌은 해결하지 않는다** — Human Gate 1에서 사용자가 결정하도록 리포트만 남긴다
- **기존 파일이 있으면 덮어쓰지 않는다** — 마이그레이션은 append, 타입은 병합
- **의존성 설치 금지** — package.json 수정 금지, 필요한 패키지는 todo로만 남김
- **사용자에게 질문 금지** — 불명확한 경우 기본 관례 따르고 리포트에 기록

## 오케스트레이터 체크리스트

4개 에이전트를 **동일한 메시지에서 병렬 디스패치**한다. 순차 실행 금지.
모두 완료 후 phase-1-report.md 생성 → Human Gate 1 제시.
