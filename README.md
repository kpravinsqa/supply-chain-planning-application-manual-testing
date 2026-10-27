# Supply Chain Planning (Xpression NextGen) — Manual Testing

![Type](https://img.shields.io/badge/testing-manual-blue) ![Cases](https://img.shields.io/badge/test%20cases-38-success) ![Defects](https://img.shields.io/badge/defects-6-orange) ![Domain](https://img.shields.io/badge/domain-Supply%20Chain%20Planning-informational)

Complete manual-testing artefact set for **Xpression NextGen (SaaS Supply Chain Planning)** (Supply Chain Planning): test plan, scenarios, detailed test cases,
requirement traceability, defect reports and a test summary report, structured the way I deliver them on real projects.

> **Confidentiality note:** this is a portfolio re-creation. Requirements, test data and defects are rewritten in generic
> terms from my project experience; **no confidential client documents, data or screenshots are included.**

**Automation companion:** [playwright-python-xpression-nextgen](https://github.com/kpravinsqa/playwright-python-xpression-nextgen). Test cases marked with an automated test name are implemented there.

## Contents

| Artefact | Link |
|---|---|
| Master test plan | [docs/01_Test_Plan.md](docs/01_Test_Plan.md) |
| Test scenarios (16) | [docs/02_Test_Scenarios.md](docs/02_Test_Scenarios.md) |
| Requirement traceability matrix | [docs/03_RTM.md](docs/03_RTM.md) |
| Test cases by module | [AUTH](test-cases/AUTH_Login_and_Roles.md) · [DMD](test-cases/DMD_Demand_Workbench.md) · [INV](test-cases/INV_Inventory_Policy.md) · [REP](test-cases/REP_Replenishment.md) · [SCN](test-cases/SCN_Scenario_Planning.md) |
| Excel workbook (dashboard, cases, RTM, defects) | [test-cases/XPR_Test_Cases.xlsx](test-cases/XPR_Test_Cases.xlsx) |
| Defect report (6) | [defects/Defect_Report.md](defects/Defect_Report.md) |
| Test summary report | [reports/Test_Summary_Report.md](reports/Test_Summary_Report.md) |
| Checklists | [Planning Grid Testing Checklist](checklists/grid_testing_checklist.md) · [Calculation Verification Checklist](checklists/calculation_checklist.md) |

## Coverage

| Module | Code | Test cases |
|---|---|---|
| Login & Roles | AUTH | 6 |
| Demand Workbench | DMD | 13 |
| Inventory Policy | INV | 6 |
| Replenishment | REP | 8 |
| Scenario Planning | SCN | 5 |
| **Total** | | **38** |

## Highlights

- 38 test cases across 5 modules and 12 requirements
- Editable data-grid testing: frozen horizon, override thresholds at exactly 20% vs 21%, revert on error, audit trail
- Reference-value checks for safety stock / reorder point at 4 service levels
- Replenishment MOQ rounding, **atomic bulk approval** and PO generation
- Critical defect example: **business rule enforced only in the UI**, bypassed via API

## Test design techniques used

Equivalence partitioning · boundary value analysis · decision tables · state transition · error guessing · exploratory testing

## Author

**Pravin Khedkar**, QA Lead / SDET · [@kpravinsqa](https://github.com/kpravinsqa)
