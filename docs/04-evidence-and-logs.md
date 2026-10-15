# Evidence & Logs Collection Guide

Evidence turns a disputed bug report into an undeniable, quickly debuggable issue.

---

## 1. Visual Evidence: Screenshots & Screen Recordings

### Screenshots
- **Annotate:** Use red rectangles, arrows, or callout numbers to highlight the exact defect area.
- **Do not crop away context:** Unless privacy-sensitive, include the URL bar, timestamp, and status messages.
- **Side-by-side Figma vs Actual:** For UI/visual bugs, show the Figma design mockup beside the actual rendering.

### Screen Recordings (Video / GIF)
- Always record video for:
  - Animation stutter or layout shifting.
  - Multi-step interactions and complex workflows.
  - Flaky or intermittent race conditions.
  - Crash-on-interaction defects.
- **Keep it under 30 seconds:** Edit or trim the video to show only the reproduction steps.

---

## 2. Browser & Frontend Logs

### Console Logs
Open DevTools (`Cmd + Option + I` or `F12`) > **Console**.
- Look for uncaught JavaScript exceptions (`Uncaught TypeError...`).
- Copy the full error message and stack trace.
- Export console messages: Right-click inside Console > **Save as...**.

### Network Activity (HAR Files)
For issues involving failed API requests, slow loading, or authentication failures:
1. Open DevTools > **Network** tab.
2. Check the **Preserve log** box.
3. Reproduce the bug.
4. Filter by `Fetch/XHR` or status code `4xx` / `5xx`.
5. Note down:
   - Request URL & HTTP Method (`POST /api/v2/checkout`)
   - HTTP Status Code (e.g. `500 Internal Server Error`)
   - Response Payload / Error JSON (`{"code": "ERR_INVALID_TOKEN", "message": "Signature verification failed"}`)
   - Correlation ID or Request ID from headers (e.g., `x-request-id: 7fa3b9...`)
6. Right-click anywhere in the Network table > **Save all as HAR with content**.

---

## 3. Backend & Mobile Logs

### Mobile Logs (iOS & Android)
- **iOS:** Capture crash logs via Xcode Organizer or MacOS Console app (`Console.app` streaming connected device logs).
- **Android:** Use `adb logcat`:
  ```bash
  adb logcat -v time *:E > android_error_log.txt
  ```

### Backend / Server Logs
When testing in local, staging, or serverless environments:
- Include the timestamp of failure (with timezone, e.g., `2026-10-15 09:12:00 UTC`).
- Provide the container/pod name or AWS CloudWatch / Datadog query link.
