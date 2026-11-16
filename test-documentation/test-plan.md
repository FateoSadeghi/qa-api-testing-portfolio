
# Test Plan
## Tool Rental API – Quality Assurance & Automation Testing

| Document Information | Details |
|---|---|
| Project Name | Tool Rental API |
| Document Type | Software Test Plan |
| Version | 1.0 |
| Status | Draft |
| Testing Type | API Functional Testing |
| Testing Approach | Manual & Automated |
| Primary Tool | Postman |
| Scripting Language | JavaScript |
| API Type | REST API |
| Base URL | https://simple-tool-rental-api.click |

---

## 1. Introduction

### 1.1 Purpose

The purpose of this test plan is to define the testing strategy, scope, objectives, resources, and execution approach for validating the Tool Rental API.

The testing process aims to verify that the API endpoints behave as expected, return appropriate HTTP status codes, process valid and invalid requests correctly, and maintain data consistency throughout the order lifecycle.

### 1.2 Project Overview

The Tool Rental API is an educational REST API that allows users to retrieve available tools, register API clients, and manage rental orders.

The existing Postman collection provides a basic automated testing workflow covering API health checks, tool retrieval, client registration, and order management.

### 1.3 Testing Objectives

The main testing objectives are:

- Verify API endpoint availability.
- Validate HTTP response status codes.
- Verify response body structure and data.
- Validate authentication and authorization.
- Test positive and negative scenarios.
- Verify CRUD operations.
- Validate order creation and update operations.
- Verify order deletion.
- Identify and document defects.
- Evaluate API reliability and data consistency.

---

## 2. Scope of Testing

### 2.1 In-Scope

The following functionalities are included in the testing scope.

| Feature | Description |
|---|---|
| API Health Check | Verify API availability |
| Tool Retrieval | Retrieve all tools |
| Tool Details | Retrieve a specific tool |
| Client Registration | Register a test API client |
| Authentication | Validate Bearer Token authentication |
| Create Order | Create a new rental order |
| Retrieve Orders | Retrieve all orders |
| Order Details | Retrieve a specific order |
| Update Order | Modify existing order information |
| Delete Order | Delete an existing order |
| Deletion Verification | Verify that deleted orders are inaccessible |

### 2.2 Out-of-Scope

The following areas are not included in the initial testing phase:

- User interface testing.
- Mobile application testing.
- Payment gateway testing.
- Performance and load testing.
- Security penetration testing.
- Production environment testing.
- Third-party integrations.

These areas may be considered in future testing phases.

---

## 3. Test Strategy

The project follows a combination of manual and automated API testing approaches.

### 3.1 Functional Testing

Validate whether API endpoints perform their intended operations.

Examples:
- Retrieve available tools.
- Create rental orders.
- Update customer information.
- Delete existing orders.

### 3.2 Positive Testing

Verify API behavior when valid input data is provided.

Examples:
- Retrieve tools using a valid category.
- Create an order using a valid tool ID.
- Retrieve an existing order using a valid order ID.

### 3.3 Negative Testing

Verify API behavior when invalid or unexpected input is provided.

Planned scenarios include:
- Invalid tool ID.
- Invalid order ID.
- Missing required fields.
- Invalid request payload.
- Missing authentication token.
- Invalid authentication token.

Expected responses must be verified against the API contract or documented behavior before assigning pass/fail results.

### 3.4 Authentication Testing

Verify that protected endpoints require valid authentication.

The existing collection uses Bearer Token authentication through the `apiToken` variable.

### 3.5 Data Validation Testing

Validate the correctness and consistency of API request and response data.

Examples:
- Verify returned tool IDs.
- Verify tool stock availability.
- Verify generated order IDs.
- Verify updated customer information.
- Verify order deletion.

### 3.6 Automated Testing

Postman and JavaScript will be used to automate API validation.

The following Postman features will be used:

- `pm.test()`
- `pm.expect()`
- `pm.response.json()`
- `pm.environment.get()`
- `pm.environment.set()`
- `pm.response.to.have.status()`

Note: The existing collection currently uses global variables for `toolId` and `orderId`. Variable scope will be reviewed and standardized during test automation improvements.

---

## 4. Test Environment

### 4.1 Environment Configuration

| Configuration | Value |
|---|---|
| Environment | Educational / Test |
| API Base URL | https://simple-tool-rental-api.click |
| Testing Tool | Postman |
| Scripting | JavaScript |
| Authentication | Bearer Token |
| Data Format | JSON |
| Version Control | GitHub |

### 4.2 Required Variables

| Variable | Description | Initial Value |
|---|---|---|
| baseUrl | API base URL | https://simple-tool-rental-api.click |
| apiToken | Authentication token | Empty |
| category | Tool category | trailers |
| toolId | Selected tool ID | Generated during testing |
| orderId | Created order ID | Generated during testing |

### 4.3 Test Data

The project will use fictional test data.

Examples:
- Random customer names.
- Test client email addresses.
- Valid tool IDs retrieved from the API.
- Generated order IDs.

No production customer information will be used.

---

## 5. Test Scenarios

The following scenarios define the initial functional test coverage.

| Test ID | Test Scenario | Priority |
|---|---|---|
| TS-001 | Verify API health status | High |
| TS-002 | Retrieve all tools | High |
| TS-003 | Retrieve tools by category | High |
| TS-004 | Retrieve a single tool | High |
| TS-005 | Verify tool availability | High |
| TS-006 | Register a new API client | High |
| TS-007 | Create a new rental order | High |
| TS-008 | Retrieve all orders | High |
| TS-009 | Retrieve a single order | High |
| TS-010 | Update an existing order | High |
| TS-011 | Verify updated order information | High |
| TS-012 | Delete an existing order | High |
| TS-013 | Verify deleted order is inaccessible | High |
| TS-014 | Submit a request without authentication | Medium |
| TS-015 | Submit a request with an invalid token | Medium |
| TS-016 | Submit an invalid tool ID | Medium |
| TS-017 | Submit an invalid order ID | Medium |
| TS-018 | Submit a request with missing fields | Medium |
| TS-019 | Submit an invalid JSON payload | Medium |
| TS-020 | Verify response body structure | Medium |

Note: TS-014 to TS-020 are planned scenarios and are not included in the original collection as implemented tests.

---

## 6. Entry Criteria

Testing can begin when the following conditions are met:

- The API endpoint is accessible.
- Postman is installed and configured.
- The Postman collection is imported.
- Required variables are configured.
- A valid API client is registered.
- A valid authentication token is available.
- Test data is prepared.

## 7. Exit Criteria

The testing phase can be considered complete when:

- All planned test cases have been executed.
- All critical test scenarios have been evaluated.
- Actual and expected results have been documented.
- Failed test cases have been investigated.
- Identified defects have been documented.
- Test execution results have been reviewed.
- A final test execution report has been prepared.

Any unexecuted tests or unresolved defects must be explicitly documented.

---

## 8. Risks and Mitigation

| Risk | Impact | Mitigation |
|---|---|---|
| API downtime | High | Verify API health before execution |
| Invalid authentication token | High | Validate token configuration |
| Stale global variables | Medium | Reset variables before each run |
| Missing test data | Medium | Generate test data dynamically |
| Incorrect test assertions | High | Review expected results against API behavior |
| Test execution dependency | Medium | Execute requests in the correct sequence |
| Shared test data conflicts | Medium | Use isolated test data and cleanup |

### 8.1 Test Execution Dependencies

The existing Postman collection contains dependencies between requests.

The intended workflow is:

1. Verify API status.
2. Retrieve available tools.
3. Save a valid tool ID.
4. Retrieve the selected tool.
5. Register a test API client manually.
6. Store the returned access token.
7. Create a rental order.
8. Retrieve all orders.
9. Retrieve the created order.
10. Update the order.
11. Delete the order.
12. Verify that the order no longer exists.

Important: The existing collection includes a `setNextRequest()` instruction that skips client registration during Collection Runner execution. Registration is intended to be completed manually before running the remaining workflow.

---

## 9. Test Deliverables

The following deliverables will be maintained in the GitHub repository:

| Deliverable | File |
|---|---|
| Test Plan | test-plan.md |
| Test Scenarios | test-scenarios.md |
| Test Cases | test-cases.md |
| Bug Reports | bug-reports.md |
| Postman Collection | tool-rental-api.postman_collection.json |
| Test Execution Report | execution-report.md |
| Screenshots | screenshots/ |

---

## 10. Defect Management

All identified defects will be documented with the following information:

- Bug ID
- Bug Title
- Environment
- Preconditions
- Steps to Reproduce
- Expected Result
- Actual Result
- Severity
- Priority
- Status
- Supporting Evidence

Defects will only be reported after they have been reproduced and verified.

---

## 11. Test Execution and Reporting

Postman Collection Runner will be used for executing automated API test requests.

Test execution results will be reviewed based on:

- Total executed tests.
- Passed tests.
- Failed tests.
- Skipped tests.
- API response status codes.
- Assertion results.
- Identified defects.

Newman may be introduced in a later phase to support command-line execution and CI/CD integration.

---

## 12. Future Improvements

The following improvements are planned for future project iterations:

- Expand negative test coverage.
- Add response schema validation.
- Improve JavaScript assertions.
- Standardize environment variables.
- Implement automated test data cleanup.
- Integrate Newman.
- Generate HTML test reports.
- Integrate GitHub Actions.
- Introduce API regression testing.

---

## 13. Conclusion

This test plan establishes a structured approach to validating the Tool Rental API.

It provides a foundation for functional testing, negative testing, authentication validation, data verification, and API automation.

The project will evolve through additional test scenarios, improved automation scripts, defect documentation, and continuous testing practices.

**Document Status:** Draft – Pending Test Case Design and Execution.

**Project:** Tool Rental API – QA & Automation Testing
