---
description: 선생님의 언어·말투·톤·이모지·호칭을 설정 (teach-me-a-lesson config 모드)
argument-hint: (선택) "반말로 발랄하게" 같은 자연어
---

`teach-me-a-lesson` 스킬을 **config 모드**로 사용해 톤·언어 설정을 진행하라.
설정 스키마·페르소나·저장 위치·절차는 스킬의 `references/tone-config.md`를 따른다.

요청: $ARGUMENTS

- **인자가 있으면(자연어):** 그 말에서 의도를 읽어 `references/tone-config.md`의 "B) 자연어" 절차대로 **언급된 항목만** 갱신한다(나머지 값 보존).
- **인자가 없으면(대화형):** "A) 대화형" 절차대로 언어 → 말투 격식 → 톤·페르소나 → 이모지·감탄사 양 → 호칭(선택)을 차례로 묻는다. 가능하면 AskUserQuestion으로 선택지를 제시한다.
- 설정은 `~/.claude/teach-me-a-lesson/config.json`에 저장한다(폴더 없으면 생성, 기존 키는 병합). 개인 톤 파일이라 배포본엔 동봉하지 않는다.
- 저장 후: **무엇이 바뀌었는지** 요약하고, **바뀐 톤으로 샘플 한 줄**을 보여줘 효과를 확인시킨다.
