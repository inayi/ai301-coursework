# Plan: Handle UnknownHashError in verify_password

## Repro Evidence
> `python3.11 -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"`
> Output:
> `Traceback (most recent call last):`
> `  File ".../core/security.py", line 37, in verify_password`
> `    return bool(pwd_context.verify(plain_password, hashed_password))`
> `  ...`
> `  File ".../passlib/context.py", line 1132, in identify_record`
> `    raise exc.UnknownHashError("hash could not be identified")`
> `passlib.exc.UnknownHashError: hash could not be identified`
>
> Running covering test with `--runxfail`:
> `pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format --runxfail`
> Output:
> `FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format`
> `E passlib.exc.UnknownHashError: hash could not be identified`

## Diagnosis
In `core/security.py`, `verify_password()` executes `return bool(pwd_context.verify(plain_password, hashed_password))` without any exception handling. When `hashed_password` is malformed or unidentifiable (such as `"not_a_valid_bcrypt_hash"`), passlib raises `passlib.exc.UnknownHashError`. Because there is no `try/except` block catching passlib exceptions at this boundary, the exception escapes to callers (such as the authentication route handler) instead of failing closed with a `False` return value.

## Scope
- **What will change:**
  - `core/security.py`: Update `verify_password()` to catch `passlib.exc.UnknownHashError` (and `ValueError` if needed for truncated hashes) and return `False`. Update docstrings if appropriate.
  - `tests/unit/test_security.py`: Remove the `@pytest.mark.xfail(strict=True)` marker from `test_verify_with_wrong_hash_format` so it becomes an active passing test.
- **What will NOT change:**
  - `hash_password()`, token handling, or JWT utility functions.
  - API routes in `api/routes/auth.py` (which already handle `False` by returning HTTP 401).
  - External dependencies or passlib configurations.

## Files
- `core/security.py`
- `tests/unit/test_security.py`

## Approach
1. Import `UnknownHashError` from `passlib.exc` in `core/security.py`.
2. Wrap `pwd_context.verify(plain_password, hashed_password)` inside a `try...except` block in `verify_password()`:
   ```python
   try:
       return bool(pwd_context.verify(plain_password, hashed_password))
   except (UnknownHashError, ValueError):
       return False

```

3. Remove the `@pytest.mark.xfail` marker above `test_verify_with_wrong_hash_format` in `tests/unit/test_security.py`.

## Test Plan

1. **Direct Function Verification:**
Re-run the reproduction snippet:
```bash
python3 -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"

```


*Expected result:* Prints `False` without raising `UnknownHashError`.
2. **Targeted Unit Test:**
Run the specific covering test without xfail flags:
```bash
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v

```


*Expected result:* `1 passed`.
3. **Security Test Suite Regression Check:**
Run all security unit tests:
```bash
pytest tests/unit/test_security.py -v

```


*Expected result:* `25 passed` (previously `24 passed, 1 xfailed`).

## Risks & Unknowns

* **Catches broader exceptions:** Catching `ValueError` alongside `UnknownHashError` covers truncated bcrypt hashes (`$2b$12$abc`), but may catch other passlib input errors. This is desired for fail-closed security behavior, but should be validated against the existing test suite to avoid masking unexpected programming errors.

## Deviations

No deviations from the plan during implementation. The changes made match the planned scope and approach exactly.

```
