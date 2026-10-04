# Evidence guide: where proof lives in a reproduction package

`rubric.md` names the checks. This file says where each proof lives and
what a pass looks like.

Modes:
- Eval: the bundle text is the whole world. Quote it. Fetch nothing.
  Ignore `scope.md` and `voice-guide.md`.
- Live: gather issue evidence from GitHub (`gh issue view`, `gh pr list`,
  `gh api`). Read the student's drafts as the candidate package.

Missing evidence grades `unclear`. Never fill a gap from memory.

## Sources

| Source | Eval bundle | Live |
|---|---|---|
| Issue body | Issue section: title, body, labels, author | top post of the issue page, sidebar for labels and assignees |
| Comment thread | Thread highlights: author, date, text | issue comments |
| Repo-facts block | Repo facts section: releases, policy text, linked PRs, commit or merge dates if given | repo Commits, Releases and Pulls pages, CONTRIBUTING, AI policy, issue's linked PRs |
| Claim comment | Candidate claim comment section | student's claim draft |
| Repro report | Candidate repro report section | student's repro draft |

Windows: 30 days for PRs, 90 days for activity. Measure back from the
bundle's `captured` date. Live: from today. No date in the bundle: grade
date checks `unclear`.

## Live mode gates

Scope first. Read `scope.md`.
- Repo line still a placeholder (`<ORG>/<PATH-REVIEW-REPO>`): stop. Tell the
  student to get the cohort's scope file from the instructor.
- Issue outside the scoped repo: refuse to grade.

Voice second. Read `voice-guide.md`. Hold each draft against every rule and
every "never post" line. Report broken rules in the summary, quoting the
rule and the line. Voice never changes a grade or the verdict.

Claim-only draft: grade every check except behavior_matches_issue. Grade it
`unclear`, evidence `not yet applicable: claim-only draft`, and leave it
out of the verdict.

Drafts count only for what they contain. Ignore other files in the
student's working directory.

House rules (live only):
- Classmates' claim comments never make an issue claimed.
- Classmates' repro comments never block yours.
- Credit goes to work posted, not to being first.

## Checks

Every fail cites the exact missing or conflicting line.

### no_active_claimants
Where: assignee and referenced PRs. Eval: the issue header and thread
list labels and author only, so no assignee line means no assignee. Live:
sidebar, and `gh pr list --search "<number>" --state all`.
Good: no assignee, and no PR for the issue opened or updated in the last
30 days. Closed PRs and older idle PRs do not count. A comment such as
"pushed a fix" counts as an active PR only if it names or links a PR, or
the repo facts show linked-PR state. Otherwise pass and note the comment.
Live house rule: classmates' claim comments never count. A classmate's
assignee or open PR still does.

### active_maintainer
Where: comment thread, and the repo-facts block for commits, merges and
releases.
Good: any one of these within 90 days: a comment on the issue from someone
other than its author, a default-branch commit or merge, a release. Cite
the date used. Stars, last-updated stamps and issue-opened dates do not
count. No dated activity and no outside comment: fail. Block gives no
dates at all: `unclear`.

### contribution_policy
Where: policy text in the repo-facts block. Live: CONTRIBUTING, AI policy,
PR template.
Good: pass if AI help is permitted or never mentioned. Fail only on an
explicit ban of AI-generated code or docs. A disclosure requirement is not
a ban. Selective-review language is not a ban. Block says policy not
checked: `unclear`.

### settled_spec
Where: issue body, comment thread, linked-PR state in the repo-facts block.
Good: you can state the bug and expected behavior in two sentences using
the issue's own words, and the work is one finite outcome. Suspected causes
and compatible fixes do not unsettle it. Fail on a tracking list, a
migration, an unbounded set of components, text requiring a product or
design decision first, or two or more closed or abandoned linked PRs with
no recent maintainer restatement of the intended solution.

### behavior_matches_issue
Where: output excerpts, logs, screenshots in the repro report, read
against the error or behavior in the issue body.
Good: the artifact shows the same error or behavior the issue names, in the
same component. Same message, same symptom. An adjacent failure fails, even
if it looks similar. A control run that contrasts with the failing run
supports a pass. An evidenced cannot-reproduce that says so plainly passes.
A confident match claim the artifact does not show fails.
Supporting reads, never separate grades: environment named (OS, runtime,
version or commit), steps runnable from a clean start, untried
environments named as untried.

### good_first_issue_label
Where: labels in the issue header or repo-facts block.
Good: label reads `good first issue` or `easy`. Spelling variants count.
`help wanted` and `beginner` do not. Preferred only. Ranks, never blocks.
