# Requirement Traceability Matrix: Supply Chain Planning (Xpression NextGen) — Manual Testing

Requirement coverage: **12/12 (100%)**

| Req ID | Module | Requirement | Scenarios | Test cases | Automated | Status |
|---|---|---|---|---|---|---|
| REQ-01 | Login & Roles | Planner and Viewer roles; unauthenticated deep links redirect to login | TS_XPR_AUTH_01 | TC_XPR_AUTH_001, TC_XPR_AUTH_002, TC_XPR_AUTH_003 | 3/3 | Covered |
| REQ-02 | Login & Roles | Viewer is read-only in UI and API | TS_XPR_AUTH_02 | TC_XPR_AUTH_004, TC_XPR_AUTH_005, TC_XPR_AUTH_006 | 3/3 | Covered |
| REQ-03 | Demand Workbench | Grid shows statistical and final forecast for 8 weekly buckets with row and grand totals | TS_XPR_DMD_01 | TC_XPR_DMD_001, TC_XPR_DMD_002 | 2/2 | Covered |
| REQ-04 | Demand Workbench | W1-W2 are frozen and cannot be overridden | TS_XPR_DMD_02 | TC_XPR_DMD_003, TC_XPR_DMD_004 | 2/2 | Covered |
| REQ-05 | Demand Workbench | Overrides beyond ±20% of statistical require a reason code; values 0-1,000,000 whole numbers | TS_XPR_DMD_03, TS_XPR_DMD_04 | TC_XPR_DMD_005, TC_XPR_DMD_006, TC_XPR_DMD_007, TC_XPR_DMD_008, TC_XPR_DMD_009, TC_XPR_DMD_010, TC_XPR_DMD_011, TC_XPR_DMD_012 | 7/8 | Covered |
| REQ-06 | Demand Workbench | Every override and clear is written to the audit trail | TS_XPR_DMD_05 | TC_XPR_DMD_013 | 1/1 | Covered |
| REQ-07 | Inventory Policy | Safety stock and reorder point calculated for service levels 90/95/98/99% | TS_XPR_INV_01 | TC_XPR_INV_001, TC_XPR_INV_002, TC_XPR_INV_003, TC_XPR_INV_004 | 4/4 | Covered |
| REQ-08 | Inventory Policy | Input validation: lead time 1-365 days, demand inputs non-negative | TS_XPR_INV_02 | TC_XPR_INV_005, TC_XPR_INV_006 | 2/2 | Covered |
| REQ-09 | Replenishment | Recommended quantity is rounded up to a multiple of supplier MOQ | TS_XPR_REP_01, TS_XPR_REP_02 | TC_XPR_REP_001, TC_XPR_REP_002, TC_XPR_REP_003, TC_XPR_REP_004 | 4/4 | Covered |
| REQ-10 | Replenishment | Bulk approval creates PO numbers; approval is all-or-nothing | TS_XPR_REP_03 | TC_XPR_REP_005, TC_XPR_REP_006, TC_XPR_REP_008 | 3/3 | Covered |
| REQ-11 | Replenishment | Rejection requires a reason of at least 5 characters | TS_XPR_REP_04 | TC_XPR_REP_007 | 1/1 | Covered |
| REQ-12 | Scenario Planning | Create what-if scenarios with uplift −50% to +100% versus current baseline | TS_XPR_SCN_01, TS_XPR_SCN_02, TS_XPR_SCN_03 | TC_XPR_SCN_001, TC_XPR_SCN_002, TC_XPR_SCN_003, TC_XPR_SCN_004, TC_XPR_SCN_005 | 4/5 | Covered |
