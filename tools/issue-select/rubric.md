# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| no_active_claimants | `issue body` or `comment thread` | The issue has no assignee AND no active Pull Requests submitted within the last 30 days. | required |
| active_maintainer | `comment thread` or `repo-facts block` | A maintainer has commented on the issue OR the default branch has commits within the last 90 days. | required |
| actionable_scope | issue body or comment thread | The issue provides either concrete reproduction/expected behavior, an explicit feature behavior and acceptance boundary, or a maintainer diagnosis with a bounded implementation target. | required |
| bounded_change | issue body or comment thread | Pass if the issue has one named user-visible bug, behavior, or documentation outcome, with a finite set of related changes. For a performance bug, multiple suspected causes or compatible optimization steps still count as bounded when they all address that one named symptom. Fail only for a tracking list, whole-codebase migration, an unbounded set of components, or text that explicitly requires a product/design decision before implementation. | required |
| contribution_policy | repo-facts block | Pass if the repository explicitly permits AI-assisted contributions OR has no statement prohibiting AI-assisted or AI-generated contributions. Fail only when the policy explicitly bans or disallows AI-generated code or documentation. | required |
| repo_in_use | `repo-facts block` | The default branch has at least 1 commit within the last 90 days. | required |
| good_first_issue_label | `issue body` or `repo-facts block` | The issue has a 'good first issue' or 'easy' label. | preferred |
| settled_spec | issue body, comment thread, and repo-facts linked-PR state | Pass if the issue states an observable bug and the expected invariant or desired behavior. Words such as “potential causes”, “suggestions”, or multiple compatible fixes for the same reported bug do not make the specification unresolved. Fail only when the evidence explicitly asks maintainers to choose between competing product/design directions, leaves the desired behavior undecided, OR shows two or more closed/abandoned linked PRs without a recent maintainer restatement of the intended solution. | required |

## Verdict rule

Accept if every required check passes. Preferred checks never change the binary verdict; they serve only to rank accepted issues. An outcome of `unclear` for any required check counts as a fail and results in a rejection.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
