# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

inayi

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6021852993
Plan for #72, building on my reproduction above (commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`).

**Diagnosis:**
`verify_password` in `core/security.py` passes stored password hashes directly to `pwd_context.verify()` with no exception handling. When `hashed_password` is not a valid format recognized by passlib (such as `"not_a_valid_bcrypt_hash"`), passlib raises `passlib.exc.UnknownHashError`, which escapes to callers instead of returning `False`. Valid bcrypt hashes verify correctly (`True` for the right password, `False` for an incorrect password), so the failure is specific to malformed/unrecognized stored hash inputs.

**Change:**
- In `core/security.py`, wrap the `pwd_context.verify(...)` call in `verify_password()` with a `try...except (UnknownHashError, ValueError)` block and return `False` when caught.
- In `tests/unit/test_security.py`, remove the `@pytest.mark.xfail(strict=True)` marker from `test_verify_with_wrong_hash_format` (manifest H-05) so it becomes an active regression test.

**Scope:**
- **In:** `core/security.py` and `tests/unit/test_security.py`.
- **Out:** `hash_password`, JWT utilities, authentication route logic (`api/routes/auth.py`), passlib configurations, and dependencies.

**Verification:**
1. Re-run direct reproduction snippet: `verify_password('password', 'not_a_valid_bcrypt_hash')` should return `False` instead of raising `UnknownHashError`.
2. Run covering unit test: `pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v` should show `1 passed`.
3. Run full security test suite: `pytest tests/unit/test_security.py -v` should show `25 passed`.

I used Claude to help draft this plan based on my own Unit 2 reproduction evidence and reviewed the proposed changes against the issue context.

---

## Your branch

**Branch**

fix/72-handle-unknown-hash-error

**Evidence**

### Before (on main at commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`)

1. Direct call with malformed hash:
```bash
python3.11 -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"

```

**Output:**

```text
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File ".../core/security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
  ...
  File ".../passlib/context.py", line 1132, in identify_record
    raise exc.UnknownHashError("hash could not be identified")
passlib.exc.UnknownHashError: hash could not be identified

```

2. Covering test with `--runxfail`:

```bash
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --runxfail

```

**Output:**

```text
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
E   passlib.exc.UnknownHashError: hash could not be identified
1 failed, 24 deselected, 2 warnings in 0.18s

```

3. Full security module run:

```bash
pytest tests/unit/test_security.py -v

```

**Output:**

```text
24 passed, 1 xfailed, 2 warnings in 0.26s

```

---

### After (on branch `fix/72-handle-unknown-hash-error`)

1. Direct call with malformed hash:

```bash
python3.11 -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"

```

**Output:**

```text
False

```

2. Targeted unit test (with `@pytest.mark.xfail` removed):

```bash
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v

```

**Output:**

```text
PASSED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
1 passed, 2 warnings in 0.18s

```

3. Full security module run:

```bash
pytest tests/unit/test_security.py -v

```

**Output:**

```text
25 passed, 2 warnings in 0.28s

```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. 15/19 agree, with pkg-02 an ERROR. This was your run, before my changes.
2. 5/5 on a partial --only run of pkg-02, 03, 09, 14 and 20. Partial runs don't count toward the bar.
3. 18/20 (bar 18/20: PASS). This is the last run and the one eval-run.txt should contain.

**Package analysis**

pkg-14 (zellij reattach leak)

- Gold: accept.
- My rubric: reject, failed on Test Plan & Automation. It had agreed with gold in run 2, so the grader is not stable on this package.
- Why the rubric read it that way: the plan's test is five SSH reattach cycles with no rgb strings in any pane. That is repeatable and has an observable outcome, but it is run by hand against a live terminal. It names no test added to the suite and no script, so a strict reading of "automated test or scripted re-run" fails it.
- Why gold accepts: the cause is grounded in the regression window and the cache control, and the scope is honest.

**Check rationale**

Pass (P): the Test Plan names a concrete, repeatable check with an observable pass/fail outcome mapped to the repro steps: an automated test (unit or integration test, CI assertion, fixture/regression test added to the suite) or a scripted re-run of the repro commands with stated expected output, alongside any optional manual verification. Fail (F): the Test Plan is only "verify it works" style manual checking, or names no observable outcome and no way to execute the check.

- Why it reads that way: your original wording failed pkg-09 and pkg-14, which gold accepts. I loosened it to accept a scripted repro re-run with stated expected output, and kept the fail for plans with no observable outcome.
- Rejected: dropping the check or making it preferred. That would let the unbuildable plans through.

**Trade-offs**

- Packages the check changes: pkg-09 and pkg-02 now agree with gold. pkg-14 is still a coin flip, because a manual live-terminal loop sits on the boundary of "scripted".
- Unaffected: unbuildable stayed 3/3 in the full run.
- Known miss, pkg-05: the new Comms check wrongly rejects it. Its policy says only "review and understand AI output", which is not a disclosure requirement. I drafted a tightening that treats disclosure as required only when the policy explicitly says to disclose or label AI use. It is not applied or tested.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
