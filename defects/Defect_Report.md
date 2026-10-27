# Defect Report: Supply Chain Planning (Xpression NextGen) — Manual Testing

Defects are re-created from real bug patterns found on the project, rewritten without client details.

| ID | Title | Module | Severity | Priority | Status |
|---|---|---|---|---|---|
| DEF-XPR-01 | Frozen-horizon override accepted through the API | Demand Workbench | Critical | P1 | Closed |
| DEF-XPR-02 | Reason code demanded at exactly 20% change | Demand Workbench | Medium | P2 | Closed |
| DEF-XPR-03 | Safety stock off by one unit at 98% service level | Inventory Policy | Medium | P2 | Closed |
| DEF-XPR-04 | Bulk approval partially commits when one item is already approved | Replenishment | High | P1 | Closed |
| DEF-XPR-05 | Trailing spaces trimmed from password | Login & Roles | Medium | P2 | Closed |
| DEF-XPR-06 | Grand total not formatted with thousands separator in Edge | Demand Workbench | Low | P3 | Deferred |

## DEF-XPR-01: Frozen-horizon override accepted through the API

| Field | Value |
|---|---|
| Module | Demand Workbench |
| Severity / Priority | Critical / P1 |
| Status | Closed |
| Environment | https://qa-ng.example (seeded 4 SKUs x 2 DCs) |
| Linked test case(s) | TC_XPR_DMD_004 |
| Steps to reproduce | 1. PUT /api/demand/{key}/override with week W1 and qty 500 |
| Expected result | 422 frozen-horizon error |
| Actual result | 200 OK; W1 changed although the UI cell is disabled |
| Root cause / notes | Frozen rule implemented only in the UI; server-side validation added |

## DEF-XPR-02: Reason code demanded at exactly 20% change

| Field | Value |
|---|---|
| Module | Demand Workbench |
| Severity / Priority | Medium / P2 |
| Status | Closed |
| Environment | https://qa-ng.example (seeded 4 SKUs x 2 DCs) |
| Linked test case(s) | TC_XPR_DMD_006 |
| Steps to reproduce | 1. Override SKU-2001 W5 from 100 to 120 without reason |
| Expected result | Saved (threshold is 'above 20%') |
| Actual result | Reason code required |
| Root cause / notes | Comparison used >= instead of > |

## DEF-XPR-03: Safety stock off by one unit at 98% service level

| Field | Value |
|---|---|
| Module | Inventory Policy |
| Severity / Priority | Medium / P2 |
| Status | Closed |
| Environment | https://qa-ng.example (seeded 4 SKUs x 2 DCs) |
| Linked test case(s) | TC_XPR_INV_002 |
| Steps to reproduce | 1. avg 100, σ 20, LT 9, SL 98%<br>2. Calculate |
| Expected result | SS 123 |
| Actual result | SS 124 |
| Root cause / notes | Floating-point 122.99999 rounded up by ceil; rounding to 6 dp applied before ceil |

## DEF-XPR-04: Bulk approval partially commits when one item is already approved

| Field | Value |
|---|---|
| Module | Replenishment |
| Severity / Priority | High / P1 |
| Status | Closed |
| Environment | https://qa-ng.example (seeded 4 SKUs x 2 DCs) |
| Linked test case(s) | TC_XPR_REP_006 |
| Steps to reproduce | 1. Approve #500<br>2. Select #500 and #501<br>3. Approve selected |
| Expected result | Whole request rejected; #501 stays PROPOSED |
| Actual result | Error shown but #501 approved and PO created |
| Root cause / notes | Validation and update in the same loop; validation now runs before any update |

## DEF-XPR-05: Trailing spaces trimmed from password

| Field | Value |
|---|---|
| Module | Login & Roles |
| Severity / Priority | Medium / P2 |
| Status | Closed |
| Environment | https://qa-ng.example (seeded 4 SKUs x 2 DCs) |
| Linked test case(s) | TC_XPR_AUTH_002 |
| Steps to reproduce | 1. Log in with 'Plan@123 ' |
| Expected result | Rejected |
| Actual result | Logged in |
| Root cause / notes | Generic trim applied to all fields, including password |

## DEF-XPR-06: Grand total not formatted with thousands separator in Edge

| Field | Value |
|---|---|
| Module | Demand Workbench |
| Severity / Priority | Low / P3 |
| Status | Deferred |
| Environment | https://qa-ng.example (seeded 4 SKUs x 2 DCs) |
| Linked test case(s) | - |
| Steps to reproduce | 1. Edge 129<br>2. Open workbench |
| Expected result | 17,150 |
| Actual result | 17150 |
| Root cause / notes | Locale fallback; deferred to NG 2.7 |
