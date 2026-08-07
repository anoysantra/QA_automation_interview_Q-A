# Pytest Interview Answers

This file turns the Pytest topic list into interview-ready notes for entry-level QA Automation roles.

## 1) What is Pytest and why is it widely used?

### Definition
Pytest is a Python testing framework used to write and run test cases efficiently.

### Technical explanation
It supports simple function-based tests, fixtures, parameterization, markers, and plugins. It is widely used because it is easy to read and powerful enough for modern automation.

### Why it is used
Pytest helps QA engineers write reusable test cases, run them quickly, and integrate them into CI/CD pipelines.

### Real-world example
A tester can write a login test in a `.py` file and run it with `pytest -q`.

### Python code example
```python
# test_login.py

def test_login_success():
    assert 1 + 1 == 2
```

### Common follow-up questions
- Why is Pytest preferred over `unittest` in many projects?
- What is the role of `pytest.ini`?
- What is a fixture in Pytest?

### Key points to remember
- Pytest is simple, readable, and widely adopted.
- It works well for both API and UI automation.

---

## 2) What is parameterization in Pytest?

### Definition
Parameterization lets you run the same test multiple times with different input values.

### Technical explanation
It is useful when you want to test several forms of the same behavior without copying the test code multiple times.

### Why it is used
It reduces repetition and improves coverage.

### Real-world example
Testing login with multiple valid and invalid credentials.

### Python code example
```python
import pytest

@pytest.mark.parametrize("username,password", [
    ("valid_user", "correct_pass"),
    ("invalid_user", "wrong_pass")
])
def test_login(username, password):
    assert username != ""
    assert password != ""
```

### Common follow-up questions
- What is the difference between `@pytest.mark.parametrize` and fixture parameterization?
- Why is parameterization useful in QA automation?

### Key points to remember
- Parameterization improves test coverage with less code.
- It is widely used for data-driven testing.

---

## 3) What is `conftest.py`?

### Definition
`conftest.py` is a special Pytest file used to define shared fixtures, hooks, and reusable test setup.

### Technical explanation
Fixtures defined in `conftest.py` can be used across multiple test files.

### Why it is used
It prevents code duplication and centralizes environment setup such as login, browser setup, or test data configuration.

### Real-world example
A `conftest.py` file may define a login fixture used by several UI tests.

### Common follow-up questions
- Can one `conftest.py` file be shared across folders?
- What is the benefit of putting fixtures there?

### Key points to remember
- `conftest.py` centralizes reusable test setup.
- It is often used in Selenium and Playwright frameworks.

---

## 4) Why is `pytest.ini` written?

### Definition
`pytest.ini` is the main configuration file for Pytest.

### Technical explanation
It can define test discovery paths, markers, logging options, and command-line behavior.

### Why it is used
It makes test execution more predictable and keeps project conventions consistent.

### Real-world example
A `pytest.ini` file may register markers like `smoke` and `regression`.

### Python example
```ini
[pytest]
markers =
    smoke: smoke test
    regression: regression test
```

### Common follow-up questions
- What happens if there is no `pytest.ini`?
- Why are custom markers useful?

### Key points to remember
- `pytest.ini` controls how Pytest behaves.
- It is useful for marker registration and test configuration.

---

## 5) What are custom CLI options in Pytest?

### Definition
Custom CLI options allow you to pass extra arguments into the test runner.

### Technical explanation
You define an option using `pytest_addoption`, then read it in fixtures or tests.

### Why it is used
It helps switch environments like QA, staging, or prod without changing code.

### Python code example
```python
# conftest.py

def pytest_addoption(parser):
    parser.addoption("--env", action="store", default="qa", help="Environment: qa, staging, or prod")


def pytest_configure(config):
    print("Environment:", config.getoption("--env"))
```

### Common follow-up questions
- Why use environment flags for test automation?
- What is the benefit of keeping environment in config instead of code?

### Key points to remember
- CLI options make tests more flexible and reusable.
- This is especially helpful in CI/CD.

---

## 6) What are soft assertions in Pytest?

### Definition
Soft assertions allow a test to continue running even after one assertion fails.

### Technical explanation
This is useful when a test needs to collect multiple failure messages in the same run.

### Why it is used
It helps identify all related issues in one execution instead of stopping at the first failure.

### Real-world example
A validation test may check several fields of a response body and report each mismatch.

### Common follow-up questions
- How are soft assertions different from regular assertions?
- Does Pytest support soft assertions out of the box?

### Key points to remember
- Standard `assert` stops the test at the first failure.
- Soft assertions help gather more context.

---

## 7) What is the difference between `@pytest.mark.parametrize` and fixture parameterization?

### Definition
Both allow running tests with different input values, but they are used differently.

### Technical explanation
- `@pytest.mark.parametrize` is used directly on a test function.
- Fixture parameterization uses a fixture with a `params` list.

### Why it is used
They allow data-driven testing in different styles.

### Python code example
```python
import pytest

@pytest.mark.parametrize("browser", ["chrome", "firefox"])
def test_browser(browser):
    assert browser in ["chrome", "firefox"]


@pytest.fixture(params=["chrome", "firefox", "edge"])
def browser_name(request):
    return request.param


def test_browser_fixture(browser_name):
    assert browser_name in ["chrome", "firefox", "edge"]
```

### Common follow-up questions
- When would you choose one form over the other?
- What is the role of `request.param`?

### Key points to remember
- `parametrize` is usually simpler for direct test inputs.
- Fixture parameterization is useful when you want to reuse setup logic.

---

## 8) What are Pytest markers?

### Definition
Markers are labels that group or classify tests.

### Technical explanation
Examples include `smoke`, `regression`, `slow`, and `api`.

### Why it is used
They help run targeted tests in CI or locally.

### Real-world example
A team may run only smoke tests before merging code to `main`.

### Python code example
```python
import pytest

@pytest.mark.smoke
def test_login():
    assert True
```

### Common follow-up questions
- How do markers help in CI/CD?
- Why register markers in `pytest.ini`?

### Key points to remember
- Markers improve organization and selective test execution.
- They are especially useful in large automation projects.

---

## 9) What is the `request` fixture in Pytest?

### Definition
The `request` fixture gives test code access to information about the current test item.

### Technical explanation
It can provide `request.param`, `request.node`, and `request.addfinalizer` for parameterized tests and cleanup.

### Why it is used
It helps build dynamic fixtures and manage cleanup logic.

### Real-world example
You may use `request.param` to find the current browser name when using fixture parameterization.

### Python code example
```python
import pytest

@pytest.fixture(params=["chrome", "firefox"])
def browser(request):
    return request.param


def test_browser_name(browser):
    assert browser in ["chrome", "firefox"]
```

### Common follow-up questions
- What is `request.addfinalizer` used for?
- Why is `request.node` useful?

### Key points to remember
- `request` is a built-in fixture that provides metadata and cleanup support.
- It is important for advanced Pytest test design.

---

## 10) What are common Pytest built-in functions?

### Definition
Pytest offers built-in constructs for skipping tests, failing tests, and customizing behavior.

### Technical explanation
Common functions include:
- `pytest.skip()` → skip the test
- `pytest.fail()` → fail the test with a message

### Why it is used
These functions help control flow when a test environment is not ready or a condition is not met.

### Real-world example
Skip a test when a required environment variable is missing.

### Python code example
```python
import pytest


def test_example():
    if True:
        pytest.skip("Environment not configured")
```

### Common follow-up questions
- How is `skip` different from `fail`?
- When would you use `skip` in CI?

### Key points to remember
- `skip` marks the test as skipped.
- `fail` intentionally marks the test as failed.

---

## 11) What is setup, call, and teardown in Pytest?

### Definition
These phases describe how a test is prepared, executed, and cleaned up.

### Technical explanation
- Setup → create test prerequisites
- Call → execute the test body
- Teardown → clean up resources

### Why it is used
To ensure tests are isolated and reliable.

### Real-world example
A UI test may open a browser before the test and close it afterwards.

### Common follow-up questions
- How does a fixture provide setup and teardown?
- Why is teardown necessary?

### Key points to remember
- Fixtures help implement this lifecycle cleanly.
- Good teardown prevents test pollution and flaky behavior.

---

## 12) What is the role of `yield` in fixtures?

### Definition
A fixture can use `yield` to perform setup before the test and cleanup after the test.

### Technical explanation
After `yield`, the code below it runs as teardown logic.

### Why it is used
It supports resource cleanup like closing browsers, database connections, or temporary files.

### Python code example
```python
import pytest

@pytest.fixture
def sample_fixture():
    print("setup")
    yield
    print("teardown")
```

### Common follow-up questions
- Why not just use `return`?
- What is the teardown stage in a fixture?

### Key points to remember
- `yield` is the standard way to implement fixture teardown.
- Cleanup is critical for stable tests.

---

## 13) What is `pytest-xdist` and why is it used?

### Definition
`pytest-xdist` is a Pytest plugin that runs tests in parallel.

### Technical explanation
It is useful for reducing overall test execution time by distributing tests across CPU cores.

### Why it is used
Large suites can take a long time to finish; parallel execution improves speed.

### Real-world example
Running `pytest -n auto` to distribute tests across workers.

### Common follow-up questions
- What is the benefit of parallel execution?
- Does parallel execution always make tests faster?

### Key points to remember
- Parallel execution improves throughput.
- It can sometimes introduce flakiness if tests are not isolated.

---

## 14) What are the key command-line options used in Pytest?

### Definition
Pytest command-line options change how tests are discovered and executed.

### Technical explanation
Common options include:
- `pytest -q` → quiet output
- `pytest -k login` → run tests matching a keyword
- `pytest -m smoke` → run only marked tests
- `pytest -n auto` → parallel execution

### Why it is used
They help test selection and execution efficiency.

### Common follow-up questions
- Which option is most useful in CI pipelines?
- How do markers work with command-line options?

### Key points to remember
- Pytest command-line usage is an important interview topic.
- It helps in local development and CI execution.

---

## 15) How is Pytest different from `unittest`?

### Definition
Pytest and `unittest` are both Python testing frameworks, but Pytest is usually simpler and more flexible.

### Technical explanation
`unittest` uses classes and `TestCase`, while Pytest mainly uses plain functions and fixtures. Pytest also offers stronger plugin support and easier parameterization.

### Why it is used
Pytest is often preferred for beginner-friendly test automation and modern QA projects.

### Common follow-up questions
- Which one is better for entry-level automation?
- Which one has richer plugin support?

### Key points to remember
- Pytest is simpler to start with.
- `unittest` is more traditional but more verbose.

---

## Follow-up Question 1: What is the benefit of using fixtures in Pytest?

### Definition
A fixture is a reusable setup object used by tests.

### Technical explanation
Fixtures provide the test environment by preparing resources such as browser instances, test data, or database connections.

### Why it is used
They avoid duplicate setup logic and keep tests clean and maintainable.

### Real-world example
A fixture can create a browser context for UI tests and tear it down after the test finishes.

### Common follow-up questions
- Why is fixture reuse helpful across many tests?
- How is a fixture different from a normal function?

### Key points to remember
- Fixtures centralize setup and cleanup.
- They are one of the most important Pytest concepts.

---

## Follow-up Question 2: Why is `pytest -q` commonly used?

### Definition
`pytest -q` runs tests in a quiet mode with concise output.

### Technical explanation
It reduces noise and gives quick test summaries, which is useful in local runs and CI logs.

### Why it is used
It improves readability and speeds up feedback during development.

### Real-world example
A tester runs `pytest -q` before pushing code to confirm the key tests pass.

### Common follow-up questions
- What does `-k` do in Pytest?
- Why are markers important in CI runs?

### Key points to remember
- `pytest -q` is a simple command for quick verification.
- It is commonly used in interviews and day-to-day automation work.

---

## Follow-up Question 3: Why do we use test markers like `smoke` and `regression`?

### Definition
Pytest markers label tests so they can be grouped and executed selectively.

### Technical explanation
Markers such as `smoke` or `regression` help teams control which suite runs in different stages of delivery.

### Why it is used
They make automation more organized and help optimize CI speed.

### Real-world example
A CI pipeline may run only smoke tests on every commit, while full regression tests run nightly.

### Common follow-up questions
- How do markers help with CI performance?
- Why register markers in `pytest.ini`?

### Key points to remember
- Markers improve organization and execution control.
- They are useful in both local and pipeline test runs.
