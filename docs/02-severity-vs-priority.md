# Severity vs. Priority Matrix

One of the most common pitfalls in QA defect reporting is confusing **Severity** (technical impact) with **Priority** (urgency to resolve).

- **Severity** is determined by **QA / Engineering**: *How bad is the technical damage or system failure?*
- **Priority** is determined by **Product / Business / Triaging Team**: *How urgently do we need to fix this in the product roadmap?*

---

## 1. Severity Levels

| Level | Name | Technical Definition | Examples |
|---|---|---|---|
| **S1** | **Blocker / Critical** | Complete crash, data loss, security vulnerability, or inability to perform core business function with **no workaround**. | - Database corruption on transaction commit.<br>- Complete authentication failure (all users locked out).<br>- Critical payment processing crash. |
| **S2** | **Major** | A major feature is broken or severely degraded, but an awkward or temporary workaround exists. | - In-app credit card checkout fails, but PayPal checkout works.<br>- Bulk CSV export fails when >500 rows, but single export works. |
| **S3** | **Minor / Moderate** | Non-critical functionality has an error or edge case, does not halt the main workflow. | - Sorting by "Date Created" sorts alphabetically instead of chronologically.<br>- Search results pagination shows 11 items instead of configured 10. |
| **S4** | **Trivial / Cosmetic** | Visual defects, typos, misaligned UI components, or minor UX inconveniences that do not affect functionality. | - Typo in tooltip text.<br>- Button padding is 8px instead of 16px specified in Figma. |

---

## 2. Priority Levels

| Level | Name | Urgency Definition | SLA Target (Example) |
|---|---|---|---|
| **P0** | **Urgent / Hotfix** | Drop everything and fix immediately. Blocks release or production deployment. | Fix within 4–12 hours |
| **P1** | **High** | Must be fixed in the current sprint or upcoming scheduled release. | Fix within current sprint |
| **P2** | **Medium** | Normal queue. Can be scheduled in the next sprint or regular release cycle. | Next 1–2 sprints |
| **P3** | **Low** | Backlog / polish. Fix when time permits. | Product backlog |

---

## 3. Discrepancy Examples: High Severity vs Low Priority (and vice versa)

### High Severity, Low Priority (S1 / P3)
- **Scenario:** The app crashes with a kernel panic or segfault, but only when running on an obsolete operating system version (e.g., Windows 7 or iOS 12) that constitutes <0.01% of active users and is officially out of support.
- **Why:** The technical impact is total failure (S1), but business priority is low (P3).

### Low Severity, High Priority (S4 / P0)
- **Scenario:** The company logo or CEO's name is misspelled on the public homepage header right before a major press release or product launch.
- **Why:** Zero functional impact (S4), but massive brand reputation urgency (P0).

---

## 4. Prioritization Matrix Guide

```
+-----------------------------------------------------------+
| SEVERITY \ IMPACT   | High Business Risk | Low Business Risk |
+---------------------+--------------------+-------------------+
| S1 (Critical/Crash) |       P0 (Hotfix)  |     P1 or P2      |
| S2 (Major Broken)   |       P1 (Sprint)  |     P2            |
| S3 (Minor Flaw)     |       P2           |     P3 (Backlog)  |
| S4 (Cosmetic/Typo)  |       P1 (If VIP)  |     P3 (Backlog)  |
+-----------------------------------------------------------+
```
