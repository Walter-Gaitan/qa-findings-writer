# QA Findings Writer

A comprehensive guide and template repository for writing clear, actionable, and deterministic Quality Assurance (QA) findings and bug reports.

## 🎯 Purpose

A great bug report saves engineering time, eliminates back-and-forth communication, accelerates time-to-resolution, and prevents regression. This repository provides:
- Standardized documentation on the structure and anatomy of QA findings.
- Clear distinction between **Severity** (technical impact) and **Priority** (business urgency).
- Practical guidelines for writing minimal, deterministic steps to reproduce.
- Best practices for attaching evidence (HAR logs, screenshots, stack traces).
- Ready-to-use templates for GitHub Issues, Jira tickets, and test management tools.

---

## 📚 Guide Index

| Topic | File | Description |
|---|---|---|
| **Finding Anatomy** | [`docs/01-finding-anatomy.md`](docs/01-finding-anatomy.md) | Standard fields and structure of a defect report |
| **Severity vs Priority** | [`docs/02-severity-vs-priority.md`](docs/02-severity-vs-priority.md) | Standard definitions, impact matrix, and scoring criteria |
| **Steps to Reproduce** | [`docs/03-writing-steps-to-reproduce.md`](docs/03-writing-steps-to-reproduce.md) | Rules for writing reproducible, deterministic steps |
| **Evidence & Logs** | [`docs/04-evidence-and-logs.md`](docs/04-evidence-and-logs.md) | Capturing visual, network, and system evidence |
| **Good vs Bad Examples** | [`docs/05-good-vs-bad-examples.md`](docs/05-good-vs-bad-examples.md) | Real-world side-by-side comparisons |
| **QA Submission Checklist**| [`docs/06-qa-review-checklist.md`](docs/06-qa-review-checklist.md) | Pre-flight checklist before submitting any finding |

---

## 📋 Ready-to-Use Templates

- **GitHub Issue Templates**: Located in [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/)
  - Functional Bug Report ([`bug_report.md`](.github/ISSUE_TEMPLATE/bug_report.md))
  - UI/UX Defect ([`ui_ux_defect.md`](.github/ISSUE_TEMPLATE/ui_ux_defect.md))
  - API / Backend Defect ([`api_backend_defect.md`](.github/ISSUE_TEMPLATE/api_backend_defect.md))
- **Jira Markdown Template**: [`templates/jira_bug_template.md`](templates/jira_bug_template.md)
- **JSON Schema Template**: [`templates/bug_report_template.json`](templates/bug_report_template.json)

---

## ⚡ Quick Rules of Thumb

1. **One Bug Per Ticket**: Never bundle multiple issues into a single finding unless one directly causes the other.
2. **Title Formula**: `[Component/Module] What happens vs what should happen under [Condition/Context]`
   - *Example:* `[Checkout] 500 Internal Error thrown when applying expired coupon code`
3. **Always State Expected vs Actual**: Never assume the expected behavior is obvious.
4. **Isolate the Minimum Steps**: Find the shortest sequence that reliably triggers the defect.
5. **Attach Evidence**: If it's UI, attach an annotated screenshot or video. If it's backend/API, attach request/response payloads, status codes, and correlation IDs.
