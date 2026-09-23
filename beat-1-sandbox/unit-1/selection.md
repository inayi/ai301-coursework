# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72

**Verdict output**

Checks passed: no_active_claimants, active_maintainer, clear_reproducible_scope, repo_in_use
Verdict: accept

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
  "checks": [
    {"name": "no_active_claimants", "grade": "pass", "evidence": "assignees: [] and no linked/referenced PR; the only comment is a classmate's 'I'd like to claim this one' (student claim comments don't block per Path Review house rule)"},
    {"name": "active_maintainer", "grade": "pass", "evidence": "no maintainer comment on the thread (commenter authorAssociation: NONE), but default branch has a commit at 2026-09-16T21:42:18Z, 6 days before today (2026-09-22), within the 15-day window"},
    {"name": "clear_reproducible_scope", "grade": "pass", "evidence": "issue body names exact files (`core/security.py`, `tests/unit/test_security.py`), the failing test id, and an estimated effort of 1-2 hours"},
    {"name": "repo_in_use", "grade": "pass", "evidence": "most recent default-branch commit is 2026-09-16, well within 30 days of today (2026-09-22)"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

The committed full run recorded: "agreement: 18/20 scored items  (bar:
18/20: PASS)". Its category line was "categories: claimed 4/4
clear-accept 6/8 dead-repo 3/3 policy 1/1 scope 4/4". The partial
`--only` runs used while revising checks were diagnostic runs, not the
committed full-run record.

**Issue analysis**

I used `issue-15`. My rubric's decision is `reject`, which matches the
gold label `reject`. The snapshot says, "this issue: assignees: none;
linked PRs: zulip/zulip#20840 (closed); zulip/zulip#23123 (closed)."
Although the issue has a friendly label and an active repository, the two
closed linked PRs are evidence that this is not a fresh, settled first
contribution. This matches the gold-label explanation: "years of design
debate and two abandoned PRs behind a friendly label."

**Check rationale**

`settled_spec`: "Pass if the issue states an observable bug and the
expected invariant or desired behavior. Words such as “potential causes”,
“suggestions”, or multiple compatible fixes for the same reported bug do
not make the specification unresolved. Fail only when the evidence
explicitly asks maintainers to choose between competing product/design
directions, leaves the desired behavior undecided, OR shows two or more
closed/abandoned linked PRs without a recent maintainer restatement of the
intended solution."

I wrote it this way to distinguish an actionable bug with several possible
technical fixes from a task whose product or design direction is genuinely
unsettled. It also catches old issues where repeated unsuccessful attempts
are a warning that the apparent small task has hidden complexity.

**Trade-offs**

The check deliberately does not reject a performance bug merely because it
lists several hypotheses or fixes. The `issue-19` snapshot says, "There
are two potential causes which should be fixed," followed by several
suggestions, but its gold-label note calls it a "maintainer-diagnosed
performance bug with named causes, unclaimed." The trade-off is that a
task with a vaguely described bug but no visible disagreement can still
pass; the check only rejects uncertainty that is explicit in the
available evidence.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. I selected this issue because it is a bounded Python security fix with
an identified implementation area, `core/security.py`, and a corresponding
test file, `tests/unit/test_security.py`. That gives me a focused task that
fits the available unit time while letting me practice security-oriented
debugging and tests.

2. The verdict correctly identified that the issue is unassigned, the
repository is active, and the change has a concrete scope. I also weighed
the fact that the requested change removes an existing xfail marker, which
means I need to understand the current test failure rather than only make
the test pass. That implementation-learning value is specific to this
issue and is not captured by the binary rubric verdict.

3. Claiming it should be straightforward under the classroom house rule:
other student claim comments do not block the issue. The main difficulty
will be reproducing the security behavior and making a minimal fix that
does not weaken the intended protection or introduce a regression.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
