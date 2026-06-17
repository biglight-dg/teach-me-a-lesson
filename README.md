# teach-me-a-lesson — AI·개발 입문 친절한 선생님 스킬

Claude·AI 툴·개발/IT 입문 개념을 **완전 초보·비개발자에게 친절한 선생님처럼** 설명하고, 곁에서 꾸준히 도와주는 [Claude 스킬](https://docs.claude.com/en/docs/claude-code/skills)입니다.

정답을 던지는 대신, **비유 하나로 "아, 그거구나!"** 하는 순간을 만드는 데 집중합니다.

## 무엇을 하나요

다섯 가지 모드로 움직입니다(말로 요청해도, 슬래시 커맨드로 불러도 됩니다).

| 모드 | 커맨드 | 하는 일 |
|------|--------|---------|
| **explain** | `/tl-explain <주제>` | 개념을 비유·표·핵심교훈으로 쉽게 설명 (기본) |
| **mistake** | `/tl-mistake` | 방금 무엇이·왜 잘못됐는지 비난 없이 진단하고 고치는 법 안내 |
| **bad-habit** | `/tl-bad-habit` | 반복되는 나쁜 습관을 찾아 더 나은 방식 제안 |
| **knowledge** | `/tl-knowledge <주제>` | 배운 개념을 지식 파일(마크다운 노트)로 저장 |
| **config** | `/tl-config` | 선생님의 언어·말투·톤·이모지·호칭 설정 |

또한 스킬이 켜져 있는 동안 **상시 조력자**로 작동합니다: 위험한 행동(모르는 명령어 붙여넣기, API 키 노출, 되돌리기 힘든 작업), 오개념에 기반한 요청, 비효율적 접근이 보이면 — 잔소리 없이 **부드럽게 짚어주고**, 결정은 사용자에게 맡깁니다.

> 참고: 상시 짚어주기는 이 스킬이 로드돼 있는 동안(대화 맥락) 작동합니다. 매 입력마다 자동 검사하는 훅(hook)이 아닙니다.

### 발동 예시

- "MCP가 뭔지 진짜 쉽게 알려줘. 나 완전 초보야"
- "API랑 SDK가 자꾸 헷갈려. 차이 좀 비유로 설명해줘"
- "터미널이 무서운데 꼭 써야 해?"
- "내가 방금 .env를 깃허브에 올린 것 같은데 뭐가 문제야?" → mistake
- "내 나쁜 습관 좀 짚어줘" → bad-habit

## 설치

### 1) 스킬 폴더 복사

```bash
# macOS / Linux
cp -r teach-me-a-lesson ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse teach-me-a-lesson $env:USERPROFILE\.claude\skills\
```

### 2) 슬래시 커맨드 설치 (선택, /tl-* 쓰려면)

스킬 폴더 안 `commands/`의 파일들을 커맨드 폴더로 복사합니다.

```bash
# macOS / Linux
cp teach-me-a-lesson/commands/tl-*.md ~/.claude/commands/

# Windows (PowerShell)
Copy-Item teach-me-a-lesson\commands\tl-*.md $env:USERPROFILE\.claude\commands\
```

커맨드 없이도 "쉽게 설명해줘" 같은 말로 스킬이 자동 발동합니다. 커맨드는 모드를 명시적으로 부를 때 편합니다.

## (선택) 내 지식 파일 연결하기

이 스킬은 **지식 파일**(마크다운 노트 모음)이 있으면 그것을 우선 근거로 사용합니다. 없으면 Claude 자체 지식으로 설명하므로 **지식 파일 없이도 그대로 작동**합니다.

- 기본 조회/저장 폴더: 작업 폴더의 `./knowledge/` 또는 `~/.claude/teach-me-a-lesson/knowledge/`
- 이미 모아둔 노트 폴더가 있으면 그 경로를 쓰면 됩니다.
- 자세한 규칙·인덱스(선택) 형식은 `references/knowledge-files.md` 참고.

> 이 저장소에는 개인 지식 문서가 포함되어 있지 않습니다. 교육 방법론(스킬 본체)만 공개합니다.

## 톤·언어 설정하기

선생님의 **언어·말투·분위기**를 취향대로 바꿀 수 있습니다. 한국어는 존댓말/반말뿐 아니라 **분위기(다정·담백·발랄·깍듯)**까지 조절됩니다.

- `/tl-config` — 언어 → 말투 격식(해요체/합쇼체/반말) → 톤·페르소나 → 이모지량 → 호칭을 차례로 묻고 저장
- 자연어로도 됩니다 — "반말로 발랄하게 해줘", "영어로 설명해줘", "이모지 좀 빼줘"
- 설정은 `~/.claude/teach-me-a-lesson/config.json`에 저장됩니다(개인 톤 파일이라 배포본엔 동봉 안 함). 설정이 없으면 **기본값(다정한 선생님, 해요체)**으로 작동합니다.
- 어떤 톤이든 교육 품질(비유·비난 금지·과부하 금지·출처)은 그대로 유지됩니다. 자세한 건 `references/tone-config.md` 참고.

## 구성

```
teach-me-a-lesson/
├── SKILL.md                      # 발동 조건 + 5개 모드 + 상시 짚어주기 + 톤 설정 + 워크플로우
├── references/
│   ├── teaching-style.md         # 비유 만드는 법, 좋은/나쁜 예, 부드럽게 교정하는 화법
│   ├── knowledge-files.md        # 지식 파일 조회·저장 규칙 (범용)
│   ├── modes.md                  # 5개 모드 상세 + 상시 짚어주기 예시
│   └── tone-config.md            # 언어·말투·톤·이모지·호칭 설정 스키마와 페르소나
├── commands/                     # /tl-* 슬래시 커맨드 (커맨드 폴더로 복사해 사용)
├── evals/
│   └── evals.json
├── README.md
└── LICENSE
```

## 라이선스

MIT License. 자유롭게 사용·수정·재배포하세요.
