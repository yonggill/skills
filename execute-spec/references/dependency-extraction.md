# Dependency Extraction — feature-spec → DAG

Phase 0에서 각 feature-spec을 파싱해 manifest를 만들 때 참조한다.

## 추출 대상 요약

| manifest 필드 | 원 소스 |
|---------------|--------|
| `id` | 파일 경로에서 `{NN}-{page}/{MM}-{feature}` |
| `title` | frontmatter `title` 또는 첫 `#` 헤딩 |
| `page_id` | 파일 경로의 `{NN}-{page}` 부분 |
| `complexity` | 섹션 14 "복잡도" 값, 없으면 `"medium"` |
| `us_ac_count` | 섹션 2의 `[ ] AC-` 개수 |
| `depends_on` | 섹션 9 + 섹션 10 (아래 규칙) |
| `shared_resources.tables` | 섹션 4 테이블 이름 |
| `shared_resources.apis` | 섹션 5 `METHOD path` |
| `shared_resources.types` | 섹션 5 `interface {Name}` |
| `shared_resources.components_hint` | 섹션 3 컴포넌트 계층 중 재사용 힌트 |

## `depends_on` 결정 규칙

의존성은 **같은 페이지 내 연관 기능 (섹션 9)** 과 **크로스 페이지 의존성 (섹션 10)** 두 군데에서 나온다.

### 섹션 9: 페이지 내 연관 기능

```markdown
## 9. 페이지 내 연관 기능
| 기능명 | 상호작용 방식 | 데이터 공유 |
|--------|-------------|------------|
| 알림 규칙 설정 | 목록에서 편집 버튼 → 설정 페이지 | rule_id 공유 |
```

**변환**:
- "기능명"을 같은 페이지의 feature-spec 파일명과 매칭 (제목 유사도 또는 직접 매핑)
- 매칭 성공 → `depends_on: ["{page-id}/{feature-id}"]`
- 매칭 실패 → manifest의 `warnings`에 기록, 해당 depends_on은 비움

### 섹션 10: 크로스 페이지 의존성

```markdown
### 선행 페이지
| 페이지 | 의존 내용 |
|--------|----------|
| 계약 관리 | 계약 ID 목록 제공 |
```

**변환**:
- "페이지" 이름 → page_id로 매핑 (페이지 명세 frontmatter 또는 2단계 메뉴 정의 참조)
- 선행 페이지의 모든 기능이 완료되기를 기다린다는 뜻이 아니다. 의미상 어떤 **데이터**가 필요한지에 따라 결정:
  - "목록 제공" 같은 읽기 의존 → `page-id/01-` (일반적으로 첫 기능이 목록 조회)
  - 특정 액션 필요 (예: "계약 승인 후") → 해당 액션 기능 ID
  - 불확실 → 페이지의 대표 기능 1개만 의존으로 등록, warnings에 기록

### 후행 페이지는 의존성 아님

섹션 10의 "후행 페이지"는 이 기능이 제공하는 데이터를 쓰는 쪽이다. 본 기능의 `depends_on`이 아니라 **역방향 참조**. manifest의 `reverse_deps`에 기록하되 DAG 위상정렬에는 쓰지 않는다.

## 위상정렬과 레벨 할당

```
level = max(level of each dep) + 1
level = 1 if depends_on is empty
```

구현 의사코드:

```
unresolved = features
level = 1
while unresolved:
  ready = [f for f in unresolved if all(d.level < level for d in f.depends_on)]
  if not ready: raise CycleDetected
  for f in ready: f.level = level
  unresolved -= ready
  level += 1
```

### 순환 참조 처리

A가 B에 의존하고 B가 A에 의존하는 경우 — 대부분 스펙 작성 오류. 발견 시:

1. manifest의 `cycles` 배열에 기록
2. 순환에 포함된 기능들은 **같은 레벨**에 강제로 배치하고 warnings로 노출
3. Phase 2 시작 전 Human Gate는 아니지만, Phase 1 리포트의 경고 섹션에 기록

## 공유 리소스 카탈로그 병합 규칙

여러 스펙이 같은 테이블/타입을 정의하는 경우 manifest.shared에서 병합:

```json
"shared": {
  "tables": {
    "notifications": {
      "defined_in": ["01-notification-center/01-notification-list-view", "01-notification-center/02-notification-rule-settings"],
      "columns": [
        { "name": "id", "type": "UUID", "consistent": true },
        { "name": "user_id", "type": "UUID", "consistent": true },
        { "name": "priority", "type": "INT | ENUM", "consistent": false, "defined_in": {...} }
      ]
    }
  }
}
```

`consistent: false`가 하나라도 있으면 manifest.shared.conflicts에 추가. Phase 1 Schema Consolidator가 읽고 충돌 리포트로 올린다.

## 예시: manifest의 한 기능 엔트리

```json
{
  "id": "01-notification-center/02-notification-rule-settings",
  "path": "docs/specs/feature-specs/01-notification-center/02-notification-rule-settings.md",
  "title": "알림 규칙 설정",
  "page_id": "01-notification-center",
  "complexity": "medium",
  "us_ac_count": 9,
  "depends_on": ["01-notification-center/01-notification-list-view"],
  "level": 2,
  "shared_resources": {
    "tables": ["notifications", "notification_rules"],
    "apis": ["GET /api/notifications/rules", "PUT /api/notifications/rules/:id"],
    "types": ["NotificationRule", "NotificationRuleRequest"],
    "components_hint": ["Form", "Modal", "Toggle"]
  },
  "status": "pending"
}
```
