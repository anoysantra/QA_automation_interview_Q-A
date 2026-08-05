# API Testing Interview Answers

This file converts the API interview questions into beginner-friendly, interview-ready answers for entry-level QA Automation roles.

## 1) What is an API?

### Definition
An API (Application Programming Interface) is a way for two software systems to communicate with each other.

### Technical explanation
APIs define the rules for requests and responses. A client sends a request, and a server returns a response. In testing, we usually check the request format, response status, response body, and headers.

### Why it is used
APIs are used because they let applications exchange data without relying on a user clicking through the UI. For example, the frontend can request product data from the backend through an API.

### Real-world example
When you open an e-commerce website, the frontend may call an API like `/products` to fetch product names and prices.

### Python code example
```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/posts/1")
print(response.status_code)
print(response.json())
```

### Common follow-up questions
- What is the difference between UI testing and API testing?
- Which HTTP methods are commonly used in API automation?
- How do you validate the response structure?

### Key points to remember
- API testing checks the backend contract.
- You usually validate status code, headers, and response body.
- API testing is faster and more stable than testing only through the UI.

---

## 2) What are common HTTP methods in API testing?

### Definition
HTTP methods define the type of action the client wants to perform on a resource.

### Technical explanation
The main methods are:
- `GET` → fetch data
- `POST` → create data
- `PUT` → replace/update the full resource
- `PATCH` → partial update
- `DELETE` → remove data

### Why it is used
These methods map to common business actions in web applications.

### Real-world example
A login page may use `POST /login`, while fetching order details may use `GET /orders/123`.

### Python code example
```python
import requests

get_resp = requests.get("https://jsonplaceholder.typicode.com/posts/1")
post_resp = requests.post(
    "https://jsonplaceholder.typicode.com/posts",
    json={"title": "QA", "body": "Automation", "userId": 1}
)
print(get_resp.status_code)
print(post_resp.status_code)
print(post_resp.json())
```

### Common follow-up questions
- What is the difference between `PUT` and `PATCH`?
- Which status code indicates success for a `GET` request?
- When would you prefer `PATCH` over `PUT`?

### Key points to remember
- `GET` should not change data.
- `POST` is typically used to create.
- `PATCH` is used for small updates.

---

## 3) What are common API status codes?

### Definition
HTTP status codes tell the client whether the request succeeded, failed, or needs further action.

### Technical explanation
Common examples:
- `200` → OK
- `201` → Created
- `204` → No Content
- `400` → Bad Request
- `401` → Unauthorized
- `403` → Forbidden
- `404` → Not Found
- `429` → Too Many Requests
- `500` → Internal Server Error

### Why it is used
Status codes help us quickly understand the result of an API call.

### Real-world example
If a user submits missing login data, the server may return `400 Bad Request`.

### Python code example
```python
import requests

resp = requests.get("https://jsonplaceholder.typicode.com/nonexistent")
print(resp.status_code)
```

### Common follow-up questions
- What does `429 Too Many Requests` mean?
- When do you expect `401` vs `403`?
- Why is checking status code important in automation?

### Key points to remember
- A `2xx` response means success.
- A `4xx` response usually means the client did something wrong.
- A `5xx` response means the server failed.

---

## 4) What is the difference between `json=payload` and `data=payload` in `requests`?

### Definition
Both send request data, but they are encoded differently.

### Technical explanation
- `json=payload` sends the payload as JSON.
- `data=payload` sends form-encoded data or raw bytes, depending on the content.

### Why it is used
Use `json=` when the API expects JSON. Use `data=` when the server expects form data such as `application/x-www-form-urlencoded`.

### Real-world example
A REST API may expect JSON bodies for `POST` requests, while a login form may submit form data.

### Python code example
```python
import requests

payload = {"name": "Alice", "job": "QA"}

resp_json = requests.post("https://reqres.in/api/users", json=payload)
print(resp_json.status_code)
print(resp_json.json())

resp_data = requests.post(
    "https://httpbin.org/post",
    data={"name": "Alice", "job": "QA"}
)
print(resp_data.status_code)
print(resp_data.text)
```

### Common follow-up questions
- Which one is preferred for REST APIs?
- What happens if the server expects JSON but you send form data?
- Can `data=` be used with nested dictionary payloads?

### Key points to remember
- `json=` is the normal choice in modern REST API automation.
- `data=` is more common for form submissions.

---

## 5) How do you pass dynamic query parameters and headers in an API test?

### Definition
Dynamic query parameters are values added to the URL at runtime, and headers are metadata sent with the request.

### Technical explanation
You can build query strings dynamically from variables such as test data, dates, or user IDs. Headers may include `Authorization`, `Content-Type`, and custom metadata.

### Why it is used
This helps you create reusable tests for different users, environments, and authentication flows.

### Real-world example
A request to fetch user bookings may use a dynamic user ID in the URL and a bearer token in the header.

### Python code example
```python
import requests

base_url = "https://reqres.in/api/users"
params = {"page": 2}
headers = {
    "Authorization": "Bearer sample_token",
    "Content-Type": "application/json"
}

response = requests.get(base_url, params=params, headers=headers)
print(response.status_code)
print(response.json())
```

### Common follow-up questions
- How do you avoid hardcoding tokens in your test suite?
- What is the difference between query parameters and headers?
- How do you pass environment-specific values?

### Key points to remember
- Query parameters are part of the URL.
- Headers are separate and usually include auth and content rules.

---

## 6) How do you handle a chained API test where output of API #1 is required for API #2?

### Definition
A chained API test means the response of one API call is used as input for the next request.

### Technical explanation
This is common in login flows or workflows where the first API returns an ID or token that must be used in the next request.

### Why it is used
It simulates a real user journey and validates the dependency between multiple APIs.

### Real-world example
Login API returns a token; the next API uses that token to fetch user profile details.

### Python code example
```python
import requests

login_resp = requests.post(
    "https://reqres.in/api/login",
    json={"email": "eve.holt@reqres.in", "password": "cityslicka"}
)
login_data = login_resp.json()

token = login_data.get("token")

profile_resp = requests.get(
    "https://reqres.in/api/users/2",
    headers={"Authorization": f"Bearer {token}"}
)

print(profile_resp.status_code)
print(profile_resp.json())
```

### Common follow-up questions
- What if the first API response is empty or invalid?
- How do you handle failures in intermediate steps?
- What is a good assertion for chained API tests?

### Key points to remember
- Always validate that the first response is successful before continuing.
- Use the returned field carefully and assert it exists.

---

## 7) How do you validate the response body?

### Definition
Response body validation means checking that the API response contains the expected structure and values.

### Technical explanation
You usually validate:
- response is JSON or text
- expected keys exist
- required fields have expected values
- response data matches the business rule

### Why it is used
It confirms that the API is not only returning a successful status, but also returning the correct payload.

### Real-world example
A `GET /users/1` API should return a JSON object with fields like `id`, `name`, and `email`.

### Python code example
```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/users/1")
body = response.json()

assert response.status_code == 200
assert body["id"] == 1
assert "name" in body
assert "email" in body
```

### Common follow-up questions
- Why not only check the status code?
- How do you handle optional fields?
- What is schema validation?

### Key points to remember
- Status code alone is not enough.
- Response validation should match the expected contract.

---

## 8) What is JSON schema validation?

### Definition
Schema validation checks whether the response structure matches a predefined expected format.

### Technical explanation
A JSON schema describes the keys, data types, and sometimes nested structure of the response. Libraries like `jsonschema` help validate the response automatically.

### Why it is used
It catches contract mismatches early, especially when APIs evolve.

### Real-world example
If the API is expected to return an object with `id` as an integer and `name` as a string, schema validation ensures that contract is maintained.

### Python code example
```python
import requests
from jsonschema import validate

response = requests.get("https://jsonplaceholder.typicode.com/users/1")
body = response.json()

schema = {
    "type": "object",
    "required": ["id", "name", "email"],
    "properties": {
        "id": {"type": "integer"},
        "name": {"type": "string"},
        "email": {"type": "string"}
    }
}

validate(instance=body, schema=schema)
print("Schema validation passed")
```

### Common follow-up questions
- What is the difference between manual assertion and schema validation?
- When should you prefer schema validation?
- Can it validate nested objects?

### Key points to remember
- Schema validation is powerful for contract checks.
- It is especially useful for large response payloads.

---

## 9) What is negative API testing?

### Definition
Negative API testing checks how the API behaves when invalid or incomplete input is provided.

### Technical explanation
Examples include:
- wrong data type
- missing required headers
- invalid auth token
- missing required fields
- invalid URL path

### Why it is used
It helps reveal whether the system fails safely and returns meaningful error messages.

### Real-world example
Sending a `POST` request without a required `Authorization` header should return `401` or `403` instead of processing the request.

### Python code example
```python
import requests

response = requests.post(
    "https://reqres.in/api/login",
    json={"email": "eve.holt@reqres.in"}
)

print(response.status_code)
print(response.text)
```

### Common follow-up questions
- What status codes are expected in negative cases?
- How do you decide whether the API behavior is correct?
- Why is error handling important in QA?

### Key points to remember
- Negative testing proves the software handles bad input gracefully.
- The response should be predictable and helpful.

---

## 10) What is rate limiting and what does `429` mean?

### Definition
Rate limiting is a server-side control that restricts how many requests a client can send in a given time window.

### Technical explanation
When the limit is exceeded, the server may respond with `429 Too Many Requests`.

### Why it is used
This protects the server from abuse, accidental overuse, or traffic spikes.

### Real-world example
A public API may allow only 100 requests per minute from the same IP or token.

### Python code example
```python
import requests

for _ in range(5):
    response = requests.get("https://httpbin.org/rate-limit/1")
    print(response.status_code)
```

### Common follow-up questions
- How would you test this in automation?
- What should the test assert if the server returns `429`?
- Can rate limits be environment-specific?

### Key points to remember
- `429` means the client sent too many requests.
- It is a server-side safety mechanism.

---

## 11) How do sessions, cookies, and JWT tokens work in API tests?

### Definition
These are different ways a server can remember or authorize a user during requests.

### Technical explanation
- `Session` stores cookies and connection state across requests.
- `Cookies` are small data pieces saved by the browser or client.
- `JWT` is a token that carries identity information and is usually sent in the `Authorization` header.

### Why it is used
They help keep a user logged in and allow secure access to protected resources.

### Real-world example
After login, a website may return a JWT token that must be sent with every request to access account data.

### Python code example
```python
import requests

session = requests.Session()
login_resp = session.post(
    "https://reqres.in/api/login",
    json={"email": "eve.holt@reqres.in", "password": "cityslicka"}
)
print(login_resp.status_code)

profile_resp = session.get("https://reqres.in/api/users/2")
print(profile_resp.status_code)
```

### Common follow-up questions
- Why are cookies important in browser-based flows?
- How is JWT different from a session cookie?
- What is the best way to store tokens in automation?

### Key points to remember
- Tokens and cookies are used to maintain identity and access control.
- In automation, avoid hardcoding secrets or credentials.

---

## 12) What is Postman and why is it useful?

### Definition
Postman is a popular tool for manually testing APIs.

### Technical explanation
It lets a tester send requests, inspect responses, organize collections, and test APIs without writing code first.

### Why it is used
Postman is helpful for quickly validating endpoints, checking payloads, and trying different headers and parameters.

### Real-world example
A QA engineer uses Postman to test a new `/register` API and verify the expected JSON response before automating it with Python.

### Common follow-up questions
- Why use Postman before writing Python automation?
- Can Postman be used to generate API test scripts?
- Is Postman enough for full automation?

### Key points to remember
- Postman is good for manual exploration and debugging.
- Automation frameworks like `requests` or Playwright are used when you need repeatable test execution.

---

## Follow-up Question 1: What is the difference between UI testing and API testing?

### Definition
UI testing validates the visible user interface, while API testing validates the backend communication between applications.

### Technical explanation
UI tests interact with buttons, forms, and pages. API tests interact with endpoints, request methods, and response payloads.

### Why it is used
UI tests confirm user experience, while API tests confirm system logic and backend correctness.

### Real-world example
A UI test may verify that a login button works. An API test may verify that the login endpoint returns a valid token.

### Common follow-up questions
- Which one is faster to automate?
- Which one is more stable for regression testing?

### Key points to remember
- UI testing checks what the user sees.
- API testing checks what the application sends and receives.

---

## Follow-up Question 2: Why is checking the status code important in API automation?

### Definition
A status code tells you whether an API request succeeded, failed, or needs additional action.

### Technical explanation
Automation should not only verify that a response came back, but also that the response belongs to the expected outcome.

### Why it is used
It helps quickly identify whether the request passed or failed and whether the problem is on the client or server side.

### Real-world example
A `200` response for a user profile request is expected, while a `401` response means the user is not authorized.

### Common follow-up questions
- What is the difference between `4xx` and `5xx` statuses?
- Can a test be considered successful even if the body is wrong?

### Key points to remember
- Status code is the first layer of API validation.
- It gives immediate insight into the result of the request.

---

## Follow-up Question 3: Why do we use authentication headers in API testing?

### Definition
Authentication headers provide proof that the client is allowed to access a protected resource.

### Technical explanation
Headers such as `Authorization: Bearer <token>` are commonly added to requests to identify the user or service making the call.

### Why it is used
They protect endpoints and help verify that the caller is legitimate.

### Real-world example
A test may send a bearer token to access a profile endpoint that should only work for logged-in users.

### Common follow-up questions
- What happens when the token is invalid?
- Why is it important to avoid hardcoding secrets in code?

### Key points to remember
- Headers carry metadata and authentication data.
- Use secure and environment-safe token handling in automation.
