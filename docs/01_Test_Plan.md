# Test Plan: Supply Chain Planning (Xpression NextGen) — Manual Testing

| Item | Detail |
|---|---|
| Project | Xpression NextGen (SaaS Supply Chain Planning) |
| Domain | Supply Chain Planning |
| Document | Master Test Plan (IEEE 829 aligned) |
| Prepared by | Pravin Khedkar, QA Lead |
| Version | 1.2 |

> Portfolio re-creation. Requirements, data and defects are rewritten in generic terms; no confidential client
> information is included.

## 1. Introduction
Xpression NextGen is the cloud-native successor of the classic SCP product. Planners review statistical demand forecasts in an editable workbench, apply overrides with reason codes, calculate inventory policy (safety stock, reorder point), approve replenishment recommendations into purchase orders, and model what-if scenarios. This plan covers the NG 2.6 release on the web client and REST APIs.

## 2. Objectives
- Verify forecast override rules (frozen horizon, ±20% reason-code threshold, audit trail) and totals
- Verify safety stock and reorder point calculations against reference values
- Verify replenishment MOQ rounding, approval atomicity and PO generation
- Verify read-only users cannot change plans in the UI or API

## 3. Scope
### 3.1 In scope
- **Login & Roles** (AUTH): 6 test cases
- **Demand Workbench** (DMD): 13 test cases
- **Inventory Policy** (INV): 6 test cases
- **Replenishment** (REP): 8 test cases
- **Scenario Planning** (SCN): 5 test cases


### 3.2 Out of scope
- Statistical forecasting algorithm accuracy (covered by the data-science team and the GAM engine DB suite)
- ERP purchase-order interface (integration test phase)
- Single sign-on provider configuration
- Load testing

## 4. Test approach
- Grid-focused testing: cell editing, keyboard navigation, totals, highlighting and revert on error
- Calculation checks with a reference spreadsheet for SS = ceil(z·σ·√LT) and ROP = ceil(avg·LT + SS)
- Boundary value analysis on the threshold (exactly 20% vs 21%), uplift (−50/+100) and lead time (1/365)
- Role-based checks for Planner vs Viewer; API negative testing with Postman; automation for regression

**Test design techniques:** equivalence partitioning, boundary value analysis, decision tables, state transition,
error guessing, and exploratory charters for high-risk areas.

**Test types:** Boundary, Functional, Negative, Security, UI.

## 5. Test environment
| Environment | Purpose | Details |
|---|---|---|
| QA tenant | Functional and regression | https://qa-ng.example (seeded 4 SKUs x 2 DCs) |
| Staging tenant | Release validation | Production-like configuration and data volumes |
| Browsers | Compatibility | Chrome, Edge |

**Tools:** Azure DevOps (boards and test plans), Postman, Excel reference calculators, Python + Playwright, SQL

## 6. Entry criteria
- Build deployed to QA with release notes
- Smoke suite passed
- Test data loaded and verified
- Requirements signed off and test cases peer-reviewed

## 7. Exit criteria
- 100% of P1 and 95% of all planned test cases executed
- No open Critical / High defects
- All Medium defects triaged with an agreed fix version
- Regression suite green, Test Summary Report signed off

## 8. Suspension and resumption
- Suspend when the smoke suite fails, the environment is unavailable for more than 4 hours, or a Critical defect blocks more than 30% of cases.
- Resume after the fix is deployed and the smoke suite passes again.

## 9. Defect management
Defects are logged in JIRA with severity (Critical / High / Medium / Low) and priority (P1 to P4), triaged daily with
Dev and PO, and retested and regression-tested before closure. See [Defect Report](../defects/Defect_Report.md).

## 10. Risks and mitigation
| Risk | Impact | Mitigation |
|---|---|---|
| Wrong totals after override | Planners order the wrong quantities | Row and grand-total checks after every edit |
| Edits allowed in the frozen horizon | Supplier commitments broken | Frozen-cell checks for UI and API |
| Partial bulk approvals | Duplicate or missing POs | Atomicity test with one already-approved item |
| Floating-point drift in SS/ROP | Off-by-one units | Reference values computed independently |

## 11. Deliverables
- Test plan (this document), [Test Scenarios](02_Test_Scenarios.md), [Test Cases](../test-cases/), [RTM](03_RTM.md)
- [Defect Report](../defects/Defect_Report.md), [Test Summary Report](../reports/Test_Summary_Report.md)
- Excel workbook: [`test-cases/XPR_Test_Cases.xlsx`](../test-cases/XPR_Test_Cases.xlsx)

## 12. Roles and responsibilities
| Role | Responsibility |
|---|---|
| QA Lead | Test strategy, planning, estimation, reporting, sign-off |
| QA Engineer | Test design, execution, defect logging, regression |
| Automation (SDET) | Smoke and regression automation, CI integration |
| Developer | Defect fixes, unit tests, root-cause analysis |
| Product Owner | Requirement clarification, UAT acceptance |

## 13. Schedule
| Phase | Duration |
|---|---|
| Requirement analysis and test planning | 1 week |
| Test design and review | 1.5 weeks |
| Cycle 1: functional execution | 2 weeks |
| Defect fixing and Cycle 2: regression | 1 week |
| UAT support and sign-off | 0.5 week |
