# Case Files

```console
rogue-prompt:~$ cd 02-case-files
```

**The method in `01`, run against public cases.**

One file per case. Same structure every time, so the set can be read as a body of work rather than as separate articles. Each file ends by stating what it moves, including when the answer is nothing.

---

## The files

| ID | Case | PIR | Verdict | Status |
|---|---|---|---|---|
| [`CF-01`](cf-01-exploitgym.md) | OpenAI ExploitGym sandbox escape, July 2026 | PIR-2, PIR-5 | drafting | drafting |
| [`CF-02`](cf-02-gtg-1002.md) | GTG-1002 AI-orchestrated espionage, 2025 | PIR-1, PIR-2 | drafting | drafting |
| [`CF-03`](cf-03-promptsteal.md) | PROMPTSTEAL, APT28 runtime LLM use | PIR-1 | drafting | drafting |

---

## Structure

Every file carries the same sections. The consistency is the point: it is what allows the set to be compared, and what makes an outlier visible.

```
## Source            Primary publication, date, publisher, visibility scope
## Actor             Designation, provider's confidence wording, attribution state
## Extraction        The field table, filled
## Verdict           Force multiplier or new capability, with the counterfactual stated
## Hunt hypothesis   Claim, telemetry, falsification, baseline. Or an honest null.
## What this moves   Effect on standing claims, including none
```

---

## On null results

Not every case produces something a defender can hunt for. Much of what providers observe happens on platforms the enterprise does not own and generates no local telemetry.

A case file that terminates at the actor profile and says so is a legitimate output. Manufacturing a hunt hypothesis to fill the section is how this kind of work becomes noise.

---

## Standing claims under test

**`[OPEN]`** Most attributed misuse is force multiplier rather than new capability. Stated in the root README. Each case file either confirms, weakens, or leaves it untouched.

**`[OPEN]`** AI tooling choices may be durable enough to be attributive. Habits of use could prove stickier than infrastructure, because they reflect how a team works. Under test as capability facets accumulate.

**`[OPEN]`** The attribution tells that carry the most weight in human intrusion analysis are measuring scarcity, and they degrade in proportion to how unscarce the actor is. Argued in the Substack piece, tested here.

> _All opinions are my own and do not reflect my employer._
