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
  "item": "[https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72)",
  "checks": [
    {"name": "no_active_claimants", "grade": "pass", "evidence": "assignees: []; repo has zero pull requests and the issue timeline shows no cross-referenced or connected PR"},
    {"name": "active_maintainer", "grade": "pass", "evidence": "main pushed 2026-09-16T21:50:20Z by Andrew Burke, 0 days before grading"},
    {"name": "clear_reproducible_scope", "grade": "pass", "evidence": "names core/security.py and tests/unit/test_security.py, plus the xfail marker (manifest H-05) to remove"},
    {"name": "repo_in_use", "grade": "pass", "evidence": "latest default-branch commit 2026-09-16T21:42:18Z, within 30 days"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
