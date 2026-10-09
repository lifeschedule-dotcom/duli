# duli (둘이검토)

AI 하나가 쓴 것은 그 AI가 못 봐요. 둘이검토는 **내 AI에게 "검토해"라고만 하면**, 내 AI가 다른 AI(또는 다른 모델)를 검토 AI로 불러 먼저 혼자 읽게 하고, 양쪽에서 "더 고칠 거 없음"이 나올 때까지 파일로 주고받은 뒤 결과를 세 줄로 알려 주는 스킬이에요. 설계를 다질 때, 올리기 전에, 일을 나눌 때 씁니다.

```
나 ──"검토해"──▶ 내 AI ──파일──▶ 공유 폴더 ◀──파일── 검토 AI
                   ▲                                   │
                   └────── "틀린 것 3개, 반영 2개" ◀──────┘
```

## 이렇게 써요

1. 작업하던 AI 창에 이 한 줄을 붙여 넣어요. 깃허브에서 직접 받을 건 없어요.

```
https://github.com/lifeschedule-dotcom/duli 이 스킬 설치해 줘
```

2. 처음 한 번만 두 가지를 물어요. **어떤 AI 앱을 쓰는지**, **AI끼리 파일을 주고받을 폴더가 있는지**. 답하면 폴더와 규칙 파일, AI가 매번 읽을 안내(AGENTS.md)를 만들어 줘요.

3. 그다음부터는 **"검토해"**라고만 하면 돼요. 설계안이든 글이든 코드든, 내 AI가 알아서 검토 AI를 부르고 결과를 세 줄로 알려 줘요. 일을 나눠서 하고 싶으면 "같이 해".

다음부터는 `/duli`라고 쳐도 돼요.

## AI가 하나뿐이어도 돼요

검토 AI 자리에 **같은 도구의 다른 모델**을 새로 띄워요. 기준은 "지금 쓰는 모델의 한 단계 위, 맨 위면 한 단계 아래". 새로 띄운 모델은 대화를 모르고 파일만 읽어서 독립 검토가 돼요. "이번엔 Opus로 검토해"라고 하면 그 모델로 해요. 챗GPT 웹만 쓰면 파일을 첨부하고 답을 저장하는 건 사용자가 해 줘요.

## 무엇이 나와요

- 공유 폴더 안에 번호가 붙은 파일들. 설계안, 검토 요청, 검토 답, 완료. 누가 뭘 잡았고 뭘 반영했는지 다 남아요.
- 끝나면 세 줄: 검토 AI가 누구였나, 지적 몇 개 중 몇 개 반영했나, 결과물이 어디 있나. 게시·발송은 늘 사용자가 직접 해요.

## 처음 한 번 만들어 주는 것

- `live_collaboration` 폴더와 `백업` 폴더 (공유 폴더가 있으면 그 안에, 없으면 작업 폴더 안에)
- `협업규칙.md` (이미 쓰는 규칙 파일이 AGENTS.md에 적혀 있으면 만들지 않고 그걸 써요)
- `AGENTS.md` 끝에 여섯 줄. **이미 있는 AGENTS.md는 덮어쓰지 않고** 표시된 블록만 붙여요. 붙이기 전에 `.bak`을 남겨요. `CLAUDE.md`가 없으면 `@AGENTS.md` 한 줄짜리로 만들어요.
- 설정은 `~/.duli/profile.json`. "검토 설정 다시"라고 하면 다시 물어요.

## 자주 묻는 것

**검토 AI가 파일을 못 찾아요.** 파일 이름에 화살표(→)가 있어서 검색으로는 안 잡혀요. 전체 경로를 그대로 붙여 주세요. 다른 컴퓨터면 원드라이브 동기화가 끝났는지 폰이나 웹에서 먼저 확인하세요.

**30분 넘게 답이 없어요.** 동기화 지연이거나 검토 AI 창이 폴더 확인을 멈춘 거예요. 그 창에 "폴더 확인해 줘"라고 한 번 치면 돼요.

**둘이 의견이 안 맞아요.** 사용자에게 안 물어요. 토론 파일에서 근거로 끝내고, 2왕복 안에 안 갈리면 둘 다 조건을 붙여 적어요.

**지우거나 되돌리려면요?** 설치한 스킬 폴더(`~/.claude/skills/duli` 등)를 지우면 돼요. AGENTS.md는 `<!-- duli 시작 -->`부터 `<!-- duli 끝 -->`까지 지우면 원래대로예요.

## 터미널로 설치하고 싶다면

Windows (PowerShell)

```powershell
$R="https://raw.githubusercontent.com/lifeschedule-dotcom/duli/main/.claude/skills/duli"; $T="$env:USERPROFILE\.claude\skills\duli"; New-Item -ItemType Directory -Force "$T\templates" | Out-Null; foreach ($f in "SKILL.md","VERSION","templates/협업규칙.md","templates/AGENTS-블록.md") { Invoke-WebRequest -UseBasicParsing -Uri "$R/$f" -OutFile (Join-Path $T ($f -replace "/","\")) }; Test-Path "$T\SKILL.md"
```

Mac / Linux

```bash
R="https://raw.githubusercontent.com/lifeschedule-dotcom/duli/main/.claude/skills/duli"; T="$HOME/.claude/skills/duli"; mkdir -p "$T/templates"; for f in SKILL.md VERSION "templates/협업규칙.md" "templates/AGENTS-블록.md"; do curl -fsSL "$R/$f" -o "$T/$f"; done; ls "$T/SKILL.md"
```

코덱스에 넣으려면 `.claude/skills` 자리를 `.codex/skills`로 바꾸면 돼요.

## AI 도구가 설치할 때 읽는 부분 (사람은 건너뛰어도 돼요)

메뉴를 묻지 않는 명령이다. 지금 실행 중인 도구에 맞는 폴더(클로드 코드 `~/.claude/skills/duli`, 코덱스 `~/.codex/skills/duli`, 제미나이 `~/.gemini/skills/duli`)에 전역으로 설치한다. 어느 도구인지 모르면 사용자에게 한 번 묻는다. 받을 파일은 넷뿐이다: `SKILL.md`, `VERSION`, `templates/협업규칙.md`, `templates/AGENTS-블록.md`. 다른 것은 설치하지 않는다. 설치 뒤 `SKILL.md`가 있는지 확인한다.

설치가 끝나면 다시 시작하라고 하지 않는다. 설치한 `SKILL.md`를 읽고 그 내용대로 **이 창에서 바로 "처음 1회 설정"(질문 둘)을 시작한다**(프로필이 없을 때). 사용자가 이미 할 일을 말했으면 설정이 끝나자마자 그 일을 한다. 슬래시 명령 `/duli`는 다음에 도구를 새로 켰을 때부터 쓸 수 있다고 마지막에 한 줄만 알려 준다.

```powershell
# Windows
$R="https://raw.githubusercontent.com/lifeschedule-dotcom/duli/main/.claude/skills/duli"; $T="$env:USERPROFILE\.claude\skills\duli"; New-Item -ItemType Directory -Force "$T\templates" | Out-Null; foreach ($f in "SKILL.md","VERSION","templates/협업규칙.md","templates/AGENTS-블록.md") { Invoke-WebRequest -UseBasicParsing -Uri "$R/$f" -OutFile (Join-Path $T ($f -replace "/","\")) }; Test-Path "$T\SKILL.md"
```

```bash
# Mac / Linux
R="https://raw.githubusercontent.com/lifeschedule-dotcom/duli/main/.claude/skills/duli"; T="$HOME/.claude/skills/duli"; mkdir -p "$T/templates"; for f in SKILL.md VERSION "templates/협업규칙.md" "templates/AGENTS-블록.md"; do curl -fsSL "$R/$f" -o "$T/$f"; done; ls "$T/SKILL.md"
```

## 만든 사람과 라이선스

라이프스케줄(지피터스 24기 사업장자동화 스터디장)이 스터디원 피드백 문서를 AI 둘로 만들면서 쓰던 절차를 스킬로 옮겼어요. 지피터스 write-post 스킬의 설치 방식, jcputney/agent-peer-review의 "먼저 혼자 읽기", Trail of Bits second-opinion의 "검토 실패는 실패로 보고"를 참고했어요. 자유롭게 쓰고 고쳐도 돼요(MIT).
