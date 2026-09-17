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

| Check                    | Evidence                               | Pass condition                                                                                                     | Weight    |
| ------------------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | --------- |
| no_active_claimants      | `issue body` or `comment thread`       | The issue has no assignee AND no linked or referenced Pull Requests submitted within the last 30 days.             | required  |
| active_maintainer        | `comment thread` or `repo-facts block` | A maintainer has commented on the issue or updated the repository within the last 15 days.                         | required  |
| clear_reproducible_scope | `issue body`                           | The issue body includes explicit steps to reproduce the issue or specific file locations/requirements for the fix. | preferred |
| repo_in_use              | `repo-facts block`                     | The default branch has at least 1 commit within the last 30 days.                                                  | preferred |

## Verdict rule

Accept if every required check passes. Preferred checks do not affect the binary verdict; they serve only to rank accepted issues. An outcome of `unclear` for any required check counts as a fail and results in a rejection.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
