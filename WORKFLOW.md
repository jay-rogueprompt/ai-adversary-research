# Publishing Workflow

**`[DESIGN]`** How the repo and Substack relate, and what goes where.

```console
rogue-prompt:~$ cat workflow
```

---

## The split

They are not the same content in two voices. They do different jobs.

| | Repo | Substack |
|---|---|---|
| **Job** | Reference | Argument |
| **Lifespan** | Standing, updated in place | Dated, never revised after publication |
| **Voice** | Structured, labeled, tabular | Narrative, one idea, accessible |
| **Reader** | Someone checking your method | Someone deciding if you are worth following |
| **Unit** | The file | The post |
| **Changes when** | A claim moves | Never |

The repo says what is true as of now. Substack says what you argued on a date. Keeping those separate is what lets you update a claim without rewriting history, and what lets a post stand as a record of when you called something.

---

## Direction depends on the piece

**Method and framework: repo first.**

Publish the file, then write the Substack post arguing for it. The post links to the canonical version. This is right because method needs to be stable before you argue from it, and because the argument reads better when the reader can go check the thing.

Example: `collection-plan.md` ships, then a post on why most AI security research has no adversary in it.

**Breaking cases: Substack first.**

A disclosure lands. Post within days, because speed of translation is the capability being demonstrated. The structured case file follows into `02-case-files/` as the canonical record within a week.

This order matters. A fast, dated post proves you can read a report and say something useful about it while it is still live. A case file published three weeks later proves something else, and both are worth proving, but only the first one has a clock on it.

**Quarterly synthesis: repo first, then a bigger post.**

The quarterly review updates the standing claims in the repo. The post explains what moved and why, which is the most valuable thing you will publish, because almost nobody publicly revises their own positions.

---

## The conversion

Turning a repo file into a post is subtraction, not translation.

**Cut:** tables, label markers, framework citation lines, the sourcing block, status columns, the discipline section.

**Keep:** the claim, the reasoning, the honest limits.

**Add:** a reason to care stated in the first two paragraphs, one narrative thread, and a specific case rather than a general method.

**Always:** one link back to the canonical repo file, at the end, in a single line. Not five links. One.

The failure mode is publishing the repo file with the tables removed. It reads as documentation and nobody finishes it. A post needs an argument someone could disagree with, stated early enough that they know what they are disagreeing with.

---

## Cadence

| Interval | Repo | Substack |
|---|---|---|
| **Per event** | Case file within a week | Post within days |
| **Monthly** | One worked case file | One post from it |
| **Quarterly** | Standing claims updated | Synthesis post |

Two posts a month is a real cadence and it is sustainable. Four is not, and a stalled cadence reads worse than a slower one.

---

## What never crosses over

Collection tradecraft. Persona work, access development, vetting, how presence is sustained. Not in the repo, not on Substack, not in a talk.

Analytic method is published. Collection method is not. These are different categories and the distinction is the one that keeps the rest publishable.

Anything from an employer environment. Both surfaces state this explicitly and both statements stay.

---

## Reuse into other formats

The case file structure is deliberately conference-shaped. Source, actor, extraction, verdict, hunt hypothesis, what it moves is a talk outline.

A quarterly synthesis is a CFP submission. Three case files on one theme is a talk. The body of work is the abstract pipeline, and that is the second reason the structure stays consistent across files.
