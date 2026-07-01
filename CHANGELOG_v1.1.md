# FileBuddyAI Dashboard Changelog — v1.1

**Release:** June 30, 2026
**Baseline:** FileBuddyAI_Dashboard_RealDoc_4.html (v1.0)
**New Version:** FileBuddyAI_Dashboard_RealDoc_4_v1.1.html

---

## Change Summary

v1.1 consolidates eight targeted UI improvements based on broker feedback (Experiment 2A interviews) and functional requirements. All changes maintain the design system (Navy #0A1628, Sky #0EA5E9, Teal #0D9488, Syne + Geist fonts, three-signal compliance system). Three-signal system (red/amber/green) remains unmixed and intact.

---

## Change Details

### Change 1: Removed "Errors Prevented" stat card; replaced with transaction volume metrics

**What changed:** The top-right stat card previously displayed "Errors Prevented (MTD)" with a dollar figure ($41K). Replaced with two new metrics:
- Total Monthly Transaction Volume ($847,500, Sky blue)
- Total Monthly Gross Commission Income ($127,050, Verified green)

**Evidence:** Jerry Ascencio (Experiment 2A) explicitly rejected aggregate dollar-savings positioning. Joe Castillo corroborated: brokers act on per-finding dollar exposure, not cumulative savings scorecards. Transaction volume and GCI are operational context metrics that frame the compliance task intensity without positioning FilebuddyAI as a cost-cutting tool.

**Location:** Dashboard header, top-right position (changed from 4-card layout to 5-card layout)

---

### Change 2: Removed "Errors Prevented" panel from sidebar

**What changed:** Eliminated the `panel-savings` element (slide-out right panel triggered by clicking the Errors Prevented card). Panel contained cumulative error prevention data and was structurally redundant after Change 1.

**Evidence:** Removing cost-savings framing from the UI reflects the founding thesis: FilebuddyAI decouples compliance capacity from the hiring cycle. Cost reduction is a byproduct, not the positioning strategy. Sidebar panels now contain: Compliance Details, Contingency Risk Details, Agent Performance, and Transaction Status (four core broker use cases).

**Location:** Right-slide panel system (panel-savings div removed)

---

### Change 3: Removed "Hours Saved" metric from sidebar

**What changed:** Eliminated the sidebar widget displaying "Hours saved this month" (previously under sidebar-savings div). This metric was removed as part of the shift away from cost-reduction framing.

**Evidence:** Same as Change 2. Hours saved (and hours prevented) are operational metrics that invite comparison with cheaper tools. Brokers care about liability reduction and visibility, not time auditing. (Daisy Lopez-Cid: "The value is that I know what is happening in every file." Not "I saved 6 hours.")

**Location:** Dashboard left sidebar

---

### Change 4: Renamed "Completed" to "Closed" throughout UI

**What changed:** Global text replacement:
- Transaction status label: "Completed" → "Closed"
- Navigation panel title: "Completed Transactions" → "Closed Transactions"
- Status filter tag: "completed" → "closed"

**Evidence:** Real estate terminology standard. "Closed" is the legal and industry-standard term for a finalized transaction. Joe Castillo and broker team use "closed" exclusively. UI should mirror broker language, not introduce parallel terminology.

**Location:** Dashboard nav, transaction list headers, status filters, panel titles

---

### Change 5: Renamed "Cost Risks" to "Contingency Risks" globally

**What changed:** Renamed all instances of cost-risk terminology:
- CSS classes: `.cost-risk` → `.contingency-risk`
- JavaScript event handlers: `panel-costrisk` → `panel-contingencyrisk`
- UI labels: "Cost Risk" → "Contingency Risk"
- Badge colors: Amber (⚠️) remains unchanged

**Evidence:** Experiment 2A interviews revealed broker confusion between "cost risk" (financial error) and "contingency risk" (timeline or legal gap that creates transaction friction). "Contingency Risk" is the clearer frame: risks that require verification or action before closing. Reduces cognitive friction in the dashboard experience.

**Location:** Risk categorization system, issue cards, detail panels, filter tags

---

### Change 6: Unified 60/40 grid layout for Rows 2 and 3

**What changed:** Restructured the dashboard layout from a variable-width flex layout to a consistent 60/40 split grid:
- **Row 2:** Agent Compliance Scores (60%) | Upcoming Closings (40%)
- **Row 3:** Transactions Reviewed (60%) | Live Issues Feed (40%)

Previously: Rows were stacked vertically with uneven width distribution.

**Evidence:** Ray Hernandez, Daisy Lopez-Cid, and Marisol Torres independently described the same desired dashboard layout in Experiment 2A: agent-level compliance visibility paired with transaction pipeline visibility. The 60/40 split reflects real estate broker workflow: primary focus on agent performance (left), supporting context on pipeline status (right).

**Technical implementation:** 
- Two grid containers (content-grid for Row 2, bottom-grid for Row 3)
- CSS: `display: grid; grid-template-columns: 60% 40%; gap: 20px; align-items: start;`
- Cards: `min-width: 0; overflow: hidden;` to prevent content overflow in grid cells

---

### Change 7: Fixed HTML structure (removed extra closing div)

**What changed:** Removed malformed closing div tag at line 1243 that was breaking the layout grid. The extra `</div>` was closing the content-grid prematurely, causing Row 3 to overlap Row 2 visually.

**Evidence:** HTML validation. The extra closing tag was introduced during a prior iteration and prevented the 60/40 grid from rendering correctly. Row 3 blocked Row 2 from display despite correct CSS rules.

**Location:** HTML structure, line 1243 (between Upcoming Closings card and bottom-grid container)

---

### Change 8: Fixed duplicate class attribute on ps-upload element

**What changed:** Merged duplicate class attributes on the FileBuddyAI prototype panel upload screen:
- Before: `<div class="pscreen" id="ps-upload" class="pscreen-upload">`
- After: `<div class="pscreen pscreen-upload" id="ps-upload">`

**Evidence:** Invalid HTML. Browsers ignore the second class attribute when duplicates appear on the same element. This prevented the upload screen styling from applying correctly. The fix ensures both `.pscreen` (base styles) and `.pscreen-upload` (layout override) are applied.

**Impact on user experience:** The prototype panel (File Review modal) now displays correctly with proper justification and alignment when the upload screen is active. All modal screens (Upload, Processing, Results, Detail, Send, Success) now render with consistent styling.

**Location:** HTML prototype modal structure, upload screen element

---

## Design System Status

All changes preserve the locked design system:
- Primary Navy: #0A1628
- Secondary Sky: #0EA5E9
- Accent Teal: #0D9488
- Verified Green: #047857
- Primary Font: Syne (headings, UI labels)
- Numeric Font: Geist (all dollar/numeric values)
- Signal System: Red (compliance) / Amber (contingency risk) / Green (passed) — never merged

No design system deviations in v1.1.

---

## Testing Checklist

- [x] Dashboard renders at correct dimensions (420px × 540px prototype modal)
- [x] 60/40 grid displays Row 2 and Row 3 side-by-side
- [x] Row 3 does not overlap Row 2
- [x] Page body scrolls when content exceeds viewport
- [x] Clicking issues in Results screen shows Detail drill-down with all sections (What we found, Regulation, Document excerpt, Action)
- [x] "Send to Agent," "See in Doc," and back navigation work in detail panel
- [x] Prototype modal opens and closes without layout shift
- [x] All stat cards and metric labels display correctly
- [x] No console errors
- [x] Three-signal system remains unmixed (red/amber/green never combined)

---

## Backward Compatibility

v1.1 is backward-compatible with the broker discovery workflow. No breaking changes to customer-facing functionality. The operating file remains on GitHub as v1.0 for reference.

---

## Next Steps

- Commit to GitHub as v1.1
- Update GitHub Pages live demo link to v1.1
- Queue additional changes for v1.2 (to be determined based on next broker feedback or learning priority)
