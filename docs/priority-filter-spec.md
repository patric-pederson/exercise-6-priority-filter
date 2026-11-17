Priority Filter Specification

## Goal
Give managers a fast, client-side way to filter equipment requests by priority level so urgent items stand out immediately without altering stored request records.

## User Need
As a manager reviewing incoming equipment requests, I need to quickly narrow the request list to items that require attention (such as `High` priority or `High` + `Medium` priority) and easily return to the full list.

## Functional Rules
1. **Filter Controls:** Display four filter buttons above the equipment requests table: `All` (default), `Needs Attention (High & Medium)`, `High Only`, and `Low Only`.
2. **Default State:** On initial page load, `All` is active and all 6 existing equipment requests are displayed in their original order.
3. **Filtering Behavior:**
   - Selecting `Needs Attention (High & Medium)` displays only requests with `priority === "High"` or `priority === "Medium"`.
   - Selecting `High Only` displays only requests with `priority === "High"`.
   - Selecting `Low Only` displays only requests with `priority === "Low"`.
   - Selecting `All` restores the full list of requests.
4. **Result Counter & Empty State:** Display a visible count of currently shown requests (e.g., `Showing 2 of 6 requests`). If a filter returns zero matching items, display a clear `No matching equipment requests` message instead of a blank table.
5. **Non-Destructive Filtering:** Filtering operates strictly on the rendered view in memory; underlying request objects are never deleted, mutated, or reordered.

## Constraints
- Must use existing `priority` values (`High`, `Medium`, `Low`) already present in the application data.
- Must operate 100% client-side with no login, authentication, or external database.
- Must preserve all existing equipment requests and table columns (`ID`, `Item`, `Department`, `Priority`, `Status`)[cite: 1].

## Acceptance Criteria
- **AC-1 (Default View):** Loading the page displays all 6 equipment requests with the `All` filter active and a counter reading `Showing 6 of 6 requests`.
- **AC-2 (Needs Attention Filter):** Clicking `Needs Attention (High & Medium)` displays only the 4 `High` and `Medium` requests (`REQ-101`, `REQ-103`, `REQ-104`, `REQ-105`), hides `Low` priority rows, and updates the counter to `Showing 4 of 6 requests`.
- **AC-3 (High Only Filter):** Clicking `High Only` displays only the 2 `High` priority requests (`REQ-101`, `REQ-103`) and updates the counter to `Showing 2 of 6 requests`.
- **AC-4 (Reset to All & Data Preservation):** Clicking `All` after filtering immediately restores all 6 original requests with their original IDs, items, departments, priorities, and statuses intact[cite: 1].
- **AC-5 (Empty State Handling):** If the dataset contains zero requests matching an active filter, the table body displays `No matching equipment requests` without throwing console errors.

## Out of Scope
- User authentication, role-based permissions, or backend database persistence[cite: 1].
- Creating, editing, or deleting equipment requests.
- Multi-column sorting or free-text search.

## Verification Results
- **AC-1 (Default View):** Pass — Initial load displays all 6 requests, highlights `All`, and shows `Showing 6 of 6 requests`.
- **AC-2 (Needs Attention Filter):** Pass — Selecting `Needs Attention (High & Medium)` displays only `High` and `Medium` rows (4 of 6) and hides `Low` rows.
- **AC-3 (High Only Filter):** Pass — Selecting `High Only` displays only `REQ-101` and `REQ-103` (2 of 6).
- **AC-4 (Reset to All & Data Preservation):** Pass — Returning to `All` displays all 6 unmodified requests.
- **AC-5 (Empty State Handling):** Pass — Filtering against an empty match renders the fallback empty-state row cleanly.
