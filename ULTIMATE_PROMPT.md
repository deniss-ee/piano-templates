# Ultimate AI Agent Prompt — Piano Templates Project

> **Copy everything below the line into a new AI chat session.**

---

You are working on the **Piano Templates** project — a template library for subscription modals, authentication pages, and My Account management for **Õhtuleht** (Estonian news publisher).

## PROJECT CONTEXT

- **Stack:** Plain HTML5/CSS3, no build tools, no npm. AngularJS (legacy, EOL) for dynamic behavior. Piano Platform for paywall/subscription.
- **Language:** Estonian (`lang="et"`). UI text wrapped in `<t>` translation tags.
- **Template system:** Server-side variable replacement using `[%% variable %%]` syntax.
- **Two CSS systems:** (1) Design system `style.css` for modals, (2) `my-account-bundle.css` (15,561 lines, never edit) for My Account, overridden by custom CSS files.

## REPOSITORY STRUCTURE

```
/design system/          — Modal component library (13+ templates) + DESIGN_SYSTEM.md + style.css (master tokens)
/Modals/Master/          — Piano modal master template + style.css (DUPLICATE of design system/style.css — keep synced)
/Modals/Slider/          — Carousel component (design system aligned)
/My account/             — Account management (AngularJS)
/Piano ID/               — Login/register pages
/claude/                 — Redesigned My Account templates (active work)
/newsletters/            — Newsletter signup pages
/Landings/               — Landing pages
```

## DESIGN TOKENS (from style.css :root)

```css
/* Primary */
--ol__red__700: #e3000f;        /* Brand red — titles, links, primary buttons */
--ol__red__800: #af0510;        /* Hover */
--ol__red__50: #fff0f1;         /* Light red bg */

/* Secondary */
--ol__yellow__500: #fcd700;     /* Modal yellow bg */
--ol__yellow__400: #ffe80d;     /* Banner bg */

/* Monochrome */
--ol__monochrome__950: #17191a; /* Body text */
--ol__monochrome__500: #657275; /* Secondary text */
--ol__monochrome__400: #808d90; /* Icons, placeholder */
--ol__monochrome__200: #cdd3d4; /* Borders */
--ol__monochrome__100: #e5e8e8; /* Hover bg */
--ol__monochrome__50: #f5f6f6;  /* Container bg */
--ol__cream__50: #fff8eb;       /* Warning bg */
--white: #ffffff;

/* Typography */
--font__family__fira: "Fira Sans Condensed", sans-serif;  /* Headlines, prices */
--font__family__inter: "Inter", sans-serif;                /* Body, buttons */
--font__size__2xl: 24px;  --font__size__base: 16px;  --font__size__sm: 14px;  --font__size__xs: 12px;
--font__weight__bold: 700;  --font__weight__semibold: 600;  --font__weight__medium: 500;

/* Spacing (4px grid) */
--spacing__1: 4px;  --spacing__2: 8px;  --spacing__3: 12px;  --spacing__4: 16px;  --spacing__6: 24px;  --spacing__8: 32px;

/* Radii */
--radius__sm: 4px;  --radius__md: 6px;  --radius__lg: 8px;  --radius__xl: 12px;  --radius__2xl: 16px;  --radius__full: 9999px;
```

## MODAL SYSTEM (design system/ and Modals/)

### Standard template structure:
```html
<!DOCTYPE html>
<html lang="et">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Descriptive Title]</title>
  <link rel="stylesheet" href="../style.css">
</head>
<body>
<div class="pn-modal pn-modal--[white|yellow|red] pn-modal--[center|left]">
  <h1 class="pn-modal__title">[%% modal-h1 %%]</h1>
  <p class="pn-modal__text">[%% modal-p %%]</p>
  <a class="btn btn--red" ng-click="startCheckout('RESOURCE_ID')" href="[%% btn-url %%]">[%% btn-text %%]</a>
  <p class="pn-modal__footer">[%% modal-foo %%]</p>
</div>
</body>
</html>
```

### Key CSS classes:
- `.pn-modal` — flex column, gap 12px, padding 24px 16px, radius 16px
- `.pn-modal--white|yellow|red` — color themes (text colors auto-adapt)
- `.pn-modal--left|center` — alignment
- `.pn-modal__title` — Fira Sans Condensed, 24px, bold, red
- `.pn-modal__text` — Inter, 16px, medium
- `.pn-modal__footer` — Inter, 12px, gray
- `.btn` — 56px height, Inter bold. Variants: `--red`, `--yellow`, `--black`, `--full`
- `.pn-slider` — carousel component using modal classes

### Responsive breakpoints:
- **648px** — two-column modal layout
- **680px** — riba border radius
- **980px** — three-column pricing grid

### Layout patterns:
1. **Simple centered** — `.pn-modal--white.pn-modal--center` (ref: passive_churn.html)
2. **Left-aligned** — `.pn-modal--white.pn-modal--left` (ref: join_newsletter.html)
3. **Two-column** — `.pn-modal__container-left` + `.pn-modal__container` (ref: join_digi-1_tags.html)
4. **Form + validation** — `.input-wrapper`, `<div custom-script>`, checkEmail regex (ref: join_newsletter-input.html)

### Template variables:
- `[%% modal-h1 %%]`, `[%% modal-p %%]`, `[%% btn-text %%]`, `[%% btn-url %%]`, `[%% modal-foo %%]`
- `[%% modal-color %%]` (white/yellow/red), `[%% modal-alignment %%]` (left/center)
- Custom: use descriptive kebab-case, e.g. `[%% benefits-item--1 %%]`

## MY ACCOUNT REDESIGN (claude/ folder)

### Established visual language:
- **Container (`.main`):** bg `--ol__monochrome__50`, padding 1rem, radius `--radius__xl` (12px)
- **Cards:** white bg, radius `--radius__lg` (8px), padding `--spacing__4` (16px), NO border/shadow/hover
- **Card gap:** `--spacing__2` (8px)
- **Section headers:** Fira Sans Condensed, 24px, semibold (600), red, letter-spacing -0.02em
- **Card titles:** Inter, 14px, bold (700), red
- **Secondary text:** Inter, 12px, normal (400), `--ol__monochrome__500`
- **Prices:** Fira Sans Condensed, 16px, extrabold (800), red
- **Manage buttons:** Inter 12px semibold, 32px height, radius `--radius__md`, gray bg → hover `--ol__monochrome__100`
- **Primary buttons:** Red bg, white text, 40px height, radius `--radius__md`
- **Icon buttons:** 30px square, radius `--radius__md`, gray → hover red
- **Links:** red, hover `--ol__red__800` with underline
- **Transitions:** 125ms ease-in-out

### Bundle override strategy:
`my-account-bundle.css` is always loaded. Custom CSS uses `!important` where needed. Key overrides: `.section-text` (float/margin/font), `.scrollable-content` (border/min-height/overflow), `.button.green` (height 40→32px).

### CSS load order:
```
my-account-bundle.css  →  style.css (tokens)  →  transactions-custom.css  →  library-custom.css  →  wallet-custom.css  →  profile-custom.css
```

### Completed templates (in claude/):
1. **Transactions** ✅ — `transactions.html` + `transactions-custom.css` (scoped `.ma-transactions`)
2. **Library** ✅ — `library_list.html` + `library_list_item.html` + `library-custom.css` (scoped `.ma-library`)
3. **Profile** ✅ — `profile.html` + `profile-custom.css` (replaces ~1800-line inline style)
4. **Wallet** ✅ — `wallet.html` + `wallet-custom.css` (scoped `.ma-wallet`)

### NOT yet redesigned:
- Library sub-templates: cancel/renew/refund confirmation modals, update payment method, upgrade options, shared subscriptions
- Wallet sub-templates: add/edit card forms, PayPal/Postfinance/provider-specific forms
- Entire tabs: Payments, Vouchers, Bills, Licensing, Newsletters, Help, Gift subscriptions

## ANGULARJS PATTERNS

```html
<div ng-show="!isUserValid()">Logged out</div>
<div ng-if="condition">Conditional</div>
<button ng-click="startCheckout('RESOURCE_ID')">Subscribe</button>
<button ng-click="login()">Log In</button>
<button ng-click="close($event)">Close</button>
<input ng-model="userEmail" type="email" />
<span>{{userEmail}}</span>
<button external-event="event-name">Tracked</button>
<span ng-repeat="item in items">{{item.name}}</span>
```

Piano functions: `startCheckout(resourceId)`, `isUserValid()`, `login()`, `logout()`

Piano ID directives (profile): `fieldProfileFirstName`, `*hideChangePassword`, `*showChangePassword`, `showIfSocialAuthAvailable`, `actionUpdateProfile`

## RULES

### ALWAYS:
- Use existing CSS classes first — don't invent new ones for modals
- Use CSS variables from `:root` — never hardcode colors/sizes
- Update BOTH `style.css` files when changing modal styles (design system/ + Modals/Master/)
- Include `lang="et"` on `<html>`
- Follow BEM naming: `.block`, `.block--modifier`, `.block__element`
- Preserve ALL Angular directives, `<t>` tags, `ng-*` attributes, `external-event` attributes
- Test mentally at 320px, 768px, 1280px
- Use 4px spacing grid
- Transitions: 125ms ease-in-out

### NEVER:
- Edit `my-account-bundle.css` (it's a generated bundle)
- Create new CSS files for modals (use existing style.css)
- Hardcode colors or sizes
- Remove or modify Angular directives
- Add npm packages (no package.json exists)
- Break BEM naming convention
- Use modern JS features incompatible with AngularJS

## REFERENCE FILES

| Purpose | File |
|---------|------|
| Simple modal | `design system/passive_churn.html` |
| Newsletter modal | `design system/join_newsletter.html` |
| Form + validation | `design system/join_newsletter-input.html` |
| Two-column | `design system/join_digi-1_tags.html` |
| Landing page | `design system/join_digi-landing.html` |
| Slider | `Modals/Slider/index.html` |
| Design tokens | `design system/style.css` |
| Full docs | `design system/DESIGN_SYSTEM.md` |
| My Account layout | `My account/My account layout/index.html` |

## HOW TO USE THIS PROMPT

1. Paste this entire document as your first message in a new AI chat
2. Upload the relevant files you want to work on
3. Ask your question or describe the task
4. The AI will follow all established patterns automatically
