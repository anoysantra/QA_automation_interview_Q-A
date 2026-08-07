# Playwright Interview Answers

This file explains the Playwright interview topics in a beginner-friendly, interview-ready format.

## 1) What is Playwright and why is it widely used?

### Definition
Playwright is a modern browser automation framework used for end-to-end testing of web applications.

### Technical explanation
It can automate Chromium, Firefox, and WebKit, supports auto-waiting, handles iframes, dialogs, and network requests, and is known for speed and reliability.

### Why it is used
It helps QA engineers test real browser behavior with less flaky synchronization issues.

### Real-world example
A test may open the login page, type credentials, click login, and verify the dashboard appears.

### Common follow-up questions
- How is Playwright different from Selenium?
- Why is Playwright considered modern for web automation?
- Does Playwright support API testing as well?

### Key points to remember
- Playwright is built for modern browser automation.
- It is known for built-in waiting and stable selectors.

---

## 2) What are the different selector types in Playwright?

### Definition
Selectors are used to find UI elements on a page.

### Technical explanation
Playwright supports CSS selectors, XPath, text selectors, role selectors, and locators built on top of the test runner.

### Why it is used
Selectors let the test identify the correct UI element reliably.

### Real-world example
A login button can be located by `page.get_by_role("button", name="Login")`.

### Python code example
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=True)
    page = browser.new_page()
    page.goto("https://example.com")
    page.locator("text=Login").click()
    browser.close()
```

### Common follow-up questions
- Which selector type is best for accessibility-driven tests?
- Why are Playwright locators preferred over raw CSS strings?

### Key points to remember
- Use the most stable and readable selector.
- `get_by_role` is often the best option for user-facing actions.

---

## 3) What is a locator in Playwright?

### Definition
A locator is a Playwright object that represents a UI element and offers methods to interact with it.

### Technical explanation
Locators are designed to be auto-waiting and to work well with dynamic pages. They can be chained or filtered.

### Why it is used
This reduces flaky tests because Playwright waits for the element to be ready before interacting with it.

### Real-world example
A test can locate a row in a table and then find a button inside that row.

### Common follow-up questions
- How is a locator different from a raw selector string?
- Why do locators help with synchronization?

### Key points to remember
- Locators are the main UI interaction mechanism in Playwright.
- They are more stable and maintainable than ad-hoc element lookup.

---

## 4) What is locator filtering vs chaining?

### Definition
Locator filtering and chaining are ways to narrow down a set of elements or locate nested elements more precisely.

### Technical explanation
- Filtering reduces a set of locators based on a condition.
- Chaining means using one locator to find another inside it.

### Why it is used
This helps target complex UI structures more reliably.

### Real-world example
A table row can be selected first, then a nested button inside it can be clicked using chaining.

### Common follow-up questions
- Why is chaining helpful in POM based tests?
- When would filtering be a better choice?

### Key points to remember
- Use chaining for nested UI components.
- Use filtering when you need to narrow a locator set.

---

## 5) How do Playwright tests handle synchronization and flaky tests?

### Definition
Synchronization means waiting for the UI to be ready before interacting with elements.

### Technical explanation
Playwright automatically waits for the element to be visible, enabled, attached, and stable before actions like click and fill.

### Why it is used
This reduces flakiness caused by slow rendering or ajax updates.

### Real-world example
A login button becomes enabled only after a loading animation ends. Playwright automatically waits and then clicks.

### Common follow-up questions
- What is the difference between auto-waiting and explicit waits?
- Why are explicit waits still useful?

### Key points to remember
- Playwright's auto-waiting is one of its biggest advantages.
- Use explicit waits only when the situation needs a custom condition.

---

## 6) How do you handle alerts, dialogs, uploads, and downloads?

### Definition
These are common browser interactions that require special handling.

### Technical explanation
Playwright supports dialogs, file uploads, download events, and even route interception for network simulation.

### Why it is used
Real applications often depend on these UI interactions, and tests must validate them.

### Real-world example
A file upload field accepts a PDF and the test verifies the file has been attached.

### Common follow-up questions
- How do you accept a browser alert in Playwright?
- How are downloads usually validated in automation?

### Key points to remember
- Playwright provides built-in APIs for these interactions.
- They should be handled with stable assertions rather than blind clicks.

---

## 7) What is the Page Object Model in Playwright?

### Definition
POM is a test design pattern that separates page selectors and actions into reusable classes.

### Technical explanation
A page class can define locators and methods such as `login()` or `search_product()`.

### Why it is used
It improves maintainability and readability as the test suite grows.

### Real-world example
A `LoginPage` class contains locators for username, password, and submit button.

### Common follow-up questions
- Why is POM recommended for large suites?
- How do you avoid duplicating selectors across test files?

### Key points to remember
- POM helps keep tests clean and maintainable.
- Each page should encapsulate its own page-specific actions.

---

## 8) What is `page.evaluate()`?

### Definition
`page.evaluate()` runs JavaScript in the browser context and returns the result to the test.

### Technical explanation
It is used when the application state or behavior is easier to read through script execution than through UI actions.

### Why it is used
It helps verify DOM values, read attributes, or trigger browser-side behaviors.

### Real-world example
Reading the current URL or checking if a form field is visible through the DOM.

### Python code example
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=True)
    page = browser.new_page()
    page.goto("https://example.com")
    title = page.evaluate("() => document.title")
    print(title)
    browser.close()
```

### Common follow-up questions
- When should `page.evaluate()` be used carefully?
- Is it better than using page locators when possible?

### Key points to remember
- Use it when direct locator APIs are not enough.
- It is useful, but not the first choice for the main interaction flow.

---

## 9) What are Playwright hooks?

### Definition
Hooks are lifecycle methods that run before or after tests.

### Technical explanation
Common hooks in Playwright and Pytest integration include setup and teardown logic, test environment preparation, and browser reuse.

### Why it is used
Hooks make test setup and cleanup cleaner and easier to reuse.

### Real-world example
Opening a browser context before each test and closing it after the test finishes.

### Common follow-up questions
- What is the purpose of a fixture in combined Playwright + Pytest setups?
- Why is teardown important in UI automation?

### Key points to remember
- Hooks improve reliability and reduce repeated setup code.
- They are essential in maintainable test frameworks.

---

## 10) How do you pass query parameters in Playwright API testing?

### Definition
Query parameters are values passed in the URL for API requests.

### Technical explanation
You can pass query strings in the URL or use request options such as `params` in the API request object.

### Why it is used
This supports filtering, pagination, and dynamic requests in API tests.

### Real-world example
A request to fetch page 2 of users may include `?page=2`.

### Python code example
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=True)
    context = browser.new_context()
    page = context.new_page()
    response = page.request.get("https://reqres.in/api/users", params={"page": 2})
    print(response.status)
    print(response.json())
    browser.close()
```

### Common follow-up questions
- Which is better for API tests: Playwright request or `requests`?
- Why is passing parameters dynamically useful?

### Key points to remember
- Query parameters are used to filter or paginate API calls.
- This is common in backend response testing.

---

## 11) What is `storage_state` and why is it important?

### Definition
`storage_state` stores browser authentication state so the browser can reuse logged-in sessions.

### Technical explanation
This prevents the need to log in repeatedly in every test. It can be useful for UI automation where authentication is required.

### Why it is used
It speeds up tests and improves reliability by reusing a trusted logged-in context.

### Real-world example
A test suite stores a logged-in session and then starts from the dashboard page.

### Common follow-up questions
- What problem does storage state solve?
- Why is it helpful in CI runs?

### Key points to remember
- Storage state improves test speed and reduces login repetition.
- It is especially useful for authenticated workflows.

---

## 12) What is network mocking in Playwright?

### Definition
Network mocking lets a test intercept and control HTTP requests and responses.

### Technical explanation
This can be used to simulate backend responses, test edge cases, or avoid depending on real external services.

### Why it is used
It helps create stable and isolated tests.

### Real-world example
A test may mock a slow API response to verify the loading spinner behavior.

### Common follow-up questions
- Why is mocking useful in frontend automation?
- Does mocking remove the need for real integration tests?

### Key points to remember
- Mocking is useful for stability and controlled test scenarios.
- Use it where the real service is unavailable or too slow.

---

## 13) What is the difference between Playwright and Selenium?

### Definition
Both automate browsers, but they have different design philosophies and features.

### Technical explanation
Playwright generally offers better auto-waiting, modern browser support, and a simpler API for many web interactions. Selenium is more mature and widely adopted across legacy environments.

### Why it is used
Choosing the right tool depends on the team, project age, and test requirements.

### Real-world example
A greenfield project may prefer Playwright, while an enterprise suite with legacy Selenium infrastructure may keep Selenium.

### Common follow-up questions
- Which framework is easier for beginners?
- Which one is better for fast-moving modern web apps?

### Key points to remember
- Playwright is often preferred for modern automation workflows.
- Selenium still has strong ecosystem support and legacy usage.

---

## 14) What are common Playwright + Pytest practices?

### Definition
Combining Playwright with Pytest enables clean, reusable, and scalable browser automation tests.

### Technical explanation
Common practices include fixtures, `conftest.py` setup, markers such as `smoke` and `regression`, and parameterized tests.

### Why it is used
Pytest adds structure, test organization, and reporting while Playwright handles browser automation.

### Real-world example
A repo can use Pytest to organize test cases and Playwright to run browser actions.

### Common follow-up questions
- Why combine Playwright with Pytest?
- What is the benefit of using fixtures for browser setup?

### Key points to remember
- Pytest provides structure and reporting.
- Playwright handles browser interactions.

---

## 15) How are reports and parallel execution handled in Playwright projects?

### Definition
Reports summarize test results, and parallel execution spreads test runs across workers.

### Technical explanation
In automation projects, reports help make failures visible and easier to debug. Parallel execution reduces runtime on large suites.

### Why it is used
It improves feedback speed and test visibility for QA and CI pipelines.

### Real-world example
A CI job runs smoke tests in parallel, then publishes results to a report file for the team.

### Common follow-up questions
- Why are reports important in QA automation?
- What are the risks of parallel execution?

### Key points to remember
- Reporting helps teams understand failures quickly.
- Parallelization improves speed but requires isolated tests.

---

## Follow-up Question 1: Why is Playwright considered more reliable for modern web automation?

### Definition
Playwright is considered reliable because it reduces many timing and synchronization issues common in UI automation.

### Technical explanation
Its built-in waiting and locator strategy help tests interact with elements only when they are ready, which reduces flaky behavior.

### Why it is used
It helps teams create robust browser automation faster.

### Real-world example
A button appears only after page rendering; Playwright waits automatically and then clicks it.

### Common follow-up questions
- What makes Playwright better than raw Selenium scripts?
- Why is auto-waiting useful in interviews?

### Key points to remember
- Playwright provides stable browser automation out of the box.
- It is especially helpful for dynamic UI flows.

---

## Follow-up Question 2: What is the role of `get_by_role()` in Playwright?

### Definition
`get_by_role()` locates an element by its accessible role, such as button, link, or textbox.

### Technical explanation
This selector is aligned with accessibility best practices and typically makes tests more readable and less fragile.

### Why it is used
It enables tests to target UI elements in a user-oriented way.

### Real-world example
A tester can locate a login button using `page.get_by_role("button", name="Login")`.

### Common follow-up questions
- Why is role-based selection recommended?
- How is it different from CSS selectors?

### Key points to remember
- Role-based selectors are user-focused and maintainable.
- They are a strong choice for accessibility-aware automation.

---

## Follow-up Question 3: Why is `storage_state` useful in Playwright automation?

### Definition
`storage_state` stores browser authentication data so tests can reuse a logged-in session.

### Technical explanation
This avoids repeated login in every test and improves speed and consistency for authentication-heavy workflows.

### Why it is used
It helps reduce test execution time and makes authenticated UI tests easier to maintain.

### Real-world example
A suite stores a login session once and then reuses it to test account settings pages.

### Common follow-up questions
- Why is login reuse helpful in CI?
- Does storing auth state create security concerns?

### Key points to remember
- `storage_state` helps reuse authenticated sessions.
- It should be handled carefully in secure test environments.
