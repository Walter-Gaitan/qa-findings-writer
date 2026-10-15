---
name: API / Backend Defect
about: Report a backend API failure, incorrect status code, data contract breach, or server error
title: "[API][METHOD /endpoint] Issue summary"
labels: ["backend", "api", "triage-needed"]
assignees: ""
---

## Summary
<!-- Brief description of the API defect -->

## Endpoint & Environment
- **Endpoint URL:** `[e.g. POST /api/v2/orders]`
- **Environment:** [e.g. Staging / Dev / Sandbox]
- **API Version / Commit:** [e.g. v2.3.1]
- **Correlation / Request ID:** `[e.g. req_6b3e9a]`

## cURL Request to Reproduce
```bash
curl -X POST "https://api.example.com/endpoint" \
  -H "Authorization: Bearer <TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "key": "value"
  }'
```

## Expected Response
- **Status Code:** `200 OK` (or expected code)
- **Response Body:**
```json
{
  "status": "success"
}
```

## Actual Response
- **Status Code:** `500 Internal Server Error` (or actual code)
- **Response Body / Error:**
```json
{
  "error": "InternalServerError",
  "message": "..."
}
```

## Database / Backend Context (If Known)
<!-- Notes on database state, table schemas, message queues, or third-party service logs -->
