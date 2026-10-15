# Jira Defect Template (Copy-Paste)

Copy and paste the template below directly into Jira's description box.

```text
h2. Summary
*Summary:* [One clear sentence describing the bug]

h2. Environment
* *Environment:* Staging / QA / Prod
* *Version / Build:* vX.Y.Z (Commit: abc1234)
* *Client / OS:* Chrome 130 / macOS 15.0 / iPhone 15 iOS 17.5
* *User Account / Role:* Admin / Standard User / Guest

h2. Preconditions
* [List any specific setup or test data needed prior to step 1]

h2. Steps to Reproduce
# Navigate to '...'
# Click on '...'
# Enter '...' into field '...'
# Observe behavior

h2. Expected Result
[What should happen based on acceptance criteria or specs]

h2. Actual Result
[What actually happened, including error text]

h2. Reproducibility
* Rate: Always (100%) / Intermittent (X/Y)
* Severity: S1 (Blocker) / S2 (Major) / S3 (Minor) / S4 (Trivial)

h2. Evidence & Logs
{code:json}
// Paste network error payload or console log here
{code}
!screenshot.png|thumbnail!
```
