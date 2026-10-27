# Replenishment (REP): Test Cases

8 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_XPR_REP_001: Round up to MOQ multiple

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-09 / TS_XPR_REP_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Review SKU-1001 (req 1130, MOQ 250) and SKU-2001 (95, MOQ 48) |
| Expected result | Recommended 1,250 and 96 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_replenishment.py::test_recommended_qty_rounded_up_to_moq` |

## TC_XPR_REP_002: Exact multiple not rounded

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-09 / TS_XPR_REP_01 |
| Priority / Type | P2 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Review SKU-3001 (2500, MOQ 500) |
| Expected result | Recommended 2,500 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_replenishment.py::test_recommended_qty_rounded_up_to_moq` |

## TC_XPR_REP_003: Edit to valid multiple recalculates value

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-09 / TS_XPR_REP_02 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. SKU-1002 qty 500 → 700 |
| Expected result | Value $2,940.00 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_replenishment.py::test_edit_qty_to_moq_multiple_recalculates_value` |

## TC_XPR_REP_004: Edit to non-multiple rejected

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-09 / TS_XPR_REP_02 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. SKU-1002 qty 650 |
| Expected result | 'Quantity must be a multiple of the MOQ (100)'; reverted |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_replenishment.py::test_edit_qty_not_multiple_of_moq_rejected` |

## TC_XPR_REP_005: Bulk approve two recommendations

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-10 / TS_XPR_REP_03 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Tick #500 and #502<br>2. Approve selected |
| Expected result | Both APPROVED with PO-000500 / PO-000502; approved value $2,960.50 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_replenishment.py::test_bulk_approve_generates_po_numbers` |

## TC_XPR_REP_006: Approval is atomic

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-10 / TS_XPR_REP_03 |
| Priority / Type | P1 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Approve #500<br>2. Then approve #500 and #501 together |
| Expected result | 409; #501 remains PROPOSED |
| Result (C1 → C2) | Fail → Pass (DEF-XPR-04) |
| Automation | `tests/api/test_planning_api.py::test_cannot_approve_twice` |

## TC_XPR_REP_007: Reject requires reason

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-11 / TS_XPR_REP_04 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Reject #503 with 'no'<br>2. then 'Supplier on credit hold' |
| Expected result | First blocked; second REJECTED |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_replenishment.py::test_reject_requires_reason` |

## TC_XPR_REP_008: Status filter

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-10 / TS_XPR_REP_03 |
| Priority / Type | P3 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Approve one<br>2. Filter APPROVED |
| Expected result | Exactly 1 row |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_replenishment.py::test_status_filter` |
