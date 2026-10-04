# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

inayi

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5976275142
I'd like to claim this issue.

I think this issue is straightforward and I am confident to fix it. My plan is:

1. Fork and set up the repository locally according to `docs/SETUP.md`.
2. Record my setup environment (OS, Python, `passlib`, `bcrypt`, and `pytest` versions).
3. Run the covering test (`tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format`) with `--runxfail` to observe the underlying exception.
4. Test direct calls to `verify_password()` with valid bcrypt hashes as controls, alongside malformed, empty, and truncated hash strings to determine the full scope of exceptions to catch.
5. Post a reproduction report with full environment details and test output, then follow up with a PR that catches the required exceptions, fails closed by returning `False`, and removes the `@pytest.mark.xfail` marker for manifest ID `H-05`.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5976370402
## Reproduction report for #72

I reproduced this. `verify_password()` raises `UnknownHashError` for a non-bcrypt stored hash instead of returning `False`. It also raises `ValueError` for some malformed bcrypt-shaped hashes, which the issue doesn't mention.

### Environment

| | |
|---|---|
| OS | Windows 11 Pro 10.0.26200, Git Bash (MINGW64) |
| Python | 3.14.5 |
| passlib | 1.7.4 |
| bcrypt | 4.3.0 |
| pytest | 9.1.1 |
| Commit | `2f4e82f` (main, clean tree) |

Setup: I created a venv and ran `pip install -e ".[dev]"`, the same step `make setup` runs. I skipped Docker, Postgres and Redis because this test is a pure unit test with no database.

### Steps and result

1. Ran the covering test with `--runxfail`:

   ```
   pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format --runxfail --no-cov
   ```

   The test **FAILED** with:

   ```
   passlib.exc.UnknownHashError: hash could not be identified
   (passlib/context.py:1132, identify_record)
   ```

   The unmodified `core/security.py` (`verify_password`, line 27) calls `pwd_context.verify()` with no error handling, so the exception escapes.

2. Ran the whole file without `--runxfail`: `24 passed, 1 xfailed`. The strict xfail is currently masking this bug.

3. Called `verify_password("password", ...)` directly with each hash below:

| Stored hash | Result |
|---|---|
| valid bcrypt, correct password (control) | `True` |
| valid bcrypt, wrong password (control) | `False` |
| `"not_a_valid_bcrypt_hash"` | **raises `passlib.exc.UnknownHashError`** |
| `""` (empty) | **raises `UnknownHashError`** |
| `b"garbage"` (bytes) | **raises `UnknownHashError`** |
| valid hash truncated to 30 chars | **raises `ValueError`** ("checksum must be exactly 31 chars") |
| `"$2b$12$"` (prefix only) | **raises `ValueError`** ("salt too small") |
| `"$2b$99$..."` (cost out of range) | **raises `ValueError`** ("rounds (99) is too large") |
| `"$2b$12$" + "x"*53` (valid prefix, garbage body) | `False` |
| `None` | `False` |

### Findings

- Catching only `UnknownHashError` would fix the failing test. It would still leave truncated or partly malformed bcrypt hashes raising `ValueError`. A complete fail-closed fix needs to catch both `UnknownHashError` and `ValueError`.
- The setup prints a harmless `(trapped) error reading bcrypt version` traceback. It comes from passlib 1.7.4 reading bcrypt 4.x and is unrelated to this issue.

### Planned fix

In `verify_password`, catch `(UnknownHashError, ValueError)` and return `False`. Then remove the `@pytest.mark.xfail` marker (manifest H-05) from `test_verify_with_wrong_hash_format`. I'll also add parametrized test cases for the empty, truncated and bad-cost hashes above.


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

18/20

(Final run, saved as `eval-run.txt`: "agreement: 18/20 scored items  (bar: 18/20: PASS)".)

**Package analysis**

pkg-16. The gold label was reject; my rubric graded it accept (the harness note reads
"graded accept", so no check failed). Every required check in my rubric passed on it:
`no_active_claimants`, `active_maintainer`, `contribution_policy`, `settled_spec` and
`behavior_matches_issue`. My rubric reads a package as ready when the repo and issue are
sound and the report's output excerpt shows the issue's behavior. It has no check on the
environment record, on whether the steps can be followed, or on the claim comment's wording.
So a package that is rejected for one of those flaws gets through. That is the gap pkg-16
exposes.

**Check rationale**

> | behavior_matches_issue |	the repro report's output excerpt, log or screenshot, read against the error or behavior the issue describes |	The artifact shows the same error or behavior the issue names, in the same component. An adjacent failure fails. An evidenced cannot-reproduce that says so plainly also passes.	| required |

It judges the outcome, not the write-up's shape. The pass condition asks whether the
artifact shows the issue's own error in the issue's own component, which is something
another grader can apply and get the same answer. "An adjacent failure fails" is aimed at
the wrong-target packages, where a report reproduces a different error than the one the issue
names. The last sentence keeps a plainly evidenced cannot-reproduce from being punished,
because an honest negative is a valid result. I rejected a shape-based check, such as counting
steps or requiring a template's headings, because the rubric's own guidance says those make
graders disagree with themselves.

**Trade-offs**

The rubric covers the wrong-target family (wrong-target 3/4) and the repo-health families
(no-evidence 4/4, unfollowable-comms 3/3), and it passes the bar at 18/20. It gives up
the environment-record and claim-wording families, which no check reads. The two misses
show it: pkg-16 (gold reject) is graded accept because no check reads what it got wrong,
and pkg-01 (gold accept) is rejected because `active_maintainer` failed on it. I accept
both. Adding a stricter check for the pkg-16 style of flaw could start rejecting good
packages. The last full run is the evidence that the rubric clears the bar as it stands.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
