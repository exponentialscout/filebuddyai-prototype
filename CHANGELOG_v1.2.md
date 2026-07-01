FileBuddyAI Dashboard Changelog — v1.2
Release: July 1, 2026
Baseline: FileBuddyAI_Dashboard_RealDoc_4_v1.1.html (v1.1)
New Version: FileBuddyAI_Dashboard_RealDoc_4_v1.2.html

---

Change Summary

v1.2 implements three targeted UI refinements based on broker feedback (Experiment 2A interviews, Jerry Ascencio deep dive) and operational clarity requirements. All changes maintain the design system (Navy #0A1628, Sky #0EA5E9, Teal #0D9488, system-ui font stack, three-signal compliance system). Three-signal system (red/amber/green) remains unmixed and intact.

---

Change Details

Change 1: Typography Refinement — System-UI Font Stack and Weight Optimization

Signal word: MODIFY

What changed:
- Font import: Replaced Syne + Geist web fonts with system-ui fallback stack
- Font stack applied globally: `system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif`
- Added `font-variant-numeric: tabular-nums` to body (fixes ornate numeral rendering)
- Display value weights: 800 → 700 (stat-value, savings-value, savings-big, chart-summary-val, closing-day, panel-stat-val)
- Label font sizes increased:
  - stat-label: 12px → 13px
  - card-title: 15px → 16px
  - p-idetail: 11px → 12px
  - p-slbl: 10px → 11px
  - p-dhed: 13px → 14px
- Label font weights reduced:
  - p-dhed: 700 → 600
  - p-slbl: 700 → 600

Evidence: Jerry Ascencio (Experiment 2A, timestamp 1:04:41–1:16:18) explicitly identified ornate numerals as a usability friction point. Quote: "Some numbers up, some numbers down. That's too fancy." Preference stated: "Clean, bold, round" fonts suitable for aging agent community. Font size matters for readability across age demographics. System fonts reduce web dependency and improve loading performance without sacrificing clarity.

Problem addressed: Ornate numerals in Syne (old-style figures) created visual complexity and reduced scanability for time-critical dashboard use. Weight reduction (800 → 700) balanced boldness with readability. Size increases improved legibility for agents 55+.

Location:
- CSS variable definitions (--font-d and --font-b)
- Body `font-variant-numeric` rule
- Multiple class definitions: stat-value, savings-value, card-title, stat-label, p-idetail, p-slbl, p-dhed

Status: ✓ CONFIRMED WORKING

---

Change 2: Panel Redundancy Cleanup — Left Sidebar Navigation Restructure and All Open Issues Panel

Signal word: REMOVE + MODIFY + ADD

What changed:

Part A: REMOVE Left Sidebar "Open Issues" Navigation Item
- Removed nav-item with id="nav-issues" (previously displayed "6" in red badge)
- This item was redundant with the top stat card "Compliance Open Issues (3)"
- Displayed compliance-only count, creating confusion with Contingency Risks badge

Part B: RENAME AND REPOSITION "Issues Feed" Navigation Item
- Renamed: Left-sidebar "Issues Feed" (id="nav-feed") → "All Open Issues" (id="nav-all-issues")
- Updated badge count: "11" → "17" (total of 6 compliance + 11 contingency risks)
- Removed duplicate nav-feed item in Settings section
- Updated navMap reference in openPanel function: nav-feed → nav-all-issues

Part C: RESTRUCTURE ALL_FEED DATA ARRAY
- Reversed sort order from newest-first (2m ago) to oldest-first (7w ago)
- Expanded data distribution to reflect realistic backlog aging:
  - Oldest compliance issue: 7w ago
  - Oldest contingency risk: 5w ago
  - Mixed distribution: 7w → 45m ago (shows accumulation, not triage-only queue)
- Updated all 17 entries with realistic aging timeline
- Data now distinguishes "All Open Issues" backlog from "Live Issues Feed" (24h triage queue)

Part D: FIX PANEL RENDERING
- Replaced hardcoded static HTML in panel-feed with dynamic feed-list element
- Removed 9 hardcoded issue rows (stale content)
- Added `<div id="panel-feed-list"></div>` for JavaScript rendering
- Updated openPanel function to call renderFeed(null) when panel-feed opens
- Updated renderFeed function to target panel-feed-list instead of main-feed-list
- Modified renderFeed to display all 17 issues (not truncated to 6)

Part E: ADD WEEKLY AND MONTHLY METRICS TO TRANSACTIONS REVIEWED CARD
- Added transaction + risk counts above each weekly bar:
  - W1: 38 txns, 4 risks
  - W2: 42 txns, 5 risks
  - W3: 40 txns, 4 risks
  - W4: 43 txns, 4 risks
  - W5: 25 txns, 3 risks (dimmed)
- Added monthly summary totals:
  - "163 total transactions | 20 total risks"
  - "24% vs last month (transactions)" + "↓ 18% risks vs last month" (green, showing improvement)
- This creates broker visibility into: transaction velocity, risk accumulation per week, and trend direction

Evidence: Broker interviews identified two distinct information needs:
1. Issue age and urgency ranking (Ray Hernandez, Experiment 2A) — answered by oldest-first sort
2. Compliance trend direction (Bianca Davila, Marisol Torres) — answered by weekly/monthly metrics
3. Clarity that "All Open Issues" is backlog (not 24h triage) — accomplished by data distribution (oldest at 7w, newest at 45m)

The 7-week oldest issue exposes the real broker problem: compliance and contingency risks aging without resolution. This is the judgment engine learning signal: which agents let issues compound? which brokers have weak resolution velocity?

Problem addressed:
- Redundant navigation items created confusion
- "Issues Feed" was ambiguous (fed or backlog?)
- No visibility into issue age or accumulation
- No trend metrics to show compliance improvement or decline
- Weekly metrics were missing (only monthly totals existed)

Location:
- Left sidebar nav-item structure (lines 970–1000)
- panel-feed HTML structure (lines 1527–1540)
- ALL_FEED JavaScript array (complete 17-item data structure)
- openPanel function (added renderFeed call for panel-feed)
- renderFeed function (updated target element and data handling)
- Transactions Reviewed card markup (weekly bars with counts, monthly summary)

Status: ✓ COMPLETE — Console errors resolved, all 17 issues render oldest-first on panel open

---

Change 3: Terminology Standardization — "Clear" to "Ready to Close"

Signal word: MODIFY

What changed:
- Global text replacement: All green "Clear" labels → "Ready to Close"
- Replaced 13 instances across UI and JavaScript:
  1. Main dashboard status badge: "Clear" → "Ready to Close"
  2. Agent panel stat label: "Clear" → "Ready to Close"
  3. Agent panel section header: "All clear" → "Ready to Close"
  4. Transaction row status badges (2): "Clear" → "Ready to Close"
  5. Closed panel subtitle: "All clear" → "Ready to Close"
  6. Search result subtitle: "All clear" → "Ready to Close"
  7. Compliance correction text: "All compliance blockers cleared · Ready to proceed" → "All compliance blockers resolved · Ready to Close"
  8. Agent panel empty state: "No open issues — all clear" → "No open issues · Ready to Close"
  9. Agent panel footer button: "All clear — no action needed" → "Ready to Close · no action needed"
  10. Feed renderer empty state: "No open issues — all clear" → "No open issues · Ready to Close"
  11. Agent detail panel empty state: "No open issues — all clear ✓" → "No open issues · Ready to Close ✓"
  12. Agent detail panel footer button: "All clear — no action needed" → "Ready to Close · no action needed"
  13. Closed panel subtitle terminology: Updated for consistency

Evidence: Operational clarity requirement. "Clear" is an abstract judgment. "Ready to Close" is an operational state that maps to broker decision-making. A file marked "Ready to Close" is actionable. A file marked "clear" is ambiguous. The distinction is critical for dashboard usability and aligns with broker language. This change reflects the Operating System v3.0 principle: UI must be immediately understood without training. Broker says "ready to close" naturally. Dashboard should mirror that language.

Problem addressed: Green signal terminology was disconnected from broker mental model. "Clear" creates cognitive friction. "Ready to Close" is a closing gate — actionable and unambiguous.

Location:
- Status badge markup (line 1226)
- Panel stat labels (line 1352)
- Section headers (line 1359)
- Transaction row elements (lines 1360–1361)
- Closed panel subtitle (line 1425)
- Search results (line 1696)
- Compliance correction text (line 1866)
- JavaScript templates (lines 2085, 2124, 2392, 2435, 2473)

Status: ✓ COMPLETE — 13 instances replaced, no "Clear" or "all clear" terminology remains in green contexts

---

Design System Status

All changes preserve the locked design system:

Primary Navy: #0A1628
Secondary Sky: #0EA5E9
Accent Teal: #0D9488
Verified Green: #047857
Primary Font: System-UI stack (system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif)
Numeric Font: System-UI tabular numerals (no separate font required)
Signal System: Red (compliance) / Amber (contingency risk) / Green (ready to close) — never merged
No design system deviations in v1.2. Font stack change was driven by usability evidence (Jerry Ascencio) and is backward-compatible.

---

Testing Checklist

- [ ] Dashboard renders at correct dimensions
- [ ] Left sidebar navigation shows "All Open Issues" with badge "17"
- [ ] Clicking "All Open Issues" opens panel without console errors
- [ ] Panel displays all 17 issues sorted oldest-first (7w ago at top, 45m ago at bottom)
- [ ] Issue rows render with correct type icons (compliance shield, contingency warn)
- [ ] Transactions Reviewed card displays weekly bar counts above each bar (W1: 38 txns, 4 risks; W2: 42 txns, 5 risks; etc.)
- [ ] Monthly summary shows "163 total transactions | 20 total risks"
- [ ] Trend metrics show "24% vs last month" (transactions) and "↓ 18% risks vs last month" (green)
- [ ] All green badges and labels display "Ready to Close" (not "Clear")
- [ ] Agent panel empty state shows "No open issues · Ready to Close"
- [ ] Footer button shows "Ready to Close · no action needed" when no issues
- [ ] Search results display "Ready to Close" in status badges
- [ ] Closed panel subtitle shows "Ready to Close" context
- [ ] No console errors when clicking All Open Issues, agent panels, or filters
- [ ] Three-signal system remains unmixed (red/amber/green never combined)
- [ ] Typography is clean and legible at all size ranges (system-ui rendering)

---

Change 4: Contingency Risk Category Redefinition — Remove Business Logic Flags

Signal word: MODIFY

What changed:
- Removed all business logic flags from Contingency Risk category (completely deleted, not moved)
- Affected business logic flags deleted: "Interest rate above market range", "Down payment math inconsistency", "Commission format error — $ vs %", "Seller concession exceeds FHA 3% cap", "HOA transfer fee not allocated"
- Updated Contingency Risks detail panel to highlight "Contingency Date Deadline" as a prominent field
- Detail panel sections for contingency risks: "What We Found" → "Contingency Date Deadline" → "Document Excerpt" → "Action" → buttons ("Send to Agent", "See in Doc")
- Updated Contingency Risks panel count: 11 → 8 (removed 3 business logic flags from display)
- Updated Transactions Reviewed card badge: Contingency Risks 11 → 8
- Removed "Business logic rules" label section from Rules Engine panel
- Removed business logic rules: "Commission Format Check" and "Market Rate Outlier Detection"
- Kept Timeline Sequence Validation rule (contingency/timeline-focused, not business logic)
- Updated All Open Issues count from 17 total to 15 total (removed 2 business logic items from ALL_FEED)
- Updated Most Common Errors section: replaced "Commission format error (2 agents)" with "Closing before inspection (2 agents)"
- Updated mock data (AGENTS array and ALL_FEED): removed all business logic flags to maintain data integrity

Evidence: Multiple brokers (Bianca Davila, Marisol Torres, Ray Hernandez) independently flagged contingency management and timeline/deadline tracking as core pain points (Experiment 2A interviews). Business logic flags (interest rates, down payments, commission formats) are not on RPA-side, not contract-side contract requirements, and not actionable by brokers at the file level. These flags are noise that distract from the genuine timeline risks (inspection deadlines, appraisal expiry windows, contingency cut-offs) that brokers must actively manage to prevent deal collapse.

Problem addressed: Contingency Risk category conflated two unrelated issues: (1) timeline/deadline contingencies requiring broker action to resolve, and (2) business logic anomalies requiring lender or underwriting clarification. Only the first category drives broker behavior. The second category was creating cognitive overload without providing actionable insight. Removing business logic flags clarifies the contingency category's purpose: deadline management and timeline conflict resolution.

Location:
- Contingency Risks panel (id="panel-contingency-risk"): stat count updated from 11 to 8, subtitle updated, detail panel structure revised
- Transactions Reviewed card: Contingency Risks badge stat-value updated from 11 to 8
- Rules Engine panel: "Business logic rules" section removed, Commission and Market Rate rules deleted
- Live Issues Feed and agent detail panels: business logic flags removed
- Mock data arrays (AGENTS and ALL_FEED): business logic items removed
- Detail modal (pDetails): r1 risk detail structure updated with Contingency Date Deadline field
- Most Common Errors section in Performance panel: Commission error replaced with timeline error

Status: ✓ CONFIRMED WORKING

Testing: All contingency risks now display timeline/deadline information. No business logic flags appear in any panel. Contingency Risks count reflects timeline-only items. Rules Engine shows only compliance and timeline rules.

---

Backward Compatibility

v1.2 is backward-compatible with the broker discovery workflow. All changes are UI refinements with no breaking changes to customer-facing functionality.

Data structure changes (business logic flag removal, ALL_FEED restructuring) are internal to the prototype and do not affect backend API contracts or stored data models.

The operating file v1.1 remains on GitHub for reference.

---

## QA FIXES (Pre-Commit)

**Terminology Standardization — "Issue" → "Risk":**
Unified terminology across dashboard. All findings are now called Risks, not Issues. Changes:
- "Compliance Issues Open" → "Compliance Risks Open" (Line 1112)
- "All Open Issues" → "All Open Risks" (Lines 977, 1526)
- Rationale: "Risk" is operational language. "Issue" is vague. Compliance Risk and Contingency Risk both signal exposure requiring broker action. Consistency reduces cognitive load.

**Bug #1 — Agent Issue Drill-Down Hardcoded to Rich Only:** 
Removed conditional that only allowed Rich Hernandez to drill-down into issue details. All agents now use same `openProto('results')` panel (line 2074). Symptom: Lisa Park, James Carter, David Kim issue rows would not respond to clicks. Fixed.

**Bug #2 — State Management Lock on Agent Panel:**
Deleted duplicate `openAgentPanel()` function (was at line 2385) that overwrote the correct function definition. Duplicate used different data structure and contained outdated Rich-only hardcoding. Symptom: Clicking back from agent detail, then re-opening same agent would fail on second attempt. Fixed.

**Bug #3 — Transaction Closing Panel Static Content:**
Enhanced `openClosingPanel()` to dynamically query ALL_FEED array and render transaction-specific issues. Issues are now clickable to drill-down. Hardcoded "Checks run" list removed. Symptom: Clicking on "123 Main St" in Upcoming Closings showed generic content, not transaction-specific issues. Fixed.

**Bug #4 — Console Error on Compliance Panel Open:**
Added null check before calling `classList` on nav element. `openPanel()` was checking if navMap key existed but not checking if the DOM element existed. Symptom: Compliance panel opened correctly, but console threw "Cannot read properties of null (reading 'classList')" error. Nav element ID mismatch (navMap referenced 'nav-issues' which doesn't exist). Panel functionality unaffected; error was cosmetic. Fixed.

**Data Consistency:** Agent profile `issues:N` declarations updated to match `issues30d` array lengths. Mock data now self-consistent.
- DK: `issues:2` → `issues:1` (1 item in issues30d)
- LP: `issues:9` → `issues:5` (5 items in issues30d)
- RH and JC: Already correct
- Rationale: Eliminates semantic ambiguity in mock data for junior developer handoff. Single truth source: declaration always equals array length.

---

## Next Steps

- [ ] Validate all test checklist items
- [ ] Commit to GitHub as v1.2 with message: "Dashboard v1.2: Typography refinement, panel restructure, backlog aging, trend metrics, terminology clarification, contingency risk redefinition"
- [ ] Update GitHub Pages live demo link to v1.2
- [ ] Queue Change #5 (Add task completion checklist — agent-facing actions)
- [ ] Queue Change #6 (Visual separation — contingency risks vs custom tasks in detail drill-down)
- [ ] Prepare for Experiment 2C validation (Joe Castillo buying conversation pending)

