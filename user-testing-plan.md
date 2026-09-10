# Ledgerly — Usability Testing Plan

**Format:** 5 tasks, moderated, ~10–12 minutes per participant. Run against either the live HTML prototype (`ledgerly-interactive-prototype.html`) or the Figma prototype in Presentation mode. Recruit 4–5 participants who track personal expenses informally (notes app, spreadsheet, or nothing) — that mismatch is where the most useful friction shows up.

Before starting, read aloud: *"Think out loud as you go. There are no wrong answers — if something is confusing, that's useful information, not a mistake on your part."*

---

### Task 1 — Add an expense
**Prompt to participant:** "Add a ₹500 food expense."

- **Objective:** Validate that the add-expense entry point (FAB) and the category/amount/save sequence are discoverable without instruction.
- **Expected user action:** Tap the FAB on Home → enter 500 in Amount → open category picker → select Food → (description optional in real life, required in this build) → Save.
- **Success criteria:** Transaction appears in Recent Transactions on Home and in category totals within one attempt, under 30 seconds, without the participant asking "where do I add something?"
- **Possible usability issue:** The FAB may be missed if the participant expects an "Add" item inside the bottom nav instead of a floating button; the required Description field may stall users who expected amount + category to be sufficient.
- **Feedback question:** "Was it clear where to start? Was anything asked of you that felt unnecessary?"

### Task 2 — Find and view a transaction
**Prompt to participant:** "Find your most recent transaction and view its details."

- **Objective:** Test whether Home's "Recent transactions" and the History tab are both viable, discoverable paths.
- **Expected user action:** Tap a transaction card directly from Home, or navigate to History first.
- **Success criteria:** Participant reaches Transaction Details in under 15 seconds via either path.
- **Possible usability issue:** Participants may not realize transaction cards are tappable if the affordance (hover/press state) isn't obvious on a touch device.
- **Feedback question:** "Did you expect tapping the transaction to do what it did?"

### Task 3 — Edit an existing transaction
**Prompt to participant:** "Edit an existing transaction — change the amount."

- **Objective:** Confirm Edit is reachable from Details and that the pre-filled form doesn't feel like starting over.
- **Expected user action:** Open a transaction → tap Edit → change amount → Save Changes.
- **Success criteria:** Updated amount reflects immediately in Transaction Details and in any totals the participant checks afterward.
- **Possible usability issue:** Participants may look for an edit affordance directly on the transaction card or in History (swipe-to-edit expectation from other apps) instead of going through Details first.
- **Feedback question:** "Is this how you expected to edit something? Where else did you look first?"

### Task 4 — Delete a transaction
**Prompt to participant:** "Delete a transaction."

- **Objective:** Verify the confirmation modal prevents accidental loss without feeling like a nag.
- **Expected user action:** Open a transaction → Delete → confirm in the modal.
- **Success criteria:** Participant reads and acts on the confirmation deliberately (not a reflexive double-tap), and the transaction is gone from History afterward with visible feedback (toast).
- **Possible usability issue:** If the confirmation copy is too generic, participants may not register *which* transaction they're deleting — watch for hesitation or a "wait, was that the right one?" moment.
- **Feedback question:** "Did you feel confident that was the transaction you meant to delete?"

### Task 5 — Identify top spending category
**Prompt to participant:** "Check which category you spent the most money on this month."

- **Objective:** Test whether Home's category summary is sufficient or participants need to dig into Analytics.
- **Expected user action:** Either read the category bars directly on Home, or navigate to Analytics for the explicit "Highest spending category" callout.
- **Success criteria:** Participant states the correct top category confidently, from either screen.
- **Possible usability issue:** Home only shows the top 3 categories by amount — if the participant's assumption doesn't match what's summarized, they may need Analytics but not think to look there.
- **Feedback question:** "Where did you expect to find this, before you found it?"

---

## Post-test feedback form (5 questions)

1. On a scale of 1–5, how easy was it to complete these tasks without help? *(1 = very difficult, 5 = very easy)*
2. Which screen or step, if any, made you pause or hesitate? Why?
3. Did the app behave the way you expected after each tap, or were there surprises?
4. Was there anything you wanted to do that wasn't possible in this prototype?
5. What's one thing you'd change about how expenses are added or reviewed?

---

## What to capture during each session
- Time to completion per task
- Number of mis-taps or backtracks
- Verbatim quotes at moments of hesitation (these are gold for the "Improvements" section of your README)
- A 1–5 confidence rating you assign per task, independent of the participant's own score, based on how much hesitation you observed

## Suggested synthesis step
After all sessions, group findings into **Keep / Fix / Investigate further** and prioritize fixes that affected more than one participant before cosmetic feedback. Document the before → after change for each fix you make — that comparison is what turns this from "a prototype" into "a case study" for your portfolio.
