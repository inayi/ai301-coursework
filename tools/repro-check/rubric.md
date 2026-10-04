# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check                  | Evidence                                                   | Pass condition | Weight |
|------------------------|------------------------------------------------------------|----------------|--------|
| no_active_claimants | `issue body` or `comment thread` | The issue has no assignee AND no active Pull Requests submitted within the last 30 days. | required |
| active_maintainer | `comment thread` or `repo-facts block` | A user has commented on the issue OR the default branch has commits or merges OR there's a release within the last 90 days. | required |
| contribution_policy | repo-facts block | Pass if the repository explicitly permits AI-assisted contributions OR has no statement prohibiting AI-assisted or AI-generated contributions. Fail only when the policy explicitly bans or disallows AI-generated code or documentation. | required |
| settled_spec | issue body, comment thread, and repo-facts linked-PR state | Pass if the issue names one user-visible bug, behavior, or docs outcome, states the expected behavior, and needs a finite set of related changes. Multiple suspected causes or compatible fixes for that one problem are fine. Fail only if it is a tracking list, a migration, or an unbounded set of components. Also fail it if it explicitly needs a product or design decision first, or if it has two or more closed or abandoned linked PRs and no recent maintainer restatement of the intended solution. | required |
| behavior_matches_issue |	the repro report's output excerpt, log or screenshot, read against the error or behavior the issue describes |	The artifact shows the same error or behavior the issue names, in the same component. An adjacent failure fails. An evidenced cannot-reproduce that says so plainly also passes.	| required |
| good_first_issue_label | `issue body` or `repo-facts block` | The issue has a 'good first issue' or 'easy' label. | preferred |

## Verdict rule

Accept if every required check passes. Preferred checks never change the binary verdict; they serve only to rank accepted issues. An outcome of `unclear` for any required check counts as a fail and results in a rejection. Each failed check must cite the exact missing or conflicting evidence.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
