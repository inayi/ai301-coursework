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
Reproduction report for [[#72](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72)](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72)

**Result:** *Reproduced*. `verify_password()` raises `passlib.exc.UnknownHashError` on malformed stored hashes instead of failing closed and returning `False`.

### Environment

* **OS:** Windows (win32)
* **Python:** 3.14.5 (using `.venv`)
* **Dependencies:** `passlib` 1.7.4, `bcrypt` 4.3.0, `pytest` 9.1.1
* **Setup:** Followed `docs/SETUP.md` (`.env`, Docker Compose, and `make setup`)

---

### Steps to Reproduce

1. Bypassed the `@pytest.mark.xfail` marker on the covering test to observe the unhandled exception:
```cmd
.\.venv\Scripts\python.exe -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv --runxfail --tb=long

```
2. Direct function call under test:
```python
from core.security import verify_password

verify_password("password", "not_a_valid_bcrypt_hash")

```
---

### Observed Output

**Running pytest with `--runxfail`:**

```text
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format

>       result = verify_password("password", wrong_hash)

core\security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
.venv\Lib\site-packages\passlib\context.py:1132: in identify_record
    raise exc.UnknownHashError("hash could not be identified")
E   passlib.exc.UnknownHashError: hash could not be identified

```
---

### Expected vs. Actual Behavior

* **Expected:** `verify_password("password", "not_a_valid_bcrypt_hash")` should return `False`.
* **Actual:** `verify_password()` lets `passlib.exc.UnknownHashError` escape unhandled from `core/security.py:37`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
