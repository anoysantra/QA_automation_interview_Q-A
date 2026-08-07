# Playwright Python Cheat Sheet for Interviews

> A polished, interview-friendly reference for Playwright with Python, covering core APIs, waits, assertions, and UI handling.

---

## 1. Setup & Browser Management

- `sync_playwright()` — starts the synchronous Playwright context for script-style automation.
- `async_playwright()` — starts the asynchronous Playwright context for modern async workflows.
- `playwright.chromium.launch()` — launches a Chromium browser instance.
- `playwright.firefox.launch()` — launches a Firefox browser instance.
- `playwright.webkit.launch()` — launches a WebKit browser instance.
- `browser.new_context()` — creates an isolated browser context with separate cookies and session state.
- `browser.new_page()` — opens a new tab inside the active browser context.
- `browser.close()` — closes the browser and releases all resources.

---

## 2. Page Navigation & Lifecycle

- `page.goto(url)` — navigates to a URL.
- `page.reload()` — reloads the current page.
- `page.go_back()` — moves to the previous page in history.
- `page.go_forward()` — moves to the next page in history.
- `page.set_content(html)` — renders custom HTML content directly.
- `page.wait_for_load_state("load")` — waits until the page finishes loading.
- `page.wait_for_load_state("domcontentloaded")` — waits for DOM content to appear.
- `page.wait_for_load_state("networkidle")` — waits until network activity becomes idle.

---

## 3. Modern Locators

- `page.get_by_role(role, **kwargs)` — finds elements by ARIA role like button, link, heading.
- `page.get_by_text(text)` — finds visible text-based elements.
- `page.get_by_label(text)` — finds form fields linked to labels.
- `page.get_by_placeholder(text)` — finds inputs with placeholder text.
- `page.get_by_alt_text(text)` — finds images by alt text.
- `page.get_by_title(text)` — finds elements by title attribute.
- `page.get_by_test_id(id)` — finds elements using `data-testid`.
- `page.locator(selector)` — uses CSS or XPath-based selectors as a fallback.

---

## 4. Explicit Waits & Synchronization

- `page.wait_for_url(url)` — waits until the URL matches the expected value.
- `locator.wait_for(state="visible")` — waits until the element is visible.
- `locator.wait_for(state="attached")` — waits until the element is attached to the DOM.
- `locator.wait_for(state="hidden")` — waits until the element disappears.
- `locator.wait_for(state="detached")` — waits until the element is removed from the DOM.
- `page.wait_for_selector(selector)` — waits for a selector to appear.
- `page.wait_for_function(expression)` — waits until JavaScript returns truthy.
- `page.wait_for_timeout(milliseconds)` — adds a hard delay; avoid in production tests.

---

## 5. User Actions

- `locator.click()` — clicks an element with built-in auto-waiting.
- `locator.fill(value)` — clears and fills an input field.
- `locator.press(key)` — presses keyboard keys like Enter, Escape, Tab.
- `locator.check()` — checks a checkbox or radio button.
- `locator.uncheck()` — unchecks a checkbox.
- `locator.select_option(value)` — selects an option in a dropdown.
- `locator.hover()` — hovers over an element.
- `locator.set_input_files(files)` — uploads files to a file input.

---

## 6. Reading Values & Attributes

- `locator.inner_text()` — returns visible text inside an element.
- `locator.all_inner_texts()` — returns text from all matching elements.
- `locator.get_attribute(name)` — gets an HTML attribute value.
- `locator.is_visible()` — checks whether an element is visible.
- `locator.is_enabled()` — checks if an element is enabled.
- `locator.is_editable()` — checks if an input is editable.
- `page.evaluate(script)` — executes JavaScript inside the browser context.

---

## 7. Handling Multiple Elements

- `locator.all()` — returns all matching elements as a list.
- `locator.count()` — counts the number of matching elements.
- `locator.first()` — targets the first matching element.
- `locator.last()` — targets the last matching element.
- `locator.nth(index)` — targets a specific element by index.
- `locator.filter(**kwargs)` — narrows down matching elements.

---

## 8. Assertions with Playwright Expect

- `expect(locator).to_be_visible()` — asserts an element is visible.
- `expect(locator).to_be_enabled()` — asserts an element is enabled.
- `expect(locator).to_have_text(expected)` — asserts the text matches.
- `expect(locator).to_have_value(value)` — asserts the input value matches.
- `expect(locator).to_have_count(count)` — asserts the number of elements matches.
- `expect(page).to_have_url(url)` — asserts the current URL matches.

---

## 9. UI Components Handling (All-in-One Section)

This section covers the most common UI automation scenarios such as alerts, iframes, uploads, downloads, date pickers, select dropdowns, tabs, new windows, screenshots, forms, clicks, and other interactive UI actions using Playwright’s built-in functions and explicit waits.

- `Alerts / Popups` — use `page.on("dialog")`, `dialog.accept()`, and `dialog.dismiss()`.
- `Iframes` — use `page.frame_locator()` or `page.frame(name)` to switch into embedded frames.
- `File Uploads` — use `locator.set_input_files("path/to/file")` for uploading files.
- `File Downloads` — use `page.wait_for_event("download")` and `download.path()` to handle downloads.
- `Date Picker` — use `locator.fill()` or `locator.click()` with controlled date input selection.
- `Select Dropdown` — use `locator.select_option()` for `<select>` elements.
- `Multiple Tabs / New Windows` — use `context.wait_for_event("page")` or `page.wait_for_event("popup")`.
- `Screenshots` — use `page.screenshot()` or `locator.screenshot()` for visual evidence.
- `Forms / Input Handling` — use `fill()`, `press()`, `check()`, `uncheck()`, and `select_option()`.
- `Clicking & Interaction` — rely on `locator.click()`, `locator.hover()`, and auto-waiting features.
- `Explicit Waits` — use `wait_for_load_state()`, `wait_for_url()`, `locator.wait_for()`, and `expect(...).to_be_visible()` for stability.

> In short: Playwright handles modern UI components efficiently with built-in auto-waiting, robust locators, and simple APIs for forms, dialogs, uploads, downloads, frames, tabs, and screenshots.

---

## 10. Common Interview Notes

- Playwright is faster and more reliable than Selenium for many modern web apps because it uses auto-waiting and browser-native automation.
- `expect()` makes assertions more readable and stable.
- `Locator` is the preferred way to interact with UI elements.
- Use `pytest` with Playwright fixtures for clean test structure.
- Use `conftest.py` for reusable fixtures, setup, and browser context management.

---

## 11. Quick Example

```python
from playwright.sync_api import sync_playwright
from playwright.sync_api import expect

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()
    page.goto("https://example.com")

    page.get_by_text("More information").click()
    expect(page).to_have_url("https://www.iana.org/domains/example")

    browser.close()
```

---

## 12. Very Short Interview Summary

- Use `locator` for UI interactions.
- Use `expect()` for assertions.
- Use `wait_for` methods for synchronization.
- Use `page` and `context` for navigation and multi-tab handling.
- Use `frame_locator()` for iframes and `set_input_files()` for uploads.
