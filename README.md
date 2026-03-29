# Writing Assistant — 내 글에 영혼을 불어넣는 AI 글쓰기 코치

Writing Assistant는 Claude Code에서 동작하는 글쓰기 코치 스킬입니다.
막연한 아이디어를 바로 초안으로 밀어붙이지 않고, 목적·독자·구조를 먼저 정렬한 뒤 글을 완성합니다.
핵심은 **페르소나 깎기 루프**, **6장르 가이드**, **10차원 Style Card**, **7단계 글쓰기 루프**입니다.
에세이부터 보고서까지, 한 번 쓰고 끝나는 도구가 아니라 **쓸수록 내 문체를 더 잘 이해하는 편집 파트너**를 지향합니다.

## Quick Start

```bash
# 설치
cp -r skills/ ~/.claude/skills/
cp -r commands/ ~/.claude/commands/

# 사용
/write 에세이 — AI가 바꾼 글쓰기 습관
/write persona — 내 문체 분석 (Style Card 생성)
```

추가 예시:

```text
/write 블로그 — 검색 의도: "AI 글쓰기 도구 추천"
/write 칼럼 — 핵심 주장: "AI는 사고력을 외주화한다"
/write 보고서 — 파일 참고: report-data.xlsx
```

## 핵심 기능

### 1. 페르소나 깎기 루프
내가 쓴 글 샘플 2~5개를 바탕으로 반복 패턴을 추출하고, 이를 Style Card로 구조화합니다.
초안에 적용한 뒤 사용자 피드백을 `keep/discard`로 판정해 다시 반영하므로, 문체가 일회성 흉내가 아니라 점진적으로 정교해집니다.

### 2. 6장르 가이드
에세이, 칼럼, 기사, 블로그, 뉴스레터, 보고서를 기본 장르로 지원합니다.
각 장르마다 요구되는 구조, 리드 방식, 근거 처리, 엔딩 감각이 다르므로 장르별 플레이북에 맞춰 글의 골격을 잡습니다.

### 3. 10차원 문체 분석
문체를 막연한 취향이 아니라 10개의 분석 축으로 다룹니다.
목소리, 관점 거리, 문장 길이, 문단 호흡 같은 요소를 분리해 보기 때문에 “왜 이 글이 나답게 느껴지는지”를 설명 가능한 규칙으로 바꿀 수 있습니다.

### 4. 7단계 글쓰기 루프
주제 구체화 → 개요 작성 → 승인 게이트 → 초안 → 퇴고 범위 선택 → 검토 → 최종본 정리의 흐름으로 진행합니다.
특히 **개요 승인 전에는 초안으로 넘어가지 않는 규칙**이 있어, 글의 방향이 흔들린 채 장문을 쓰는 낭비를 줄여줍니다.

### 5. GPTs 호환 Style Card
`.style-card.md`는 Claude Code와 GPTs에서 동일한 형식으로 사용할 수 있습니다.
한 번 만든 문체 기준을 다른 환경으로 옮겨도 깨지지 않으므로, 글쓰기 워크플로우를 도구에 종속시키지 않고 이어갈 수 있습니다.

## 사용 예시

### 1. `/write 에세이`
개인 경험을 통찰로 연결하는 글을 쓰고 싶을 때 사용합니다.
도구는 먼저 주제와 각도를 구체화하고, 제목 후보와 핵심 메시지가 포함된 개요를 제안합니다.
개요를 승인하면 그 구조를 바탕으로 초안을 쓰고, 이후 문장·구조·문체 중 어떤 범위를 손볼지 선택할 수 있습니다.

### 2. `/write persona`
내 문체를 먼저 분석하고 싶을 때 사용합니다.
직접 쓴 글 샘플 2~5개를 바탕으로 10차원 Style Card 초안을 만들고, “맞는 점 / 어색한 점” 피드백으로 다듬습니다.
완성된 `.style-card.md`는 다음 글쓰기 세션부터 자동 로드되어 기본 문체 기준으로 작동합니다.

### 3. `/write 보고서`
보고서나 업무 문서처럼 요약, 판단 근거, 실행 제안이 중요한 글에 적합합니다.
파일 경로나 초안이 있으면 먼저 읽고, 빠진 근거와 보강이 필요한 항목을 식별한 뒤 구조를 정리합니다.
필요하면 팩트체크나 플랫폼 변환 모드와 연결해 경영진 보고용, 공유용 버전으로 다시 다듬을 수 있습니다.

## Style Card

프로젝트 루트에 `.style-card.md`가 있으면 세션 시작 시 자동으로 로드합니다.
파일이 없으면 사용자의 글 샘플 2~5개를 요청해 새 Style Card를 생성합니다.
GPTs에서 내보낸 Style Card도 **동일 형식**이면 그대로 사용할 수 있습니다.

### 10차원 목록
1. 목소리 (`voice`)
2. 관점 거리 (`perspective_distance`)
3. 문장 길이 (`sentence_length`)
4. 문단 호흡 (`paragraph_rhythm`)
5. 어휘 수준 (`vocabulary_level`)
6. 전환 습관 (`transition_habits`)
7. 강조 방식 (`emphasis_patterns`)
8. 사례 사용법 (`evidence_usage`)
9. 오프닝/엔딩 패턴 (`opening_ending_patterns`)
10. 말버릇/금지어 (`verbal_habits_banned_phrases`)

### canonical format

```markdown
# Style Card

- profile_name:
- source_samples:
- default_intensity: medium
- updated_at:

## 1. voice
- keep:
- avoid:

## 2. perspective_distance
- keep:
- avoid:

## 3. sentence_length
- keep:
- avoid:

## 4. paragraph_rhythm
- keep:
- avoid:

## 5. vocabulary_level
- keep:
- avoid:

## 6. transition_habits
- keep:
- avoid:

## 7. emphasis_patterns
- keep:
- avoid:

## 8. evidence_usage
- keep:
- avoid:

## 9. opening_ending_patterns
- keep:
- avoid:

## 10. verbal_habits_banned_phrases
- keep:
- avoid:

## Change Log
- YYYY-MM-DD: keep/discard | dimension | reason | note
```

## 파일 구조

```text
writing-assistant/
├── commands/
│   └── write.md
├── skills/
│   ├── writing-assistant.md
│   └── references/
│       ├── genre-playbooks.md
│       ├── style-system.md
│       ├── review-lenses.md
│       └── prompt-templates.md
├── gpts-output/
│   ├── 00_instructions_v2.md
│   ├── 04_style_reference_ingestion_v2.md
│   └── 06_outline_draft_revise_loop_v2.md
├── CLAUDE.md
└── README.md
```

## 전문가 기반

이 스킬은 세 가지 축을 바탕으로 설계되었습니다.

- **William Zinsser** — 명료성, 간결함, 불필요한 장식 제거
- **Ann Handley** — 실용성, 리듬, 독자와의 연결감
- **Donald Schön** — 반성적 개선 루프, 피드백 기반 반복 개선

## License

MIT
