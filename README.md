# duli (둘이검토)

AI 하나가 쓴 것은 그 AI가 못 봐요. 둘이검토는 **다른 AI(또는 다른 모델)가 먼저 혼자 읽고** 틀린 것·안 통할 것·더 나은 길을 적어 주고, "더 고칠 거 없음"이 양쪽에서 나올 때까지 주고받는 절차예요. 설계를 검토할 때, 일을 나눠서 할 때, 결과물을 올리기 전에 씁니다. 공유 폴더로 파일을 주고받아서 누가 뭘 고쳤는지 다 남아요.

## 이렇게 써요

1. 작업하던 AI 도구 창에 이 한 줄을 붙여 넣어요.

```
https://github.com/wootwj-dotcom/duli 이 스킬 설치해 줘
```

클로드 코드, 코덱스 앱, 제미나이 CLI 어디든 돼요. 깃허브에서 직접 받을 건 없어요.

2. 처음 한 번만 여섯 가지를 물어요. 닉네임, 쓰는 AI 도구, 컴퓨터 대수, 공유 폴더, 이미 있는 협업 규칙 파일, 검토 짝꿍으로 쓸 모델. 답하면 공유 폴더와 협업 규칙 파일, AI가 매번 읽을 안내(AGENTS.md)를 만들어 주고, 짝꿍 AI 창에 붙여 넣을 프롬프트를 줘요.

3. 그다음부터는 이렇게 말하면 돼요.

| 말 | 하는 일 |
|---|---|
| "설계 검토해" | 지금까지 대화한 설계를 파일로 정리해 짝꿍이 먼저 읽고 틀린 전제·빠진 경우·더 단순한 대안을 적어요 |
| "같이 해", "나눠서 해" | 조사·비교는 짝꿍에게, 합치기·판단은 반장이 맡아요 |
| "마무리 검토해", "더 나은 방향 없어?" | 결과물을 짝꿍이 먼저 읽고 틀린 것·안 통할 것·개인정보를 잡아요. 지적마다 채택·반박·보류를 표로 정해요 |

다음부터는 `/duli`라고 치면 돼요. 코덱스처럼 슬래시 명령이 없는 도구에서는 "둘이검토 해 줘"라고 하면 돼요.

## AI가 하나뿐이어도 돼요

짝꿍 자리에 **다른 모델**을 새로 띄워요. 어떤 모델로 할지는 처음 설정에서 한 번 묻고 저장해요. 비우면 "지금 쓰는 모델의 한 단계 위, 이미 맨 위면 한 단계 아래"로 골라요. "이번엔 ○○로 검토해"라고 하면 그때만 바꿔요. 새로 띄운 모델은 대화를 모르고 파일만 읽어서 독립 검토가 돼요. 챗GPT 웹처럼 폴더를 못 읽는 도구가 짝꿍이면, 파일을 첨부하고 답을 저장하는 건 사용자가 해 줘요.

## 무엇이 나와요

- 공유 폴더 안에 번호가 붙은 파일들: 설계안, 작업 분배, 검토 요청, 답, 토론, 완료. 누가 언제 뭘 고쳤는지 이 파일들이 기록이에요.
- 마지막에 사용자가 받는 것: 바뀐 것 3줄, 토론으로 정한 것, 결과물 경로. 게시·발송은 늘 사용자가 직접 해요.

## 처음 한 번 만들어 주는 것

- `live_collaboration` 폴더(공유 폴더가 있으면 그 안에, 없으면 지금 작업 폴더 안에)와 `백업` 폴더
- `협업규칙.md` (이미 쓰는 규칙 파일이 있으면 만들지 않고 그걸 써요)
- `AGENTS.md`에 다섯 줄 덧붙이기. **이미 있는 AGENTS.md는 덮어쓰지 않고** 끝에 표시된 블록만 붙여요. 붙이기 전에 `.bak`을 남기고, 붙인 줄을 보여 줘요. `CLAUDE.md`가 없으면 `@AGENTS.md` 한 줄짜리로 만들어요.
- 설정은 `~/.duli/profile.json`에 저장돼요. "프로필 다시 설정"이라고 하면 다시 물어요.

## 자주 묻는 것

**짝꿍 AI가 파일을 못 찾아요.** 파일 이름에 화살표(→)가 있어서 검색으로는 안 잡힐 때가 있어요. 전체 경로를 그대로 붙여 주세요. 다른 컴퓨터면 원드라이브 동기화가 끝났는지 폰이나 웹에서 먼저 확인하세요.

**30분 넘게 답이 없어요.** 동기화 지연이거나 짝꿍 창이 폴더 확인을 멈춘 거예요. 짝꿍 창에 "폴더 확인해 줘"라고 한 번 치면 돼요.

**둘이 의견이 안 맞아요.** 사용자에게 안 물어요. 토론 파일에서 근거로 끝내고, 2왕복 안에 안 갈리면 둘 다 조건을 붙여 적어요.

**지우거나 되돌리려면요?** 설치한 스킬 폴더(`~/.claude/skills/duli` 등)를 지우면 돼요. AGENTS.md는 `<!-- duli 시작 -->`부터 `<!-- duli 끝 -->`까지 지우면 원래대로예요.

## 터미널로 설치하고 싶다면

Windows (PowerShell)

```powershell
$R="https://raw.githubusercontent.com/wootwj-dotcom/duli/main/.claude/skills/duli"; $T="$env:USERPROFILE\.claude\skills\duli"; New-Item -ItemType Directory -Force "$T\templates" | Out-Null; foreach ($f in "SKILL.md","VERSION","templates/협업규칙.md","templates/AGENTS-블록.md") { Invoke-WebRequest -UseBasicParsing -Uri "$R/$f" -OutFile (Join-Path $T ($f -replace "/","\")) }; Test-Path "$T\SKILL.md"
```

Mac / Linux

```bash
R="https://raw.githubusercontent.com/wootwj-dotcom/duli/main/.claude/skills/duli"; T="$HOME/.claude/skills/duli"; mkdir -p "$T/templates"; for f in SKILL.md VERSION "templates/협업규칙.md" "templates/AGENTS-블록.md"; do curl -fsSL "$R/$f" -o "$T/$f"; done; ls "$T/SKILL.md"
```

코덱스에 넣으려면 `.claude/skills` 자리를 `.codex/skills`로 바꾸면 돼요.

## AI 도구가 설치할 때 읽는 부분 (사람은 건너뛰어도 돼요)

메뉴를 묻지 않는 명령이다. 지금 실행 중인 도구에 맞는 폴더(클로드 코드 `~/.claude/skills/duli`, 코덱스 `~/.codex/skills/duli`, 제미나이 `~/.gemini/skills/duli`)에 전역으로 설치한다. 어느 도구인지 모르면 사용자에게 한 번 묻는다. 받을 파일은 넷뿐이다: `SKILL.md`, `VERSION`, `templates/협업규칙.md`, `templates/AGENTS-블록.md`. 다른 것은 설치하지 않는다. 설치 뒤 `SKILL.md`가 있는지 확인한다.

설치가 끝나면 다시 시작하라고 하지 않는다. 설치한 `SKILL.md`를 읽고 그 내용대로 **이 창에서 바로 "처음 1회 설정"을 시작한다**(프로필이 없을 때). 사용자가 이미 할 일을 말했으면 설정이 끝나자마자 그 문으로 들어간다. 슬래시 명령 `/duli`는 다음에 도구를 새로 켰을 때부터 쓸 수 있다고 마지막에 한 줄만 알려 준다.

```powershell
# Windows
$R="https://raw.githubusercontent.com/wootwj-dotcom/duli/main/.claude/skills/duli"; $T="$env:USERPROFILE\.claude\skills\duli"; New-Item -ItemType Directory -Force "$T\templates" | Out-Null; foreach ($f in "SKILL.md","VERSION","templates/협업규칙.md","templates/AGENTS-블록.md") { Invoke-WebRequest -UseBasicParsing -Uri "$R/$f" -OutFile (Join-Path $T ($f -replace "/","\")) }; Test-Path "$T\SKILL.md"
```

```bash
# Mac / Linux
R="https://raw.githubusercontent.com/wootwj-dotcom/duli/main/.claude/skills/duli"; T="$HOME/.claude/skills/duli"; mkdir -p "$T/templates"; for f in SKILL.md VERSION "templates/협업규칙.md" "templates/AGENTS-블록.md"; do curl -fsSL "$R/$f" -o "$T/$f"; done; ls "$T/SKILL.md"
```

## 만든 사람과 라이선스

라이프스케줄(지피터스 24기 사업장자동화 스터디장)이 스터디원들과 AI 둘로 피드백 문서를 만들면서 쓰던 절차를 스킬로 옮겼어요. 지피터스 write-post 스킬의 설치 방식과 처음 설정 흐름, jcputney/agent-peer-review의 "먼저 혼자 읽기·지적별 상태", Trail of Bits second-opinion의 "검토 실패는 실패로 보고"를 참고했어요. 자유롭게 쓰고 고쳐도 돼요(MIT). 궁금한 점은 지피터스 게시판에 남겨 주세요.
