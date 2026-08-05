# General Testing Concepts Interview Answers

This file covers common manual and automation testing concepts asked in entry-level QA interviews.

## 1) What is functional testing?

### Definition
Functional testing checks whether the application works as expected according to business requirements.

### Technical explanation
The tester validates features such as login, search, add to cart, checkout, and form submissions.

### Why it is used
It ensures the application performs the intended actions correctly.

### Real-world example
Testing that a login form accepts a valid username and password and shows the correct dashboard.

### Common follow-up questions
- What is the difference between functional and non-functional testing?
- Which tools are used for functional automation?

### Key points to remember
- Functional testing checks what the system should do.
- It is usually driven by requirements or user stories.

---

## 2) What is non-functional testing?

### Definition
Non-functional testing checks how the system behaves under different conditions, not just whether the feature works.

### Technical explanation
It covers reliability, performance, usability, security, and compatibility.

### Why it is used
A system may work functionally but still be slow, unstable, or difficult to use.

### Real-world example
Checking whether a website loads under 2 seconds during peak traffic is a performance concern.

### Common follow-up questions
- What kinds of non-functional testing exist?
- Why do recruiters ask this question often?

### Key points to remember
- Functional = does it work?
- Non-functional = how well does it work?

---

## 3) What is load testing?

### Definition
Load testing checks how the application behaves under expected user load.

### Technical explanation
It simulates normal traffic levels to see whether the system stays stable and fast.

### Why it is used
To verify that typical usage is handled comfortably.

### Real-world example
Testing a shopping website during a normal sales day with 5,000 simultaneous users.

### Common follow-up questions
- How is load testing different from stress testing?
- What metrics do we usually observe?

### Key points to remember
- Load testing uses normal expected traffic.
- It helps find performance bottlenecks before peak usage.

---

## 4) What is stress testing?

### Definition
Stress testing pushes the system beyond its normal limit to see how it fails and recovers.

### Technical explanation
The goal is not just to break the app, but to learn how it behaves when overloaded.

### Why it is used
It helps identify failure points and recovery behavior.

### Real-world example
Simulating 50,000 users on a site designed for 5,000 users to observe errors, timeouts, or crashes.

### Common follow-up questions
- What happens if the system crashes under stress?
- What is the difference between spike testing and stress testing?

### Key points to remember
- Stress testing is about pushing the system beyond its intended threshold.
- The aim is to understand failure behavior and resilience.

---

## 5) What is smoke testing?

### Definition
Smoke testing is a quick, high-level test run to confirm that the most important functions of the application work after a build.

### Technical explanation
A smoke suite is small and fast. If it fails, the build is usually rejected and deeper testing is not worth starting.

### Why it is used
It saves time by catching obvious breakages early.

### Real-world example
Checking that the app launches, the homepage loads, and the user can login.

### Common follow-up questions
- Is smoke testing manual or automated?
- What is the difference between smoke and sanity testing?

### Key points to remember
- Smoke test = broad but shallow.
- It validates the build is stable enough for more testing.

---

## 6) What is sanity testing?

### Definition
Sanity testing is a narrow, focused check after a small code change or bug fix.

### Technical explanation
Unlike smoke testing, sanity testing is more targeted and verifies that the specific fix works.

### Why it is used
It quickly confirms whether the recent issue has been resolved without doing a full regression cycle.

### Real-world example
If a bug fix changed the password reset flow, the sanity test may only validate that reset flow and its immediate outcome.

### Common follow-up questions
- Why is sanity testing faster than regression testing?
- How is it different from smoke testing?

### Key points to remember
- Smoke test = overall build health.
- Sanity test = specific fix verification.

---

## 7) What is regression testing?

### Definition
Regression testing checks previously working functionality to ensure a new change did not break it.

### Technical explanation
Whenever code is changed, the risk of unintended side effects exists. Regression testing helps catch those issues.

### Why it is used
It protects existing features and reduces release risk.

### Real-world example
After a developer changes a checkout flow, regression testing ensures add-to-cart and payment steps still work.

### Common follow-up questions
- What kinds of tests are usually part of regression testing?
- Why is automation important for regression suites?

### Key points to remember
- Regression testing protects stability.
- It is usually automated in modern QA teams.

---

## 8) What is black-box testing?

### Definition
Black-box testing checks the software from the outside without knowing its internal code.

### Technical explanation
The tester focuses only on input and output behavior.

### Why it is used
It mirrors the end-user perspective.

### Real-world example
A QA tester validates that entering valid credentials logs the user in, without checking the backend logic.

### Common follow-up questions
- What is the difference between black-box and white-box testing?
- Which approach is more common in QA automation?

### Key points to remember
- Black-box testing is input/output focused.
- It does not require internal code knowledge.

---

## 9) What is white-box testing?

### Definition
White-box testing is performed with knowledge of the internal logic, structure, and code of the application.

### Technical explanation
It is often used by developers and helps test branch coverage, loops, decision paths, and code-level behavior.

### Why it is used
It improves confidence that internal logic behaves correctly.

### Real-world example
Testing a function that calculates discounts using multiple possible input values and logical branches.

### Common follow-up questions
- Do QA engineers usually perform white-box testing?
- What is the role of code coverage in white-box testing?

### Key points to remember
- White-box testing requires code knowledge.
- It is more common in unit testing and development practices.

---

## 10) What is gray-box testing?

### Definition
Gray-box testing is a middle ground between black-box and white-box testing.

### Technical explanation
The tester has partial knowledge of the internal structure, such as database tables, APIs, or application architecture, but still tests from the outside.

### Why it is used
It allows better test design without needing full access to source code.

### Real-world example
A QA engineer knows that a page calls an API endpoint and uses that knowledge to design sharper negative tests.

### Common follow-up questions
- When would gray-box testing be chosen?
- How is it different from exploratory testing?

### Key points to remember
- Gray-box testing combines external behavior with some internal knowledge.
- It is useful for targeted, high-risk testing.

---

## 11) What is exploratory testing?

### Definition
Exploratory testing is an unscripted, learning-based way of testing where the tester explores the app while designing and executing test cases at the same time.

### Technical explanation
It is useful for finding hidden issues that predefined scripts may miss.

### Why it is used
It helps testers think like users and discover bugs in new or unfamiliar areas.

### Real-world example
A tester clicks through a workflow in unexpected ways to find issues in validation messages or navigation.

### Common follow-up questions
- Can exploratory testing be formalized in an interview?
- Why is it useful in Agile teams?

### Key points to remember
- It is flexible and discovery-driven.
- It complements scripted testing rather than replacing it.

---

## 12) What is the defect life cycle?

### Definition
The defect life cycle is the process a bug goes through from identification to closure.

### Technical explanation
A common flow is:
- New
- Assigned
- Open
- Fixed
- Retest
- Closed

### Why it is used
It gives the team a standard workflow for managing bugs.

### Real-world example
A tester reports a login bug, the developer fixes it, QA retests it, and the bug is closed if resolved.

### Common follow-up questions
- What happens if the bug is not reproducible?
- Why is retesting important?

### Key points to remember
- A bug moves through a structured lifecycle.
- Clear status tracking helps teams manage quality effectively.

---

## 13) What is the difference between a test plan, test case, and test scenario?

### Definition
These three concepts are related but different.

### Technical explanation
- Test plan → high-level document describing the testing approach, scope, and schedule.
- Test scenario → a high-level business situation to be tested.
- Test case → a step-by-step procedure with inputs, expected results, and pass/fail criteria.

### Why it is used
They help organize testing from strategy to execution.

### Real-world example
A test scenario may be “User logs in successfully.” The test case then lists the exact steps and expected result.

### Common follow-up questions
- Which one is most detailed?
- Which is created first?

### Key points to remember
- Plan = strategy
- Scenario = what to test
- Case = exact steps and expected outcome

---

## 14) What is test case design and why is it needed?

### Definition
Test case design means deciding how to create test cases that cover important behaviors and risk areas.

### Technical explanation
Common techniques include:
- Boundary Value Analysis (BVA)
- Equivalence Partitioning
- Decision Table

### Why it is used
These techniques help make test coverage better and avoid missing critical input combinations.

### Real-world example
If a field accepts ages between 18 and 65, BVA may test 17, 18, 64, 65, and 66.

### Common follow-up questions
- What is boundary value analysis?
- Why use equivalence partitioning?

### Key points to remember
- Good test design saves time and improves coverage.
- These techniques are frequently asked in interviews.

---

## 15) What is Agile, Scrum, and JIRA?

### Definition
These are commonly used concepts in modern software teams.

### Technical explanation
- Agile is a delivery approach based on iterative development.
- Scrum is a framework inside Agile for organizing work in sprints.
- JIRA is a tool used to manage tickets, stories, bugs, and sprints.

### Why it is used
They help teams deliver in smaller, frequent releases and keep work visible.

### Real-world example
A team works in 2-week sprints, creates stories in JIRA, and updates their testing progress daily.

### Common follow-up questions
- Why is Agile important for QA?
- What does a sprint mean in Scrum?

### Key points to remember
- QA works closely with Agile teams to provide fast feedback.
- JIRA is commonly used for tracking requirements and defects.
