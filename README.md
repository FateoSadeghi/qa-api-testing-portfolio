# Tool Rental API – QA & Automation Testing

## Project Overview

This project demonstrates practical Software Quality Assurance skills through functional and automated testing of the Simple Tool Rental API.

The project focuses on API validation, positive and negative testing, authentication, CRUD operations, and automated test assertions using Postman and JavaScript.

## Objectives

- Validate API endpoints and HTTP response codes.
- Verify request and response data.
- Test authentication and authorization.
- Perform positive and negative API testing.
- Validate CRUD operations.
- Identify and document potential defects.
- Generate and analyze test execution reports.

## Tech Stack

| Tool / Technology | Purpose |
|---|---|
| Postman | API testing |
| JavaScript | Automated test assertions |
| REST API | API communication |
| JSON | Request and response data |
| Git & GitHub | Version control and documentation |
| Newman | Command-line test execution (planned) |

## API Under Test

**Application:** Simple Tool Rental API

**Base URL:** `https://simple-tool-rental-api.click`

## Test Coverage

### Existing Collection Coverage

- API health check
- Retrieve all tools
- Retrieve a single tool
- Register an API client
- Create an order
- Retrieve all orders
- Retrieve a single order
- Update an order
- Delete an order
- Verify order deletion

### Planned Additional Coverage

- Invalid request payloads
- Missing required fields
- Invalid authentication token
- Unauthorized requests
- Invalid tool IDs
- Invalid order IDs
- Boundary and negative testing
- Response body validation
- Data persistence after updates

## Repository Structure

```text
qa-api-testing-portfolio/
├── README.md
├── postman/
├── test-documentation/
├── test-results/
├── screenshots/
└── .gitignore
```

## How to Run

1. Install Postman.
2. Import the Postman collection.
3. Configure the required collection variables.
4. Register a test API client.
5. Store the returned access token in the local `apiToken` variable.
6. Execute the requests in the documented order.
7. Review the test results.

## Test Execution

Test execution results, including passed and failed assertions, will be documented in the `test-results` directory after actual execution.

## Quality Assurance Approach

This project follows a structured QA approach:

1. Requirement and API analysis
2. Test planning
3. Test scenario design
4. Test case development
5. Test execution
6. Defect reporting
7. Test result analysis

## Disclaimer

This is an educational portfolio project. Test data is fictional, and no production customer data is used.

## Author

Software QA Engineer | API Testing | Manual Testing | Test Automation

**Note:** This repository is continuously evolving as new test scenarios, automation scripts, and documentation are added.
