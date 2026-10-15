# Writing Deterministic Steps to Reproduce

"Steps to Reproduce" (STR) is the single most critical section of any QA finding. If a developer cannot reproduce the issue on their machine, resolution stalls.

---

## The 5 Golden Rules of STR

### 1. Start from a Known Clean State
Never assume the reader has the same tabs open, logged-in session, or pre-existing state.
- **Good:** "Log in as a newly created user with no payment methods attached."
- **Bad:** "Go to payment page."

### 2. One Imperative Action per Step
Use clear action verbs (Navigate, Click, Type, Select, Scroll, Drag, Wait).
- **Good:**
  1. Click "Add to Cart".
  2. Click the cart icon in the top right header.
  3. Click "Proceed to Checkout".
- **Bad:**
  1. Add an item and go through checkout until payment.

### 3. Provide Exact Test Data and Credentials
Avoid vague placeholders like *"enter valid info"* or *"upload a file"*.
- **Good:** "In the 'Phone Number' field, input `+1 (555) 019-2834`."
- **Good:** "Upload a 14MB PNG file named `profile_high_res.png`."
- **Bad:** "Enter your phone and upload an image."

### 4. Isolate the Minimal Sequence
Trim unnecessary navigation steps. If a bug triggers simply by sending an API request or opening a direct URL, don't write 8 UI clicks leading up to it.
- **Example:** If direct URL `https://staging.app/orders/999` reproduces the bug, include the direct URL and state the precondition that order #999 must exist.

### 5. Call Out Intermediate Verification Steps
If a state change is required before proceeding, note it as a checkpoint.
- **Example:**
  > 3. Click "Save Draft". Confirm the draft status indicator turns to "Saved".
  > 4. Disconnect network connectivity (simulate offline mode in DevTools).
  > 5. Click "Publish".

---

## Handling Intermittent Bugs (Flaky Issues)

If a bug does not reproduce 100% of the time:
1. **State the Probability:** e.g., *"Reproduced 3 out of 10 attempts (30%)"*.
2. **Describe Potential Factors:**
   - Network throttling (Fast 3G vs Broadband vs Offline).
   - Fast clicking / double-clicking (race conditions).
   - Cache state (first load / cold cache vs warm cache).
   - Database / data dependencies (e.g. only fails when the list has >100 entries).
3. **Capture a Recording:** Run a screen recorder while attempting reproduction to ensure the moment is captured.
