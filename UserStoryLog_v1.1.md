# FileBuddyAI User Story Log — v1.1

**Release Date:** June 30, 2026  
**Baseline:** FileBuddyAI_Dashboard_RealDoc_4.html (v1.0)  
**New Version:** FileBuddyAI_Dashboard_RealDoc_4_v1.1.html  
**Learning Objective:** Align UI to broker operational workflow and terminology; remove cost-reduction framing; establish agent-centric visibility model

---

## User Story Summary

v1.1 consolidates eight targeted improvements driven by Experiment 2A broker interviews. Changes address three strategic priorities: (1) remove cost-reduction positioning that invites comparison with cheaper tools, (2) standardize terminology to match broker language, (3) establish 60/40 layout that prioritizes agent performance visibility with supporting transaction context.

All changes preserve the locked design system (Navy #0A1628, Sky #0EA5E9, Teal #0D9488, three-signal compliance system).

---

## User Story Tracking Table

| Change ID | Feature | Source Category | Status | Priority | Evidence |
|-----------|---------|-----------------|--------|----------|----------|
| v1.1-C1 | Remove "Errors Prevented" stat card; add transaction volume metrics | Customer-Validated | Complete | High | Jerry Ascencio rejected aggregate $41K savings figure; Joe Castillo: brokers act on per-finding exposure, not cumulative totals |
| v1.1-C2 | Remove "Errors Prevented" panel from sidebar | Business-Driven | Complete | High | Cost-reduction framing conflicts with positioning as QA (proactive), not cost-cutting tool |
| v1.1-C3 | Remove "Hours Saved" metric from sidebar | Business-Driven | Complete | High | Hours saved invites comparison with cheaper tools; real value is liability reduction and visibility (Daisy Lopez-Cid) |
| v1.1-C4 | Rename "Completed" to "Closed" throughout UI | Terminology Standardization | Complete | Medium | Real estate standard term; Joe Castillo and broker team use "closed" exclusively; UI should mirror broker language |
| v1.1-C5 | Rename "Cost Risks" to "Contingency Risks" globally | Customer-Validated | Complete | Medium | Broker confusion between financial error (cost) and timeline/legal gap (contingency); clearer framing reduces cognitive load |
| v1.1-C6 | Unified 60/40 grid layout (Agent Scores 60% / Upcoming Closings 40%) | Customer-Validated | Complete | High | Ray Hernandez, Daisy Lopez-Cid, Marisol Torres independently described same desired layout; reflects broker workflow priority |
| v1.1-C7 | Fix HTML structure (remove extra closing div at line 1243) | Bug Fix | Complete | High | Extra `</div>` breaking grid rendering; Row 3 overlapping Row 2; HTML validation |
| v1.1-C8 | Fix duplicate class attribute on ps-upload element | Bug Fix | Complete | Medium | Invalid HTML; second class attribute ignored by browsers; prevented upload screen styling |

---

## Change Details with Evidence

### Change 1: Remove "Errors Prevented" stat card; add transaction volume metrics

**User Story:**  
As a broker, I need to see transaction context (volume and revenue) without being positioned as a cost-cutting tool, because I evaluate FilebuddyAI on liability reduction and operational visibility, not labor savings.

**What Changed:**
- Removed: "Errors Prevented (MTD)" stat card with $41K dollar figure
- Added: Two new metrics in top-right position
  - Total Monthly Transaction Volume ($847,500, Sky blue)
  - Total Monthly Gross Commission Income ($127,050, Verified green)
- Dashboard now uses 5-card header layout (was 4-card)

**Source Evidence:**
- Jerry Ascencio (Experiment 2A): Explicitly rejected the $41K aggregate errors-prevented figure. Brokers do not think in terms of cumulative error prevention; they think in terms of per-transaction risk.
- Joe Castillo (Experiment 2A): "Brokers act on per-finding dollar exposure, not cumulative savings scorecards."
- Operating System Principle: "Do not position on cost reduction. Cost reduction is a byproduct of automation, not a positioning strategy."

**Impact:** Removes the perception of FilebuddyAI as a cost-cutting tool. Establishes transaction volume and GCI as operational context metrics that frame compliance work intensity without claiming labor savings.

**Status:** Complete  
**Priority:** High (blocking customer perception)

---

### Change 2: Remove "Errors Prevented" panel from sidebar

**User Story:**  
As a broker, I need the sidebar to contain only actionable compliance information, not cumulative cost savings, because savings aggregation obscures the per-finding risk exposure I actually care about.

**What Changed:**
- Removed: `panel-savings` div (right-slide panel triggered by "Errors Prevented" card)
- Panel previously displayed: cumulative error prevention data, hours saved, cost avoidance
- Sidebar now contains four core panels: Compliance Details, Contingency Risk Details, Agent Performance, Transaction Status

**Source Evidence:**
- Operating System Principle (Phase 1 positioning): "FilebuddyAI decouples compliance capacity from the hiring cycle, permanently. It is not a cost-cutting tool. It is a structural operational advantage."
- Bianca Davila (Experiment 2A, Session 1): "Value is not cost savings; it's knowing what is happening in every file."

**Impact:** Streamlines sidebar to focus on compliance and performance visibility. Eliminates redundancy after Change 1. Reinforces QA positioning (proactive intervention) rather than cost-reduction positioning.

**Status:** Complete  
**Priority:** High (strategic positioning requirement)

---

### Change 3: Remove "Hours Saved" metric from sidebar

**User Story:**  
As a broker, I do not want to see labor hours in the compliance dashboard, because hours saved invites price competition I don't want to have with cheaper compliance tools.

**What Changed:**
- Removed: "Hours saved this month" widget from left sidebar (previously under sidebar-savings div)
- This metric was removed as part of shift away from cost-reduction framing

**Source Evidence:**
- Operating System Language Standards: "Do not position on cost reduction."
- Daisy Lopez-Cid (Experiment 2A): "The value is that I know what is happening in every file." (Not "I saved 6 hours.")
- Market Entry Logic: "Positioning on cost savings anchors the product in the wrong conversation and invites comparison with cheaper tools."

**Impact:** Eliminates the primary comparison metric that invites competition on price/efficiency. Reinforces that FilebuddyAI competes on visibility and liability reduction, not labor replacement.

**Status:** Complete  
**Priority:** High (customer-facing messaging consistency)

---

### Change 4: Rename "Completed" to "Closed" throughout UI

**User Story:**  
As a broker, I need the UI to use my language, not parallel terminology, because it reduces cognitive load and makes the system feel native to real estate workflow.

**What Changed:**
- Global text replacement across dashboard:
  - Transaction status label: "Completed" → "Closed"
  - Navigation panel title: "Completed Transactions" → "Closed Transactions"
  - Status filter tag: "completed" → "closed"

**Source Evidence:**
- Joe Castillo (Experiment 2A): Uses "closed" exclusively when describing transaction state
- Broker team consensus: "Closed" is the legal and industry-standard term for finalized transactions
- Operating System Principle (Jobs/Apple lens): "The system must feel native to broker workflow, not introduce parallel terminology."

**Impact:** Eliminates micro-friction from non-standard terminology. Increases intuitiveness without training. Aligns UI language with real estate contracts and legal documents.

**Status:** Complete  
**Priority:** Medium (usability improvement; not blocking)

---

### Change 5: Rename "Cost Risks" to "Contingency Risks" globally

**User Story:**  
As a broker, I need clear distinction between compliance errors and transaction timeline gaps, because these require different remediation actions and communicate different urgency levels.

**What Changed:**
- Global rename across all instances:
  - CSS classes: `.cost-risk` → `.contingency-risk`
  - JavaScript event handlers: `panel-costrisk` → `panel-contingencyrisk`
  - UI labels: "Cost Risk" → "Contingency Risk"
  - Badge colors: Amber (⚠️) preserved (unchanged)

**Technical Scope:** All references to cost-risk terminology updated; three-signal system (red/amber/green) remains unmixed.

**Source Evidence:**
- Experiment 2A broker interviews: Observed confusion between "cost risk" (financial error: missing signature, misclassified property type) and "contingency risk" (timeline or legal gap: inspection deadline, appraisal contingency, financing deadline)
- Joe Castillo: "These are different problems. One breaks the deal, the other breaks the timeline."
- Operating System Principle: "Compliance Risks (red) are contract errors. Contingency Risks (amber) are timeline or legal gaps that require verification before close."

**Impact:** Reduces cognitive friction in risk categorization. Enables brokers to triage risks correctly without training. Aligns terminology with real estate transaction structure.

**Status:** Complete  
**Priority:** Medium (terminology clarity; not blocking)

---

### Change 6: Unified 60/40 grid layout for Rows 2 and 3

**User Story:**  
As a broker, I want to see agent compliance scores and upcoming closings side-by-side, because this layout mirrors how I actually manage my office — agent performance first, pipeline visibility supporting.

**What Changed:**
- Restructured dashboard layout from variable-width flex to consistent 60/40 split grid:
  - **Row 2:** Agent Compliance Scores (60% left) | Upcoming Closings (40% right)
  - **Row 3:** Transactions Reviewed (60% left) | Live Issues Feed (40% right)
- Technical implementation:
  - Two grid containers: `content-grid` (Row 2) and `bottom-grid` (Row 3)
  - CSS: `display: grid; grid-template-columns: 60% 40%; gap: 20px; align-items: start;`
  - Cards: `min-width: 0; overflow: hidden;` to prevent content overflow
- Previously: Rows were stacked vertically with uneven width distribution

**Source Evidence:**
- Ray Hernandez (Experiment 2A): Described desire to see agent performance paired with pipeline context
- Daisy Lopez-Cid (Experiment 2A): "I need to know my agents and my closings at the same time"
- Marisol Torres (Experiment 2A): Independently arrived at same layout preference
- High Visibility principle (Operating System): "The system reveals agent-level performance, compliance patterns, and transaction status in real time."

**Impact:** Establishes agent-centric visibility as primary dashboard function with supporting transaction context. Validates High Visibility differentiation vector. Enables brokers to correlate agent performance with pipeline without scroll/navigation friction.

**Status:** Complete  
**Priority:** High (core to differentiation positioning)

---

### Change 7: Fix HTML structure (remove extra closing div)

**User Story:**  
As a developer, I need valid HTML structure so that CSS grid rules render correctly and layout components display as intended.

**What Changed:**
- Removed malformed closing div tag at line 1243
- The extra `</div>` was closing the `content-grid` prematurely, causing Row 3 to overlap Row 2 visually
- Row 3 rendered on top of Row 2 despite correct CSS grid rules

**Source Evidence:**
- HTML validation
- The extra closing tag was introduced during a prior iteration
- Prevented 60/40 grid from rendering correctly

**Impact:** Fixes layout rendering. Row 2 and Row 3 now display side-by-side as designed. No visual overlap. CSS grid functions as intended.

**Status:** Complete  
**Priority:** High (blocks Change 6 from displaying correctly)

---

### Change 8: Fix duplicate class attribute on ps-upload element

**User Story:**  
As a developer, I need valid HTML so that all CSS classes apply correctly to modal elements, ensuring consistent styling across all prototype panel screens.

**What Changed:**
- Merged duplicate class attributes on FileBuddyAI prototype panel upload screen:
  - Before: `<div class="pscreen" id="ps-upload" class="pscreen-upload">`
  - After: `<div class="pscreen pscreen-upload" id="ps-upload">`

**Source Evidence:**
- Invalid HTML. Browsers ignore the second class attribute when duplicates appear on the same element.
- This prevented the upload screen styling (`.pscreen-upload` class) from applying correctly
- Affected the prototype modal (File Review) display when upload screen was active

**Impact:** Both `.pscreen` (base modal styles) and `.pscreen-upload` (layout override) now apply correctly. All prototype panel screens (Upload, Processing, Results, Detail, Send, Success) render with consistent styling.

**Status:** Complete  
**Priority:** Medium (styling consistency; not blocking core functionality)

---

## Design System Compliance

All changes preserve the locked design system:
- Primary Navy: #0A1628
- Secondary Sky: #0EA5E9
- Accent Teal: #0D9488
- Verified Green: #047857
- Primary Font: Syne (headings, UI labels)
- Numeric Font: Geist (all dollar/numeric values)
- Signal System: Red (compliance) / Amber (contingency) / Green (passed) — never merged

**Result:** No design system deviations in v1.1.

---

## Testing Checklist (Completed)

- ✅ Dashboard renders at correct dimensions
- ✅ 60/40 grid displays Row 2 and Row 3 side-by-side
- ✅ Row 3 does not overlap Row 2
- ✅ Page body scrolls when content exceeds viewport
- ✅ Clicking issues in Results screen shows Detail drill-down
- ✅ All action buttons work ("Send to Agent," "See in Doc," navigation)
- ✅ Prototype modal opens and closes without layout shift
- ✅ All stat cards and metric labels display correctly
- ✅ No console errors
- ✅ Three-signal system remains unmixed (red/amber/green never combined)
- ✅ All terminology changes applied consistently
- ✅ Cost-reduction framing removed throughout

---

## Backward Compatibility

v1.1 is backward-compatible with the broker discovery workflow. No breaking changes to customer-facing functionality. The baseline file remains on GitHub as v1.0 for reference.

---

## Summary: Learning Validated

**Assumptions Confirmed:**
- Brokers will reject cost-reduction positioning (Jerry Ascencio, Joe Castillo)
- Brokers want agent-level visibility paired with transaction context (Ray, Daisy, Marisol)
- Brokers prefer industry-standard terminology over parallel naming (Joe Castillo)
- Three-signal system (Compliance/Contingency/Good) is the correct risk framework (all brokers)

**Assumptions Challenged:**
- None in this change batch

**Next Steps:**
- Commit to GitHub as v1.1
- Queue v1.2 for bug fixes and agent experience features
- Prepare for Experiment 2C with Joe Castillo

---

**Document Version:** 1.0  
**Last Updated:** July 1, 2026  
**Status:** Complete
