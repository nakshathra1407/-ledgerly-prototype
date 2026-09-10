# Ledgerly — Interactive Expense Tracker Prototype

**Internship task:** Interactive Prototype Creation
**Deliverable type:** High-fidelity clickable prototype + Figma rebuild spec + usability testing plan

## Objective

Design and prototype a complete expense-tracking mobile app that feels like a real, working product rather than a set of static screens — with realistic navigation, form validation, overlays, modals, and success feedback across the full add/view/edit/delete lifecycle of a transaction.

## Features

- Splash screen with automatic transition into onboarding
- 3-step onboarding (track, understand, manage)
- Login with show/hide password and inline validation states
- Home dashboard: balance, income/expenses/remaining, category summary, recent transactions
- Add Expense with amount, category picker (bottom sheet), description, date picker (calendar sheet), optional note, and validation errors on incomplete fields
- Transaction History with search, category filters, and date grouping
- Transaction Details with Edit and Delete
- Edit Expense (pre-filled form, same validation as Add)
- Delete confirmation modal with a distinct success state afterward
- Analytics: monthly total, 6-month trend, highest-spending category, per-category breakdown with bars and percentages
- Profile/Settings: notifications toggle, working dark-mode toggle, logout
- Toast success feedback for add / update / delete
- Full back-navigation stack (not hardcoded per-screen — back returns to wherever the user actually came from)

## Design process

**Wireframe → UI design → Prototype → User testing → Refinement**

1. Mapped the required screens against the primary user flow (Splash → Onboarding → Login → Dashboard, with branches for Add Expense, Transactions, Analytics, Profile) before any visual design, to make sure every screen had a clear entry and exit point.
2. Built a small design system first (color, type, spacing) so every screen after that was assembly, not re-invention. Amounts use a monospace numeral face (IBM Plex Mono) against a humanist sans (Manrope) for everything else — a small, deliberate detail that reads as "ledger" rather than generic dashboard, and makes numbers easier to compare at a glance since digits are fixed-width.
3. Built the prototype as **actual working HTML/CSS/JS**, not just static Figma frames connected by hotspots — this makes it directly testable by a real person (see `ledgerly-interactive-prototype.html`) and removes any ambiguity about how a transition or validation state should behave when you rebuild it in Figma.
4. Used the Figma spec (`figma-spec.md`) to translate every interaction in the working prototype into frame names, component variants, and prototype connections, so the Figma file matches the tested behavior exactly.
5. Wrote a 5-task usability testing plan (`user-testing-plan.md`) targeting the app's core loop: add, find, edit, delete, and understand spending.

## Prototype flow

The primary path a new user takes:

```
Splash → Onboarding (3 screens) → Login → Home
  → Add Expense → Category (sheet) → amount/description/date → Save → success toast → Home
  → Transaction History → Transaction Details → Edit → Save Changes → success toast → updated Details
  → Transaction Details → Delete → Confirmation modal → Delete → success toast → History
  → Home → Analytics → category + trend breakdown
  → Home → Profile → Logout → Login
```

Every screen either sits on the bottom navigation (Home, History, Analytics, Profile — lateral switches, no back stack) or is pushed onto a back stack (Add/Edit Expense, Transaction Details — back returns to the actual previous screen). Category and date selection use bottom sheets rather than full screen navigation, so the form underneath stays visible and in-progress input isn't lost — see the design-decision note in `figma-spec.md` §3 for the reasoning and the standalone-frame alternative kept for documentation purposes.

## Usability testing

Five tasks covering the core loop — add an expense, find a transaction, edit one, delete one, and identify the top spending category — each with a specific success criterion and a predicted failure point to watch for (e.g., the FAB being missed in favor of an expected nav-bar "Add" item, or users looking for edit affordances directly on the transaction card instead of going through Details first). Full task list, expected actions, and a 5-question feedback form are in `user-testing-plan.md`.

## Improvements to make after testing

*(Fill this in once you've actually run the 4–5 sessions — this section is what turns the project from "a prototype" into a real case study for a mentor or recruiter.)* Suggested structure per finding:

> **Finding:** [what you observed, with a participant quote if you have one]
> **Change made:** [what you changed in response]
> **Why:** [the usability principle it addresses]

## Tools used

Figma (for the final submission file) · HTML/CSS/JS (for the working interactive prototype used in testing, since it's clickable by anyone with a browser and needs no Figma account)

## Prototype

- **Working prototype (open in any browser):** `ledgerly-interactive-prototype.html`
- **Figma prototype link:** *[paste your published Figma prototype link here once built from `figma-spec.md`]*

## Files in this submission

| File | Purpose |
|---|---|
| `ledgerly-interactive-prototype.html` | Fully clickable prototype — open directly in a browser, no install needed |
| `figma-spec.md` | Screen-by-screen, component-by-component spec to rebuild this in Figma with real prototype connections |
| `user-testing-plan.md` | 5-task usability test script + feedback form |
| `README.md` | This file |

## Design system summary

- **Color:** primary `#1F6F5C` (deep teal-green), background `#F6F4EF`, surface `#FFFFFF`, text `#1B2430`, error `#C94F4F`, success `#2F9E6E` — full token table in `figma-spec.md` §1
- **Type:** Manrope (UI/headings), IBM Plex Mono (currency amounts only)
- **Spacing:** 4 / 8 / 16 / 24 / 32px scale
- **Radius:** 8 / 14 / 22 / pill
- **Style:** clean fintech-inspired, minimal shadow, no gradients, accessible contrast (text-on-surface and text-on-primary both exceed WCAG AA)
