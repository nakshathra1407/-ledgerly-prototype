# Ledgerly — Figma Rebuild Specification

This is the exact spec to recreate the working prototype (`ledgerly-interactive-prototype.html`) as a native Figma file with real prototyping connections. The HTML file is the source of truth for layout, copy, and states — open it in a browser and click through it before you build, then use this doc for frame names, component variants, and interaction wiring.

---

## 1. Design tokens

### Color
| Token | Hex | Use |
|---|---|---|
| `color/primary` | `#1F6F5C` | CTAs, active states, brand |
| `color/primary-dark` | `#154C40` | Primary hover/pressed |
| `color/primary-tint` | `#E4EFEA` | Selected backgrounds, chart highlight |
| `color/secondary` | `#2E3A46` | Device chrome, secondary text on dark |
| `color/bg` | `#F6F4EF` | Screen background |
| `color/surface` | `#FFFFFF` | Cards, inputs, sheets |
| `color/text` | `#1B2430` | Primary text |
| `color/text-secondary` | `#64707A` | Captions, labels |
| `color/success` | `#2F9E6E` | Success toast, positive states |
| `color/warning` | `#C98A2C` | Warning states |
| `color/error` | `#C94F4F` | Error states, delete |
| `color/border` | `#E5E1D6` | Card/input borders, dividers |

Category accent colors (used only for icon chips, never for text):
Food `#C9714F` · Travel `#3D7EBF` · Shopping `#A85CC1` · Bills `#4C7A6B` · Entertainment `#C9A23E` · Health `#C94F4F` · Education `#3E8FC9` · Other `#7A8790`

**Dark theme** (secondary mode, toggled from Profile): swap to bg `#12161B`, surface `#1B2129`, text `#EDEFF2`, text-secondary `#8B96A2`, border `#2A313A`, primary `#3FA189`. Set these up as a Figma **variable collection with Light/Dark modes**, not a duplicate file.

### Typography
- **Display/UI face:** Manrope (weights 400/500/600/700/800)
- **Numeric face:** IBM Plex Mono (weights 400/500/600) — used only for currency amounts, giving the ledger a "real numbers" feel distinct from the UI chrome.

| Style | Font | Size | Weight | Use |
|---|---|---|---|---|
| Display | Manrope | 26 | 800 | Onboarding/login headlines |
| Heading | Manrope | 19 | 700 | Screen titles, section headers |
| Sub | Manrope | 14 | 600 | Secondary headings |
| Body | Manrope | 14.5 | 400 | Paragraph text |
| Caption | Manrope | 12 | 400 | Metadata, timestamps |
| Amount-lg | IBM Plex Mono | 28–30 | 600 | Balance, transaction detail amount |
| Amount-sm | IBM Plex Mono | 14.5 | 600 | Amount in list rows |

### Spacing & radius
Spacing scale: `4 / 8 / 16 / 24 / 32`. Radius: `sm 8 · md 14 · lg 22 · pill 999`.

### Frame
Mobile frame: **390 × 844** (iPhone 14/15 base). Status bar 34px. Bottom nav 64px + safe area.

---

## 2. Component library (page **04 — Components**)

Build each as a Figma component with the listed variants. Use **auto layout** throughout so text/content changes reflow.

| Component | Variants |
|---|---|
| **Button/Primary** | Default, Hover, Pressed, Disabled |
| **Button/Secondary** | Default, Hover, Pressed |
| **Button/Danger** | Default, Pressed |
| **Text Field** | Default, Focused, Filled, Error |
| **Password Field** | Default, Focused, Visible, Hidden, Error |
| **Amount Field** | Empty, Filled, Error |
| **Select Field** (category/date) | Placeholder, Filled, Error |
| **Category Chip** | Default, Active (8 category color swaps as instance swap or variable) |
| **Category Icon** | 8 categories × 3 sizes (26 / 42 / 64px) |
| **Transaction Card** | Default, Pressed |
| **Bottom Navigation** | Home active, History active, Analytics active, Profile active |
| **Top Navigation** | With back, Without back (root screens) |
| **FAB** | Default, Pressed |
| **Modal / Confirmation** | Default |
| **Sheet / Bottom Sheet** | Category picker, Date picker |
| **Toast** | Success |
| **Toggle** | Off, On |
| **Empty State** | No results, No transactions |
| **Progress Dots** | 3-step, step 1/2/3 active |

Build **Button/Primary** first as the reference for how variants swap: Default `fill=color/primary`, Hover `fill=color/primary-dark`, Pressed `fill=color/primary-dark, scale 98%`, Disabled `fill=#B9C4C0, no shadow`.

---

## 3. Screens (page **06 — High Fidelity Screens**)

Frame naming exactly as below so prototype connections stay legible.

### `01_Splash`
Full-bleed `color/primary` background. Centered: 76×76 rounded-22 icon tile (wallet icon, white @15% fill), "Ledgerly" (Display, white), tagline "Know where it goes." (Body, white @85%).
**Interaction:** After Delay 1.5s → `02_Onboarding_1`, animation **Dissolve, 400ms**. Also On Click anywhere → same target (lets testers skip the wait).

### `02_Onboarding_1` / `_2` / `_3`
Top-right "Skip" (hidden on screen 3). Center icon tile (120×120, `primary-tint` bg) + Display headline + Body copy. Bottom: 3-dot progress indicator (active dot = pill, 20×7), then Button/Primary labeled "Next" (screens 1–2) or "Get Started" (screen 3).
Copy:
1. "Track every expense" / "Log purchases in seconds and keep a running picture of where your money goes each day."
2. "Understand your spending" / "See category breakdowns and trends so patterns in your spending actually make sense."
3. "Manage finances easily" / "Set a rhythm for checking in on your balance — no spreadsheets, no friction."
**Interactions:** Next → **Navigate to** next onboarding frame, **Smart Animate, 300ms, Ease Out**. Skip / Get Started → **Navigate to** `03_Login`, **Slide In from Right, 300ms**.

### `03_Login`
Icon tile, Display "Welcome back", Body subtext. Text Field (Email, prefilled `aditi.rao@mail.com`). Password Field with eye-toggle icon button (On Click → **Change To** Password Field/Visible variant, no navigation). "Forgot password?" ghost button. Button/Primary "Log In". Bottom row: "New here? Create account" ghost button.
**Interactions:** Log In → **Navigate to** `04_Home`, **Smart Animate, 350ms**, **and** trigger the Toast component ("Welcome back, Aditi") via **After Delay 300ms → Change To** Toast/Show, **After Delay 2000ms → Change To** Toast/Hidden.

### `04_Home`
Top nav: greeting + name (left), profile icon button (right, → `12_Profile`). Balance card (`primary` fill, white text): "Total balance" caption + big mono figure, then a 3-up income/expenses/remaining row with vertical dividers. "Spending by category" section with mini horizontal bars (top 3 categories) + "See all" ghost → `11_Analytics`. "Recent transactions" (4 Transaction Cards) + "See all" ghost → `07_TransactionHistory`. Bottom Navigation (Home active) + FAB (+, bottom-right, floating above nav).
**Interactions:** Transaction Card On Click → `08_TransactionDetails` (**Navigate to**, **Slide In Right, 250ms**). FAB On Click → `05_AddExpense` (**Navigate to**, **Move In from Bottom, 300ms** — reinforces "adding" as a forward, modal-like action). Bottom nav items → **Navigate to** respective root screen, **Smart Animate 200ms** (no slide, these are lateral tab switches, not stack pushes).

### `05_AddExpense`
Top nav: back chevron + "Add Expense" title, no right action. Form: Amount Field (₹ prefix, large mono input), Select Field "Category" (chevron-right, opens sheet), Text Field "Description", Select Field "Date" (calendar icon, opens sheet), Text Field "Note (optional)". Sticky footer: Button/Secondary "Cancel" + Button/Primary "Save Expense" (50/50 split, 10px gap).
**Interactions:** Category select field → **Open Overlay** `Sheet_CategoryPicker`, **Move In from Bottom, 280ms**. Date select field → **Open Overlay** `Sheet_DatePicker`, **Move In from Bottom, 280ms**. Cancel → **Navigate back**. Save Expense →
- If Amount empty/0 **or** Category unset **or** Description empty: **Change To** this frame's Error variant (fields switch to Error variant in place, red border + inline message appears via component swap) — **no navigation**.
- If valid: **Navigate to** `04_Home`, **Dissolve 250ms**, then trigger Toast "Expense added successfully" the same delayed-show/hide pattern as Login.

### `Sheet_CategoryPicker` (overlay, built on top of whichever screen opened it)
Bottom sheet, handle bar, "Select category" heading + close icon button. 2-column grid of 8 Category Card components (icon 44px + label). Selected state = colored border + tinted fill matching that category's accent.
**Interactions:** Any card On Click → **Set variable** `selectedCategory`, **Close Overlay**, **Swap Overlay** back to caller with the Select Field now showing chosen category (Smart Animate the field content). Close icon / tap outside sheet → **Close Overlay**.

### `Sheet_DatePicker` (overlay)
Bottom sheet: prev/next chevrons + "Month Year" heading, 7-column weekday header, day grid. Selected day = filled pill (`primary`, white text).
**Interactions:** Chevrons → **Change To** sheet with adjacent month (no close). Day tap → **Set variable** `selectedDate`, **Close Overlay**.

### `06_CategorySelection` (standalone reference frame, page 05/06 — same content as the sheet, kept as its own frame per the brief's screen list so it can also be demoed independently)
Full-screen version of the category grid with a top nav ("Category" + back). Same 8 Category Cards. Used for documentation/testing purposes; the live prototype uses the sheet variant for a faster in-context flow — note this trade-off explicitly to your mentor as a deliberate interaction decision (modal selection keeps the user's form state visible underneath, reducing context loss vs. a full navigation).

### `07_TransactionHistory`
Top nav: "Transactions" title, no back (root/tab screen). Search Text Field (search icon right-aligned). Horizontal scroll of Category Chips ("All" + 8 categories) — active chip filled `primary`. List grouped under date headers ("Today", "Yesterday", "Wed, 3 Sep" pattern) each containing Transaction Cards. Empty state (search icon tile + "No transactions found") when filter/search yields nothing. Bottom Navigation (History active) + FAB.
**Interactions:** Chip On Click → **Change To** active variant + **Set variable** `categoryFilter`, content updates in place (no navigation). Search field → live filter, no navigation. Transaction Card → `08_TransactionDetails`.

### `08_TransactionDetails`
Top nav: back + "Transaction" title. Centered hero: 64px Category Icon, large mono amount, description. Detail card (Category / Date / Description / Note rows, dividers between). Sticky footer: Button/Secondary "Delete" + Button/Primary "Edit".
**Interactions:** Back → **Navigate back** to wherever the user came from (History or Home). Edit → `09_EditExpense`, **Slide In Right, 250ms**, pre-filled with this transaction's data. Delete → **Open Overlay** `Modal_DeleteConfirm`, **Dissolve 200ms**.

### `Modal_DeleteConfirm` (centered modal overlay)
Centered card, max-width 300: error-tinted trash icon tile, "Delete transaction?" heading, body copy, Button/Secondary "Cancel" + Button/Danger "Delete" side by side.
**Interactions:** Cancel → **Close Overlay**. Delete → remove the transaction from the prototyped data set, **Close Overlay**, **Navigate to** `07_TransactionHistory` (**Dissolve 250ms**), then Toast "Transaction deleted".

### `09_EditExpense`
Identical layout to `05_AddExpense` but title "Edit Expense", fields pre-filled, footer button reads "Save Changes".
**Interactions:** Same validation logic as Add. On valid Save → **Navigate to** `08_TransactionDetails` (**Dissolve 250ms**, showing updated values), then Toast "Expense updated".

### `10_DeleteConfirmation`
This is the standalone-frame version of `Modal_DeleteConfirm` for the page-05/06 documentation set (see note under `06_CategorySelection` — the live flow uses the overlay so state underneath remains visible).

### `11_Analytics`
Top nav: "Analytics" title (root/tab). Summary card: "September spending" caption + big mono total, 6-bar mini trend chart (Apr–Sep, current month bar in `primary`, others in `border` gray). Highlight card (tinted `primary-tint` bg): top category icon + name + amount, labeled "Highest spending category". "By category" list: each row = icon + label + amount + percentage + horizontal bar sized to that %. Bottom Navigation (Analytics active) + FAB.
**Interactions:** Static/read-only screen; bottom nav and FAB behave as elsewhere.

### `12_Profile`
Top nav: "Profile" title (root/tab). Avatar card (initials circle + name + email + edit icon button). "Preferences" section label. Settings list card: Currency row (chevron, → static for now), Notifications row (Toggle), Dark theme row (Toggle — wire this to the color variable mode swap if you want a truly live dark-mode demo), Privacy row (chevron). Button/Secondary "Log out" in error color. Bottom Navigation (Profile active) + FAB.
**Interactions:** Toggles → **Change To** On/Off variant in place, **Smart Animate 160ms**. Log out → **Navigate to** `03_Login`, **Dissolve 300ms**, reset any prototype variables, then Toast "Logged out".

### `13_SuccessStates` (documentation frame, not a navigable screen)
Show the Toast component in its three copy variants next to each other for reference: "Expense added successfully" / "Expense updated" / "Transaction deleted". Each: dark pill, white checkmark badge, white label text, positioned top-of-frame, `Move In from Top + Dissolve, 240ms in / 240ms out, auto-dismiss after 2s`.

---

## 4. Global interaction rules

- **Trigger conventions:** primary actions = On Click; icon-only toggles (password eye, theme/notification switches) = On Click with **Change To**, not navigation; category cards / calendar days = On Click with **Set variable** + **Close Overlay**.
- **Timing:** 200–300ms for in-flow navigation, 350–400ms only for the splash-to-onboarding dissolve and major state completions (save/delete). Never exceed 400ms — anything slower reads as sluggish on repeated testing.
- **Back behavior:** every non-root screen's back chevron uses Figma's **Navigate back** action (not a hardcoded target) so the prototype's back stack matches real app behavior regardless of entry point (e.g., Transaction Details can be reached from Home *or* History).
- **No dead ends:** every screen has at least one forward action and, if not a bottom-nav root, a back action. Modals/sheets always have both a confirm and a dismiss path.
- **Variables to define:** `selectedCategory` (string), `selectedDate` (string), `notificationsOn` (bool), `darkModeOn` (bool), `amountValue` (string) — bind these to the form fields' displayed content so Add/Edit Expense reflect picker choices without manual screen duplication.

---

## 5. User flow diagram (page **02 — User Flow**)

Recreate as a FigJam-style flow using the Section/Frame + arrow connectors:

```
User → Splash → Onboarding → Login → Dashboard
                                        ├── Add Expense → Category → Details → Success → Home
                                        ├── Transactions → Details → Edit → Save → Updated Success
                                        │                     └→ Delete → Confirm → Success → History
                                        ├── Analytics
                                        └── Profile → Logout → Login
```

---

## 6. File structure checklist

```
01 — Cover                 (title, your name, date, one-line project summary)
02 — User Flow             (diagram above)
03 — Design System         (tokens, type scale, color swatches, spacing ruler)
04 — Components            (component set from Section 2)
05 — Wireframes            (low-fi grayscale versions of each screen — build these FIRST, before high-fi)
06 — High Fidelity Screens  (all frames from Section 3)
07 — Prototype Flow         (a copy of 06 with all Figma prototype connections wired — this is what you present in Presentation mode)
08 — User Testing           (see user-testing-plan.md — paste task cards + observation notes here)
09 — Final Screens          (polished, testing-informed final set + before/after notes)
```

Frame name prefix numbers must match the list in Section 3 (`01_Splash`, `02_Onboarding_1`, etc.) so click-through order is unambiguous to a reviewer scrubbing the page.
