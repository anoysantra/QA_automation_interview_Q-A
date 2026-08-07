# Playwright Python API Comprehensive Cheat Sheet

## 1. Setup & Browser Management
* *sync_playwright()*: Starts a thread-blocking synchronous context manager loop.
* *async_playwright()*: Starts an asynchronous context manager loop for concurrent tasks.
* *playwright.chromium.launch()*: Spawns an isolated Chromium instance. Swap with .firefox or .webkit.
* *browser.new_context()*: Spawns an independent incognito-like sandbox context profile without sharing cookies.
* *browser.new_page()*: Instantiates a new workspace tab directly inside a default context.
* *browser.close()*: Closes the browser instance fully and terminates all tracking tab streams.

## 2. Page Navigation & State Lifecycle
* *page.goto(url)*: Navigates the primary tab window frame directly to the targeted endpoint URL.
* *page.reload()*: Forces a clean server-side data pull, mimicking a manual browser refresh.
* *page.go_back()*: Steps backward exactly one history state step within the active tab context.
* *page.go_forward()*: Progresses forward exactly one history state step within the active tab context.
* *page.set_content(html)*: Programmatically injects and renders custom raw HTML layout structures on-screen.
* *page.wait_for_load_state()*: Halts script execution until state resolves ("load", "domcontentloaded", "networkidle").

## 3. Resilient Modern Locators
* *page.get_by_role(role, **kwargs)*: Tracks elements based on explicit ARIA accessibility roles (e.g., button, heading).
* *page.get_by_text(text)*: Scans the target canvas layout for matching visible plain text string values.
* *page.get_by_label(text)*: Pinpoints form inputs matching semantic HTML <label> association layout tags.
* *page.get_by_placeholder(text)*: Selects text input frames containing matching internal placeholder hint values.
* *page.get_by_alt_text(text)*: Pins graphical elements using descriptive alternative (alt) image text.
* *page.get_by_title(text)*: Isolates targeted nodes leveraging explicit browser hover tooltip title parameters.
* *page.get_by_test_id(id)*: Evaluates QA nodes customized with persistent identifiers (data-testid).
* *page.locator(selector)*: Fallback engine accommodating custom native CSS layouts or multi-layered XPath strings.

## 4. Explicit Waits & Synchronization
* *page.wait_for_url(url)*: Suspends code progression until the browser address matches a target string or regex.
* *locator.wait_for(state="visible")*: Blocks script until the node is rendered, has non-zero dimensions, and is visible.
* *locator.wait_for(state="attached")*: Waits for element creation in the DOM tree regardless of physical visibility.
* *locator.wait_for(state="hidden")*: Halts runtime until an element disappears, goes to zero-pixel size, or detaches.
* *locator.wait_for(state="detached")*: Blocks thread execution until a node is removed or unmounted entirely from the DOM.
* *page.wait_for_selector(selector)*: Legacy method blocking code until a raw query selector matches an active page node.
* *page.wait_for_function(expression)*: Continually evaluates JavaScript inside the browser until it returns truthy.
* *page.wait_for_timeout(milliseconds)*: Hard sleep timer loop. Heavily discouraged in production testing.

## 5. User Action Simulation Engine
* *locator.click()*: Performs a physical click. Checks auto-waiting criteria (visible, enabled, stable, un-intercepted).
* *locator.fill(value)*: Clears existing input field characters instantly and inputs the requested string payload.
* *locator.press(key)*: Triggers specialized keyboard hardware layout actions (e.g., "Enter", "Control+A").
* *locator.check()*: Scroll-aligns, verifies clickability, and checks a checkbox or radio element structure.
* *locator.uncheck()*: Programmatically guarantees that a checkbox element transitions to an unclicked state.
* *locator.select_option(value)*: Intercepts traditional <select> menus to lock matching choices or indexes.
* *locator.hover()*: Moves mouse tracking markers over target coordinates for hovering feedback validations.
* *locator.set_input_files(files)*: Directly mounts file payloads from system paths onto target upload fields.

## 6. Information Harvest & Extraction
* *locator.inner_text()*: Grabs the parsed, user-visible plain text currently rendered within an element.
* *locator.all_inner_texts()*: Evaluates a query and gathers an array containing text data across every single match.
* *locator.get_attribute(name)*: Pulls live parameters bound to HTML structural specifications (like href or src).
* *locator.is_visible()*: Instantly returns a boolean stating whether an element appears visually on-screen right now.
* *locator.is_enabled()*: Confirms if an interactive element is currently unlocked and functional.
* *locator.is_editable()*: Evaluates whether form fields allow text edits or values processing.
* *page.evaluate(script)*: Injects and executes custom JavaScript logic directly in the target browser window context.

## 7. Dynamic List Collections Handling
* *locator.all()*: Evaluates multi-element lists and unpacks them into standard, iterable Python object collections.
* *locator.count()*: Measures the total matching element density currently residing inside active frames.
* *locator.first()*: Filters search criteria down to isolate only the earliest index matching instance.
* *locator.last()*: Filters search criteria down to isolate only the final index matching instance.
* *locator.nth(index)*: Targets a specific position in the element collection using a 0-indexed integer parameter.
* *locator.filter(**kwargs)*: Refines search results by matching specific inner text or child element criteria.

## 8. Fluent Smart Test Assertions
* *expect(locator).to_be_visible()*: Loops element inspection checks until the targeted node is rendered visible.
* *expect(locator).to_be_enabled()*: Verifies that an element matches interactive states, emerging from a disabled profile.
* *expect(locator).to_have_text(expected)*: Asserts that an element's text content matches a given string or regex.
* *expect(locator).to_have_value(value)*: Confirms whether text inputs match target values.
* *expect(locator).to_have_count(count)*: Asserts that dynamic arrays or tables contain an exact number of child elements.
* *expect(page).to_have_url(url)*: Validates that the active browser location string exactly matches the expected URL destination schema.
# Playwright Python API Comprehensive Cheat Sheet


