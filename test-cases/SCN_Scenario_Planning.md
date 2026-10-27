# Scenario Planning (SCN): Test Cases

5 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_XPR_SCN_001: Uplift scenario math

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-12 / TS_XPR_SCN_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create 'Diwali Peak' +15% |
| Expected result | Baseline 17,150; scenario 19,722; delta +2,572 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_scenarios.py::test_create_uplift_scenario` |

## TC_XPR_SCN_002: Baseline includes overrides

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-12 / TS_XPR_SCN_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Override W3 to 600<br>2. Create scenario 0% |
| Expected result | Baseline 17,190 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_scenarios.py::test_scenario_baseline_includes_overrides` |

## TC_XPR_SCN_003: Uplift boundaries −50/+100 and −51/+101

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-12 / TS_XPR_SCN_02 |
| Priority / Type | P2 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create scenarios with each value |
| Expected result | −50 and +100 accepted; −51 and +101 rejected |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_scenarios.py::test_uplift_boundaries_accepted` |

## TC_XPR_SCN_004: Duplicate name (case-insensitive) and delete

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-12 / TS_XPR_SCN_02 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create 'Monsoon'<br>2. Create 'monsoon'<br>3. Delete 'Monsoon' |
| Expected result | Duplicate rejected; delete leaves empty state |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_scenarios.py::test_duplicate_name_and_delete` |

## TC_XPR_SCN_005: Compare two scenarios side by side

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-12 / TS_XPR_SCN_03 |
| Priority / Type | P3 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create +10% and −10%<br>2. Open compare view |
| Expected result | Weekly deltas shown per scenario |
| Result (C1 → C2) | Blocked → Pass |
| Automation | Manual only |
