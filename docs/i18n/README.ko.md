# mind-meld

에이전트가 코드를 쓰면서 끌어다 쓴 낯선 개념, 지식, 설계 결정을 — 그것을 신뢰하기 전에 — 이해하기 위한
도구 모음입니다. 가장 자주 쓰이는 자리는 에이전트가 방금 올린 풀 리퀘스트이지만, 대상은 임의의 모듈,
알고리즘, 라이브러리, 아키텍처 결정, 개념 그 자체일 수도 있습니다.

에이전트는 사람이 읽는 속도보다 빠르게 코드를 냅니다. 리뷰의 병목은 승인 버튼을 누르는 일이 아니라,
무엇을 승인하는지 이해하는 일입니다. mind-meld 라는 이름은 [벌컨의 정신
융합](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld)에서 왔습니다 — 에이전트의 머릿속으로
들어가는 길입니다.

## 세션이 흐르는 방식

```
/mind-meld 42
```

1. **microworld** — 변경을 요약한 글이 아니라, 메커니즘 자체를 구현한 인터랙티브 HTML 세계. 사람이
   탐색하고, 세션은 기다립니다.
2. **quiz** — 답이 확정된 소수의 질문으로 놓친 지점을 특정합니다. 합격/불합격을 매기지 않습니다.
3. **깊은 도구 하나** — 놓친 축에 따라 `feynman`, `five-whys`, `socratic`, `first-principles` 중 선택.
4. **short-essay** — 기억에 의지해 동료에게 설명하기. 세 축으로 채점합니다: **무엇이** 바뀌었나,
   **왜** 이 방식인가, **무엇이 깨질 수** 있나.
5. **모든 축 8/10 이상이면 통과**, 아니면 보강. 보강 2회 실패 시 다른 깊은 도구로 교체하고, 4회 실패하면
   세션을 끝내고 그 사실을 보고합니다 — 사람이 느린 것이 아니라 변경이 불명확하다는 증거입니다.

결과물은 `.mind-meld/<대상>-report.md` 입니다: 점수, 끝까지 불명확했던 지점, 그리고 에이전트에게 되물을
질문 목록. 자동으로 게시하지 않습니다. 승인은 사람이 하고, mind-meld 는 하지 않습니다.

각 도구는 단독으로도 호출할 수 있습니다.

```
/microworld src/scheduler.ts
/five-whys 42
/first-principles "vector clocks"
```

## 설치

쓰는 에이전트의 블록만 복사하면 됩니다.

**Claude Code**

```
/plugin marketplace add songsnim/mind-meld
/plugin install mind-meld@mind-meld
```

**Codex CLI**

```sh
git clone https://github.com/songsnim/mind-meld ~/.mind-meld
mkdir -p ~/.codex/skills
ln -sfn ~/.mind-meld/skills/* ~/.codex/skills/
```

**opencode**

```sh
git clone https://github.com/songsnim/mind-meld ~/.mind-meld
mkdir -p ~/.config/opencode/skills
ln -sfn ~/.mind-meld/skills/* ~/.config/opencode/skills/
```

**Cursor**

```sh
git clone https://github.com/songsnim/mind-meld ~/.mind-meld
mkdir -p ~/.cursor/skills
ln -sfn ~/.mind-meld/skills/* ~/.cursor/skills/
```

**Hermes**

```sh
git clone https://github.com/songsnim/mind-meld ~/.mind-meld
mkdir -p ~/.hermes/skills
ln -sfn ~/.mind-meld/skills/* ~/.hermes/skills/
```

갱신은 `git -C ~/.mind-meld pull` — symlink 가 따라옵니다. Claude Code 는 marketplace 로 갱신합니다.

## 구성

| 스킬 | 역할 |
| --- | --- |
| `mind-meld` | 오케스트레이터. 나머지를 라우팅합니다. |
| `microworld` | 메커니즘을 구현한 인터랙티브 HTML 세계. |
| `quiz` | 답이 확정된 소수의 질문으로 빈틈을 특정. |
| `socratic` | 한 번에 한 질문씩, 무엇이 깨지는지 스스로 보게 됩니다. |
| `feynman` | 쉬운 말로 설명하게 하고, 흐릿한 지점을 표시합니다. |
| `five-whys` | 결정을 강제한 제약까지 내려갑니다. |
| `first-principles` | 낯선 개념을 primitive 부터 다시 세웁니다. |
| `short-essay` | 측정 도구. 채점하고, 기준을 넘을 때까지 보강합니다. |

자동 발동은 `mind-meld` 만 합니다. 나머지 일곱은 명시적 호출 전용이라, 설명을 요청했는데 갑자기 소크라테스
문답이 시작되는 일은 없습니다.

## 참고

- 상태를 저장하지 않습니다. 세션 간 점수 기억 없음.
- 출력은 `.mind-meld/` 로 가고, `.git/info/exclude` 에 등록됩니다 — 리뷰 중인 diff 를 오염시키지 않습니다.
- 세션은 사용자의 언어로 진행됩니다. 제2언어로 쓴 에세이를 채점하면 이해도가 아니라 작문을 재게 됩니다.
- 스크립트·의존성·빌드 없음. `SKILL.md` 여덟 개뿐입니다.

MIT.
