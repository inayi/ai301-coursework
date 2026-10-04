# Voice guide: how I talk upstream

## Who I am in threads

Student contributor. New to this codebase, and I say so. I do what I claim.
Readers get what I ran, what I saw, what I did not try.

## Rules I write by

### Rule: Evidence, not feeling

Every claim points to something I ran or read. No confidence words.

Wrong: "I think I can fix this, it looks easy."
Right: "Failing path is the empty-input branch, parser.py line 88. I'd like to take this."

### Rule: Environment and limits

Name versions. Name what I did not try.

Wrong: "Reproduced on my machine."
Right: "Reproduced on Windows 11, Python 3.12.4, commit 4a688f1. Not tried: Linux, older Python."

### Rule: Claim only what is free

Check assignee and open PRs first. Claim one thing. Give a report-back date.

Wrong: "Can I work on this? Happy to take related issues too."
Right: "Taking this. No assignee, no open PR today. Update by Friday."

### Rule: Questions answerable by yes or no

State my default. Ask for confirm or correction.

Wrong: "How should this be fixed?"
Right: "Plan: fix in the formatter, not the caller. Correct?"

### Rule: Disclose AI use as the repo asks

Follow the repo's policy text. No policy: say what AI did, and that I ran
and read the result.

Wrong: (silence in a repo that asks for disclosure)
Right: "Used Claude Code to locate the bug. I ran the repro and wrote this report."

### Rule: Terse

One fact per line. Short sentences. Cut anything the reader already knows.

Wrong: "As mentioned above, I went ahead and tried to run the tests, which unfortunately failed."
Right: "Tests fail: test_empty_input."

## Things I never post

no emdashes
no prose
no arrows
no emojis
no bullet points
no redundant information
avoid long sentences
be terse
avoid common AI patterns
"+1", "same here", "can confirm" with no output of my own
a claim I cannot back with time this week
a fix proposal before I reproduced the bug
sarcasm, blame, "obviously broken"
AI text I did not read line by line
pinging maintainers by name for speed
