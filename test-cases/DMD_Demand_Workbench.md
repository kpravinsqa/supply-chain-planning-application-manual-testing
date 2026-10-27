# Demand Workbench (DMD): Test Cases

13 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_XPR_DMD_001: Initial grid and totals

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-03 / TS_XPR_DMD_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Open Demand Workbench |
| Expected result | 4 item-location rows; grand total 17,150; SKU-1001@DC-PUNE total 4,570 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_demand_workbench.py::test_grid_loads_with_statistical_totals` |

## TC_XPR_DMD_002: Location filter recalculates grand total

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-03 / TS_XPR_DMD_01 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Filter DC-MUMBAI |
| Expected result | 2 rows; grand total 10,800 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_demand_workbench.py::test_location_filter` |

## TC_XPR_DMD_003: W1 and W2 cells locked

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-04 / TS_XPR_DMD_02 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Inspect W1, W2 cells |
| Expected result | Cells disabled with 'Frozen horizon' tooltip |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_demand_workbench.py::test_frozen_horizon_cells_are_locked` |

## TC_XPR_DMD_004: API override in frozen week

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-04 / TS_XPR_DMD_02 |
| Priority / Type | P1 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. PUT override for W1 |
| Expected result | 422 'W1 is inside the frozen horizon and cannot be changed' |
| Result (C1 → C2) | Fail → Pass (DEF-XPR-01) |
| Automation | `tests/api/test_planning_api.py::test_override_rules` |

## TC_XPR_DMD_005: Override within threshold

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_XPR_DMD_03 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. SKU-1001 W3: 560 → 600 (+7%) |
| Expected result | Saved; cell highlighted; row total 4,610; grand 17,190 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_demand_workbench.py::test_override_within_threshold_updates_totals` |

## TC_XPR_DMD_006: Exactly ±20% needs no reason (BVA)

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_XPR_DMD_03 |
| Priority / Type | P1 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. SKU-2001 W5: 100 → 120<br>2. then 100 → 80 |
| Expected result | Both saved without reason |
| Result (C1 → C2) | Fail → Pass (DEF-XPR-02) |
| Automation | `tests/ui/test_demand_workbench.py::test_override_at_exact_threshold_needs_no_reason` |

## TC_XPR_DMD_007: ±21% without reason rejected

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_XPR_DMD_03 |
| Priority / Type | P1 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. SKU-2001 W5: 100 → 121<br>2. then 100 → 79 |
| Expected result | 'A reason code is required for changes above 20%'; value reverted |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_demand_workbench.py::test_override_above_threshold_requires_reason` |

## TC_XPR_DMD_008: Large override with reason

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_XPR_DMD_03 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Choose PROMOTION<br>2. SKU-2001 W5 → 250 |
| Expected result | Saved |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_demand_workbench.py::test_large_override_with_reason_code` |

## TC_XPR_DMD_009: Invalid values: negative, decimal, > 1,000,000

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_XPR_DMD_03 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter -5<br>2. 12.5<br>3. 1000001 |
| Expected result | 'Override must be a whole number between 0 and 1,000,000' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_demand_workbench.py::test_invalid_override_values` |

## TC_XPR_DMD_010: Override to zero needs reason

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_XPR_DMD_03 |
| Priority / Type | P2 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter 0 without reason<br>2. then with SUPPLY_CONSTRAINT |
| Expected result | Rejected first; saved with reason |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/api/test_planning_api.py::test_override_to_zero_needs_reason` |

## TC_XPR_DMD_011: Clear override reverts to statistical

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_XPR_DMD_03 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Override W3 = 600<br>2. Clear the cell |
| Expected result | Cell 560; highlight removed; totals restored |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_demand_workbench.py::test_clear_override_reverts_to_statistical` |

## TC_XPR_DMD_012: Tab/Enter navigation commits edits

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_XPR_DMD_04 |
| Priority / Type | P3 / UI |
| Preconditions | - |
| Test data | - |
| Steps | 1. Edit W3<br>2. press Tab<br>3. Edit W4<br>4. press Enter |
| Expected result | Both commits saved; focus moves right |
| Result (C1 → C2) | Pass → Pass |
| Automation | Manual only |

## TC_XPR_DMD_013: Override audit entry

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-06 / TS_XPR_DMD_05 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Override W6 610 → 900 with PROMOTION |
| Expected result | Audit: week W6, from 610, to 900, reason, user, timestamp |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/api/test_planning_api.py::test_override_audit_trail` |
