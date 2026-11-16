# API Test Cases – Tool Rental API

## Document Information

| Field | Value |
|---|---|
| Project | Tool Rental API – Portfolio |
| API | Simple Tool Rental API |
| Version | 1.0 |
| Test Type | API Functional Testing |
| Tool | Postman |
| Status | Draft – Pending Execution |

## Test Environment

- **Base URL:** `https://simple-tool-rental-api.click`
- **Authentication:** Bearer Token for order-related endpoints
- **Category:** `trailers`
- **Postman variables:**
  - `baseUrl`
  - `apiToken`
  - `category`
  - `toolId` (global variable)
  - `orderId` (global variable)

> **Execution note:** Register a test client manually before running the order tests. Copy the returned `accessToken` into the `apiToken` collection variable. Use only fictional test data.

---

## TC-001 – Verify API Health Status

**Test ID:** TC-001  
**Title:** Verify that the API is available  
**Priority:** High  
**Type:** Positive / Smoke Test  
**Automation Status:** Automated in current collection

**Preconditions:**
- The API base URL is configured.
- The API is reachable.

**Request:**
- Method: `GET`
- Endpoint: `/status`

**Test Steps:**
1. Open the Postman collection.
2. Select the `Status` request.
3. Send the request.
4. Review the HTTP status code.
5. Review the response body.

**Test Data:**
- No request body or authentication required.

**Expected Result:**
- The response status code is `200 OK`.
- The response body contains `"status": "UP"`.

---

## TC-002 – Retrieve Tools by Category

**Test ID:** TC-002  
**Title:** Retrieve tools belonging to the selected category  
**Priority:** High  
**Type:** Positive / Functional  
**Automation Status:** Automated in current collection

**Preconditions:**
- The API is available.
- The `baseUrl` variable is configured.
- The `category` variable is set to `trailers`.

**Request:**
- Method: `GET`
- Endpoint: `/tools?category={{category}}`

**Test Steps:**
1. Select the `Get all tools` request.
2. Confirm that the category variable is set to `trailers`.
3. Send the request.
4. Review the response status code and response body.
5. Check that at least one returned tool is in stock.
6. Check that the selected tool belongs to the requested category.

**Test Data:**
- `category = trailers`

**Expected Result:**
- The response status code is `200 OK`.
- At least one tool is available in the response.
- The selected tool has `inStock = true`.
- The selected tool's category is `trailers`.
- The selected tool's numeric ID is saved as the global `toolId` variable.

---

## TC-003 – Retrieve a Single Tool

**Test ID:** TC-003  
**Title:** Retrieve tool details using a valid tool ID  
**Priority:** High  
**Type:** Positive / Functional  
**Automation Status:** Automated in current collection

**Preconditions:**
- TC-002 has passed.
- A valid numeric `toolId` has been saved.

**Request:**
- Method: `GET`
- Endpoint: `/tools/{{toolId}}`

**Test Steps:**
1. Select the `Get a single tool` request.
2. Confirm that `toolId` contains the ID saved by TC-002.
3. Send the request.
4. Review the response status code.
5. Compare the returned tool ID with the saved `toolId`.
6. Check the `current-stock` value.

**Test Data:**
- `toolId =` the numeric ID saved by TC-002.

**Expected Result:**
- The response status code is `200 OK`.
- The returned tool ID matches the requested `toolId`.
- The `current-stock` value is greater than `0`.

---

## TC-004 – Register a New API Client

**Test ID:** TC-004  
**Title:** Register a new API client with valid data  
**Priority:** High  
**Type:** Positive / Authentication Setup  
**Automation Status:** Partially automated; registration is performed manually in the current workflow

**Preconditions:**
- The API is available.
- The `baseUrl` variable is configured.
- A unique email address is available for registration.

**Request:**
- Method: `POST`
- Endpoint: `/api-clients`

**Test Steps:**
1. Select the `Register a new API client` request.
2. Review the request body.
3. Send the request.
4. Verify the response status code.
5. Locate the `accessToken` in the response.
6. Copy the token into the `apiToken` collection variable.

**Test Data:**

```json
{
  "clientName": "Postman",
  "clientEmail": "unique-test-email@example.com"
}
```

**Expected Result:**
- The response status code is `201 Created`.
- An access token is returned.
- The token is stored locally in the `apiToken` collection variable for subsequent authenticated requests.

---

## TC-005 – Create a New Order

**Test ID:** TC-005  
**Title:** Create an order for an available tool  
**Priority:** High  
**Type:** Positive / Functional  
**Automation Status:** Automated in current collection

**Preconditions:**
- TC-002 has passed and a valid `toolId` is available.
- A valid `apiToken` is configured.
- The selected tool has available stock.

**Request:**
- Method: `POST`
- Endpoint: `/orders`
- Authentication: Bearer Token

**Test Steps:**
1. Select the `Create a new order` request.
2. Confirm that `apiToken` contains a valid token.
3. Confirm that `toolId` contains a valid numeric ID.
4. Send the request.
5. Verify the response status code.
6. Review the response body.
7. Save the returned `orderId` for subsequent requests.

**Test Data:**

```json
{
  "toolId": 1,
  "customerName": "Alex Morgan"
}
```

> Replace `1` with the actual numeric `toolId` returned by TC-002. The collection uses a randomly generated customer name.

**Expected Result:**
- The response status code is `201 Created`.
- The order is created successfully.
- An `orderId` is returned.
- The returned `orderId` is saved as a global variable.

---

## TC-006 – Retrieve All Orders

**Test ID:** TC-006  
**Title:** Retrieve orders belonging to the authenticated client  
**Priority:** Medium  
**Type:** Positive / Functional  
**Automation Status:** Automated in current collection

**Preconditions:**
- A valid `apiToken` is configured.
- At least one order has been created for the test client.

**Request:**
- Method: `GET`
- Endpoint: `/orders`
- Authentication: Bearer Token

**Test Steps:**
1. Select the `Get all orders` request.
2. Confirm that the Bearer Token is configured.
3. Send the request.
4. Review the response status code.
5. Review the response body.

**Test Data:**
- Valid `apiToken`.

**Expected Result:**
- The response status code is `200 OK`.

**Coverage Note:** The current Postman test checks the HTTP status code only. It does not verify the response schema or confirm that a specific order is present.

---

## TC-007 – Retrieve a Single Order

**Test ID:** TC-007  
**Title:** Retrieve an existing order by order ID  
**Priority:** High  
**Type:** Positive / Functional  
**Automation Status:** Automated in current collection

**Preconditions:**
- TC-005 has passed.
- A valid `orderId` is available.
- A valid `apiToken` is configured.

**Request:**
- Method: `GET`
- Endpoint: `/orders/{{orderId}}?invoice=true`
- Authentication: Bearer Token

**Test Steps:**
1. Select the `Get a single order` request.
2. Confirm that `orderId` contains the ID returned by TC-005.
3. Confirm that the Bearer Token is configured.
4. Send the request.
5. Review the response status code and body.

**Test Data:**
- `orderId =` the ID returned by TC-005.
- `invoice = true`

**Expected Result:**
- The response status code is `200 OK`.

**Coverage Note:** The current Postman test checks the HTTP status code only. It does not validate the returned order fields or invoice content.

---

## TC-008 – Update an Existing Order

**Test ID:** TC-008  
**Title:** Update customer information and comment for an existing order  
**Priority:** High  
**Type:** Positive / Functional  
**Automation Status:** Automated in current collection

**Preconditions:**
- TC-005 has passed.
- A valid `orderId` is available.
- A valid `apiToken` is configured.

**Request:**
- Method: `PATCH`
- Endpoint: `/orders/{{orderId}}`
- Authentication: Bearer Token

**Test Steps:**
1. Select the `Update an order` request.
2. Confirm that `orderId` is valid.
3. Confirm that the Bearer Token is configured.
4. Send the PATCH request with the updated customer name and comment.
5. Review the response status code.

**Test Data:**

```json
{
  "customerName": "Christina Morgan",
  "comment": "Pick-Up after 4PM!"
}
```

**Expected Result:**
- The response status code is `204 No Content`.

**Coverage Gap:** The current collection does not verify that the updated values are persisted. A follow-up GET request should be added to validate the updated fields.

---

## TC-009 – Delete an Existing Order

**Test ID:** TC-009  
**Title:** Delete an order created during the test run  
**Priority:** High  
**Type:** Positive / Functional / Cleanup  
**Automation Status:** Automated in current collection

**Preconditions:**
- TC-005 has passed.
- A valid `orderId` is available.
- A valid `apiToken` is configured.

**Request:**
- Method: `DELETE`
- Endpoint: `/orders/{{orderId}}`
- Authentication: Bearer Token

**Test Steps:**
1. Select the `Delete an order` request.
2. Confirm that `orderId` refers to the test order created in TC-005.
3. Confirm that the Bearer Token is configured.
4. Send the DELETE request.
5. Review the response status code.

**Test Data:**
- `orderId =` the test order ID created during the current run.

**Expected Result:**
- The response status code is `204 No Content`.
- The delete request completes successfully.

---

## TC-010 – Verify That the Order Has Been Deleted

**Test ID:** TC-010  
**Title:** Verify that a deleted order can no longer be retrieved  
**Priority:** High  
**Type:** Positive / Data Verification  
**Automation Status:** Automated in current collection

**Preconditions:**
- TC-009 has passed.
- The deleted order ID is still available in `orderId`.
- A valid `apiToken` is configured.

**Request:**
- Method: `GET`
- Endpoint: `/orders/{{orderId}}`
- Authentication: Bearer Token

**Test Steps:**
1. Select the `Check if order deleted` request.
2. Confirm that `orderId` refers to the order deleted in TC-009.
3. Confirm that the Bearer Token is configured.
4. Send the GET request.
5. Review the response status code.

**Test Data:**
- `orderId =` the ID of the order deleted in TC-009.

**Expected Result:**
- The response status code is `404 Not Found`.
- The deleted order is no longer retrievable.

---

## Execution Notes

- Execute TC-001 before the other test cases to confirm API availability.
- Execute TC-002 before TC-003 and TC-005 because those tests depend on a valid tool ID.
- Complete TC-004 manually before running authenticated order requests.
- Execute TC-005 before TC-006, TC-007, TC-008, TC-009, and TC-010.
- Execute TC-009 before TC-010.
- Do not reuse stale global values for `toolId` or `orderId` from a previous run.
- Do not publish real access tokens or personal information in this repository.
- Record actual results only after executing the test cases.

## Test Execution Results

| Test ID | Actual Result | Status | Defect ID | Comments |
|---|---|---|---|---|
| TC-001 | Not executed | Not Run | - | - |
| TC-002 | Not executed | Not Run | - | - |
| TC-003 | Not executed | Not Run | - | - |
| TC-004 | Not executed | Not Run | - | Manual setup |
| TC-005 | Not executed | Not Run | - | - |
| TC-006 | Not executed | Not Run | - | - |
| TC-007 | Not executed | Not Run | - | - |
| TC-008 | Not executed | Not Run | - | Persistence not verified |
| TC-009 | Not executed | Not Run | - | Cleanup |
| TC-010 | Not executed | Not Run | - | - |

