# Good vs. Bad Examples of QA Findings

Reviewing contrast examples is one of the most effective ways to train team members on quality defect reporting.

---

## Example 1: Frontend / UI Defect

### ❌ The Bad Report
> **Title:** Cart is broken  
> **Description:** I clicked checkout and nothing happened. Fix ASAP.  
> **Severity:** High

*Why it's bad:*
- What cart? Which platform?
- Were there items in the cart?
- Did "nothing happened" mean button disabled, network failure, or crash?
- Zero environment info, zero logs, zero steps.

---

### ✅ The Good Report
> **Title:** `[Checkout] "Pay Now" button stays disabled after entering valid postal code (UK format)`  
> **Environment:** Staging (v3.1.2) | Chrome 130 | macOS Sonoma | Viewport: Desktop 1440x900  
> **Severity:** S2 (Major) | **Priority:** P1 (High)  
>
> **Preconditions:**
> - User logged in with UK billing address.
> - Cart contains 1 tangible physical item (SKU: `BOOK-001`).
>
> **Steps to Reproduce:**
> 1. Navigate to `https://staging.shop.example/cart`.
> 2. Click "Proceed to Checkout".
> 3. In the Shipping Step, select country "United Kingdom".
> 4. In Postal Code field, enter valid alphanumeric UK postal code: `SW1A 1AA`.
> 5. Complete all remaining required fields.
> 6. Observe the "Pay Now" button at the bottom of the form.
>
> **Expected Result:**
> The "Pay Now" button becomes active and clickable once all required fields are valid.
>
> **Actual Result:**
> The button remains in a disabled state (`disabled="true"` in DOM). Console shows validation regex error: `Uncaught Error: postal_code format mismatch`.
>
> **Evidence:**
> - Attached: `uk_postal_code_disabled_button.png` (with highlighted DevTools inspector)
> - Console log: `[Error] PostalCodeValidator: value 'SW1A 1AA' failed regex ^[0-9]{5}$` (incorrect US zip validation applied).

---

## Example 2: API / Backend Defect

### ❌ The Bad Report
> **Title:** 500 error on user update  
> **Description:** API throws 500 when updating profile.

---

### ✅ The Good Report
> **Title:** `[API][PUT /v1/users/{id}] 500 Internal Server Error when updating user bio with emoji characters`  
> **Environment:** API Gateway Staging (`api.staging.example.com`) | Build `commit-4f1a2e`  
> **Severity:** S3 (Minor) | **Priority:** P2 (Medium)  
>
> **Preconditions:**
> User ID `usr_981240` exists and is active.
>
> **cURL Reproduction:**
> ```bash
> curl -X PUT "https://api.staging.example.com/v1/users/usr_981240" \
>   -H "Authorization: Bearer <VALID_JWT>" \
>   -H "Content-Type: application/json" \
>   -d '{"bio": "Software QA Engineer 🚀✨"}'
> ```
>
> **Expected Result:**
> `HTTP 200 OK` with JSON response containing updated user object with UTF-8 encoded bio string.
>
> **Actual Result:**
> `HTTP 500 Internal Server Error`
> Response body:
> ```json
> {
>   "error": "InternalServerError",
>   "message": "Incorrect string value: '\\xF0\\x9F\\x9A\\x80...' for column 'bio' at row 1",
>   "correlationId": "req_881a702c-4991"
> }
> ```
>
> **Root Cause Suspect:**
> Database column collation is configured as `utf8` (3-byte) instead of `utf8mb4` (4-byte supporting full unicode/emoji).
