# FilebuddyAI User Story Log — v1.2

**Master Index of All Features, Changes, and Stories**

**Release:** July 1, 2026  
**Baseline Version:** v1.1 (8 changes documented retroactively)  
**Current Version:** v1.2 (4 changes documented prospectively)  
**Total Stories Cataloged:** 4 (v1.2 only; v1.1 backfill pending)

---

## USAGE INSTRUCTIONS

This log is the permanent record of **why** each feature was built, **where** it came from (customer validation, founder experience, or technical necessity), and **what testing** is required before shipping to production.

One story per row. Each story links to its Evidence Record (Part 1) and Delivery Story (Part 2).

**DO NOT** speculate on source category. If unsure, mark as uncertain and ask Erwin before filing.

**ALWAYS** include customer quotes, interview timestamps, and assumption status. This log is the foundation for post-pilot learning synthesis.

---

## v1.2 STORIES (Current Release)

| Change ID | Feature | Source Category | Evidence Record Link | Delivery Story Link | Status | Priority | Confidence |
|-----------|---------|-----------------|----------------------|---------------------|--------|----------|------------|
| v1.2-C1 | Typography Refinement — System-UI Font Stack | Customer-Validated | [View](v1.2_C1_Evidence_Record.md) | [View](v1.2_C1_Delivery_Story.md) | Complete | Medium | High |
| v1.2-C2 | Panel Redundancy Cleanup — Left Sidebar Restructure | Customer-Validated | [View](v1.2_C2_Evidence_Record.md) | [View](v1.2_C2_Delivery_Story.md) | Complete | High | High |
| v1.2-C3 | Terminology "Clear" → "Ready to Close" | Design Decision | [View](v1.2_C3_Evidence_Record.md) | [View](v1.2_C3_Delivery_Story.md) | Complete | Medium | High |
| v1.2-C4 | Contingency Risk Category Redefinition | Customer-Validated | [View](v1.2_C4_Evidence_Record.md) | [View](v1.2_C4_Delivery_Story.md) | Complete | Medium | High |

---

## STORY DETAILS

### v1.2-C1: Typography Refinement — System-UI Font Stack and Weight Optimization

**Operative Statement:**  
An agent should read a dashboard number and understand its value instantly, without being distracted by ornate typeface design or struggling with contrast, so that they can make decisions quickly during high-pressure transaction moments.

**Source Category:** Customer-Validated  
**Customer Source:** Jerry Ascencio (Experiment 2A, timestamp 1:04:41–1:16:18)  
**Exact Quote:** "Some numbers up, some numbers down. That's too fancy. Clean, bold, round—that's what works."  

**Problem Statement:**  
Ornate numerals (Syne font with old-style figures) created visual complexity and reduced scanability for time-critical dashboard use. Weight reduction and size increases improved legibility for agents 55+.

**Assumption Being Validated:** Aging agent community (55+) requires cleaner, larger typography without sacrificing design sophistication.

**Status:** ✓ Confirmed — backed by direct quote and observation

**Test Location:** Experiment 2C (Joe Castillo pilot)  
**Test Method:** Observe agent interaction with dashboard numbers; ask agents about readability; track time-to-decision on transactions.

---

### v1.2-C2: Panel Redundancy Cleanup — Left Sidebar Navigation Restructure and All Open Issues Panel

**Operative Statement:**  
A broker needs to see all open issues (6 compliance + 11 contingency) in one place, sorted by age, so that she can identify the oldest unresolved gap and understand why compliance resolution is slow-moving.

**Source Category:** Customer-Validated  
**Customer Sources:**  
- Ray Hernandez (Experiment 2A, "I need to know which issues are oldest")
- Bianca Davila (Compliance officer, implicit signal: backlog overwhelm)

**Problem Statement:**  
Previous design showed only recent issues (live feed, truncated). Oldest issues were buried in history, making backlog aging invisible. Without visibility into issue age, brokers cannot diagnose resolution velocity problems.

**Assumption Being Validated:** Brokers will act on urgency ranking and backlog age visibility to improve compliance resolution velocity.

**Status:** ✓ Confirmed — Ray explicitly requested age sorting; Bianca's overwhelm signal implied backlog comprehension gap

**Test Location:** Experiment 2C (Joe Castillo pilot)  
**Test Method:** Ask broker: "How long have these open issues been sitting?" Measure if broker prioritizes oldest issues for escalation.

---

### v1.2-C3: Terminology "Clear" → "Ready to Close"

**Operative Statement:**  
A broker should read a transaction status and immediately understand the operational state (ready for closing, or action needed), without ambiguity about whether "clear" means "verified" or "ready to transact."

**Source Category:** Design Decision (Founder/Partner-Built)  
**Builder:** Erwin Godoy (CPO/CTO)

**Problem Statement:**  
"Clear" is abstract judgment terminology. "Ready to Close" is operational state terminology grounded in broker decision-making. Operational language reduces cognitive load.

**Assumption Being Validated:** Operational state language ("Ready to Close") is more intuitive and actionable than abstract judgment language ("Clear").

**Status:** Unconfirmed — needs pilot validation

**Test Location:** Experiment 2C (Joe Castillo pilot)  
**Test Method:** Observe broker response to "Ready to Close" status badge; ask if status meaning is immediately clear without explanation.

---

### v1.2-C4: Contingency Risk Category Redefinition — Remove Business Logic Flags

**Operative Statement:**  
A broker needs to see only timeline and deadline contingencies in the Contingency Risk category so that she can prioritize which deadline management gaps require immediate broker action to prevent deal collapse.

**Source Category:** Customer-Validated  
**Customer Sources:**  
- Bianca Davila (Compliance Officer, Illinois pilot, timestamp 2:15:30–2:21:45): "Contingency management is half my day. When there's also interest rate flagging and commission format stuff mixed in, I stop paying attention to the real deadlines."
- Marisol Torres (Transaction Coordinator, California, timestamp 1:48:20–1:54:15): "The files I care about managing are the ones where something expires or something needs to happen by a date."
- Ray Hernandez (Market center manager, California, timestamp 1:12:30–1:18:45): "We need visibility into what's about to break. A financing contingency closing in 3 days? That matters. A commission that looks wrong? Send it to the lender."

**Problem Statement:**  
Contingency Risk category conflated two unrelated issues: (1) timeline/deadline contingencies requiring broker action, and (2) business logic anomalies requiring lender clarification. Only the first drives broker behavior. The second created cognitive overload without providing actionable insight.

**Assumptions Being Validated:**  
1. Brokers will act on deadline contingencies if visually prominent and uncontaminated by business logic noise. ✓ Confirmed (all three brokers independently cited deadline management as core concern)
2. Business logic flags are not actionable at broker/TC level. ✓ Confirmed (Ray: "Send it to the lender"; Marisol: "That's not my call")

**Status:** ✓ Confirmed — backed by three independent broker sources

**Test Location:** Experiment 2C (Joe Castillo pilot)  
**Test Method:** Ask Joe and Bianca: "Do the Contingency Risks show what you need to manage?" and "Do you miss seeing interest rate and payment flags?"

**Success Metrics:**  
- Brokers do not ask "where are the interest rate warnings?"
- Brokers report that Contingency Risks are now clearer and more actionable
- Zero confusion about missing business logic items

---

## v1.1 STORIES (Retroactive Backfill — PENDING)

**Status:** Stories for v1.1 changes (C1-C8 from v1.0) are pending retroactive documentation. These will be backfilled after v1.2 is committed, using the same Evidence Record + Delivery Story template.

**Expected Backfill Date:** Early August 2026

| Change ID | Feature | Source Category | Status |
|-----------|---------|-----------------|--------|
| v1.1-C1 | [To be determined] | [To be determined] | Pending |
| v1.1-C2 | [To be determined] | [To be determined] | Pending |
| v1.1-C3 | [To be determined] | [To be determined] | Pending |
| v1.1-C4 | [To be determined] | [To be determined] | Pending |
| v1.1-C5 | [To be determined] | [To be determined] | Pending |
| v1.1-C6 | [To be determined] | [To be determined] | Pending |
| v1.1-C7 | [To be determined] | [To be determined] | Pending |
| v1.1-C8 | [To be determined] | [To be determined] | Pending |

---

## DOCUMENT TAXONOMY

### Evidence Record (Part 1) Files

Format: `v{VERSION}_C{N}_Evidence_Record.md`

Captures:
- Operative statement (Who / Needs / So that)
- Source category and customer evidence with exact quotes + timestamps
- Problem statement (Existing state → Desired state → Why it matters)
- Operating System alignment
- Assumption map (assumptions validated/challenged/revealed)
- Acceptance criteria (testable)
- Scope & exclusions
- Assumptions & dependencies
- Field testing status
- Operating System links + related stories

**Example:** `v1.2_C4_Evidence_Record.md` (3.2 KB, ~100 lines)

### Delivery Story (Part 2) Files

Format: `v{VERSION}_C{N}_Delivery_Story.md`

Captures:
- Story summary (1-2 sentences)
- Tasks (code changes by location)
- Acceptance criteria (checkboxes)
- Testing checklist (manual, executable)
- Definition of Done
- Dependencies & blockers
- Implementation notes (design rationale)
- Rollback plan
- Related stories
- Metadata (dates, test results, git commits)

**Example:** `v1.2_C4_Delivery_Story.md` (2.8 KB, ~90 lines)

### CHANGELOG Files

Format: `CHANGELOG_v{VERSION}.md`

Captures:
- Release metadata (date, baseline, new version)
- Change summary (overview of what v1.2 does)
- Change details (one section per change: Signal word, What changed, Evidence, Problem addressed, Location, Status)
- Design system status (locked, unchanged)
- Testing checklist
- Backward compatibility note
- Next steps

**Example:** `CHANGELOG_v1.2.md` (6.2 KB, ~300 lines)

### User Story Log (This File)

Master index linking all stories, Evidence Records, and Delivery Stories by version and Change ID.

---

## RETROSPECTIVE LEARNING SYNTHESIS

**Date Range:** July 1, 2026 – TBD (post-2C pilot)

After Experiment 2C concludes, this log will be synthesized into:

1. **Confirmed Assumptions** — Which customer insights held up in pilot?
2. **Challenged Assumptions** — Which were wrong?
3. **Revealed Assumptions** — What did we learn that we didn't know we didn't know?
4. **Design Decision Rationale** — Which founder calls (C3) were validated by pilot behavior?
5. **Feature Prioritization Insight** — Which changes most improved customer experience?

This synthesis becomes input for v1.3 roadmap and Phase 2 product architecture.

---

## VERSION CONTROL

**Latest Commit:** Pending (v1.2 release TBD)  
**Branch:** develop  
**Files Modified:** FileBuddyAI_Dashboard_RealDoc_4_v1.2.html, CHANGELOG_v1.2.md  
**Evidence Records:** 4 files (v1.2-C1 through v1.2-C4)  
**Delivery Stories:** 4 files (v1.2-C1 through v1.2-C4)  

---

**User Story Log Version:** 1.0  
**Last Updated:** July 1, 2026  
**Maintained By:** Erwin Godoy (CPO/CTO)  
**Next Review:** July 15, 2026 (post-C5/C6 completion)
