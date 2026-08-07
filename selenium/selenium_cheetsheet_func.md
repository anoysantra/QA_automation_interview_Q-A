# Selenium Python Cheat Sheet for Interviews

> A polished, interview-friendly reference for Selenium with Python, covering browser setup, locators, waits, actions, assertions, and UI handling for real-world automation.

---

## 1. Setup & Browser Management

- `from selenium import webdriver` — imports Selenium WebDriver.
- `webdriver.Chrome()` — launches a Chrome browser instance.
- `webdriver.Firefox()` — launches a Firefox browser instance.
- `webdriver.Edge()` — launches an Edge browser instance.
- `webdriver.ChromeOptions()` — configures browser behavior such as headless mode and downloads.
- `driver.get(url)` — opens a URL in the browser.
- `driver.quit()` — closes the browser and releases resources.
- `driver.close()` — closes the current browser window.

### Common Driver Setup Patterns

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

options = Options()
options.add_argument("--headless=new")
options.add_argument("--window-size=1920,1080")

driver = webdriver.Chrome(options=options)
driver.get("https://example.com")
```

### Driver Management Tips

- Use `webdriver-manager` or a local driver binary for easier setup.
- Prefer `options` over hardcoded browser behavior.
- Close the driver in `finally` or use `try/finally` for cleanup.

---

## 2. Page Navigation & Lifecycle

- `driver.get(url)` — navigates to a page.
- `driver.refresh()` — reloads the current page.
- `driver.back()` — moves to the previous page in history.
- `driver.forward()` — moves to the next page in history.
- `driver.current_url` — returns the current URL.
- `driver.title` — returns the page title.
- `driver.page_source` — returns the full HTML source.
- `driver.switch_to.new_window("tab")` — opens a new tab.
- `driver.switch_to.new_window("window")` — opens a new browser window.

### Navigation Example

```python
driver.get("https://www.google.com")
print(driver.title)
driver.back()
driver.forward()
driver.refresh()
```

---

## 3. Locators in Selenium

Locators are the main way to find UI elements.

### Core Locator Strategies

- `By.ID` — finds an element using its `id` attribute.
- `By.NAME` — finds by `name` attribute.
- `By.CLASS_NAME` — finds by class name.
- `By.TAG_NAME` — finds by HTML tag.
- `By.LINK_TEXT` — finds a link by exact visible text.
- `By.PARTIAL_LINK_TEXT` — finds a link by partial visible text.
- `By.CSS_SELECTOR` — finds elements using CSS selectors.
- `By.XPATH` — finds elements using XPath expressions.

### Finding Elements

- `driver.find_element(by, value)` — returns one matching element.
- `driver.find_elements(by, value)` — returns a list of matching elements.

### Example

```python
from selenium.webdriver.common.by import By

username = driver.find_element(By.ID, "username")
password = driver.find_element(By.NAME, "password")
button = driver.find_element(By.CSS_SELECTOR, "button.submit")
link = driver.find_element(By.PARTIAL_LINK_TEXT, "Sign")
```

### Locator Best Practices

- Prefer `id` and `name` when they are stable and unique.
- Use CSS selectors for readability and speed.
- Use XPath when the DOM structure is complex or dynamic.
- Avoid overly long and fragile XPath expressions.

---

## 4. Explicit Waits & Synchronization

Selenium waits help avoid flaky tests when UI elements appear late.

### Main Wait Types

- `implicit wait` — applies globally to all find operations.
- `explicit wait` — waits for a specific condition.
- `fluent wait` — similar to explicit wait but with polling interval and ignored exceptions.

### WebDriverWait

- `WebDriverWait(driver, timeout)` — waits up to a timeout.
- `wait.until(condition)` — waits until the condition is true.

### Common Expected Conditions (`EC`)

- `EC.presence_of_element_located((By.ID, "id"))`
- `EC.visibility_of_element_located((By.ID, "id"))`
- `EC.element_to_be_clickable((By.ID, "id"))`
- `EC.invisibility_of_element_located((By.ID, "id"))`
- `EC.text_to_be_present_in_element((By.ID, "id"), "text")`
- `EC.text_to_be_present_in_element_value((By.ID, "id"), "value")`
- `EC.alert_is_present()`
- `EC.frame_to_be_available_and_switch_to_it((By.ID, "frame"))`
- `EC.staleness_of(element)`
- `EC.title_contains("title")`
- `EC.url_contains("example")`
- `EC.number_of_windows_to_be(2)`

### Example with Explicit Wait

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By

wait = WebDriverWait(driver, 10)
button = wait.until(EC.element_to_be_clickable((By.ID, "submit-btn")))
button.click()
```

### Fluent Wait Example

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By
from selenium.common.exceptions import TimeoutException

wait = WebDriverWait(driver, 10, poll_frequency=1, ignored_exceptions=[TimeoutException])
element = wait.until(EC.presence_of_element_located((By.ID, "loader")))
```

### Wait Best Practices

- Prefer explicit waits over `time.sleep()`.
- Use waits for dynamic pages, spinners, AJAX, and delayed rendering.
- Avoid mixing too many different wait strategies in one test.

---

## 5. User Actions

- `element.click()` — clicks an element.
- `element.send_keys(value)` — types text into a field.
- `element.clear()` — clears an input field.
- `element.submit()` — submits a form.
- `element.get_property(name)` — gets a DOM property.
- `element.get_attribute(name)` — gets an attribute value.

### Advanced User Actions

- `ActionChains(driver).click()` — chainable click actions.
- `ActionChains(driver).double_click()` — double-click.
- `ActionChains(driver).context_click()` — right-click.
- `ActionChains(driver).move_to_element(element)` — hover.
- `ActionChains(driver).drag_and_drop(source, target)` — drag/drop.
- `ActionChains(driver).key_down(Keys.CONTROL).send_keys("a")` — keyboard shortcuts.

### Example

```python
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.common.keys import Keys

actions = ActionChains(driver)
actions.move_to_element(driver.find_element(By.ID, "menu")).perform()

driver.find_element(By.ID, "search-box").send_keys("Selenium")
driver.find_element(By.ID, "search-box").send_keys(Keys.ENTER)
```

---

## 6. Reading Values & Attributes

- `element.text` — returns the visible text of the element.
- `element.get_attribute("value")` — reads an HTML attribute.
- `element.is_displayed()` — checks whether it is visible.
- `element.is_enabled()` — checks whether it can be used.
- `element.is_selected()` — checks selected state (checkbox/radio/select).
- `element.tag_name` — returns the HTML tag name.
- `element.size` — returns the width and height.

### Example

```python
text = driver.find_element(By.ID, "status").text
value = driver.find_element(By.ID, "email").get_attribute("value")
print(text, value)
```

---

## 7. Handling Multiple Elements

- `driver.find_elements(...)` — returns a list of matching elements.
- `len(elements)` — counts matching elements.
- `elements[0]` — accesses the first element.
- `for el in elements` — iterates through all matches.

### Example

```python
rows = driver.find_elements(By.CSS_SELECTOR, "tbody tr")
print(len(rows))

for row in rows:
    print(row.text)
```

---

## 8. UI Components Handling (All-in-One Section)

This section covers the most common real-world UI scenarios in Selenium.

- `Alerts / Popups` — use `driver.switch_to.alert` and `alert.accept()` / `alert.dismiss()`.
- `Dropdowns` — use `Select(element)` and methods like `select_by_visible_text()`.
- `Checkboxes / Radio Buttons` — use `click()` or `is_selected()`.
- `Frames / Iframes` — use `driver.switch_to.frame()` or `switch_to.default_content()`.
- `Tabs / Windows` — use `driver.window_handles` and `switch_to.window(handle)`.
- `File Uploads` — use `send_keys("/path/to/file")` on `<input type="file">`.
- `Downloads` — validate downloaded files using file system checks or browser-specific settings.
- `Date Pickers` — use `send_keys()` or click-based selection depending on the component.
- `Shadow DOM` — use JavaScript execution or Selenium-supported shadow DOM access if required.
- `Screenshots` — use `driver.save_screenshot("path.png")`.
- `Scrolling` — use JavaScript or ActionChains for scrolling into view.
- `Cookies` — use `driver.get_cookies()` and `driver.add_cookie({...})`.

### Example: Alert Handling

```python
alert = driver.switch_to.alert
print(alert.text)
alert.accept()
```

### Example: Dropdown Handling

```python
from selenium.webdriver.support.ui import Select

select = Select(driver.find_element(By.ID, "country"))
select.select_by_visible_text("India")
```

### Example: Frame Handling

```python
driver.switch_to.frame("frame-name")
# interact with elements inside frame
driver.switch_to.default_content()
```

### Example: Window Handling

```python
handles = driver.window_handles
driver.switch_to.window(handles[1])
```

### Example: Screenshot

```python
driver.save_screenshot("screenshot.png")
```

---

## 9. JavaScript Execution & Advanced Interaction

- `driver.execute_script(script)` — runs JavaScript in the browser context.
- Useful for scrolling, highlighting, modifying DOM values, and handling awkward UI elements.

### Example

```python
driver.execute_script("window.scrollTo(0, document.body.scrollHeight)")
```

### When to Use It

- When standard Selenium methods are not enough.
- For scrolling, lazy-loading, or dynamic UI state.
- Use carefully; prefer native Selenium interactions first.

---

## 10. Cookies, Sessions & Browser State

- `driver.get_cookies()` — returns all cookies.
- `driver.add_cookie(cookie_dict)` — adds a cookie.
- `driver.delete_cookie(name)` — deletes a specific cookie.
- `driver.delete_all_cookies()` — removes all cookies.

### Example

```python
driver.add_cookie({"name": "session", "value": "abc123"})
print(driver.get_cookies())
```

---

## 11. Common Selenium Exceptions

- `NoSuchElementException` — element was not found.
- `StaleElementReferenceException` — element reference is no longer valid.
- `TimeoutException` — wait condition timed out.
- `ElementNotInteractableException` — element exists but cannot be used.
- `ElementClickInterceptedException` — another element blocked the click.
- `InvalidSelectorException` — the locator syntax is invalid.

### How to Handle Them

- Improve waits and locator stability.
- Re-find the element after page refresh or DOM change.
- Use `try/except` for resilience where appropriate.

---

## 12. Page Object Model (POM)

POM is a widely used design pattern in industry automation.

- Keeps locators and methods separate from test logic.
- Improves maintainability and readability.
- Helps scale automation frameworks for large projects.



## 13. Common Interview Notes

- Selenium is a mature and widely used browser automation framework.
- `WebDriverWait` and `expected_conditions` are essential for stable tests.
- Prefer explicit waits over `time.sleep()`.
- Use meaningful and stable locators such as `id`, `name`, or robust CSS selectors.
- Use POM for scalable and maintainable test automation.
- Selenium is still heavily used in enterprise automation, CI/CD pipelines, and legacy systems.

---

## 14. Quick Example

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
try:
    driver.get("https://example.com")
    wait = WebDriverWait(driver, 10)
    heading = wait.until(EC.visibility_of_element_located((By.TAG_NAME, "h1")))
    print(heading.text)
finally:
    driver.quit()
```

---

## 15. Very Short Interview Summary

- Use `find_element` / `find_elements` for locating UI elements.
- Use `WebDriverWait` and `expected_conditions` for synchronization.
- Use `ActionChains` for advanced user interactions.
- Use `Select` for dropdowns and `switch_to` for alerts, frames, and windows.
- Use `execute_script` only when native Selenium methods are insufficient.
