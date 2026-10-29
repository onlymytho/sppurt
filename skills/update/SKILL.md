---
name: sppt-update
description: |
  Sppurt CLI 버전 업데이트 + 릴리즈 노트 확인.
  Use when asked to "업데이트", "최신 버전", "sppt update", "버전 올려줘", "새 버전 있어?".
---

# update

Sppurt CLI를 최신 버전으로 업데이트하고 변경사항을 확인하는 워크플로우.

## When to use

- "업데이트 해줘", "최신 버전으로 올려줘"
- "새 버전 나왔어?", "지금 몇 버전이야?"
- 스킬이 안 되거나 새 커맨드가 없을 때

## Steps

### 1. 현재 버전 확인

```bash
sppt --version
```

### 2. 최신 버전 확인

```bash
npm view sppurt version
```

현재 버전과 최신 버전을 비교합니다.
- 같으면 → "이미 최신 버전입니다" 안내 후 종료
- 다르면 → 3단계로 진행

### 3. 업데이트 실행

```bash
npm update -g sppurt
```

설치 시 `postinstall` 훅이 자동으로 `setup-skills`를 실행하여 새 스킬도 함께 등록됩니다.

### 4. 업데이트 확인

```bash
sppt --version
```

버전이 올라갔는지 확인합니다.

### 5. 릴리즈 노트 확인

```bash
gh release view v<최신버전> --repo onlymytho/shopport
```

주요 변경사항을 사용자에게 요약해줍니다:
- 새로 추가된 기능/스킬
- 버그 수정 사항
- Breaking changes (있는 경우)

## 결과 요약 형식

```
📦 Sppurt 업데이트 완료
────────────────────────────────────
이전 버전:  v0.2.4
현재 버전:  v0.3.0
────────────────────────────────────
주요 변경:
• 정산 엔진 대폭 강화 (채널×PG 분리 계산)
• 알림 체계 구축
• 새 스킬: /sppt-policy-ask
────────────────────────────────────
```

## Notes

- 기존 `shopport` 패키지 사용자라면 한 번 `npm uninstall -g shopport` 후 `npm install -g sppurt`를 실행하세요. `sppt` 명령과 기존 사용자 데이터는 유지됩니다.
- `npm update -g`가 안 되면 `npm install -g sppurt@latest`로 시도
- 권한 오류 시 `sudo npm update -g sppurt` 또는 nvm/volta 사용 권장
- 업데이트 후 스킬이 갱신되지 않으면 `sppt setup-skills` 수동 실행
