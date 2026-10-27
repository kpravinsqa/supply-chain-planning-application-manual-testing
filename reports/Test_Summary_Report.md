# Test Summary Report: Supply Chain Planning (Xpression NextGen) — Manual Testing

**Release:** NG 2.6 (Workbench, Replenishment & Scenarios) · **Prepared by:** Pravin Khedkar, QA Lead · **Recommendation: GO** (with known Low/Medium issues deferred)

## 1. Execution summary

| Metric | Cycle 1 | Cycle 2 (regression) |
|---|---:|---:|
| Planned | 38 | 38 |
| Executed | 37 | 38 |
| Passed | 32 | 38 |
| Failed | 5 | 0 |
| Blocked | 1 | 0 |
| Pass rate | 84.2% | 100.0% |

## 2. Module-wise results

| Module | Cases | C1 Pass | C1 Fail | C1 Blocked | C2 Pass | C2 Pass % |
|---|---|---|---|---|---|---|
| Login & Roles | 6 | 5 | 1 | 0 | 6 | 100% |
| Demand Workbench | 13 | 11 | 2 | 0 | 13 | 100% |
| Inventory Policy | 6 | 5 | 1 | 0 | 6 | 100% |
| Replenishment | 8 | 7 | 1 | 0 | 8 | 100% |
| Scenario Planning | 5 | 4 | 0 | 1 | 5 | 100% |

## 3. Defect summary

| Severity | Count |
|---|---:|
| Critical | 1 |
| High | 1 |
| Medium | 3 |
| Low | 1 |
| **Total** | **6** |

Status: Closed: 5, Deferred: 1.
Defect density: **1.2 defects per module**; defect detection in Cycle 1: **5 failing cases**.

## 4. Automation coverage
36 of 38 test cases (95%) are automated in [playwright-python-xpression-nextgen](https://github.com/kpravinsqa/playwright-python-xpression-nextgen); the rest are manual or exploratory by design.

## 5. Open issues and risks
- **DEF-XPR-06** (Low/P3, Deferred): Grand total not formatted with thousands separator in Edge

## 6. Recommendation
All exit criteria are met. QA recommends release to production, with the deferred items tracked for the next sprint.
