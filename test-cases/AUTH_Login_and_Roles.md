# Login & Roles (AUTH): Test Cases

6 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_XPR_AUTH_001: Planner login

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-01 / TS_XPR_AUTH_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Log in as planner |
| Expected result | Workbench opens; badge 'Demand Planner' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_login.py::test_planner_login` |

## TC_XPR_AUTH_002: Password not trimmed

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-01 / TS_XPR_AUTH_01 |
| Priority / Type | P2 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. Log in with 'Plan@123 ' (trailing space) |
| Expected result | Login rejected |
| Result (C1 → C2) | Fail → Pass (DEF-XPR-05) |
| Automation | `tests/ui/test_login.py::test_invalid_login` |

## TC_XPR_AUTH_003: Deep link without session

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-01 / TS_XPR_AUTH_01 |
| Priority / Type | P2 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. Open /replenishment.html in a new private window |
| Expected result | Redirected to login |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_login.py::test_unauthenticated_deep_link_redirects_to_login` |

## TC_XPR_AUTH_004: Viewer cannot edit workbench

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-02 / TS_XPR_AUTH_02 |
| Priority / Type | P1 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. Log in as viewer<br>2. Try to edit W5 cell |
| Expected result | All cells disabled |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_demand_workbench.py::test_viewer_cannot_edit_grid` |

## TC_XPR_AUTH_005: Viewer override via API

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-02 / TS_XPR_AUTH_02 |
| Priority / Type | P1 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. PUT override with viewer token |
| Expected result | 403 'Read-only users cannot change plans' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/api/test_planning_api.py::test_viewer_is_read_only` |

## TC_XPR_AUTH_006: Viewer replenishment read-only

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-02 / TS_XPR_AUTH_02 |
| Priority / Type | P2 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. Log in as viewer<br>2. Open Replenishment |
| Expected result | No checkboxes; qty fields disabled |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_replenishment.py::test_viewer_sees_read_only_recommendations` |
