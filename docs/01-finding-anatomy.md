# The Anatomy of a High-Quality QA Finding

Every QA finding or defect report should contain structured, unambiguous information. A developer or product owner reading the ticket should never have to ask: *"What environment was this in?"* or *"What did you expect to happen?"*.

---

## 1. Title / Summary Line

The title is the most visible part of the report. It should be concise, descriptive, and structured.

### Recommended Format
```text
[Module/Feature] [Sub-component] - Specific defect behavior when [Condition/Trigger]
```

### Examples
- **Good:** `[Auth][Login] "Forgot Password" button does not send email when username contains uppercase characters`
- **Good:** `[Billing][Stripe] Checkout spinner hangs indefinitely on 3D Secure verification timeout`
- **Bad:** `Login broken`
- **Bad:** `Error on checkout page`

---

## 2. Environment & Context

Bugs are often environmental. Always document:

| Field | Description | Example |
|---|---|---|
| **Environment** | Stage, QA, UAT, Staging, Production | `Staging-US-East` |
| **App / Build Version** | Semantic version, commit hash, or release tag | `v2.14.0-rc3 (commit 8a2f4c)` |
| **Platform / OS** | Operating system and version | `macOS 15.1 (Sequoia)`, `Android 14 (OneUI 6.0)` |
| **Browser / Client** | Client name and exact version | `Chrome 130.0.6723.92 (Official Build) (arm64)` |
| **Screen / Viewport** | Screen resolution or breakpoint | `1920x1080`, `Mobile (390x844 iPhone 15)` |
| **User Role / Auth** | Role and permissions used during the test | `Tenant Admin`, `Anonymous Guest`, `Standard User` |

---

## 3. Preconditions & Test Data

State everything that must exist before step 1 begins:
- Account status (e.g. "User must have a verified email and 2 items in cart").
- Feature flag status (e.g. `FEATURE_NEW_CHECKOUT=true`).
- Test data used (e.g. test user ID, order ID, product SKU).

---

## 4. Steps to Reproduce (Deterministic)

Numbered, sequential, imperative steps that anyone on the team can execute.
- Start from a clean, known state.
- One distinct user action per step.
- Include exact values entered or buttons clicked.

```markdown
1. Navigate to `https://staging.example.com/login`.
2. Enter email `qa-test-user@example.com` and valid password.
3. Click "Sign In".
4. From the top navigation bar, click "Account Settings" > "Notifications".
5. Toggle "Email Digest" off and click "Save Preferences".
```

---

## 5. Expected Result vs. Actual Result

State both explicitly. Never leave the reader to infer what should have happened.

- **Expected Result:**
  > A green toast notification appears stating *"Preferences updated successfully"*, and the toggle remains in the OFF state after page refresh.
- **Actual Result:**
  > A red error banner appears displaying *"Unexpected server error (code: 500)"*, and the toggle reverts to ON upon page refresh.

---

## 6. Reproducibility Rate

Indicate whether the issue happens consistently or intermittently:
- `Always (5/5 attempts, 100%)`
- `Frequently (3/5 attempts, 60%)`
- `Intermittent / Rare (1/10 attempts, 10%)`
- *Note:* If intermittent, mention any suspected race conditions, network latency, or timing factors.

---

## 7. Business / User Impact

Explain how this affects the user experience, business operations, or data integrity:
- Does this block release?
- Is data corrupted or lost?
- Is there a viable workaround for the user?

---

## 8. Evidence & Technical Attachments

- **Visual Evidence:** Annotated screenshots, video recordings (MP4/GIF).
- **Technical Logs:** Browser console logs, Network HAR files, API payloads (cURL), server trace IDs or Correlation IDs.
