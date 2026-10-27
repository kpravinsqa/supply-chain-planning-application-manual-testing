# Inventory Policy (INV): Test Cases

6 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_XPR_INV_001: 95% service level reference

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-07 / TS_XPR_INV_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. avg 100, σ 20, LT 9, SL 95% |
| Expected result | z 1.65; SS 99; ROP 999 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_inventory_policy.py::test_safety_stock_and_reorder_point` |

## TC_XPR_INV_002: All service levels

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-07 / TS_XPR_INV_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Repeat with SL 90/98/99 |
| Expected result | SS 77/123/140; ROP 977/1023/1040 |
| Result (C1 → C2) | Fail → Pass (DEF-XPR-03) |
| Automation | `tests/ui/test_inventory_policy.py::test_safety_stock_and_reorder_point` |

## TC_XPR_INV_003: Zero variability

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-07 / TS_XPR_INV_01 |
| Priority / Type | P2 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. avg 50, σ 0, LT 14 |
| Expected result | SS 0; ROP 700 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_inventory_policy.py::test_safety_stock_and_reorder_point` |

## TC_XPR_INV_004: Monotonic safety stock

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-07 / TS_XPR_INV_01 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Calculate same inputs at 90→99% |
| Expected result | SS never decreases |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_inventory_policy.py::test_higher_service_level_never_lowers_safety_stock` |

## TC_XPR_INV_005: Lead time 0 / 1 / 365 / 366

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-08 / TS_XPR_INV_02 |
| Priority / Type | P1 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Calculate with each lead time |
| Expected result | 1 and 365 accepted; 0 and 366 rejected |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_inventory_policy.py::test_policy_input_validation` |

## TC_XPR_INV_006: Negative demand inputs

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-08 / TS_XPR_INV_02 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. avg -1<br>2. σ -2 |
| Expected result | 'Demand inputs cannot be negative' on the field |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_inventory_policy.py::test_policy_input_validation` |
