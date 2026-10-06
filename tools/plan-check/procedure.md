# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->
1. Read the **Repo facts** and **CONTRIBUTING.md** policies to identify repository guidelines, maintainer preferences, and constraint scope.
2. Read the **Issue** description and thread context to understand the reported bug or feature behavior.
3. Read the **Repro evidence** section to establish the empirical baseline facts and exact steps that reproduce the problem.
4. Read the **Candidate plan** (including `Cause`, `Change`, and `Test`) and the **Candidate plan comment** to evaluate the proposed solution against the evidence.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->
1. Locate the proposed root cause in `Candidate plan -> Cause` and compare it against the step-by-step observations in `Repro evidence`.
2. Extract all file paths, component names, and exclusions listed in `Candidate plan -> Change` and cross-reference them with `Repo facts` and repository structure guidelines.
3. Identify the verification method described in `Candidate plan -> Test` and check whether it includes automated execution steps or purely manual commands.
4. Compare claims made in `Candidate plan comment` against the official issue thread to verify if external comments, maintainer requests, or forum statements are accurately reflected.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
1. **Grade Root Cause Accuracy:**
   * Verify whether `Candidate plan -> Cause` logically and fully accounts for the empirical evidence in `Repro evidence`.
   * Mark **Pass (P)** if the cause directly explains the observed behavior.
   * Mark **Fail (F)** if the cause relies on unverified assumptions or contradicts the reproduction steps.

2. **Grade Scope & Boundary Definition:**
   * Check if `Candidate plan -> Change` explicitly names all modified files and specifies what remains out of scope.
   * Mark **Pass (P)** if exact files/controllers are listed and boundary limits are defined.
   * Mark **Fail (F)** if file targets are omitted, vague, or violate contribution guidelines.

3. **Grade Test Plan & Automation:**
   * Inspect `Candidate plan -> Test` to determine if an automated test execution step (e.g., unit test, integration test, or scripted assertion) is included.
   * Mark **Pass (P)** if automated test additions or assertions are specified alongside manual verification.
   * Mark **Fail (F)** if the test procedure relies exclusively on manual interactive steps without code-based assertions.

4. **Grade Evidence Alignment:**
   * Evaluate whether the proposed fix resolves the core failure without relying on unverified third-party assumptions.
   * Mark **Pass (P)** if all claims in the plan align directly with verified reproduction evidence.
   * Mark **Fail (F)** if the plan accepts unverified external claims or introduces disproven side effects.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
1. Review the individual grades assigned to all required checks (`Root Cause Accuracy`, `Scope & Boundary Definition`, `Test Plan & Automation`, and `Evidence Alignment`).
2. If any check contains missing or ambiguous details, assign **Insufficient Evidence (?)** to that specific check.
3. Apply the final verdict rule:
   * **Ready (`accept`):** Set the final verdict to `accept` if and only if **ALL** required checks evaluate to **Pass (P)**.
   * **Hold (`reject`):** Set the final verdict to `reject` if **ANY** required check evaluates to **Fail (F)** or **Insufficient Evidence (?)**.
4. Output the check results along with the final JSON block containing the verdict (`accept` or `reject`).
