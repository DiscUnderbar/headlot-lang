# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

[이 저장소에 CLAUDE.md 에서 가져옴](https://github.com/multica-ai/andrej-karpathy-skills)

- 모든 기록은 까먹을 수 있다. 그러므로 세세한 것까지 Headlot 스펙 문서에 저장한다. 하나가 빠지는 순간 완성도가 낮아지고 지적할 부분이 많아진다. 그러니까 이미 해결한 의문 "왜 이걸 이렇게 했나" 이런걸 직접 다 적어놓으라는 거다. 안그러면 이미 해결한 문제를 또 문제로 지적하게 되는 문제가 생긴다. 그러니까 이게 문제점이 이미 해결된건데 또 이걸 왜 이렇게 했냐고 질문할수도 있으니까 왜를 적어야 한다.
- 만약 이거에 문제점을 발견했을때 그냥 우회하지 말고 해결법을 정면으로 돌파하고 찾아라. 그리고 예시로 이게 의도 쉬운 게임과 맞지 않게 필요없이 어려운 기능을 찾았는데 이걸 해결하기가 어렵거나 해결하면 어떤 곳엔 더 어려워 져도 우선 그냥 막 "이건 그냥 튜툐리얼로 어렵지 않게 한다." 이런 그냥 진짜 말도 않되는 그런 그냥 막 우회하는 해결책을 생각하지 말고 우선 최대한 이거에 목적에 맞는 해결책을 찾고 그걸 써라. (참고로 전에 튜툐리얼 넣는게 왜 우회냐면 그냥 사실 이 게임에 문제를 해결하는게 아니라 유튜브에 강의 영상으로 해결한다는 식이다. 그냥 사실 어려운게 이걸 이해하는데 어려워서 이게 문제인거지 이걸 이해하는법이 그러니까 어떻게 이 기능을 이해하는 법이 없어서 그런게 아니니까)
- 딴 일 하다 떠오른 것은 `IDEAS.md`, 모르는 것은 `UNKNOWN.md`, 미룬 것은 `TODO.md`, 꽤 큰거고 진짜 이 언어의 전환점이 있는 날은 `special-occasions-history.md` (날짜 / 전 → 후 / 왜 / 무엇을 버렸나) 에 적는다.
- 내가 새로 안것 정보는 다시 재검토를 해야 한다. 언제나 확정은 없다. 이게 확정 되었다는건 없다. 절대 확정은 있을수가 없다. 말도 않된다 이걸 확정 하면 진짜 문제점이 없다고 확정하고 아무도 의심을 안하는 순간 그건 이 설계에 가장 큰 위협이 된다. 어쨋든 확실히 이게 최고에 방법일꺼라는건 없고 언제나 재검토를 해봐야 한다. 이게 이거에 좋은점이든 나쁜점이든.
- 좋은점이 있으면 적고 나쁜 점이 있을때도 적고 그냥 우선 발견한건 다 적어라. 이 기능을 만들때 그냥 다른 기능과 연계가 될때 그 다른 기능이 만약 더 게임을 일 대신 노는것처럼 생각하게 한다는 장점이나 뭐 이걸 더 사람들이 노가다 처럼 오랫동안 이걸 안하게 된다는 트레이드 오브가 있을때 이걸 알고 있으면 그 새 기능도 그 장점이 있으니까 그 장점을 더 극대화 되게 설계할수도 있고 그 단점을 보완하게 설계할수도 있고 정보가 많으면 설계할때 더 많은걸 생각할수 있게 한다.
- 모든곳에서 좋은거, 모든곳에서 나쁜건 없다. 이건 여기에 목적에 따라서 좋은 기능이 될수도 있고 나쁜 기능이 될수도 있다.
- 뭐 적을때 "트레이드오브 (정직하게)" 이렇게 하지 말라. 그냥 정직한다고 말한다고 사람들이 이걸 의심하지 않는게 아니다. 그리고 오히려 의심하지 않게 만들면 않된다. 아무도 의심하지 않는건 설계에 가장큰 위협이다.
