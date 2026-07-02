# FileBuddyAI — User Story Log v1.3

**Release:** v1.3  
**Date:** July 2, 2026  
**Change ID:** C7 (PDF Viewer with Risk Highlighting)

---

## C7: PDF VIEWER — VALIDATION NARRATIVE

### User Story

**As a** broker (Joe Castillo, pilot participant)  
**I want to** see the actual document with the AI-flagged risk highlighted  
**So that** I can confirm the finding is real and not a false positive, and make an informed decision about escalation

### Acceptance Criteria

1. **Document Display**
   - [ ] PDF renders in modal viewer with clear readability
   - [ ] Navigation controls (prev/next page) function without lag
   - [ ] Page counter shows current page / total pages
   - [ ] Browser zoom works without breaking highlight positioning

2. **Risk Highlighting**
   - [ ] Compliance risks highlight in red (#b91c1c)
   - [ ] Contingency risks highlight in amber (#b45309)
   - [ ] Highlight opacity is visible but non-intrusive (25% rest, 40% hover)
   - [ ] Highlight shape correctly maps to actual document error location
   - [ ] Clicking highlight returns to risk detail screen

3. **Navigation Flow**
   - [ ] "See in document" button on risk detail opens PDF viewer at correct page
   - [ ] Tab bar shows [Results] [Detail] [Document] only during review flow
   - [ ] Tab bar hidden during upload, processing, success, and audit screens
   - [ ] Back navigation from PDF returns to detail screen with tab state preserved

4. **Coordinate Validation**
   - [ ] Lead paint signature highlight appears at bottom-right of page 3 (normalized 0.65-0.95, 0.92-0.98)
   - [ ] Seller signature highlights on pages 1 & 32 (c1 estimate)
   - [ ] SSA unsigned highlight on page 30 (c2 estimate)
   - [ ] FRR-PA date blank highlight on page 20 (c3 estimate)
   - [ ] All coordinates accurate within ±5% of actual error location

5. **Error Handling**
   - [ ] If PDF fails to load, display clear error message (not blank screen or crash)
   - [ ] If highlight data missing for a risk, still show PDF without crash
   - [ ] Page navigation bounds checked (no page 0, no page > numPages)

### Evidence Source

**Customer Signal:** Joe Castillo (IL pilot broker, Experiment 2A)  
**Session:** Experiment 2A Interview, June 2026  
**Quote:** "I need to see it in the actual document. If the AI says something's missing, show me where it's missing. That's the difference between trusting the tool and guessing."

**Supporting Evidence:** Ray Hernandez & Marisol Torres (CA brokers, interviews)  
Both independently described need for "seeing it in the doc" to validate compliance findings before escalating to agents.

### Strategic Alignment

**QA vs QC Distinction:**
PDF viewer + highlight = QA feature. Enables brokers to catch errors **before** agent escalation, providing real-time validation at point of detection. Incumbent tools (SkySlope, Dotloop) do QC (post-upload flagging); FileBuddyAI enables QA (upstream prevention).

**High Visibility Vector:**
PDF with highlights delivers on "broker sees exactly what the system found" — actionable visibility that reduces broker anxiety and increases confidence in AI findings.

**Market Entry Logic:**
Brokers initially skeptical of AI compliance — "Can the machine really see what I see?" PDF viewer removes that friction point. Visible evidence = trust = willingness to adopt in pilot.

### Design Rationale: Modal vs Replace (DECIDED)

**Chosen:** Option B (Replace Detail Screen) — PDF as modal tab  

**Rationale:**
- Singular focus: Broker's job when clicking "See in document" is to validate one error, not compare two screens
- Full viewport: Maximizes PDF legibility; highlights are more precise with more pixels
- Tab structure explicit: [Results] [Detail] [Document] clearly signals flow
- Matches mental model: "Let me look at the doc to validate this"
- Mobile-friendly: Cleaner degradation than side-panel crowding

**Rejected:** Option A (Side-panel overlay) — Would crowd viewport on <1200px screens; detail context less useful when validating visual errors

### Implementation Notes

**Coordinate System: Normalized (0.0-1.0)**

Why normalized?
- Durable across zoom levels (browser zoom doesn't break positioning)
- Page-independent (same coordinate system for 8.5"×11" or any size)
- Easy to adjust: "Move highlight 2% to the right" = change x from 0.65 to 0.67

Conversion math:
```
Pixel coordinate → Normalized:  x_norm = x_pixel / viewport.width
Normalized → Pixel: x_pixel = x_norm * viewport.width
```

**Example: Signature Area (Lead Paint)**
- Page 3 bottom-right (typical RPA signature line location)
- Normalized box: { x: 0.65, y: 0.92, w: 0.3, h: 0.06 }
- Meaning: 65-95% across page width, 92-98% down page height
- Covers typical Buyer + Seller signature line area

**Risk Data Structure:**
Each risk in `riskHighlights` object:
```javascript
{
  page: 3,                    // Page number (1-indexed)
  box: {                      // Normalized coordinates
    x: 0.65,                  // Start x (0-1)
    y: 0.92,                  // Start y (0-1)
    w: 0.3,                   // Width as % of page
    h: 0.06                   // Height as % of page
  },
  type: 'c',                  // 'c' (compliance) or 'r' (contingency)
  title: '...'                // Risk title for tooltip
}
```

### Validation Testing Against Actual PDF

**Before Experiment 2C with Joe, Must Validate:**

1. **Lead Paint (Page 3)** — Primary test case
   - [ ] Actual signature location matches x: 0.65-0.95, y: 0.92-0.98 estimate
   - [ ] Highlight box precisely frames missing initials field
   - [ ] Adjustment needed? Document actual offsets

2. **Secondary Risks** (if Joe's PDF has them)
   - [ ] Validate c1, c2, c3, r1, r2 coordinates
   - [ ] Refine based on actual error locations

3. **PDF Quality Issues**
   - [ ] Is PDF text-based or image-based (scanned)?
   - [ ] Does PDF.js render correctly (no blank pages)?
   - [ ] Page count matches expected (45 pages)?

4. **Browser Compatibility**
   - [ ] Chrome/Edge (primary)
   - [ ] Firefox (secondary)
   - [ ] Safari (mobile consideration)

### Known Unknowns (Resolved in v1.4 or Experiment 2C)

1. **Actual PDF File** — Currently using placeholder URL
   - Status: Erwin to provide file link
   - Blocker: Cannot validate coordinates without actual file

2. **Coordinate Accuracy** — Estimates based on typical RPA structure
   - Status: Requires Joe's feedback after pilot test
   - Expected: ±5% tolerance; refine in v1.4 if >5% drift

3. **Zoom & Responsive Behavior** — Not fully tested yet
   - Status: Will test during Experiment 2C
   - Risk: Highlights may drift on mobile/tablet zoom

4. **Performance** — PDF.js rendering on large files (45+ pages)
   - Status: Assume acceptable; profile if Joe reports lag
   - Risk: Canvas rendering may slow on older devices

### Success Metrics (for Joe's Feedback)

Joe will validate C7 success by answering:

1. "Can you clearly see the error in the highlighted area?" → **Yes/No/Mostly**
2. "Does the highlight cover the right part of the document?" → **Accurate/Close/Off**
3. "Is the PDF fast enough to be useful?" → **Yes/Acceptable/Slow**
4. "Would you use this to verify findings before sending to agents?" → **Yes/Maybe/No**

### Next Steps (v1.4)

After Joe's Experiment 2C feedback:

1. **Coordinate Refinement** — Adjust box positions based on actual PDF validation
2. **Add "See in Document" to C2-C5** — Extend button to all risk types
3. **Audit Trail Wire-Up (C8)** — Add event logging for PDF viewer access
4. **Performance Profiling** — If Joe reports lag, profile PDF.js rendering
5. **Mobile Testing** — Validate on tablet/phone (zoom, touch controls)

---

## ARTIFACT STORY: PDF VIEWER IMPLEMENTATION

### What Was Built (Technical Delivery)

**Component:** PDF Viewer Screen (ps-pdf-viewer) + Tab Navigation  
**Technology Stack:** PDF.js 3.11.174 (CDN), Canvas 2D, SVG overlays, vanilla JavaScript  
**Size:** ~300 lines added (PDF integration + functions); ~50 lines modified (tab bar, button wire-up)

**Key Functions:**
- `loadPDF(url)` — Async PDF loading with error handling
- `renderPdfPage(n)` — Render page n to canvas with viewport scaling
- `drawRiskHighlights(page, viewport)` — Overlay SVG highlights for current page
- `pTab(screen)` — Unified tab + screen navigation
- `openPdfViewer(riskId)` — Launch PDF viewer at risk page

**Dependencies:**
- PDF.js library (external CDN — no build step required)
- HTML Canvas API (all browsers)
- SVG (all browsers)
- ES6 JavaScript (modern browsers, works with existing codebase)

**No New Backend Required** — All PDF rendering client-side; actual PDF file served from Google Drive or S3 URL

### Why This Approach

1. **Minimal Dependencies** — PDF.js is industry-standard, no custom PDF parsing needed
2. **Client-Side Rendering** — No server load; scales without backend changes
3. **Durable Coordinates** — Normalized system survives zoom/resize
4. **Easy to Debug** — SVG highlights visible in browser dev tools
5. **Extensible** — Can add annotations, notes, or page caching later

### Risk: PDF URL Placeholder

**Current state:** `const PDF_URL = 'https://drive.google.com/uc?export=download&id=1PlslV7yXW1GMpNzQwUlbOxl1j9G7bEUq'`

**This is a placeholder** — requires Erwin to provide actual file path or confirm this Google Drive link works.

**Validation before Experiment 2C:**
- [ ] Confirm PDF_URL is accessible (not behind auth wall)
- [ ] Confirm PDF_URL has CORS headers allowing browser access
- [ ] If not, establish alternate file hosting (S3, GitHub raw URL, etc.)

### Acceptance by Erwin/Rich (CPO/CEO Lens)

**Erwin (CPO):** 
- ✅ Non-experience satisfied? When broker sees highlight and confirms error, compliance layer disappears into background (broker trusts system).
- ✅ First-principles test: Minimum viable PDF viewer that validates AI findings — nothing more.
- ✅ Defensible moat: Visible error detection builds confidence; confidence builds volume; volume feeds data flywheel.

**Rich (CEO):**
- ✅ Field-testable? Yes — Joe can test immediately with his transactions.
- ✅ MVP locked? PDF viewer is lockable feature; can extend annotations/notes in Phase 2.
- ✅ Ready for handoff? Code is clean, functions documented, next build person (junior dev) can extend.

---

## SIGN-OFF

**Built by:** Claude (Erwin's pair programmer)  
**Reviewed by:** (Pending Erwin sign-off)  
**Tested by:** (Pending Joe's Experiment 2C feedback)  
**Status:** v1.3 Release Candidate (awaiting PDF file + coordinate validation)

**Comments:**

This change answers the highest-friction objection from broker interviews: "I can't trust a system that tells me something's wrong if I can't see it." PDF viewer + highlight removes that objection at the moment of detection.

Next: Audit trail (C8) completes the transaction lifecycle visibility that Joe specifically asked for.

---

**Document Version:** 1.0  
**Created:** July 2, 2026  
**Last Updated:** July 2, 2026  
**Status:** Ready for Experiment 2C Validation
