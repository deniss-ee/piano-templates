# Piano Templates - Modal & Authentication System

> **Last Updated:** 3 March 2026  
> **Purpose:** Template library for Piano paywall modals, Piano ID authentication, and My Account pages for Õhtuleht publication

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [Directory Structure](#directory-structure)
- [Modal Systems](#modal-systems)
- [Design System](#design-system)
- [Getting Started](#getting-started)
- [Creating New Modals](#creating-new-modals)
- [Template Variables](#template-variables)
- [AngularJS Integration](#angularjs-integration)
- [Styling Conventions](#styling-conventions)
- [Responsive Breakpoints](#responsive-breakpoints)
- [Accessibility](#accessibility)
- [Known Limitations](#known-limitations)
- [Maintenance](#maintenance)

---

## 🎯 Project Overview

This repository contains HTML/CSS templates for the Õhtuleht Kirjastuse (Õhtuleht Publishing) Piano subscription system. The project includes:

- **Paywall Modals** - Promotional and subscription modals for Piano platform
- **Piano ID** - Authentication pages (login/register)
- **My Account** - Subscriber account management interface
- **Design System** - Comprehensive component library with design tokens

### Technology Stack

| Technology | Purpose | Version |
|------------|---------|---------|
| **HTML5** | Template structure | - |
| **CSS3** | Styling with CSS Variables | - |
| **AngularJS** | Dynamic behavior (legacy) | Unknown |
| **Piano Platform** | Paywall/subscription management | External |
| **Google Fonts** | Typography (Fira Sans Condensed, Inter) | - |

### Key Characteristics

- **Template-Driven:** Server-side variable replacement (`[%% variable %%]`)
- **No Build Tools:** Plain HTML/CSS, no webpack/npm/package.json
- **Legacy Framework:** AngularJS for dynamic features
- **Component-Based CSS:** BEM-like naming with CSS custom properties
- **Mobile-First:** Responsive design with defined breakpoints

---

## 🏗️ Architecture

### Modal System Patterns

The project uses **two distinct modal approaches**:

#### 1. Piano Template Modals (Static Templates)
- **Location:** `/Modals/Master/`, `/design system/`
- **Pattern:** HTML templates with placeholder variables
- **Rendering:** Server-side template replacement
- **State:** Managed by Piano platform
- **Use Case:** Subscription offers, newsletters, promotions

#### 2. My Account Modal (AngularJS Dynamic)
- **Location:** `/My account/My account layout/`
- **Pattern:** ng-template with transclude
- **Rendering:** Client-side AngularJS
- **State:** AngularJS scope variables
- **Use Case:** Account management dialogs

### Data Flow

```
Piano Platform → Template Variables → HTML Rendering → User Interaction → AngularJS Events → Piano/Analytics
```

**Communication Methods:**
- `[%% variable %%]` - Server-side template replacement
- `ng-click="startCheckout('ID')"` - Piano checkout trigger
- `ng-click="close($event)"` - Modal close event
- `external-event="event-name"` - Analytics tracking
- `ng-model="userEmail"` - Two-way data binding

---

## 📁 Directory Structure

```
piano-templates/
├── Modals/
│   ├── Master/                    # Piano modal master templates
│   │   ├── index.html             # Template with variables
│   │   ├── rendered.html          # Example rendered output
│   │   └── style.css              # Modal styles (472 lines)
│   └── Slider/                    # Slider/carousel component
│       ├── index.html             # Slider with 5 slides
│       └── style.css              # Slider styles (design system aligned)
│
├── design system/                 # Component library & templates
│   ├── DESIGN_SYSTEM.md          # Comprehensive documentation (794 lines)
│   ├── STYLE_GUIDE.html          # Visual style guide
│   ├── style.css                 # Master stylesheet (identical to Modals/Master)
│   ├── buy_one.html              # Purchase CTA modal
│   ├── join_digi-1.html          # Digital package promo
│   ├── join_digi-1_tags.html     # Digital package with tags
│   ├── join_digi-2.html          # Digital package variant 2
│   ├── join_digi-2_tags.html     # Digital package variant 2 with tags
│   ├── join_digi-landing.html    # Full landing page
│   ├── join_newsletter.html      # Simple newsletter signup
│   ├── join_newsletter-input.html # Newsletter with email form
│   ├── passive_churn.html        # Subscription renewal failure
│   ├── retention.html            # Retention message
│   └── ribad.html                # Top banner bar
│
├── My account/                    # Account management interface
│   ├── my-account-layout.css     # Layout styles (782 lines)
│   ├── myaccountbundle.css       # Bundled AngularJS styles (15,561 lines)
│   ├── My account layout/
│   │   └── index.html            # Main layout with ng-template modal
│   ├── My Account Library/
│   │   ├── library-shelf.html
│   │   ├── library-shelf-REDESIGNED.html
│   │   └── piano.html
│   └── My Account Transactions/
│       ├── index.html
│       └── piano.html
│
├── Piano ID/                      # Authentication pages
│   ├── piano-id-layout.css       # Auth page styles
│   ├── Piano ID Login Page/
│   │   └── index.html
│   └── Piano ID Register page/
│       └── index.html
│
└── style.css                      # Root stylesheet
```

---

## � Slider Component

### Overview

The slider component is a carousel/slideshow system that has been redesigned to match the modal design system. It uses the same design tokens, typography, spacing, and transition patterns as the modals.

**File:** [Modals/Slider/index.html](Modals/Slider/index.html)

### Features

- ✅ **Design System Aligned:** Uses modal CSS variables and design tokens
- ✅ **Responsive Navigation:** Previous/next buttons with hover states
- ✅ **Bullet Indicators:** Active state tracking with smooth transitions
- ✅ **Autoplay:** Configurable auto-advance with pause on interaction
- ✅ **Edge Handling:** Optional button hiding at first/last slide
- ✅ **Template Variables:** Dynamic content via `[%% variable %%]` placeholders

### Structure

```html
<div class="pn-modal pn-modal--white pn-modal--center pn-slider">
  <div class="slides">
    <div class="slide">
      <h3 class="pn-modal__title pn-slider__title">[%% slide-headline-1 %%]</h3>
      <p class="pn-modal__text pn-slider__text">[%% slide-text-1 %%]</p>
      <a class="btn btn--red" href="[%% slide-url-1 %%]">[%% slide-button-copy-1 %%]</a>
    </div>
    <!-- Additional slides -->
  </div>
  
  <!-- Navigation -->
  <button class="slider-button slider-button--prev" data-dir="prev">
    <!-- SVG icon -->
  </button>
  <button class="slider-button slider-button--next" data-dir="next">
    <!-- SVG icon -->
  </button>
  
  <!-- Bullet indicators -->
  <div class="bullets"></div>
</div>
```

### Design System Integration

#### Typography
- **Title:** Uses `.pn-modal__title` (Fira Sans Condensed, 24px, bold)
- **Text:** Uses `.pn-modal__text` (Inter, 16px, medium)
- **Button:** Uses `.btn--red` (56px height, Inter, bold)

#### Spacing
- **Slide Padding:** `var(--spacing__6) var(--spacing__4)` (24px 16px)
- **Gap:** `var(--spacing__3)` (12px between elements)
- **Bullets:** `var(--spacing__1)` gap (4px)

#### Colors
- **Active Bullet:** `var(--ol__red__700)` (#e3000f)
- **Inactive Bullet:** rgba(227, 0, 15, 0.25)
- **Button Background:** `var(--white)` with shadow
- **Button Hover:** `var(--ol__monochrome__50)`

#### Transitions
- **Slide Animation:** 125ms ease-in-out (matches modal timing)
- **Button Hover:** 125ms ease-in-out
- **Bullet Hover:** 125ms ease-in-out with scale(1.2)

#### Border Radius
- **Navigation Buttons:** `var(--radius__full)` (fully rounded)
- **Bullets:** `var(--radius__full)` (circular)

### Configuration

The slider includes JavaScript configuration options:

```javascript
const hideButtonsOnEdges = true;  // Hide prev/next at edges
const autoplay = true;             // Enable auto-advance
const autoplayInterval = 3000;     // 3 seconds per slide
```

### Template Variables

| Variable | Description | Example |
|----------|-------------|----------|
| `[%% is-first-slide-show %%]` | Show/hide first slide | `true` or `false` |
| `[%% slide-headline-N %%]` | Slide title | "Special Offer" |
| `[%% slide-text-N %%]` | Slide description | "Get 50% off..." |
| `[%% slide-url-N %%]` | Button link | "#subscribe" |
| `[%% slide-button-copy-N %%]` | Button text | "Learn More" |

### Responsive Behavior

**Desktop (> 648px):**
- Full-size navigation buttons (48px)
- Standard title size (24px)
- Padding: 24px 16px

**Tablet (421px - 648px):**
- Medium navigation buttons (40px)
- Reduced title size (20px)
- Padding: 40px 24px

**Mobile (≤ 420px):**
- Small navigation buttons (32px)
- Small SVG icons (24px)
- Padding: 32px 16px
- Reduced bullet spacing

### Usage Example

```html
<!-- Include modal design system first -->
<link rel="stylesheet" href="../Master/style.css">
<link rel="stylesheet" href="style.css">

<!-- Slider with 3 promotional slides -->
<div class="pn-modal pn-modal--white pn-modal--center pn-slider">
  <div class="slides">
    <div class="slide">
      <h3 class="pn-modal__title pn-slider__title">70% Off First Year</h3>
      <p class="pn-modal__text pn-slider__text">Subscribe now and save</p>
      <a class="btn btn--red" href="#subscribe">Get Started</a>
    </div>
    <!-- More slides -->
  </div>
  <button class="slider-button slider-button--prev" data-dir="prev">...</button>
  <button class="slider-button slider-button--next" data-dir="next">...</button>
  <div class="bullets"></div>
</div>
```

---

## �🎨 Modal Systems

### System 1: Piano Template Modals

**File:** [Modals/Master/index.html](Modals/Master/index.html)

```html
<div class="pn-modal pn-modal--[%% modal-color %%] pn-modal--[%% modal-alignment %%]">
  <img class="pn-modal__logo [%% logo-visibility %%]" 
       src="https://b.ohtuleht.ee/html5/Ohtuleht/Piano/logo-ol-[%% logo-color %%].svg" 
       alt="Õhtuleht" />
  <h1 class="pn-modal__title">[%% modal-h1 %%]</h1>
  <p class="pn-modal__text">[%% modal-p %%]</p>
  <a class="btn btn--[%% btn-color %%]" 
     ng-click="startCheckout('TMEQ915RQ4DM')" 
     href="[%% btn-url %%]">[%% btn-text %%]</a>
  <p class="pn-modal__footer">[%% modal-foo %%]</p>
</div>
```

**Features:**
- ✅ Variable-based content
- ✅ Color theming (white/yellow/red)
- ✅ Alignment modifiers (left/center)
- ✅ Piano checkout integration
- ❌ No close button UI
- ❌ No accessibility attributes

### System 2: My Account Modal

**File:** [My account/My account layout/index.html](My account/My account layout/index.html)

```html
<script id="template/modal/window.html" type="text/ng-template">
  <div class="myaccount-custom-modal tp-modal {{ windowClass }}" 
       ng-class="{in: animate}" 
       ng-style="{'z-index': 1050 + index*10}">
    <div class="myaccount-custom-modal-container">
      <div class="modal-close" ng-click="close($event)"></div>
      <div ng-transclude></div>
    </div>
  </div>
</script>
```

**Features:**
- ✅ Reusable AngularJS component
- ✅ Close button with click handler
- ✅ Dynamic z-index stacking
- ✅ Transclude for custom content
- ❌ No ARIA attributes
- ❌ No keyboard handling

---

## 🎨 Design System

### CSS Custom Properties (Design Tokens)

All design tokens are defined in `:root` and available globally:

#### Color Palette

**Primary Red:**
```css
--ol__red__700: #e3000f;  /* Primary brand color - buttons, titles */
--ol__red__800: #af0510;  /* Hover states */
```

**Secondary Yellow:**
```css
--ol__yellow__500: #fcd700;  /* Modal backgrounds */
--ol__yellow__400: #ffe80d;  /* Banner backgrounds */
```

**Monochrome:**
```css
--ol__monochrome__950: #17191a;  /* Body text */
--ol__monochrome__500: #657275;  /* Footer text */
--ol__monochrome__200: #cdd3d4;  /* Borders */
```

#### Typography

**Fonts:**
```css
--font__family__fira: "Fira Sans Condensed", sans-serif;  /* Headlines */
--font__family__inter: "Inter", sans-serif;               /* Body text */
```

**Sizes:**
```css
--font__size__2xl: 24px;    /* Modal titles */
--font__size__base: 16px;   /* Body text, buttons */
--font__size__xs: 12px;     /* Footer text */
```

**Weights:**
```css
--font__weight__bold: 700;    /* Titles, buttons */
--font__weight__medium: 500;  /* Body text */
```

#### Spacing (4px base unit)

```css
--spacing__1: 4px;    /* Minimal gaps */
--spacing__2: 8px;    /* Form gaps */
--spacing__3: 12px;   /* Component gaps (modal internal) */
--spacing__4: 16px;   /* Section padding */
--spacing__6: 24px;   /* Modal padding */
--spacing__8: 32px;   /* Button padding */
```

#### Border Radius

```css
--radius__sm: 4px;    /* Buttons, badges */
--radius__lg: 8px;    /* Cards, inputs */
--radius__2xl: 16px;  /* Modal containers */
```

### Component Classes

#### Modal Container

```css
.pn-modal {
  display: flex;
  flex-direction: column;
  gap: var(--spacing__3);
  padding: var(--spacing__6) var(--spacing__4) var(--spacing__4);
  border-radius: var(--radius__2xl);
  background: var(--white);
}
```

**Modifiers:**
- `.pn-modal--white` - White background (default)
- `.pn-modal--yellow` - Yellow 500 background
- `.pn-modal--red` - Red 700 background
- `.pn-modal--left` - Left-aligned content
- `.pn-modal--center` - Center-aligned content

#### Typography Components

```css
.pn-modal__title {
  font-family: var(--font__family__fira);
  font-size: var(--font__size__2xl);
  font-weight: var(--font__weight__bold);
  line-height: 1.2;
  color: var(--ol__red__700);
}

.pn-modal__text {
  font-family: var(--font__family__inter);
  font-size: var(--font__size__base);
  font-weight: var(--font__weight__medium);
  line-height: 1.35;
  color: var(--ol__monochrome__950);
}

.pn-modal__footer {
  font-size: var(--font__size__xs);
  font-weight: var(--font__weight__medium);
  color: var(--ol__monochrome__500);
}
```

#### Buttons

```css
.btn {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  height: 56px;
  padding: 0 var(--spacing__8);
  border-radius: var(--radius__sm);
  font-family: var(--font__family__inter);
  font-size: var(--font__size__base);
  font-weight: var(--font__weight__bold);
  transition: background-color 125ms ease-in-out;
}

.btn--red { background: var(--ol__red__700); color: white; }
.btn--yellow { background: var(--ol__yellow__500); color: var(--ol__yellow__950); }
.btn--full { width: 100%; }
```

---

## 🚀 Getting Started

### Prerequisites

- Text editor (VS Code recommended)
- Web browser for testing
- Basic understanding of HTML/CSS
- Familiarity with AngularJS (for dynamic features)
- Access to Piano platform (for deployment)

### Local Development

1. **Clone or navigate to the repository:**
   ```bash
   cd /path/to/piano-templates
   ```

2. **Open templates in browser:**
   - Open HTML files directly in browser
   - Use a local server for AngularJS features:
     ```bash
     # Python 3
     python3 -m http.server 8000
     
     # Node.js
     npx http-server
     ```

3. **Edit templates:**
   - Modify HTML in `/design system/` or `/Modals/Master/`
   - Update styles in `style.css`
   - Test responsive behavior at different viewport sizes

### File Linking

All templates link to the master stylesheet:

```html
<!-- From design system folder -->
<link rel="stylesheet" href="../style.css">

<!-- From Modals/Master folder -->
<link rel="stylesheet" href="style.css">
```

---

## ✨ Creating New Modals

### Quick Start Template

```html
<!DOCTYPE html>
<html lang="et">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>Your Modal Title</title>
  <link rel="stylesheet" href="../style.css">
</head>
<body>

<div class="pn-modal pn-modal--white pn-modal--center">
  <h1 class="pn-modal__title">[%% modal-title %%]</h1>
  <p class="pn-modal__text">[%% modal-description %%]</p>
  <button class="btn btn--red">[%% cta-text %%]</button>
  <p class="pn-modal__footer">[%% footer-text %%]</p>
</div>

</body>
</html>
```

### Layout Patterns

#### 1. Simple Centered Modal
**Use Case:** Confirmations, simple messages  
**Reference:** [passive_churn.html](design system/passive_churn.html)

```html
<div class="pn-modal pn-modal--white pn-modal--center">
  <h1 class="pn-modal__title">Title</h1>
  <p class="pn-modal__text">Message</p>
  <button class="btn btn--red">Action</button>
</div>
```

#### 2. Left-Aligned with Footer
**Use Case:** Newsletter signups, informational modals  
**Reference:** [join_newsletter.html](design system/join_newsletter.html)

```html
<div class="pn-modal pn-modal--white pn-modal--left">
  <h1 class="pn-modal__title">Title</h1>
  <p class="pn-modal__text">Description</p>
  <button class="btn btn--red">Subscribe</button>
  <p class="pn-modal__footer">Terms and conditions</p>
</div>
```

#### 3. Two-Column Responsive
**Use Case:** Promotional offers with benefits list  
**Reference:** [join_digi-1_tags.html](design system/join_digi-1_tags.html)

```html
<div class="pn-modal pn-modal--yellow pn-modal--left">
  <div class="pn-modal__container-left">
    <h1 class="pn-modal__title">Special Offer</h1>
    <ul class="list">
      <li class="list__item">
        <div class="list__bullet"></div>
        <div class="list__text">Benefit 1</div>
      </li>
    </ul>
  </div>
  
  <div class="pn-modal__container">
    <div class="card card--white card--center">
      <div class="price--lg">
        <span class="price__value">€9.99</span>
        <span class="price__period">/month</span>
      </div>
      <button class="btn btn--red">Subscribe</button>
    </div>
  </div>
</div>

<style>
  @media (min-width: 648px) {
    .pn-modal--left {
      flex-direction: row;
      align-items: center;
      gap: var(--spacing__6);
    }
    .pn-modal__container-left { flex: 1; }
    .pn-modal__container { flex: 0 0 auto; width: 350px; }
  }
</style>
```

#### 4. Form with Validation
**Use Case:** Email collection, data entry  
**Reference:** [join_newsletter-input.html](design system/join_newsletter-input.html)

```html
<div class="pn-modal pn-modal--white pn-modal--left">
  <h1 class="pn-modal__title">[%% title %%]</h1>
  
  <form class="form-group">
    <div class="input-wrapper" id="email-wrapper">
      <input type="email" 
             class="input" 
             id="user-email"
             ng-model="userEmail"
             placeholder="your@email.com">
      <label class="input-error" id="email-error"></label>
    </div>
    <button class="btn btn--red btn--full" type="submit">Submit</button>
  </form>
</div>

<div custom-script>
  // Email validation regex
  var checkEmail = function(email) {
    var regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
  };
  
  // Add validation logic here
</div>
```

---

## 🔧 Template Variables

### Standard Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `[%% modal-h1 %%]` | Main title | "Subscribe Now!" |
| `[%% modal-p %%]` | Body text | "Get unlimited access..." |
| `[%% btn-text %%]` | Button label | "Start Free Trial" |
| `[%% btn-url %%]` | Button href | "#" or external URL |
| `[%% modal-foo %%]` | Footer text | "Terms apply" |

### Color Modifiers

| Variable | Values | Effect |
|----------|--------|--------|
| `[%% modal-color %%]` | `white`, `yellow`, `red` | Background color |
| `[%% modal-alignment %%]` | `left`, `center` | Content alignment |
| `[%% btn-color %%]` | `red`, `yellow`, `black` | Button color |
| `[%% logo-color %%]` | `red`, `white` | Logo variant |

### Conditional Visibility

```html
<!-- Show/hide logo -->
<img class="pn-modal__logo [%% logo-visibility %%]" src="..." />
<!-- logo-visibility = "" (visible) or "hidden" (hidden) -->
```

### Custom Variables

Create descriptive names for your content:

```html
[%% benefits-promo %%]         <!-- "70% off first year!" -->
[%% benefits-item--1 %%]       <!-- "Unlimited article access" -->
[%% benefits-price %%]         <!-- "€37.76" -->
[%% terms-and-condition-href %%]  <!-- URL to T&C page -->
```

---

## ⚛️ AngularJS Integration

### Common Directives

#### Conditional Rendering

```html
<!-- Show for logged-out users -->
<div ng-show="!isUserValid()">
  <p>Please log in to continue</p>
</div>

<!-- Show for expired subscriptions -->
<div ng-if="libraryItem.expired">
  <p>Your subscription has expired</p>
</div>
```

#### Event Handlers

```html
<!-- Piano checkout trigger -->
<button ng-click="startCheckout('RESOURCE_ID')">Subscribe</button>

<!-- Login trigger -->
<button ng-click="login()">Log In</button>

<!-- Close modal -->
<div class="modal-close" ng-click="close($event)"></div>

<!-- Custom function -->
<button ng-click="toggleRenew(libraryItem)">Toggle Auto-Renew</button>
```

#### Data Binding

```html
<!-- Two-way binding -->
<input ng-model="userEmail" type="email" />
<p>You entered: {{userEmail}}</p>

<!-- One-way binding -->
<span>{{libraryItem.resourceName}}</span>
<span>{{libraryItem.nextBillingDate}}</span>
```

#### Dynamic Styling

```html
<!-- Conditional classes -->
<div ng-class="{in: animate, 'error-state': hasError}">

<!-- Dynamic styles -->
<div ng-style="{'z-index': 1050 + index*10}">
```

#### Analytics Tracking

```html
<!-- Event tracking -->
<button external-event="cta-login" 
        ng-click="login()">
  Log In
</button>

<!-- Event with data -->
<button external-event="newsletter-submit"
        external-event-user-email="{{userEmail}}"
        external-event-agree-newsletter="{{agreeNewsletter}}">
  Submit
</button>
```

### Piano Integration

#### Checkout Trigger

```html
<a class="btn btn--red" 
   ng-click="startCheckout('TMEQ915RQ4DM')" 
   href="#">
  Subscribe Now
</a>
```

**Resource ID Format:** `TMEQ915RQ4DM` (Piano resource identifier)

#### Common Piano Functions

- `startCheckout(resourceId)` - Initiate subscription flow
- `isUserValid()` - Check if user is logged in
- `login()` - Trigger login modal
- `logout()` - Log out user

---

## 🎨 Styling Conventions

### BEM-Like Naming

```css
/* Block */
.pn-modal { }

/* Block with modifier */
.pn-modal--white { }
.pn-modal--yellow { }

/* Element */
.pn-modal__title { }
.pn-modal__text { }

/* Element with modifier */
.pn-modal__footer--dark { }
```

### Component Structure

```
Component Base → Color Modifier → Alignment Modifier → Element → Element Modifier
```

Example:
```html
<div class="pn-modal pn-modal--yellow pn-modal--left">
  <h1 class="pn-modal__title">...</h1>
  <p class="pn-modal__footer pn-modal__footer--dark">...</p>
</div>
```

### Color Theming

Components automatically adapt to parent background:

```css
/* Default (white background) */
.pn-modal__title { color: var(--ol__red__700); }

/* Yellow background */
.pn-modal--yellow .pn-modal__title { color: var(--ol__red__700); }
.pn-modal--yellow .pn-modal__text { color: var(--ol__yellow__950); }

/* Red background */
.pn-modal--red .pn-modal__title { color: var(--ol__yellow__400); }
.pn-modal--red .pn-modal__text { color: var(--white); }
```

### Scoped Reset Strategy

To prevent parent styles from interfering:

```css
/* Reset only Piano components */
.pn-modal *,
.pn-modal *::before,
.pn-modal *::after {
  margin: 0 !important;
  padding: 0 !important;
}

/* Re-apply intentional spacing */
.pn-modal {
  padding: var(--spacing__6) var(--spacing__4) var(--spacing__4) !important;
}
```

---

## 📱 Responsive Breakpoints

### Key Breakpoints

| Breakpoint | Usage | Example |
|------------|-------|---------|
| **648px** | Two-column modal layout | [join_digi-1_tags.html](design system/join_digi-1_tags.html) |
| **680px** | Riba border radius | [ribad.html](design system/ribad.html) |
| **980px** | Three-column pricing grid | [join_digi-landing.html](design system/join_digi-landing.html) |

### Mobile-First Approach

```css
/* Mobile (default) */
.pn-modal--left {
  display: flex;
  flex-direction: column;
}

/* Desktop (648px+) */
@media (min-width: 648px) {
  .pn-modal--left {
    flex-direction: row;
    align-items: center;
  }
}
```

### Testing Viewports

- **Mobile:** 320px - 640px
- **Tablet:** 640px - 980px
- **Desktop:** 980px+

---

## ♿ Accessibility

### Current State

**Implemented:**
- ✅ Semantic HTML structure
- ✅ Color contrast for text (generally good)
- ✅ Focus styles on inputs (`:focus` border change)
- ✅ Hover states on buttons and links

**Missing (Critical):**
- ❌ ARIA attributes (`role="dialog"`, `aria-modal`, `aria-labelledby`)
- ❌ Focus trap within modals
- ❌ Keyboard navigation (ESC to close, TAB management)
- ❌ Screen reader announcements
- ❌ Focus return on modal close

### Accessibility Improvements Template

Add these attributes to enhance accessibility:

```html
<div class="pn-modal pn-modal--white pn-modal--center"
     role="dialog"
     aria-modal="true"
     aria-labelledby="modal-title"
     aria-describedby="modal-description">
  
  <h1 id="modal-title" class="pn-modal__title">
    Modal Title
  </h1>
  
  <p id="modal-description" class="pn-modal__text">
    Modal description for screen readers
  </p>
  
  <button class="modal-close" 
          aria-label="Close modal"
          ng-click="close($event)">
    <span aria-hidden="true">×</span>
  </button>
  
  <button class="btn btn--red">
    Subscribe
  </button>
</div>
```

### Keyboard Navigation (To Implement)

```javascript
// Add to custom-script section
document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape') {
    // Close modal logic
    angular.element('#modal').scope().close();
  }
});
```

---

## ⚠️ Known Limitations

### Technical Debt

1. **AngularJS Dependency**
   - Framework is no longer maintained (EOL: January 2022)
   - Limits modern JavaScript features
   - Performance concerns with large applications

2. **No Build Process**
   - No minification or bundling
   - No SASS/PostCSS preprocessing
   - Manual dependency management

3. **Duplicate Stylesheets**
   - [Modals/Master/style.css](Modals/Master/style.css) and [design system/style.css](design system/style.css) are identical
   - Update both when making changes

4. **No Centralized Modal Manager**
   - Each modal is isolated
   - No shared state management
   - Difficult to implement global modal features

### Missing Features

- **Focus Management:** No focus trap or keyboard navigation
- **Click Outside to Close:** Backdrop click not implemented
- **State Persistence:** Modal state lost on page refresh
- **Animation System:** Limited CSS transitions only
- **Loading States:** No spinner or loading indicators
- **Error Handling:** Basic form validation only

### Browser Support

**Tested/Supported:**
- ✅ Chrome/Edge (Blink engine)
- ✅ Safari (WebKit)
- ✅ Firefox (Gecko)

**Limited Support:**
- ⚠️ Internet Explorer 11 (requires polyfills)

---

## 🔧 Maintenance

### Updating Styles

**To modify design tokens:**

1. Edit [design system/style.css](design system/style.css) or [Modals/Master/style.css](Modals/Master/style.css)
2. Update CSS variables in `:root`:
   ```css
   :root {
     --ol__red__700: #e3000f; /* Update this */
   }
   ```
3. **Important:** Keep both files synchronized (they're duplicates)

### Adding New Components

1. Create HTML in `/design system/` folder
2. Follow naming convention: `action_description.html`
3. Use existing CSS classes from design system
4. Document new patterns in [DESIGN_SYSTEM.md](design system/DESIGN_SYSTEM.md)

### Testing Checklist

Before deploying new modals:

- [ ] Test on mobile (320px), tablet (768px), desktop (1280px)
- [ ] Verify all template variables render correctly
- [ ] Test AngularJS directives (if used)
- [ ] Check color contrast (WCAG AA minimum)
- [ ] Validate HTML (W3C validator)
- [ ] Test in Chrome, Safari, Firefox
- [ ] Verify Piano integration (checkout flow)
- [ ] Check analytics events fire correctly

### Version Control

**Critical Files to Track:**
- All HTML templates
- `style.css` (both copies)
- [DESIGN_SYSTEM.md](design system/DESIGN_SYSTEM.md)
- This README

**Can Ignore:**
- Browser cache files
- Local server files
- `.DS_Store` (macOS)

---

## 📚 Additional Resources

### Documentation Files

- [design system/DESIGN_SYSTEM.md](design system/DESIGN_SYSTEM.md) - Comprehensive component documentation (794 lines)
- [design system/STYLE_GUIDE.html](design system/STYLE_GUIDE.html) - Visual style guide with live examples
- This README - Project overview and development guide

### Reference Templates

**Simple Modals:**
- [passive_churn.html](design system/passive_churn.html) - Centered modal
- [join_newsletter.html](design system/join_newsletter.html) - Left-aligned modal

**Complex Modals:**
- [join_newsletter-input.html](design system/join_newsletter-input.html) - Form with validation
- [join_digi-1_tags.html](design system/join_digi-1_tags.html) - Two-column responsive
- [join_digi-landing.html](design system/join_digi-landing.html) - Multi-section landing page

**Specialized:**
- [ribad.html](design system/ribad.html) - Top banner bar
- [buy_one.html](design system/buy_one.html) - Purchase CTA
- [Modals/Slider/index.html](Modals/Slider/index.html) - Carousel/slideshow component

### External Links

- **Piano Platform:** https://piano.io/
- **AngularJS Docs:** https://docs.angularjs.org/
- **Google Fonts:** https://fonts.google.com/

---

## 🤝 Contributing

### Code Style Guidelines

**HTML:**
- Use semantic HTML5 elements
- Include `lang="et"` attribute
- Add descriptive `title` tags
- Maintain consistent indentation (2 spaces)

**CSS:**
- Use CSS custom properties for values
- Follow BEM naming convention
- Add vendor prefixes for compatibility
- Group related properties

**JavaScript:**
- Minimize inline scripts
- Use `<div custom-script>` for validation
- Document complex logic
- Follow AngularJS best practices

### Pull Request Template

```markdown
## Description
[Brief description of changes]

## Type of Change
- [ ] New modal template
- [ ] Style update
- [ ] Bug fix
- [ ] Documentation

## Testing
- [ ] Tested on mobile/tablet/desktop
- [ ] Validated HTML
- [ ] Verified AngularJS directives
- [ ] Checked accessibility

## Screenshots
[If applicable]
```

---

## 📝 License

[Add license information if applicable]

---

## 📧 Contact

For questions about Piano integration or template deployment, contact:
[Add contact information]

---

**Last Updated:** 3 March 2026  
**Maintainer:** [Your name/team]
