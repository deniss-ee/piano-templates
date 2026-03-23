# Piano Templates — My Account Redesign: Handoff Document

> **Created:** 23 March 2026
> **Purpose:** Continue the My Account template redesign in a new chat session. Paste this as your first message.

---

## PROJECT SUMMARY

We are redesigning the **My Account** section of the Piano platform for **Õhtuleht** (Estonian news publisher). The goal is to modernize AngularJS templates by:

1. Replacing table-based layouts with flexbox card-based designs
2. Using the existing `style.css` design system tokens exclusively
3. Preserving ALL Angular/Piano directives and functionality
4. Creating a consistent visual language across all tabs

---

## DESIGN SYSTEM ESTABLISHED

All redesigned templates follow these patterns:

### Visual Language
- **Container (`.main`):** `background: var(--ol__monochrome__50)` (#f5f6f6), `padding: 1rem`, `border-radius: var(--radius__xl)` (12px)
- **Cards:** `background: var(--white)`, `border-radius: var(--radius__lg)` (8px), `padding: var(--spacing__4)` (16px), NO border, NO shadow, NO hover effect
- **Card list gap:** `var(--spacing__2)` (8px)
- **Section headers:** Fira Sans Condensed, `font-size: var(--font__size__2xl)` (24px), `font-weight: var(--font__weight__semibold)` (600), `color: var(--ol__red__700)` (#e3000f), `letter-spacing: -0.02em`
- **Card titles/names:** Inter, `font-size: var(--font__size__sm)` (14px), `font-weight: bold` (700), `color: var(--ol__red__700)`
- **Secondary text (dates, details):** Inter, `font-size: var(--font__size__xs)` (12px), `font-weight: normal` (400), `color: var(--ol__monochrome__500)` (#657275)
- **Prices:** Fira Sans Condensed, `font-size: var(--font__size__base)` (16px), `font-weight: extrabold` (800), `color: var(--ol__red__700)`
- **Manage/action buttons:** Inter 12px semibold, `height: 32px`, `border-radius: var(--radius__md)` (6px), gray bg `var(--ol__monochrome__50)`, hover `var(--ol__monochrome__100)`
- **Primary buttons (Save, etc.):** `background: var(--ol__red__700)`, white text, `height: 40px`, `border-radius: var(--radius__md)`
- **Icon buttons (delete, mail, download):** 30px square, `border-radius: var(--radius__md)`, gray color, hover turns red
- **Links:** `color: var(--ol__red__700)`, hover `var(--ol__red__800)` with underline
- **Transitions:** `125ms ease-in-out` (matching design system)
- **Mobile breakpoint:** `480px` for card stacking, `600px` for profile form

### Bundle Override Strategy
- `my-account-bundle.css` is still loaded — all custom CSS uses `!important` where needed to override bundle defaults
- Key bundle overrides: `.section-text` (float, margin, font), `.scrollable-content` (border, min-height, overflow), `.button.green` (height 40px→32px, min-height, min-width)

---

## COMPLETED TEMPLATES

### 1. Transactions ✅
**Files:**
- `transactions.html` — Angular `ng-template`, card-based layout
- `transactions-custom.css` — Scoped under `.ma-transactions`

**Key changes:**
- `<table class="vanilla-table">` → `<div class="ma-tx-list">` with `<div class="ma-tx-card">`
- Inline SVG icons replace `icon-mail` / `icon-download` sprite classes
- `ng-show="canResendReceipt"` moved to `.ma-tx-actions` wrapper
- Also contains `.main` background override (shared by all tabs)

**Angular directives preserved:** `ng-show="transactions.length > 0"`, `ng-repeat="transaction in transactions | orderBy:'date':reverse"`, `ng-click="resendReceipt(transaction)"`, `ng-click="downloadTransactionInfo(transaction)"`, `ng-show="canResendReceipt"`, `<t>` translation tag

### 2. Library ✅
**Files:**
- `library_list.html` — Outer container (`library_list.shtml`), added `.ma-library` wrapper
- `library_list_item.html` — Subscription rows (`_library_list_item.shtml`), card-based
- `library-custom.css` — Scoped under `.ma-library` / `.ma-library-items`

**Key changes:**
- `<table class="vanilla-table">` → `<div class="ma-lib-list">` with `<div class="ma-lib-card">`
- Toggler (`.toggler-container`) hidden with sr-only pattern (`.ma-lib-toggler-hidden`) — stays in DOM for Angular binding, auto-renew toggle is in dropdown menu instead
- "Jaga sõpradega" button (`.button.green`) styled as red pill: `background: var(--ol__red__50)`, `color: var(--ol__red__700)`, forced `height: 32px` to match dropdown toggle (bundle forces `min-height: 40px`)
- `overflow: hidden` removed from `.ma-lib-card` so dropdown menus render outside card
- Pending warning as card footer with cream background
- Tabs restyled as pill buttons (white bg active, transparent inactive)
- Notice banners for postponed upgrades / shared access in cream bg

**Angular directives preserved:** All `ng-repeat`, `ng-if`, `ng-show`, `ng-click`, `ng-bind-html`, `ng-disabled`, `ng-model`, `ng-change`, `ng-class`, `tp-toggle`, `tp-menu`, `tp-menu-item`, `external-event`, `tabset`, `tab`, `library-table`, `upgrade-options`, `my-account-print-address-form`

**Note:** Only `library_list.shtml` and `_library_list_item.shtml` were redesigned. Other sub-templates in library.html (confirmation modals, payment method management, upgrade options, shared subscriptions, address forms) were NOT touched.

### 3. Profile ✅
**Files:**
- `profile.html` — Piano ID profile template (standalone, NOT ng-template)
- `profile-custom.css` — Full replacement for the original ~1800-line inline `<style>` block

**Key changes:**
- This is a Piano ID template with its OWN inline CSS (separate from `my-account-bundle.css`). Uses Piano-specific directives like `fieldProfileFirstName`, `*hideChangePassword`, `*showChangePassword`, `showIfSocialAuthAvailable`, `actionUpdateProfile`, etc.
- Added `.ma-profile__card` wrapper divs to group form fields into white cards
- `.tp-form` no longer has its own card styling — it's a row inside cards
- `.tp-form .control-group` uses `flex-direction: column; justify-content: flex-start; align-items: flex-start;` — label sits above controls
- NO border-top/border-bottom separators between form rows or social items
- Social accounts (Apple, Facebook, Google, Twitter, LinkedIn, OpenID) styled as rows with connect/disconnect buttons
- Social "link" button: red bg, white text. "Unlink": gray bg
- Connected status: green text with checkmark icon

**Card grouping:**
- Card 1: Eesnimi + Perekonnanimi + E-post (always visible)
- Card 2: Password view mode (`*hideChangePassword`) OR current/new/confirm password fields (`*showChangePassword`)
- Card 3: Custom fields (if any)
- Card 4: Social accounts (`showIfSocialAuthAvailable`)

### 4. Wallet ✅
**Files:**
- `wallet.html` — Only `wallet_list.shtml` redesigned (the main list view)
- `wallet-custom.css` — Scoped under `.ma-wallet`

**Key changes:**
- `<table class="vanilla-table wallet-list">` → `<div class="ma-wallet-list">` with `<div class="ma-wallet-card">`
- "Lisa makseviis" dropdown button restyled to brand red
- Delete icon as inline SVG, turns red on hover
- "Vaikimisi" (Default) as text label, "Määra vaikimisi" (Set as default) as small gray button
- State badge in green

**Angular directives preserved:** `ng-repeat="card in cards track by card.ccid"`, `ng-show`, `ng-hide`, `ng-if`, `ng-click`, `ng-disabled`, `ng-bind-html`, `ng-class`, `data-e2e`, `data-toggle`

**Note:** Other wallet sub-templates (wallet_item form, paypal, postfinance, account, zlick) were NOT redesigned.

---

## CSS LOAD ORDER

```
my-account-bundle.css     ← Piano's default (15,561 lines, kept as-is)
style.css                 ← Design system tokens (:root variables)
transactions-custom.css   ← Transactions + shared .main styles
library-custom.css        ← Library (depends on transactions-custom for .main)
wallet-custom.css         ← Wallet
profile-custom.css        ← Profile (standalone, replaces inline <style>)
```

---

## NOT YET REDESIGNED

These templates/sections still use the old design:

### From library.html (sub-templates):
- `_library_item_cancel_confirm.shtml` — Cancel subscription confirmation modal
- `_library_item_renew_confirm.shtml` — Renew confirmation modal
- `_library_item_deferred_cancel_confirm.shtml` — Deferred cancel confirmation
- `_library_item_refund_confirm.shtml` — Refund confirmation
- `_library_update_payment_method.shtml` — Update payment method modal (complex, has card list + add new card flows)
- `upgrade_options.shtml` — Upgrade screen with radio selection, billing plan details, address collection, review/confirm
- `_library_item_leave_shared_subscription_confirm.shtml` — Leave shared subscription
- Shared subscription management screens
- Print address form component

### From wallet.html (sub-templates):
- `wallet_item.shtml` — Add/edit card form
- `wallet_add_datatranspostfinance.shtml` — Add Postfinance
- `wallet_add_account.shtml` — Add account
- `wallet_add_paypal.shtml` — Add PayPal
- Various provider-specific form templates (OBI, Braintree, Stripe, Zlick, etc.)

### Other My Account tabs (not started):
- Payments
- Vouchers
- Bills
- Licensing
- Newsletters
- Help
- Gift subscriptions

---

## KEY TECHNICAL NOTES

1. **AngularJS (legacy)** — Templates use `ng-*` directives, `<t>` translation tags, custom elements (`<tp-menu>`, `<library-table>`, etc.). These must NEVER be modified.

2. **Piano Platform directives** — Profile template uses Piano-specific directives like `fieldProfileFirstName`, `*hideChangePassword`, `showIfSocialAuthAvailable`, `actionUpdateProfile`, etc. Profile also has Angular-like syntax (`*ngIf` style) that's actually Piano's own template engine.

3. **Two separate CSS systems:**
   - My Account tabs (transactions, library, wallet): Override `my-account-bundle.css` with custom CSS
   - Profile: Has its own inline `<style>` block (~1800 lines), replaced entirely by `profile-custom.css`

4. **Bundle gotchas found:**
   - `button.button { min-height: 40px }` and `a.button { height: 40px; line-height: 40px }` — must override with `!important`
   - `.section-text` has `float: left`, `margin-bottom: 26px`, `position: relative; top: 3px` — all overridden
   - `.scrollable-content` has `border-top`, `min-height: 240px`, `overflow-y: auto` — all overridden
   - `.vanilla-flat-tabs` has `float: right`, `text-transform: uppercase` — overridden for pill-style tabs

5. **No build process** — Plain HTML/CSS, no npm/webpack. Files are loaded directly.

6. **Language:** Estonian (`lang="et"`). All UI text is wrapped in `<t>` tags for Piano's translation system.

---

## DESIGN TOKENS REFERENCE (from style.css)

```css
/* Colors used in redesign */
--ol__red__700: #e3000f;      /* Primary: titles, names, prices, links, primary buttons */
--ol__red__800: #af0510;      /* Hover states */
--ol__red__50: #fff0f1;       /* Light red bg (share button, delete hover) */
--ol__red__100: #ffdddf;      /* Active states */
--ol__monochrome__50: #f5f6f6;  /* Main container bg, hover bg */
--ol__monochrome__100: #e5e8e8; /* Secondary button bg, borders */
--ol__monochrome__200: #cdd3d4; /* Input borders */
--ol__monochrome__300: #aab3b6; /* Divider dots */
--ol__monochrome__400: #808d90; /* Icon default color, placeholder text */
--ol__monochrome__500: #657275; /* Secondary text, tab inactive */
--ol__monochrome__950: #17191a; /* Primary text, manage button text */
--ol__cream__50: #fff8eb;       /* Warning/notice backgrounds */
--white: #ffffff;               /* Cards, inputs */

/* Typography */
--font__family__fira: "Fira Sans Condensed", sans-serif;  /* Section headers, prices */
--font__family__inter: "Inter", sans-serif;                /* Everything else */

/* Spacing (4px grid) */
--spacing__1: 4px;   --spacing__2: 8px;   --spacing__3: 12px;
--spacing__4: 16px;  --spacing__5: 20px;  --spacing__6: 24px;

/* Radii */
--radius__sm: 4px;   --radius__md: 6px;   --radius__lg: 8px;   --radius__xl: 12px;
```

---

## HOW TO CONTINUE

1. Upload the project files to the new chat: `style.css`, `my-account-bundle.css`, `README.md`
2. Paste this document as context
3. Upload whichever template pair (template + rendered) you want to work on next
4. Reference this document for established patterns — the AI should match the existing card-based design exactly

