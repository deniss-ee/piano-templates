# AI Agent Prompt - Piano Templates Project

> **Purpose:** Use this prompt to onboard AI agents (Claude, GPT, etc.) to work on this project effectively.

---

## 📋 Copy-Paste Prompt for AI Agents

```
You are working on the Piano Templates project - a template library for subscription modals, authentication pages, and account management for the Õhtuleht publication (Estonian news publisher).

## PROJECT CONTEXT

**Technology Stack:**
- HTML5 templates with server-side variable replacement using [%% variable %%] syntax
- CSS3 with CSS Custom Properties (design tokens)
- AngularJS (legacy) for dynamic behavior
- Piano Platform integration for paywall/subscription management
- No build tools (plain HTML/CSS, no npm/webpack)

**Repository Structure:**
- `/Modals/Master/` - Piano modal master templates
- `/Modals/Slider/` - Carousel/slideshow component (design system aligned)
- `/design system/` - Component library with 13+ template variations
- `/My account/` - Account management interface (AngularJS-based)
- `/Piano ID/` - Authentication pages (login/register)

**Key Files:**
- `design system/DESIGN_SYSTEM.md` - Comprehensive design system documentation (794 lines)
- `design system/style.css` - Master stylesheet with design tokens (472 lines)
- `Modals/Master/style.css` - Duplicate of design system stylesheet
- `Modals/Slider/style.css` - Slider component styles (design system aligned)
- `My account/myaccountbundle.css` - Bundled AngularJS styles (15,561 lines)

## ARCHITECTURE PATTERNS

**Two Modal Systems:**

1. **Piano Template Modals** (Static)
   - Templates use placeholder variables: [%% variable %%]
   - Server-side rendering replaces variables with actual content
   - No JavaScript state management in templates
   - Files in: /design system/ and /Modals/Master/

2. **My Account Modal** (Dynamic)
   - AngularJS ng-template with transclude support
   - Client-side rendering with scope variables
   - Located in: /My account/My account layout/index.html

**Component Naming Convention:**
- BEM-like structure: `.block`, `.block--modifier`, `.block__element`
- Example: `.pn-modal`, `.pn-modal--yellow`, `.pn-modal__title`

**CSS Variables Pattern:**
```css
:root {
  --ol__red__700: #e3000f;      /* Primary brand color */
  --ol__yellow__500: #fcd700;   /* Secondary color */
  --font__family__inter: "Inter", sans-serif;
  --spacing__3: 12px;           /* 4px base unit */
}
```

## MODAL TEMPLATE STRUCTURE

**Standard Template:**
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

<div class="pn-modal pn-modal--white pn-modal--center">
  <h1 class="pn-modal__title">[%% modal-title %%]</h1>
  <p class="pn-modal__text">[%% modal-description %%]</p>
  <button class="btn btn--red">[%% cta-text %%]</button>
  <p class="pn-modal__footer">[%% footer-text %%]</p>
</div>

</body>
</html>
```

**Component Classes:**
- `.pn-modal` - Base modal container
- `.pn-modal--white|yellow|red` - Color variants
- `.pn-modal--left|center` - Alignment
- `.pn-modal__title` - Heading (Fira Sans Condensed, 24px, bold)
- `.pn-modal__text` - Body text (Inter, 16px, medium)
- `.pn-modal__footer` - Footer/disclaimer (Inter, 12px)
- `.btn` - Button (56px height, Inter, bold)
- `.btn--red|yellow|black` - Button color variants
- `.btn--full` - Full width button
- `.pn-slider` - Slider/carousel component (uses modal classes)
- `.slider-button` - Navigation buttons (circular, with shadow)
- `.bullet` - Slide indicators (circular, red theme)

## ANGULARJS INTEGRATION

**Common Directives:**
```html
<!-- Conditional rendering -->
<div ng-show="!isUserValid()">Logged out content</div>
<div ng-if="condition">Conditional content</div>

<!-- Event handlers -->
<button ng-click="startCheckout('RESOURCE_ID')">Subscribe</button>
<button ng-click="login()">Log In</button>
<div class="modal-close" ng-click="close($event)"></div>

<!-- Data binding -->
<input ng-model="userEmail" type="email" />
<span>{{userEmail}}</span>

<!-- Analytics -->
<button external-event="event-name" ng-click="action()">Track Me</button>
```

**Piano Platform Functions:**
- `startCheckout(resourceId)` - Initiate subscription flow
- `isUserValid()` - Check user authentication
- `login()` - Trigger login modal

## TEMPLATE VARIABLES

**Standard Variables:**
- `[%% modal-h1 %%]` - Main title
- `[%% modal-p %%]` - Body text
- `[%% btn-text %%]` - Button label
- `[%% btn-url %%]` - Button href
- `[%% modal-foo %%]` - Footer text
- `[%% modal-color %%]` - Color variant (white/yellow/red)
- `[%% modal-alignment %%]` - Alignment (left/center)

**Custom Variable Naming:**
- Use descriptive kebab-case names
- Group with prefixes: [%% benefits-item--1 %%], [%% benefits-item--2 %%]

## RESPONSIVE BREAKPOINTS

- **648px** - Two-column modal layout (left content + right pricing card)
- **680px** - Riba (banner) border radius
- **980px** - Three-column pricing grid

**Mobile-First Approach:**
```css
/* Mobile default */
.pn-modal--left { flex-direction: column; }

/* Desktop */
@media (min-width: 648px) {
  .pn-modal--left { flex-direction: row; }
}
```

## LAYOUT PATTERNS

**1. Simple Centered Modal**
- Use: Confirmations, simple messages
- Reference: design system/passive_churn.html
- Classes: `.pn-modal--white .pn-modal--center`

**2. Left-Aligned Modal**
- Use: Newsletters, informational
- Reference: design system/join_newsletter.html
- Classes: `.pn-modal--white .pn-modal--left`

**3. Two-Column Responsive**
- Use: Promotional offers with benefits
- Reference: design system/join_digi-1_tags.html
- Structure: `.pn-modal__container-left` + `.pn-modal__container`

**4. Form with Validation**
- Use: Email collection, data entry
- Reference: design system/join_newsletter-input.html
- Includes: `.input-wrapper`, `.input-error`, custom-script validation

## KNOWN LIMITATIONS

**Critical Issues:**
- ❌ No accessibility features (ARIA, focus trap, keyboard nav)
- ❌ No centralized modal manager
- ❌ AngularJS is EOL (January 2022)
- ❌ Duplicate stylesheets (Modals/Master/style.css and design system/style.css)
- ❌ No build process or package.json

**Missing Features:**
- Focus management and keyboard navigation
- Click outside to close functionality
- ARIA attributes and screen reader support
- ESC key to close modals

## CODING GUIDELINES

**When Creating New Modals:**
1. Place HTML in `/design system/` folder
2. Follow naming: `action_description.html`
3. Link to stylesheet: `<link rel="stylesheet" href="../style.css">`
4. Use existing CSS classes (don't create new ones unless necessary)
5. Include `lang="et"` attribute (Estonian)
6. Add template variables for dynamic content

**When Modifying Styles:**
1. Edit design system/style.css (master copy)
2. Update Modals/Master/style.css (keep synchronized)
3. Use CSS custom properties, never hardcode values
4. Follow BEM naming convention
5. Add vendor prefixes for compatibility

**Best Practices:**
- Use CSS variables from :root for all values
- Maintain 4px spacing grid (spacing__1 through spacing__96)
- Keep color theming automatic (components adapt to parent background)
- Test at mobile (320px), tablet (768px), desktop (1280px)
- Validate HTML with W3C validator

## REFERENCE FILES

**Templates to Study:**
- design system/join_newsletter-input.html - Form with email validation
- design system/join_digi-1_tags.html - Two-column responsive layout
- design system/join_digi-landing.html - Multi-section landing page
- design system/passive_churn.html - Simple centered modal
- Modals/Slider/index.html - Carousel/slideshow component (design system aligned)
- My account/My account layout/index.html - AngularJS modal template

**Documentation:**
- design system/DESIGN_SYSTEM.md - Complete component documentation
- README.md - Project overview and development guide

## COMMON TASKS

**Task: Create a new modal**
1. Copy appropriate reference template from design system/
2. Update title, meta description
3. Replace content with template variables
4. Apply correct color/alignment modifiers
5. Test responsive behavior
6. Validate HTML

**Task: Update styling**
1. Locate CSS variable in :root
2. Update value in design system/style.css
3. Copy changes to Modals/Master/style.css
4. Test across all templates

**Task: Add form validation**
1. Use join_newsletter-input.html as reference
2. Create .input-wrapper with .input element
3. Add <div custom-script> with validation logic
4. Use checkEmail regex pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/
5. Toggle .input-wrapper--bad class for errors

## ACCESSIBILITY IMPROVEMENTS

**Add these to new modals:**
```html
<div class="pn-modal" 
     role="dialog" 
     aria-modal="true" 
     aria-labelledby="modal-title">
  <h1 id="modal-title" class="pn-modal__title">Title</h1>
  <button class="modal-close" aria-label="Close modal">
    <span aria-hidden="true">×</span>
  </button>
</div>
```

## YOUR ROLE

When working on this project:
1. **Understand the context** - This is a template library, not a web app
2. **Preserve patterns** - Follow existing conventions strictly
3. **Use existing components** - Don't reinvent CSS classes
4. **Test responsively** - Always consider mobile/tablet/desktop
5. **Document changes** - Update DESIGN_SYSTEM.md when adding components
6. **Maintain duplicates** - Keep both style.css files synchronized
7. **Respect limitations** - Work within AngularJS constraints
8. **Prioritize consistency** - Match existing modal styles and structure

## IMMEDIATE ACTIONS

Before making any changes:
1. Read design system/DESIGN_SYSTEM.md (794 lines of component documentation)
2. Review 2-3 reference templates from design system/
3. Understand the variable replacement system [%% variable %%]
4. Check responsive breakpoints (648px, 680px, 980px)
5. Familiarize yourself with BEM naming pattern

## QUALITY CHECKLIST

Before completing any task:
- [ ] HTML validates (W3C)
- [ ] Uses existing CSS classes
- [ ] Template variables properly formatted
- [ ] Responsive at 320px, 768px, 1280px
- [ ] Color contrast meets WCAG AA
- [ ] AngularJS directives work (if used)
- [ ] Both style.css files updated (if CSS changes)
- [ ] Follows BEM naming convention
- [ ] Documentation updated (if new patterns)
```

---

## 🎯 How to Use This Prompt

### For AI Assistants (Claude, GPT, etc.)

1. **Start a new conversation** with your AI assistant
2. **Copy the entire prompt** from the code block above
3. **Paste it** as the first message in your conversation
4. **Ask specific questions** or request specific tasks

### Example Usage

```
[Paste the full AI Agent Prompt above]

Then ask:
"I need to create a new modal for a student discount promotion. 
It should have a yellow background, show a list of 3 benefits, 
and include a pricing card with a 50% discount badge."
```

The AI will now understand the project structure and can:
- Generate appropriate HTML using correct classes
- Use proper template variables
- Follow responsive patterns
- Match existing design system

### For Team Members

**When onboarding a new developer:**
1. Share this file
2. Have them read README.md
3. Point them to design system/DESIGN_SYSTEM.md
4. Let them study 2-3 reference templates

**When requesting AI assistance:**
1. Always include this prompt first
2. Reference specific files (the AI knows the structure)
3. Ask for explanations of existing patterns
4. Request code that follows project conventions

---

## 🔄 Updating This Prompt

**When the project evolves, update this section:**

### Version History

- **3 March 2026** - Initial creation based on comprehensive project analysis
  - Documented two modal systems (Piano + My Account)
  - Added AngularJS integration patterns
  - Listed all 13+ template variations
  - Noted critical limitations and missing features

### When to Update

Update this prompt when:
- [ ] New modal patterns are established
- [ ] CSS architecture changes
- [ ] New dependencies are added
- [ ] AngularJS is replaced/updated
- [ ] Accessibility features are implemented
- [ ] Build process is added

---

## 📊 Success Metrics

**An AI agent properly understands this project when it can:**

1. ✅ Create a new modal using correct HTML structure
2. ✅ Use appropriate CSS classes without creating new ones
3. ✅ Apply template variables with correct syntax
4. ✅ Implement responsive layouts at correct breakpoints
5. ✅ Integrate AngularJS directives properly
6. ✅ Maintain consistency with existing templates
7. ✅ Update both style.css files when needed
8. ✅ Follow BEM naming conventions
9. ✅ Understand limitations and work within constraints
10. ✅ Reference documentation files correctly

---

## 🎓 Learning Path for New Agents

**Step 1: Understand Structure (15 min)**
- Read project context
- Review directory structure
- Understand two modal systems

**Step 2: Study Design System (30 min)**
- Read design system/DESIGN_SYSTEM.md
- Review CSS custom properties
- Understand component classes

**Step 3: Analyze Examples (20 min)**
- Study passive_churn.html (simple)
- Study join_newsletter-input.html (form)
- Study join_digi-1_tags.html (complex)

**Step 4: Practice (variable)**
- Create a test modal
- Modify existing template
- Update styles using CSS variables

**Total Onboarding Time:** ~65 minutes

---

## ⚙️ Advanced Configuration

### For Specialized AI Agents

**Accessibility-Focused Agent:**
```
In addition to the base prompt above, focus on:
- Adding ARIA attributes to all modals
- Implementing focus trap patterns
- Creating keyboard navigation (ESC to close)
- Ensuring WCAG 2.1 AA compliance
- Adding skip links and landmarks
```

**Performance-Focused Agent:**
```
In addition to the base prompt above, focus on:
- Identifying duplicate stylesheets (Modals/Master + design system)
- Suggesting CSS minification strategies
- Analyzing bundle size (15,561 lines in myaccountbundle.css)
- Recommending modern alternatives to AngularJS
- Creating build process proposals
```

**Design-Focused Agent:**
```
In addition to the base prompt above, focus on:
- Ensuring consistent spacing (4px grid)
- Verifying color contrast ratios
- Implementing smooth transitions
- Creating additional layout patterns
- Documenting component variations
```

---

## 🚨 Critical Warnings for AI Agents

**DO NOT:**
- ❌ Create new CSS files (use existing style.css)
- ❌ Hardcode colors/sizes (use CSS variables)
- ❌ Modify myaccountbundle.css directly (it's bundled)
- ❌ Break BEM naming convention
- ❌ Assume modern JavaScript features (AngularJS constraints)
- ❌ Add npm packages (no package.json)
- ❌ Change viewport breakpoints without documentation

**ALWAYS:**
- ✅ Use existing CSS classes first
- ✅ Update both style.css files (Modals/Master + design system)
- ✅ Test on mobile/tablet/desktop
- ✅ Include template variables in new content
- ✅ Follow HTML5 semantic structure
- ✅ Add lang="et" to HTML tag
- ✅ Link to ../style.css from design system folder

---

**Last Updated:** 3 March 2026  
**Next Review:** When major architectural changes occur
