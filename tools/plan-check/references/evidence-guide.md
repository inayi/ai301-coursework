# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:** Eval bundle: the plan's `Cause:` line under "Candidate plan", read against the numbered steps and the Expected/Actual lines under "Repro evidence" (and the issue body under "Issue"). Live mode: the draft plan's cause statement, the student's posted repro comment, and the issue thread.

**What good looks like:** The stated cause explains the specific behavior the repro steps show (e.g. the symptom appears at step 3 and disappears after step 4), and does not rest on a mechanism the evidence contradicts, never tested, or borrowed from a forum comment. If the evidence has a control (a case that works), the cause accounts for the difference.

## Scope

**Where it lives:** Eval bundle: the `Change:` paragraph under "Candidate plan", specifically its `In:` and `Out:` statements, checked against the "Repo facts" block. Live mode: the draft plan's in-scope and not-in-scope lines.

**What good looks like:** The plan names the concrete files or functions it will touch and says what it will leave alone, so the change is one bounded fix. A drive-by rewrite, "fix the module", or an unnamed target area fails.

## Executability

**Where it lives:** Eval bundle: the `Change:` paragraph of the candidate plan (files, approach, order of work), plus the repo facts for whether those paths exist. Live mode: the draft plan and the repo's file layout and docs.

**What good looks like:** A stranger could open the named file, make the described change, and know when they are done, without asking the author anything. The plan states what to change and where, not just the goal.

## Test plan

**Where it lives:** Eval bundle: the `Test:` paragraph under "Candidate plan", read against the steps and artifacts under "Repro evidence". Live mode: the draft plan's test section and the repo's existing test setup.

**What good looks like:** It names an automated check (a unit/integration test, CI assertion, or scripted suite) that runs in code, and ties it to the repro: the observation that failed at a specific repro step must pass after the change. Manual-only steps or "verify it works" fail.

## Honesty

**Where it lives:** Eval bundle: the candidate plan and plan comment for stated risks, unknowns, and deviations, compared with what the "Repro evidence" actually establishes. Live mode: the draft plan and comment, and any later note in the thread or PR recording a mid-build change.

**What good looks like:** Unknowns are stated as unknowns ("not yet confirmed whether...") and claims match what was actually verified. Confident wording about untested behavior is false confidence. A deviation found mid-build is recorded openly in the plan or comment, not silently absorbed.

## Comms

**Where it lives:** Eval bundle: the "Candidate plan comment", read against "Thread highlights" and the "Repo facts" block (bug-report template, contribution policy, AI-disclosure requirements). Live mode: the draft comment against the live issue thread, CONTRIBUTING.md, and issue/PR templates.

**What good looks like:** The comment responds to what the thread and maintainers actually said and follows the repo's stated asks (template fields, claim etiquette, disclosure, review-bandwidth notes). Boilerplate that would fit any issue, or that ignores a stated policy, does not.
