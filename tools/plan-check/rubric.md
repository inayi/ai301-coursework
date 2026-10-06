# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Root Cause Accuracy | The repro evidence read against the candidate plan's Cause section | Pass (P): the plan's proposed diagnosis directly accounts for the facts and empirical data in the issue description or reproduction benchmarks. Fail (F): the plan attributes the bug to an unverified assumption, a tangential component, or a disproven theory that contradicts the issue's baseline reproduction steps and evidence. | required |
| Scope & Boundary Definition | The repo facts read against the candidate plan's Change section | Pass (P): the plan explicitly identifies all files or components it modifies and explicitly states which components or systems are strictly out of scope. Fail (F): the plan gives vague target areas (e.g. "fix the module"), omits specific file targets, or does not define what will remain untouched. | required |
| Test Plan & Automation | The candidate plan's Test section | Pass (P): the Test Plan names a concrete, repeatable check with an observable pass/fail outcome mapped to the repro steps: an automated test (unit or integration test, CI assertion, fixture/regression test added to the suite) or a scripted re-run of the repro commands with stated expected output, alongside any optional manual verification. Fail (F): the Test Plan is only "verify it works" style manual checking, or names no observable outcome and no way to execute the check. | required |
| Evidence Alignment | The candidate plan read against the repro evidence | Pass (P): the proposed changes logically resolve the issue without introducing side effects disproven by existing controls or control experiments. Items the plan has not yet verified are acceptable when the plan states them as open questions or checks to be done before the PR. Fail (F): the plan accepts third-party forum claims or anecdotal comments as fact without verifying them against the baseline issue evidence, or presents an unverified assumption as settled. | required |
| Comms & Repo Conventions | The candidate plan comment read against the thread highlights and the repo facts block (contribution policy, AI-use disclosure, templates) | Pass (P): the comment follows explicit maintainer direction in the thread and satisfies every requirement the repo facts state, including an AI-use disclosure when the policy explicitly requires disclosing or labeling AI usage (treat every package as AI-assisted work). A policy that only says AI is welcome and the contributor must review and understand the output is not a disclosure requirement. Fail (F): the comment ignores maintainer direction in the thread, or omits a disclosure the policy explicitly requires, or another step the repo's stated policy requires. If the repo states no disclosure requirement, the absence of one is not a fail. | required |

## Verdict rule

- **Ready (accept):** all required checks evaluate to Pass (P).
- **Hold (reject):** any required check evaluates to Fail (F) or Insufficient Evidence (?). `unclear` counts as fail.
