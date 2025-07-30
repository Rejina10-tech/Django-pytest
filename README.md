# Django-pytest
# Testing Django Applications with pytest-django: Test Database Handling

---

## 1. Introduction

When testing Django applications with `pytest-django`, the test framework automatically creates and manages a temporary database to ensure tests run in isolation and do not affect our real data.

---

## 2. Step-by-Step Overview

### Step 1: Install Dependencies

Install `pytest-django` using poetry:

```bash
poetry add pytest-django

```

### Step 2: Install Configuration

Create a `pytest.ini` file in your project root:

```ini
[pytest]
DJANGO_SETTINGS_MODULE = config.settings
python_files = tests.py test_*.py *_tests.py
```

---

##  3. Running Database Tests

By default, `pytest-django` blocks DB access unless enabled. Use the `@pytest.mark.django_db` decorator or the `db` fixture to mark such tests:

To run the tests and create the test DB:

```bash
pytest --create-db -v
```

This will:
- Load `DJANGO_SETTINGS_MODULE`
- Create a temporary test DB
- Run migrations
- Tear down the DB when tests complete

---

##  4. Sample Test Output

```
platform linux -- Python 3.12.3, pytest-8.4.1, django-5.2
collected 5 items

apps/api_auth/tests/views/test_login.py::test_user_create PASSED     [ 20%]
apps/api_auth/tests/views/test_login.py::test_login_success PASSED   [ 40%]
apps/api_auth/tests/views/test_login.py::test_token_obtain_wrong_password PASSED [ 60%]
apps/api_auth/tests/views/test_password.py::test_password_reset_request_success PASSED [ 80%]
apps/api_auth/tests/views/test_password.py::test_password_reset_confirm_success PASSED [100%]
```

 Percentages show test progress, **not test quality**.

---

##  5. Important Notes

- The test DB is **completely isolated** from production.
- Data **does not persist** across tests.
- Tests **must** explicitly declare DB access or they will fail.

---

##  6. Useful Pytest Flags

| Flag          | Description                               |
|---------------|-------------------------------------------|
| `--reuse-db`  | Reuse existing test DB (faster)           |
| `--create-db` | Force DB re-creation before running tests |


---

## 7. Run pytest
```
pytest
```

