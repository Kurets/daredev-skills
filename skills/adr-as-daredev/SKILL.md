---
name: adr-as-daredev
description: "Apply Daredev's conservative approach to architecture decision records (ADRs). Use only when the user explicitly asks to review scoped goals or specs for ADRs or to draft an ADR. Never run automatically after a goal or before a commit."
---

# ADR as Daredev

Triage decisions, not goals. Prefer no ADR. A record earns its place when a future maintainer can see what the code does
but could still undo an important choice without understanding what it protects.

## Start with explicit scope

- Run only on a user invocation such as `/skill:adr-as-daredev` or an explicit request to check a spec for ADRs. Goal
  completion, uncommitted changes, and commit requests are not triggers.
- Require a named goal, spec, or bounded set of files with decision context. A directory of goal packages is a valid
  batch. If no source is named, the entire repo is offered, or the files show behavior without decision context, ask for
  a narrower or better source. This is insufficient evidence, not a finding that no ADR is needed.
- Read the scoped sources and follow directly linked specs, PRs, and tickets that bear on the decision. Report a source
  you couldn't access if it matters. Don't search unrelated history or broaden the candidate search. Use targeted checks
  of relevant implementation, tests, and repo docs to verify a candidate and find its documentation home.

## Decide what is worth recording

1. Identify the choice, its rationale, and the constraint or trade-off a future maintainer needs to know. Combine
   related rollout and cleanup goals that describe the same decision. Don't treat proposals, old plans, or draft review
   comments as proof of what was decided.
2. Verify the decision against the implementation. A verified change on the current branch can qualify even if
   uncommitted or unmerged; state that status. If it is accepted but not implemented, flag it as a candidate to revisit,
   not an ADR to write now. If the implementation diverges from the plan, record the implemented choice only if its
   rationale is supported; otherwise ask.
3. Skip behavior that code and tests already explain adequately. Look for an enduring consequence that isn't obvious
   there, not for a large diff or a particular kind of change. Ask a focused question if missing rationale could change
   the recommendation. Never invent motives, rejected alternatives, or trade-offs.
4. Check existing ADRs and relevant architecture, interface, or operational docs. If a doc already explains the choice
   and its trade-off, leave it there. If a relevant doc is the right home but has a gap, flag that specific update
   instead of creating a parallel record.

## Report the result

State which sources were reviewed. For each distinct candidate, give one outcome, a short reason, and the decisive
source or implementation reference:

- **Recommend an ADR** — state the proposed title and the non-obvious choice worth preserving.
- **Flag a doc update** — give the existing file path and exactly what rationale, constraint, or correction it needs.
- **Already recorded** — point to the existing coverage; leave it alone.
- **Skip** — say why nothing needs recording. If nothing qualifies, say so plainly.
- **Ask** — identify the missing decision context, implementation evidence, or rationale and say what would resolve it.

For example, using a transactional outbox to prevent lost events without a distributed transaction may deserve an ADR.
Explaining a retention window in the existing storage docs is a doc update. A sorting fix whose behavior and constraints
are clear in tests is usually a skip.

## Draft only when requested

Follow the target repo's ADR location, naming, and format, including any conventions for status and supersession. If the
repo has no ADR location convention, ask where ADRs belong before drafting. Don't choose or create a directory yourself.

If the repo has no format, use this short Markdown structure:

```markdown
# <Title that states the decision>

- **Decided:** YYYY-MM-DD
- **References:** [Jira ticket](…), [Implementation PR](…)

## Context
What problem or constraint made the choice necessary?

## Decision and rationale
What did we choose, and why? Include alternatives only when there is evidence they were considered.

## Consequences
What does the choice enable, what trade-off did we accept, and what should maintainers avoid breaking?
```

Use the decision date if known. If only the writing date is known, label it **Recorded** instead. Omit a time of day
and any unavailable reference links. Keep the ADR understandable without access to the linked PR, issue, or temporary
goal artifacts.

Triage is read-only. Don't create or update files without a request to do so. Never stage, commit, or push as part of
this skill; a separate explicit request can use the repo's normal workflow.
