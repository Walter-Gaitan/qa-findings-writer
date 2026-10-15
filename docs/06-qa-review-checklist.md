# QA Finding Pre-Submission Checklist

Before clicking **"Create Issue"** or submitting your finding in Jira, Linear, or GitHub, run through this quick checklist:

### 1. Duplication & Isolation
- [ ] **No Duplicate:** Have I searched existing tickets to make sure this isn't already reported?
- [ ] **Single Issue:** Does this report describe only **one** defect? (If there are multiple side effects with different causes, split them).

### 2. Clarity & Steps
- [ ] **Clear Title:** Does the title summarize `[Module] Defect behavior when [Condition]`?
- [ ] **Clean Starting Point:** Did I state the preconditions and starting point clearly?
- [ ] **Deterministic Steps:** Can an engineer with no prior context reproduce this by strictly following steps 1 through N?
- [ ] **Specific Test Data:** Did I provide concrete values, test user accounts, or input data instead of generic placeholders?

### 3. Verification & Impact
- [ ] **Explicit Expected vs Actual:** Did I clearly state both what actually happened AND what should have happened?
- [ ] **Accurate Severity:** Is the Severity rating aligned with the technical impact guidelines (S1–S4)?
- [ ] **Reproducibility Rate:** Did I state if this is 100% reproducible or intermittent?

### 4. Technical Artifacts & Evidence
- [ ] **Visual Proof:** Did I attach an annotated screenshot or video recording?
- [ ] **Console / Network:** Did I include DevTools console errors or network request/response details if applicable?
- [ ] **IDs / Traces:** Did I capture correlation IDs, order IDs, or user IDs used during the test?
- [ ] **Sanitized Data:** Did I ensure no sensitive customer passwords, real credit cards, or PII are exposed in the screenshots or logs?
