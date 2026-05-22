# Practical Accessibility — Course Notes
> Course by Sara Soueidan | practical-accessibility.today
> Hashtag: #PracticalA11y | Contact: sara@practical-accessibility.today

---

## Chapter 1 — Welcome to the Course

**Course Philosophy:**
- Accessibility is about creating a more equitable and inclusive digital world.
- The course provides foundational, evergreen accessibility knowledge for web designers and developers.
- Chapters alternate between theoretical and practical content — each builds on previous ones. **Do not skip chapters.**
- Every chapter includes a Table of Contents and video time-markers for navigation.

**Course Structure:**
- Videos + full text versions with code snippets and live examples.
- End-of-chapter recommended resources.
- A **Toolkit page** collects the most practical tools and standards for quick reference.

**Questions & Support:** sara@practical-accessibility.today

---

## Chapter 2 — What is Web Accessibility?

> "The power of the Web is in its universality. Access by everyone regardless of disability is an essential aspect." — Sir Tim Berners-Lee

### Definition
Web accessibility = **removing barriers to access** so that websites and applications can be used by people with disabilities.

### The Term "a11y"
- Numeronym: 11 letters between "a" and "y" in "accessibility".
- Pronounced "A-one-one-Y" or "A-eleven-Y".
- Best practice: spell out "Accessibility (a11y)" the first time.
- Font note: Course uses **Atkinson Hyperlegible Font** (free, by Braille Institute) for improved character recognition.

### Accessibility vs. Inclusive Design vs. Usability

| Concept | Focus |
|---|---|
| **Accessibility** | Equal access for people with disabilities |
| **Inclusive Design** | All people regardless of ability, language, culture, age, etc. |
| **Usability** | How effectively, efficiently, and satisfactorily users accomplish goals |

- Accessible design ⊂ Inclusive Design.
- Accessibility compliance ≠ usability. "Think of accessibility as the lowest bar." — Kate Kalcevich, Fable.
- **Captions** are a classic example of accessibility features benefiting everyone.

### Types of Disabilities
- **Visual**: blindness, low vision, cataracts, glaucoma
- **Hearing**: deafness, partial hearing loss
- **Mobility**: paralysis, amputation, muscular dystrophy, arthritis
- **Cognitive/Learning**: attention deficit, dyslexia, brain injury, memory loss

> Over 1 billion people worldwide live with some form of disability. 100% of the population will face some form of disability at some point.

### Assistive Technology (AT)
- Examples: screen readers, keyboards, braille displays, voice recognition, switch controls, screen magnifiers, dark mode, high-contrast modes.
- People may use **multiple ATs simultaneously**.
- Having AT doesn't guarantee access — accessible design and implementation is required.

### Testing with Disabled Users
- Simulating disabilities is not enough — testing with real disabled users is necessary.
- 70% of accessibility practitioners report having no disability (WebAIM 2021 survey).

### 📚 Key Resources
- [How People with Disabilities Use the Web — W3C](https://www.w3.org/WAI/people-use-web/)
- [Browsing with Assistive Technology video series — Tetralogical](https://tetralogical.com/blog/2021/12/24/browsing-with-assistive-technology-videos/)
- [Designing Safer Web Animation For Motion Sensitivity](https://alistapart.com/article/designing-safer-web-animation-for-motion-sensitivity/)
- [The Little Book of Accessibility](https://accessibility.me.uk/)

---

## Chapter 3 — The Web Content Accessibility Guidelines (WCAG)

### What is WCAG?
- **WCAG** = Web Content Accessibility Guidelines, developed by W3C's Web Accessibility Initiative (WAI).
- Defines how to make web content accessible to people with disabilities.
- Enables organizations to measure accessibility against documented success criteria.
- Covers design, content, and code.

### WCAG Versions
| Version | Published | Key Notes |
|---|---|---|
| **WCAG 1.0** | May 1999 | HTML-focused, 14 guidelines |
| **WCAG 2.0** | Dec 2008 | Introduced POUR principles, technology-agnostic |
| **WCAG 2.1** | June 2018 | Extends 2.0 (backwards-compatible); adds mobile, cognitive coverage |
| **WCAG 2.2** | Oct 2023 | Extends 2.1; fills known gaps |
| **WCAG 3 (Silver)** | In progress | Major overhaul; "W3C Accessibility Guidelines" — removes "Web" |

> Course reference: **WCAG 2.1** as primary standard; WCAG 2.2 mentioned where relevant.

### The Four Principles — P.O.U.R.
1. **Perceivable** — Information must be perceivable (can't be invisible to all senses)
2. **Operable** — UI controls must be operable (keyboard, mouse, voice, etc.)
3. **Understandable** — Content must be understandable
4. **Robust** — Must work with current and future user agents and AT

### Structure of WCAG 2.1
- **4 Principles** → **13 Guidelines** → **78 Success Criteria**
- Each SC is a testable, technical statement at one of three conformance levels.

#### Conformance Levels
| Level | Description |
|---|---|
| **A** | Minimum / critical (30 criteria). Not meeting this makes content impossible to access. |
| **AA** | Standard / essential (20 criteria). Required by most laws; legal safe bet. |
| **AAA** | Enhanced / highest (28 criteria). Not always achievable; W3C doesn't mandate across the board. |

> **Recommended default**: WCAG 2.1 Level AA — covers both desktop and mobile.

> WCAG is a **binary standard** — you either pass or you don't. "Partially supported is not supported."

### 📚 Key Resources
- [WCAG 2.1](https://www.w3.org/TR/WCAG21/)
- [How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG21/quickref/)
- [Understanding WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
- [WCAG 2.2 What's New (Video)](https://www.youtube.com/watch?v=IYLAFqiOKCI)
- [WCAG 3.0 (Silver) — Working Draft](https://www.w3.org/TR/wcag-3.0/)
- [Accessible contrast ratios and A-levels explained](https://www.accessibility-developer-guide.com/knowledge/colours-and-contrast/accessible-contrast-ratios/)

---

## Chapter 3.1 — Does WCAG Conformance Guarantee Usability?

**Short answer: No.**

### Why WCAG Alone Is Not Enough
1. **Conformance ≠ usability**: A site can pass all WCAG criteria and still be unusable.
2. **WCAG doesn't cover all accessibility issues**: Even Level AAA compliance won't reach all disabilities.
3. **WCAG doesn't address usability**: No requirements for expected keyboard interactions, persistent focus indicators, etc.
4. **AT/browser bugs**: WCAG doesn't mitigate against bugs in assistive technologies.

> "WCAG does not guarantee (or even remotely assure) something is accessible. Including users is the only way to get confidence a thing works." — Adrian Roselli

### WCAG as a Floor, Not a Ceiling
> "View WCAG not as an end goal, but as a floor." — Sheri Byrne-Haber

- Use WCAG as a **baseline**, not a checklist to tick and forget.
- Conduct **usability testing with disabled users** to uncover barriers not covered by WCAG.
- Inclusive design goes beyond compliance — consider diverse user needs proactively.

### Practical Example (GOV.UK)
GOV.UK's contact form offers communication method choices (text-only, voice-only, custom) — a technically WCAG-conformant form wouldn't offer these options, yet they dramatically improve accessibility for deaf, non-verbal, anxious, and autistic users.

---

## Chapter 3.2 — WCAG Supporting Documents

### Three Key Supporting Documents for WCAG 2.1

1. **Understanding WCAG 2.1** — Explains intent, benefits, examples, test cases, and technique links for each guideline and SC.

2. **Techniques for WCAG 2.1** — Collection of practical techniques (sufficient, advisory) and common failures, each with description, code examples, and tests.

3. **How to Meet WCAG (Quick Reference)** — Combined checklist with filters for roles, topics, technologies, and conformance levels. Links to Understanding pages and Techniques.

### Navigation Between Documents
- WCAG → Understanding pages → Techniques
- Quick Reference is the best starting point for day-to-day work.

### Normative vs. Non-Normative
- **Normative**: Must follow for conformance (the WCAG standard itself)
- **Non-normative (informative/advisory)**: Supporting docs — helpful but not required for conformance
- You may use **other techniques** not listed in the documents, as long as the SC is satisfied.

> Deep understanding of HTML/ARIA + testing is more reliable than just following technique checklists.

### 📚 Key Resources
- [How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG21/quickref/)
- [Understanding WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
- [Techniques for WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)

---

## Chapter 4 — Setting Up a Screen Reader Testing Environment

### Why Manual Testing Matters
- Automated checkers catch only **30–50%** of accessibility issues.
- Manual screen reader testing catches issues automated tools miss.

### Screen Reader Market (WebAIM Survey)
- 90%+ of screen reader users are on **Windows**
- Most popular: **JAWS** > **NVDA** > **VoiceOver**

### Key Screen Reader + Browser Pairings

| Screen Reader | Browser | Platform |
|---|---|---|
| **JAWS** | Chrome | Windows |
| **NVDA** | Firefox | Windows |
| **VoiceOver** | Safari | macOS/iOS |
| **Narrator** | Edge | Windows |
| **TalkBack** | Chrome | Android |

### Setting Up NVDA (Windows/Mac via VM)
1. Download from [NVAccess](https://www.nvaccess.org/download/)
2. Enable **Visual Highlight**: NVDA > Preferences > Settings > Vision
3. Enable **Speech Viewer**: NVDA > Tools > Speech Viewer
4. Mac: Set **Laptop keyboard layout** in NVDA preferences

### macOS Setup
- Enable keyboard navigation: System Preferences > Keyboard > "Use keyboard navigation to move focus between controls"
- Enable tabbing in Safari: Preferences > Advanced > "Press tab to highlight each item"
- Map Insert key using **[Karabiner Elements](https://karabiner-elements.pqrs.org/)** (free)

### Virtual Testing (no Windows machine needed)
- **[Assistiv Labs](https://assistivlabs.com/)** — Remote screen reader testing in the browser (NVDA, JAWS, WHCM). Free 6-month trial available through course link.

### Screen Reader Cheat Sheets (Deque University)
- [Desktop Screen Readers Survival Guide](https://dequeuniversity.com/screenreaders/survival-guide)
- [NVDA keyboard shortcuts](https://dequeuniversity.com/screenreaders/nvda-keyboard-shortcuts)
- [JAWS keyboard shortcuts](https://dequeuniversity.com/screenreaders/jaws-keyboard-shortcuts)
- [VoiceOver keyboard shortcuts](https://dequeuniversity.com/screenreaders/voiceover-keyboard-shortcuts)

### 📚 Key Resources
- [WebAIM Screen Reader User Survey](https://webaim.org/projects/screenreadersurvey9/)
- [Browsing with a desktop screen reader — Tetralogical](https://tetralogical.com/blog/2021/12/24/browsing-with-assistive-technology-videos/)
- [Relevant combinations of screen readers and browsers](https://www.powermapper.com/tests/screen-readers/aria/)

---

## Chapter 5 — What is the Accessibility Tree?

### From HTML → DOM → Accessibility Tree
1. Browser parses HTML → creates **DOM tree**
2. DOM tree + CSS → visual UI for sighted users
3. In parallel, browser generates **accessibility tree** for AT

### The Accessibility Tree
- A subset of the DOM: only elements relevant to accessibility are included.
- `<div>`s and `<span>`s (generic elements) are often **not** included by default.
- Used by screen readers, braille displays, and other AT.

### Four Core Properties in the Accessibility Tree
| Property | Description |
|---|---|
| **Role** | What kind of thing is it? (button, link, heading, etc.) |
| **Name** | How can we refer to it? (accessible name) |
| **Description** | Additional info about the element |
| **State** | Current state (expanded/collapsed, checked/unchecked, etc.) |

Also includes: **properties** (focusable, required) and **relationships** (labelled by, described by, owned by).

### What Determines Accessibility Tree Content
- **HTML semantics** (implicit roles via ARIA API mappings)
- **CSS styles** (e.g., `display: none` removes from tree)
- **ARIA attributes** (can add, modify, or remove semantics)

### How to Inspect the Accessibility Tree
- **Chrome/Edge DevTools** → Accessibility panel (recommended)
- Reveals: role, name, description, state, focusable status

### Platform Accessibility APIs
| OS | Accessibility API |
|---|---|
| Windows | MSAA/Accessible2 & UI Automation |
| macOS | NSAccessibility |
| Linux | ATK & AT-SPI |
| iOS | UIAccessibility |
| Android | Accessibility framework |

> Different AAPIs can produce slightly different accessibility trees. This is normal — don't try to "fix" it.

### Key Concept: HTML Accessibility API Mappings
- [HTML Accessibility API Mappings (HTML-AAM)](https://www.w3.org/TR/html-aam-1.0/) — full list
- [ARIA in HTML](https://www.w3.org/TR/html-aria/) — developer-friendly reference

### 📚 Key Resources
- [Semantics to Screen Readers](https://alistapart.com/article/semantics-to-screen-readers/)
- [Accessibility APIs: A key to Web accessibility](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)

---

## Chapter 6 — Semantic HTML Accessibility

### What is Semantic HTML?
- HTML is descriptive: every element describes what it represents.
- "Use semantic HTML" = use the right element for its correct purpose.
- **114 semantic elements** in HTML — all have meaning.

### Why Semantic HTML Matters
- Universal language for all devices and AT.
- Provides accessibility information (roles, states, properties) via implicit ARIA mappings.
- Provides built-in keyboard interactions for interactive elements.
- Benefits SEO, reader modes, forced color modes.

### Key Nuances

#### 1. Not All Elements Have Equivalent ARIA Roles
- `<picture>` has no role mapping — "not interesting for accessibility".
- The `<img>` inside `<picture>` is what matters for accessibility.

#### 2. Not All Elements Have Unique Roles
- `<ol>` and `<ul>` both map to the `list` role.
- Still use the correct one for semantic clarity.

#### 3. `<div>` and `<span>` ARE Semantic — They're Generic Containers
- They map to the `generic` role.
- OK to use for layout, **not** for meaningful content that needs a semantic element.

#### 4. Some Elements Are Only Exposed Contextually
- `<a>` without `href` → generic role (not a link!)
- `<section>` → generic unless given an accessible name (then → `region` landmark)
- `<aside>` → generic in some contexts unless named

#### 5. Not All Roles Are Exposed by Default
- `<strong>`, `<em>` etc. → text-level semantics may not be announced unless user adjusts verbosity.

### CSS Can Break HTML Semantics
- `display: flex` on `<table>` used to remove table semantics (now fixed in most browsers; test anyway).
- `list-style: none` on `<ul>` removes list semantics in some Safari versions.
  - **Fix**: Add `role="list"` explicitly, or use `list-style-type: ""` (empty string) to preserve semantics.
- `<section>` needs an accessible name to be exposed as a landmark.

### ARIA Can Modify HTML Semantics
- `aria-pressed` on `<button>` → may expose it as a "toggle button".
- ARIA can override, supplement, or suppress native semantics.

### Checklist: Choosing the Right Element
- Does it map to a meaningful ARIA role?
- Does it have built-in keyboard behavior?
- Does it need an accessible name?
- Are CSS styles inadvertently affecting its semantics?

### 📚 Key Resources
- [The Practical Value of Semantic HTML](https://www.brucelawson.co.uk/2018/the-practical-value-of-semantic-html/)
- [Tables, CSS Display Properties, and ARIA — Adrian Roselli](https://adrianroselli.com/2018/02/tables-css-display-properties-and-aria.html)
- [Voiceover and list-style-type: none](https://www.scottohara.me/blog/2019/01/12/lists-and-safari.html)
- [Use the dialog element (reasonably)](https://www.scottohara.me/blog/2019/03/05/dialog-uses.html)

---

## Chapter 6.1 — Heading Structure

### Why Headings Matter for AT Users
- Screen readers read pages linearly by default, but users rely on **heading shortcuts** to jump to sections.
- **85.7%** of screen reader users find heading levels very/somewhat useful (WebAIM survey).
- Proper headings are required for WCAG SC 1.3.1, 2.4.6, and 2.4.10.

### Rules for Headings

#### One `<h1>` per page
- Describes the page's primary topic.
- Should be the first child of `<main>`.
- Should match or closely match the page `<title>`.

#### The Document Outline Algorithm Does NOT Exist
- Was never implemented in any browser. It never will be.
- Using multiple `<h1>` tags inside `<section>` elements does NOT create nested outlines.
- **Always use the correct heading level** that reflects actual content hierarchy.

#### Use `<h2>`–`<h6>` to Create Hierarchy
- `<h2>` → major page sections
- `<h3>` → subsections of `<h2>`, etc.
- **Do not skip heading levels.**
- **Do not use headings for styling only.** (CSS violation of SC 1.3.1)
- **If it looks like a heading, it must be a heading.**

#### Sub-headings / Taglines
- Use `<hgroup>` with one `<h*>` + `<p>` for subheadings.
- Do not put multiple headings inside `<hgroup>`.

### WCAG Success Criteria for Headings
- **SC 1.3.1** (Level A) — Visual headings must be semantically marked up as headings.
- **SC 2.4.6** (Level AA) — Headings must be descriptive.
- **SC 2.4.10** (Level AAA) — Section headings required for content divided into sections.

### Fixing Broken Headings with ARIA
```html
<div class="h2" role="heading" aria-level="2">This is a heading</div>
<!-- Semantically equivalent to: -->
<h2>This is a heading</h2>
```

### Tools for Visualizing Heading Structure
- **[h123 bookmarklet](https://hinderlingvolk.com/h123/)** — Quick heading outline overlay
- **[Web Developer Toolbar Chrome Extension](https://chrispederick.com/work/web-developer/)** — Full page outline in separate page
- **[W3C Markup Validation Service](https://validator.w3.org/)** — Check "Show outline" option

### 📚 Key Resources
- [Accessible heading structure](https://www.a11yproject.com/posts/how-to-accessible-heading-structure/)
- [There is no document outline algorithm](https://adrianroselli.com/2016/08/there-is-no-document-outline-algorithm.html)
- [Heading off confusion: When do headings fail WCAG?](https://www.tpgi.com/heading-off-confusion-when-do-headings-fail-wcag/)

---

## Chapter 6.2 — Landmark Regions

### What Are Landmarks?
- Key navigable areas of a page, similar to physical landmarks.
- Help screen reader users **orient themselves** and **navigate efficiently**.
- 25%+ of screen reader users navigate by landmarks regularly (WebAIM survey).

### Eight Landmark Types and Their HTML Elements

| ARIA Role | HTML Element | Notes |
|---|---|---|
| `banner` | `<header>` | Only when direct child of `<body>` |
| `navigation` | `<nav>` | Each should have a unique label |
| `main` | `<main>` | Only one per page |
| `contentinfo` | `<footer>` | Only when direct child of `<body>` |
| `complementary` | `<aside>` | Sidebar/related content |
| `form` | `<form>` | Only exposed as landmark when named |
| `search` | `<search>` | New native HTML element |
| `region` | `<section>` + name | Only exposed when given accessible name |

### Labelling Multiple Landmarks of the Same Type
```html
<nav aria-label="Site"><!-- main nav --></nav>
<nav aria-label="Breadcrumbs"><!-- breadcrumbs --></nav>

<!-- Or reference a heading: -->
<nav aria-labelledby="categories_label">
  <h2 id="categories_label">Categories</h2>
</nav>
```

### The Search Landmark (`<search>`)
```html
<search>
  <form action="search.php">
    <label for="query">Find an article</label>
    <input id="query" name="q" type="search">
    <button type="submit">Go!</button>
  </form>
</search>
```

### Custom Region Landmark
```html
<section aria-labelledby="editor_label">
  <h2 id="editor_label">Editor</h2>
  <!-- content -->
</section>
```

### Best Practices
- Use **as few landmarks as possible** — too many reduce efficiency.
- All page content should be within a landmark.
- Use headings within landmarks for fine-grained navigation.
- Don't include the word "navigation" in a `<nav>` label (creates duplicate announcement).

### Tools
- **[WAVE browser extension](https://wave.webaim.org/extension/)** — Visualizes landmark regions in context.
- **[ARIA Landmarks Example — W3C](https://www.w3.org/TR/wai-aria-practices/examples/landmarks/HTML5.html)**

### 📚 Key Resources
- [Accessible Landmarks](https://www.scottohara.me/blog/2018/03/03/landmarks.html)
- [The search element](https://www.scottohara.me/blog/2023/03/24/search-element.html)
- [Foundations: landmarks](https://tetralogical.com/blog/2022/06/08/landmarks/)

---

## Chapter 6.3 — Buttons vs. Links

### The Core Difference
- **Buttons** → trigger actions on the page (open dialog, submit form, toggle UI)
- **Links** → navigate to another place (different page, section within page, file, email)

### Buttons
- Implicit `button` role
- Focusable by default (no `tabindex` needed)
- Keyboard: **Space** and **Enter**
- Can be disabled with `disabled` attribute
- Do nothing without JavaScript (unless inside a form)

### Links
- Require `href` attribute to be a link (`<a>` without `href` = generic role, not focusable)
- Keyboard: **Enter** only
- Can be right-clicked, opened in new tab
- Work **without JavaScript**
- Can be "disabled" by removing `href` + using `role="link"` + `aria-disabled="true"`

### How to Choose
Ask yourself:
1. Does it navigate to another page/section? → **Link**
2. Does it trigger an action on the current page? → **Button**
3. Does it work without JavaScript? → likely **Link**
4. Can you right-click it to open in new window? → **Link**

### Enhancing a Link into a Button (progressive enhancement)
```html
<a href="#" role="button">Do something</a>
```
Must also:
1. Override link semantics with `role="button"`
2. Prevent default link behavior with JavaScript
3. Handle both `keydown` (Enter → fires immediately) and `keyup` (Space → fires on release)

### 📚 Key Resources
- [When going somewhere does a thing: on links and buttons](https://www.sarasoueidan.com/blog/on-buttons-and-links/)
- [A complete guide to links and buttons](https://css-tricks.com/a-complete-guide-to-links-and-buttons/)
- [Disabling a link](https://www.scottohara.me/blog/2021/05/28/disabled-links.html)

---

## Chapter 6.4 — Practical Semantics: Site-Wide Navigation

### Building an Accessible Navigation Component

**Step 1: Use `<nav>`** → exposes navigation landmark
```html
<nav aria-label="Site">
  <ul>
    <li><a href="/products/">Products</a></li>
    <li><a href="/team/">Team</a></li>
    <li><a href="/press/">Press</a></li>
  </ul>
</nav>
```

**Step 2: Use `<ul>` for grouping links** → announces count of items and position to screen readers.

**Step 3: Label multiple navigations uniquely** with `aria-label` or `aria-labelledby`.

**Step 4: Convey current page state** with `aria-current="page"`:
```html
<a href="/products/" aria-current="page">Products</a>
```

**CSS Hook — style using ARIA state:**
```css
a[aria-current="page"] { /* current link styles */ }
```

**Preserve list semantics in Safari:**
```html
<ul role="list">...</ul>
```
Or: use `list-style-type: ""` instead of `list-style: none`.

### Key Semantic Info to Convey
- **Role**: What it is (navigation)
- **Name**: What it's called (Site, Breadcrumbs, etc.)
- **State**: Which item is current (`aria-current="page"`)

---

## Chapter 7 — ARIA 101

### What is WAI-ARIA?
- **Accessible Rich Internet Applications** — a W3C standard that extends HTML semantics.
- Provides roles, states, and properties to make dynamic content and custom widgets accessible.
- **Does not replace HTML. Does not add behavior.**

### ARIA is Like CSS for Assistive Technologies
- CSS = visual presentation layer
- ARIA = "semantic affordance" layer for screen readers

### Three Types of ARIA Attributes

| Type | Prefix | Purpose |
|---|---|---|
| **Roles** | `role=""` | Describe what an element is |
| **States** | `aria-*` | Express current state (dynamic, JS-managed) |
| **Properties** | `aria-*` | Describe properties (name, description, relationships) |

#### Common State Attributes
- `aria-expanded` — expanded/collapsed
- `aria-pressed` — toggle button state (true/false)
- `aria-current` — current item in a set (e.g., `aria-current="page"`)
- `aria-hidden` — hide from accessibility tree

#### Common Property Attributes
- `aria-label` — provides an accessible name (string)
- `aria-labelledby` — references another element as the name
- `aria-describedby` — references another element as description
- `aria-controls` — identifies the element(s) controlled

### Types of ARIA Roles
1. **Abstract** — Don't use directly (internal building blocks)
2. **Landmark** — Page regions (banner, main, navigation, etc.)
3. **Document structure** — Headings, lists, articles, images, etc.
4. **Widget** — Interactive components (tabs, switch, menu, dialog, etc.)
5. **Live region** — Dynamic update regions
6. **Window** — Modal dialogs, etc.

### What ARIA Does NOT Do
- Does **not** add behavior or interactivity
- Does **not** affect the DOM
- Does **not** make elements focusable
- Does **not** affect styling
- Does **not** impact all AT (e.g., Forced Colors modes read from HTML, not ARIA)

> "ARIA is a promise. If you use role='button', you must implement button behavior."

### Strict Rules About ARIA
- Not all roles are valid on all elements (check [ARIA in HTML spec](https://www.w3.org/TR/html-aria/))
- Some roles have required parent-child relationships (e.g., `tab` must be inside `tablist`)
- You cannot invent custom role values
- Some roles suppress children's semantics (e.g., `role="button"` suppresses children)

### JavaScript is Required for Interactive ARIA
- States like `aria-expanded` must be updated dynamically via JS.
- Interactive roles (button, tab, checkbox, etc.) need JS keyboard handling.
- Use **progressive enhancement**: add ARIA attributes from JS, not hard-coded.

### ARIA Support
- Varies across browsers, screen readers, and platforms.
- Reference: **[a11ysupport.io](https://a11ysupport.io/)** — but always test yourself.

### 📚 Key Resources
- [Demystifying WAI-ARIA](https://alistapart.com/article/aria-and-progressive-enhancement/)
- [ARIA is spackle not rebar — Eric Bailey](https://css-tricks.com/aria-spackle-not-rebar/)
- [Quick Note on ARIA and Windows High Contrast Mode](https://www.scottohara.me/blog/2019/03/14/aria-high-contrast.html)

---

## Chapter 7.1 — Applied ARIA: Creating a Custom Button

### Custom Button Checklist
When building a custom control with `role="button"`:

1. **Semantics**: `role="button"` on the element
2. **Focusability**: `tabindex="0"` to add to tab order
3. **Keyboard — Enter**: fires `keydown` event
4. **Keyboard — Space**: fires `keyup` event (not keydown!)
5. **Disabled state**: `aria-disabled="true"` + visual styles
6. **Focus indicator**: visible `:focus-visible` styles
7. **Touch accessibility**: test with mobile screen readers
8. **Forced Colors**: ensure visible in Windows High Contrast Mode

```html
<div class="btn" role="button" tabindex="0" aria-disabled="false">Do something</div>
```

```javascript
// Match native button keyboard behavior exactly:
btn.addEventListener("keydown", (e) => {
  if (e.keyCode === 13) doSomething(); // Enter: fires on keydown
});
btn.addEventListener("keyup", (e) => {
  if (e.keyCode === 32) doSomething(); // Space: fires on keyup
});
```

> **Tip**: Use `all: unset` on a native `<button>` to strip default browser styles — much easier than building from scratch with `<div>`.

### Custom Control Accessible Development Checklist (W3C Using ARIA)
- ✅ Focusable
- ✅ Keyboard operable (expected keys)
- ✅ Touch operable
- ✅ Expected key behavior (matches native)
- ✅ Visible focus indicator
- ✅ Accessible name (label)
- ✅ Correct role
- ✅ States and properties exposed
- ✅ Sufficient color contrast
- ✅ Works in High Contrast Mode

### 📚 Key Resources
- [Brief Note on Buttons, Enter, and Space — Adrian Roselli](https://adrianroselli.com/2022/02/brief-note-on-buttons-enter-and-space.html)

---

## Chapter 7.2 — The Five Rules of ARIA Use

> 2022 WebAIM Million: Home pages with ARIA had **70% more detected errors** than those without.

### Rule 1: Prefer Native HTML
> "If you can use a native HTML element with the semantics and behavior you require already built in, do so."

```html
<!-- ✅ Do this: -->
<button>Click me</button>
<!-- ❌ Not this: -->
<div role="button">Click me</div>
```

**Exceptions:** Feature not yet in HTML, native can't be styled as needed, or accessibility support is broken.

### Rule 2: Don't Change Native Semantics (Unless You Have To)
```html
<!-- ❌ Don't: -->
<h2 role="tab">Tab panel title</h2>
<!-- ✅ Do: -->
<div role="tab"><h2>Tab panel title</h2></div>
```

Use ARIA on wrapper elements, not on the meaningful semantic elements.

### Rule 3: All Interactive ARIA Controls Must Be Keyboard Operable
- Required by **SC 2.1.1 Keyboard (Level A)**.
- If a user can click/tap, they must also be able to do it with a keyboard.

### Rule 4: Don't Use `role="presentation"` or `aria-hidden` on Focusable Elements
- This causes users to focus on "nothing" — keyboard focus lands on element but screen reader won't announce it.
```html
<!-- ❌ Never do this: -->
<button aria-hidden="true">Do something</button>
```

### Rule 5: All Interactive Elements Must Have an Accessible Name
- Form inputs, buttons, links, custom controls — all must have names.
- Use `<label>` for form controls, `aria-label`/`aria-labelledby` as fallback.

### Additional Guidance

**Redundant ARIA** (avoid):
```html
<!-- Redundant — button already has implicit button role -->
<button role="button">press me</button>
<!-- Redundant — input already has required semantics -->
<input type="text" required aria-required="true">
```

**No ARIA > Bad ARIA**: Incorrect ARIA misrepresents the interface and can create severe barriers.

### 📚 Key Resources
- [Using ARIA — W3C](https://www.w3.org/TR/using-aria/)

---

## Chapter 7.3 — The ARIA Authoring Practices Guide (APG)

### What is the APG?
- A W3C guide (not a standard) demonstrating how to use ARIA for custom UI components.
- Contains 29 patterns with: ARIA attributes used, expected keyboard interactions, markup, CSS/JS links, live demos.

### What the APG Is NOT
- **Not** a specification — it's non-normative.
- **Not** production-ready for all patterns.
- **Not** a copy-paste cookbook.

> "Note: Testing assistive technology interoperability is essential before using code from this guide in production."

### How to Use the APG Responsibly
1. Use as a **starting point**, not a final answer.
2. Always perform your own testing.
3. Modify patterns to fit your specific context.
4. Check heading levels in patterns against page structure.
5. Prefer simpler, native HTML solutions when available.

### Recommended Workflow for Custom Widgets
1. Reach for HTML elements whenever possible
2. Simplify interaction patterns
3. Know your ARIA attributes
4. Consult APG for custom widgets
5. Research other community implementations
6. Test across ATs and with AT users

### 📚 Key Resources
- [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/)
- [The ARIA Authoring Practices Guide Can Lead You Astray](https://adrianroselli.com/2023/09/aria-guide.html)

---

## Chapter 8 — Disclosure Widgets

### What is a Disclosure Widget?
- A control (usually a button) that **reveals and hides content**.
- Used as a building block in: accordions, dropdown navigations, off-canvas menus, dialogs.

### Option 1: Native HTML `<details>` & `<summary>`

```html
<details>
  <summary>Trigger label</summary>
  <p>Hidden content revealed when trigger is activated.</p>
</details>

<!-- Initially open: -->
<details open>
  <summary>Trigger label</summary>
  <p>Content visible by default.</p>
</details>
```

**Built-in features:**
- `<summary>` is keyboard operable (Space + Enter)
- Browser toggles `open` attribute automatically
- Content is found by browser's **Find in Page** (auto-expands on match)
- Announced differently across screen readers (button / disclosure triangle / summary) — this is normal

**Limitations:**
- Announcement is inconsistent across AT combinations
- Find-in-page auto-expand may be unwanted for some patterns (dialogs, tabs, etc.)
- Not suitable for patterns needing specific semantics (e.g., Tabs, Menus)

### Option 2: Custom ARIA Disclosure Widget

```html
<div class="disclosure-widget">
  <button aria-expanded="false" aria-controls="panel_id">Trigger label</button>
  <div id="panel_id" hidden>
    <!-- content -->
  </div>
</div>
```

**JavaScript (update state on click):**
```javascript
trigger.addEventListener("click", function() {
  const expanded = this.getAttribute("aria-expanded") === "true";
  this.setAttribute("aria-expanded", String(!expanded));
  panel.toggleAttribute("hidden");
});
```

**CSS hook (optional — hide panel via CSS using ARIA state):**
```css
.disclosure-widget > button[aria-expanded="false"] + div {
  display: none;
}
```

### Progressive Enhancement Pattern (Best Practice)
Start with content visible (no button); add button via JavaScript:
```html
<!-- Initial HTML (no JS): content is accessible -->
<div class="disclosure-widget">
  <div class="panel">Content always accessible without JS.</div>
</div>
```
JS creates and prepends the `<button>`, hides content, manages `aria-expanded`.

> **Why?** JavaScript can fail. Content should always be accessible by default.

### `aria-controls` Note
- Optional; only supported well by JAWS.
- Always place the content panel **immediately after** its trigger in DOM regardless.

### 📚 Key Resources
- [Disclosure Widgets — Adrian Roselli](https://adrianroselli.com/2020/05/disclosure-widgets.html)
- [Details / Summary Are Not [insert control here]](https://adrianroselli.com/2020/05/details-summary-are-not-insert-control-here.html)
- [Everyone has JavaScript, right?](https://kryogenix.

org/2013/03/everyone-has-javascript-right/)
- [Using the aria-controls attribute](https://www.heydonworks.com/article/aria-controls-is-poop)

---

## Chapter 9.1 — Building an Accordion (Part 1): Native HTML

### What is an Accordion?
- A **group of collapsible, related sections of content**.
- Often used to save vertical space by hiding content until needed.
- **Exclusive accordion**: only one section open at a time.
- An accordion = a grouping of disclosure widgets.

### Requirements for Accessible Accordions
1. Create a series of accessible disclosure widgets
2. Semantically group them (expose the relationship to AT)
3. Give the group a name (communicate purpose)
4. If exclusive: implement group behavior (open one → close others)

### Grouping Options

**As a Named Group** (not in page outline):
```html
<div role="group" aria-labelledby="group-label">
  <span id="group-label" hidden>Product Description</span>
  <details name="accordion">...</details>
  <details name="accordion">...</details>
</div>
```

**As a Landmark Region** (appears in page outline):
```html
<section aria-labelledby="group-label">
  <h2 id="group-label">About this product</h2>
  <details name="accordion">...</details>
  <details name="accordion">...</details>
</section>
```

> Prefer `hidden` over `visually-hidden` for the label to avoid duplicate announcements.

### Exclusive Accordion: HTML `name` Attribute
```html
<details name="faq">
  <summary>Question 1</summary>
  <p>Answer 1</p>
</details>
<details name="faq">
  <summary>Question 2</summary>
  <p>Answer 2</p>
</details>
```
- Same `name` value on all `<details>` → browser enforces only one open at a time.
- No JavaScript needed for basic exclusive behavior.
- Browser limits: can't have bulk expand/collapse, or prevent zero-open state without JS.

### Usability Considerations for Exclusive Accordions
Per Eric Eggert's "Exclusive Accordions Exclude":
- Higher cognitive load (can't compare two sections simultaneously)
- More keystrokes for keyboard users
- Screen readers lose heading navigation when sections are closed
- Low-vision users lose orientation when content shifts
- Dragon users have difficulty with `<details>`

> HTML spec warning: "Before using this feature, authors should consider whether this grouping is helpful or harmful to users."

### 📚 Key Resources
- [Accordions on Desktop: When and How to Use](https://www.nngroup.com/articles/accordions-complex-content/)
- [Exclusive accordions exclude — Eric Eggert](https://yatil.net/blog/exclusive-accordions-exclude)
- [Designing for progressive disclosure — Steven Hoober](https://www.uxmatters.com/mt/archives/2017/09/designing-for-progressive-disclosure.php)

---

## Chapter 9.2 — Building an Accordion (Part 2): ARIA + JavaScript

### When to Use ARIA Accordion Instead of Native HTML
- When you need headings inside accordion triggers (to preserve heading semantics)
- When you need bulk expand/collapse functionality
- When you need exact-exclusive behavior (always exactly one open)
- When AT support for `<details>` is inconsistent for your use case

### Accordion with Headings (Correct Pattern)
```html
<section aria-labelledby="region_label">
  <h2 id="region_label">FAQ</h2>

  <div class="disclosure-widget">
    <h3>
      <button aria-expanded="false" aria-controls="panel1">Question 1?</button>
    </h3>
    <div id="panel1" hidden>
      Answer 1 content.
    </div>
  </div>

  <div class="disclosure-widget">
    <h3>
      <button aria-expanded="false" aria-controls="panel2">Question 2?</button>
    </h3>
    <div id="panel2" hidden>
      Answer 2 content.
    </div>
  </div>
</section>
```

**Key**: Put `<button>` **inside** the `<h3>` (not the other way around) to preserve heading semantics.

### Making Accordion Content Searchable with `hidden="until-found"`
```javascript
panel.setAttribute("hidden", "until-found"); // instead of plain "hidden"
```
- Browser expands the section when find-in-page matches content inside.
- Only supported in Chromium browsers (as of chapter creation; 2025 Interop project).
- **Caveat**: Once revealed, it stays expanded (no native way to re-hide after search).
- **Watch out**: CSS `[hidden] { display: none !important; }` will break this. Fix:
```css
[hidden]:not(:is([hidden="until-found"])) {
  display: none !important;
}
```

### Progressive Enhancement Pattern
- Start with all sections **expanded** (accessible without JS)
- JS creates buttons, hides panels, manages `aria-expanded`
- If JS fails, content remains accessible

### 📚 Key Resources
- [Making collapsed content accessible with hidden=until-found](https://developer.chrome.com/articles/hidden-until-found/)
- [More Progressively enhanced ARIA accordions](https://www.scottohara.me/blog/2023/09/12/progressively-enhanced-accordion.html)

---

## Chapter 10 — Hiding Content: HTML, CSS, and ARIA

### The Core Question
**Who are you hiding from? Who should still have access?**

### CSS Hiding Techniques

| Technique | Visually Hidden | Layout Space | Accessibility Tree | Keyboard Accessible |
|---|---|---|---|---|
| `opacity: 0` | ✅ | Takes space | ✅ Included | ✅ Yes |
| `clip-path: inset(100%)` | ✅ | Takes space | ✅ Included | ✅ Yes |
| `position: absolute` + off-screen | ✅ | No space | ✅ Included | ✅ Yes (⚠️ if interactive, must be visible) |
| `visibility: hidden` | ✅ | Takes space | ❌ Excluded | ❌ No |
| `display: none` | ✅ | No space | ❌ Excluded | ❌ No |

### HTML Hiding Techniques

| Technique | Visually Hidden | Accessibility Tree | Keyboard |
|---|---|---|---|
| `hidden` attribute | ✅ | ❌ Excluded | ❌ No |
| `disabled` attribute | ❌ Visible | ✅ Included (disabled state shown) | ❌ Not focusable |
| `inert` attribute | ❌ Visible | ❌ Excluded | ❌ No |
| `tabindex="-1"` | ❌ Visible | ✅ Included | ❌ Not tab-focusable |

### ARIA Hiding Techniques

| Technique | Semantics | Children | Focusable Elements |
|---|---|---|---|
| `aria-hidden="true"` | Hides element + all children | Also hidden | ⚠️ Still focusable (dangerous!) |
| `role="none"` / `role="presentation"` | Suppresses element semantics only | Mostly preserved (unless required children) | Still exposed if focusable |

> **Never use `aria-hidden` on focusable elements** — keyboard focus will land on an invisible element.

### The Visually-Hidden Utility Class
```css
.visually-hidden:not(:focus):not(:active) {
  width: 1px;
  height: 1px;
  overflow: hidden;
  clip: rect(0 0 0 0); /* IE */
  clip-path: inset(50%);
  position: absolute;
  white-space: nowrap;
}
```
- Hides text **visually** while keeping it **screen-reader accessible**.
- Use for static supplementary text only — **not** for interactive elements.
- The `:not(:focus):not(:active)` ensures interactive elements become visible when focused.

### Exposing Hidden Text via ARIA Reference
```html
<!-- Hidden text used ONLY as an accessible name -->
<span id="btn-label" hidden>Menu</span>
<button aria-labelledby="btn-label">
  <!-- icon here -->
</button>
```
When `hidden` content is referenced by `aria-labelledby`, the browser exposes it as an accessible name (even though it's hidden).

### Key Decision Framework
1. **Hide from everyone**: `display: none`, `hidden`, `visibility: hidden`
2. **Hide visually, keep for AT**: `.visually-hidden` class
3. **Hide from AT, keep visible**: `aria-hidden="true"` (only on non-interactive elements)
4. **Hide interactive + non-interactive from everything**: `inert`
5. **Remove from tab order only**: `tabindex="-1"`

### 📚 Key Resources
- [Inclusively Hidden — Scott O'Hara](https://www.scottohara.me/blog/2017/04/14/inclusively-hidden.html)
- [Know your ARIA: hidden vs none](https://www.scottohara.me/blog/2018/05/05/hidden-vs-none.html)
- [inert explainer](https://github.com/WICG/inert)

---

## Chapter 10.1 — Case Study: Inclusively Hidden Custom Form Controls

### The Problem
When creating custom-styled checkboxes/radio buttons by hiding the native control and showing an SVG:
- `visually-hidden` class and off-canvas positioning = **breaks mobile screen reader touch navigation**
- Touch screen reader users (TalkBack, VoiceOver iOS) explore by literally dragging their finger — they expect to "touch" the control where it visually is.

### The Correct Technique: Opacity + Overlay
```css
.c-custom-checkbox {
  position: relative; /* positioning context */
}

.c-custom-checkbox input[type="checkbox"] {
  position: absolute;  /* remove from flow */
  width: 1em;
  height: 1em;
  opacity: 0;          /* invisible, but present */
  z-index: 1;          /* ensure it overlaps the SVG */
}
```

**Why this works:**
- Checkbox remains at its natural position on the page
- Touch screen users can find and interact with it
- Screen readers can access it
- Visually replaced by the SVG

### Styling the SVG to Match Native States
```css
/* Focus */
input:focus-visible + svg { outline: 2px solid deeppink; }

/* Checked */
input:checked + svg .checkbox__checkmark { stroke: currentColor; }

/* Disabled */
input:disabled + svg { /* disabled styles */ }
```

### Forced Colors Support
```css
@media screen and (forced-colors: active) {
  svg .checkbox__background { /* forced color styles */ }
}
```

### 📚 Key Resources
- [One last time: custom styling radio buttons and checkboxes](https://www.sarasoueidan.com/blog/inclusively-hidden-controls/)
- [Assistive Tech: TalkBack (Video)](https://tetralogical.com/blog/2021/12/24/browsing-with-assistive-technology-videos/)

---

## Chapter 11 — Accessible Names and Descriptions

### What is an Accessible Name (accName)?
- A string of text programmatically associated with an element, exposed via the accessibility tree.
- Used to identify and label UI elements to AT users.
- **Different from a visual label**: a label may be visually present but not programmatically associated.

### Label vs. Name
- A **visible label** is what sighted users see.
- An **accessible name** is what AT users hear/read.
- They should ideally be identical (required by SC 2.5.3 Label in Name).

```html
<!-- Has visual label but NO accessible name: -->
<span>Username</span>
<input type="text">

<!-- Has visual label AND accessible name: -->
<label for="username">Username</label>
<input type="text" id="username">
```

### Which Elements Need an Accessible Name?
- **Must have**: All interactive elements — buttons, links, inputs, custom widgets
- **Benefit from**: Landmark regions (when multiple of same type), tables, dialogs, form groups
- **Not allowed to have**: `<div>`, `<span>`, `<p>`, `<em>`, `<strong>`, `<mark>`, `<time>`, and other "Name prohibited" role elements

```html
<!-- ❌ Invalid — generic elements can't have accessible names -->
<div aria-label="some name">...</div>
<span aria-label="Twitter">icon</span>
```

### Inspecting accNames in DevTools
- Chrome/Edge DevTools → Accessibility panel
- Shows: name, description, role, and what technique provided the name

### Accessible Descriptions (accDesc)
- Supplementary, longer text that provides additional context (hints, requirements, errors).
- Associated using `aria-describedby`:
```html
<label for="pw">Password</label>
<input type="password" id="pw" aria-describedby="pw-hint">
<p id="pw-hint">At least 8 characters with one special character.</p>
```
- **Difference from name**: Descriptions are optional, announced after name + role, may be skipped by some AT.
- `aria-describedby` content is **flattened to plain text** (structure/links lost).

### WebAIM 2022 Million Survey Stats
- 50.1% of home pages had **empty links**
- 27.2% had **empty buttons**
- 46.1% had **missing form labels**

### 📚 Key Resources
- [What is an accessible name](https://www.tpgi.com/what-is-an-accessible-name/)
- [Accessible Description Exposure](https://www.scottohara.me/blog/2019/10/17/accessible-descriptions.html)
- [Naming things to improve accessibility](https://hidde.blog/naming-things-to-improve-accessibility/)

---

## Chapter 11.1 — Techniques for Accessible Names & Descriptions

### Priority Order (highest to lowest precedence)
1. `aria-labelledby`
2. `aria-label`
3. Native HTML naming mechanism (e.g., `<label>`, `alt`, `<legend>`, `<title>`)
4. `title` attribute (avoid — many issues)
5. `placeholder` (avoid — inaccessible)

### Technique 1: `<label>` (Best for Form Controls)
```html
<label for="email">Email address</label>
<input type="email" id="email">
```
- Most robust, widely supported.
- Clicking label focuses the input.
- Only works on **labelable elements** (`<input>`, `<button>`, `<select>`, `<textarea>`, `<meter>`, `<progress>`, `<output>`).

### Technique 2: `aria-labelledby` (Reference Existing Element)
```html
<span id="nav-label">Site navigation</span>
<nav aria-labelledby="nav-label">...</nav>
```
- Concatenates text from multiple elements:
```html
<button aria-labelledby="action item-name">
  <span id="action">Add</span>
  <span id="item-name">MacBook Pro</span>
</button>
<!-- Announced as: "Add MacBook Pro, button" -->
```
- Can reference hidden elements (referenced in `aria-labelledby` overrides `hidden`).

### Technique 3: `aria-label` (Invisible String Label)
```html
<button aria-label="Close dialog">×</button>
<nav aria-label="Breadcrumbs">...</nav>
```
- Use when no visible text exists or can be provided.
- Does **not** translate well in auto-translate tools.
- Must match visible label if one exists (SC 2.5.3).

### Technique 4: `alt` Attribute (Images Only)
```html
<img src="logo.png" alt="Company Name — Home">
<img src="decorative.png" alt=""> <!-- empty = decorative -->
```

### Technique 5: Native HTML Naming
- `<button>` text content → name
- `<input type="submit" value="Send">` → "Send"
- `<legend>` → names its `<fieldset>`
- `<caption>` → names its `<table>`
- `<figcaption>` → names its `<figure>`

### Providing Accessible Descriptions
```html
<!-- aria-describedby: associate description text -->
<input type="text" id="phone" aria-describedby="phone-format">
<p id="phone-format">Format: +1 (555) 555-5555</p>

<!-- aria-description (newer, direct string): -->
<button aria-description="Opens in a new window">External link</button>
```

---

## Chapter 11.2 — Accessible Name Computation Algorithm

### How Browsers Determine the Accessible Name
The browser follows a strict priority order (Accessible Name and Description Computation spec):

1. `aria-labelledby` (highest priority — overrides everything)
2. `aria-label`
3. Native HTML mechanism (`alt`, `<label>`, `value`, text content, etc.)
4. `title` attribute (lowest priority fallback — avoid)

**When multiple naming methods conflict, the highest-priority wins.**

### Key Implications
- If you have both `alt` and `aria-label`, `aria-label` wins.
- If you use `aria-labelledby` pointing to a hidden element, that hidden element's text is still used.
- `title` is used as name only when no other method is present — and even then, it's inconsistent.

### 📚 Key Resources
- [Accessible Name and Description Computation — W3C](https://www.w3.org/TR/accname-1.1/)

---

## Chapter 11.3 — Accessible Names for Icon Buttons

### The Problem
Icon-only buttons/links have no visible text — screen readers need a text alternative.

### Solutions (in order of preference)

**Option 1: Visually hidden `<span>` inside button**
```html
<button>
  <span class="visually-hidden">Search</span>
  <svg aria-hidden="true">...</svg>
</button>
```

**Option 2: `aria-label` on the button**
```html
<button aria-label="Search">
  <svg aria-hidden="true">...</svg>
</button>
```

**Option 3: `aria-labelledby` referencing hidden text**
```html
<button aria-labelledby="btn-label">
  <span id="btn-label" hidden>Search</span>
  <svg aria-hidden="true">...</svg>
</button>
```

**Option 4: SVG `<title>` element**
```html
<button>
  <svg role="img" aria-labelledby="icon-title">
    <title id="icon-title">Search</title>
    <!-- SVG paths -->
  </svg>
</button>
```
⚠️ Less reliable — inconsistent support across AT.

### Always Hide Decorative Icons from AT
```html
<svg aria-hidden="true" focusable="false">...</svg>
```
- `aria-hidden="true"` removes from accessibility tree.
- `focusable="false"` prevents SVGs from receiving focus in IE11.

### Icon Fonts Warning
```html
<!-- ❌ Icon fonts produce unicode characters that AT may announce: -->
<button><i class="fa fa-search"></i></button>
<!-- ✅ Always provide text alternative: -->
<button aria-label="Search"><i class="fa fa-search" aria-hidden="true"></i></button>
```

---

## Chapter 11.4 — Concatenating accNames with `aria-labelledby`

### DRY Accessible Names
Use `aria-labelledby` to concatenate text from multiple elements — avoids duplicating accessible name text in the DOM.

**Example: Blog pagination**
```html
<!-- Instead of duplicating "Page" in each button's name: -->
<nav aria-label="Pagination">
  <a href="/page/1" aria-labelledby="page-label p1">
    <span id="p1">1</span>
  </a>
  <a href="/page/2" aria-labelledby="page-label p2">
    <span id="p2">2</span>
  </a>
</nav>
<span id="page-label" hidden>Page</span>
<!-- Each link announced as "Page 1", "Page 2", etc. -->
```

**Example: Repeated action buttons ("Read more")**
```html
<article>
  <h2 id="article1-title">Article Title</h2>
  <a href="/article1" aria-labelledby="read-more article1-title">
    <span id="read-more" hidden>Read more about</span>
  </a>
</article>
<!-- Announced as "Read more about Article Title, link" -->
```

---

## Chapter 11.5 — Label in Name: Unique Names for Repeated Controls

### The Problem
Multiple identical buttons ("Read more", "Add to cart") are confusing for:
- **Screen reader users**: Can't distinguish them in a list of all buttons
- **Voice control users**: Can't activate a specific one by speaking its label

### Solutions

**Option 1: Visually-hidden additional text**
```html
<button>
  Add to cart
  <span class="visually-hidden"> — MacBook Pro</span>
</button>
<!-- Announced: "Add to cart — MacBook Pro" -->
```

**Option 2: `aria-labelledby` concatenation (DRY)**
```html
<article>
  <h2 id="product1">MacBook Pro</h2>
  <button aria-labelledby="cart-label product1">
    <span id="cart-label" hidden>Add to cart</span>
  </button>
</article>
<!-- Announced: "Add to cart MacBook Pro, button" -->
```

### SC 2.5.3 Label in Name (Level A)
> "For UI components with labels that include text or images of text, the name contains the text that is presented visually."

- The accessible name must **contain** the visible label text.
- Voice control users speak the visible label — it must match (or be contained in) the accName.

```html
<!-- ❌ Violates 2.5.3: visible "Search" but name is "Submit query" -->
<button aria-label="Submit query">Search</button>

<!-- ✅ Correct: name contains visible text -->
<button aria-label="Search for articles">Search</button>
```

---

## Chapter 12 — Enhancing Navigation into a Drop-Down

### Navigation vs. Menu — Critical Distinction
- **Navigation** = links to pages (use `<nav>`, links, `aria-expanded`)
- **ARIA Menu** = application-like widget (menubar, menu, menuitem) — for **app menus, NOT site navigation**

> ⚠️ Never use ARIA `menu`, `menubar`, or `menuitem` roles for website navigation. These imply keyboard behavior (arrow key navigation) that users don't expect for navigation links.

### Building Accessible Drop-Down Navigation

**Basic structure:**
```html
<nav aria-label="Site">
  <ul>
    <li>
      <a href="/products/">Products</a>
      <button aria-expanded="false" aria-controls="products-submenu">
        <span class="visually-hidden">Products submenu</span>
        <!-- chevron icon, aria-hidden -->
      </button>
      <ul id="products-submenu" hidden>
        <li><a href="/products/laptops">Laptops</a></li>
        <li><a href="/products/phones">Phones</a></li>
      </ul>
    </li>
  </ul>
</nav>
```

**Key requirements:**
- Top-level links remain **links** (not converted to buttons)
- Separate **toggle button** for expanding/collapsing the submenu
- `aria-expanded` on the toggle button communicates state
- Submenu hidden with `hidden` attribute (managed by JS)
- Esc key closes the open submenu

### Keyboard Interactions
- **Tab/Shift+Tab**: Move through all focusable elements
- **Enter/Space**: Activate toggle button
- **Esc**: Close open submenu, return focus to toggle

---

## Chapter 13 — Enhancing to a Slide-Out Navigation Drawer

### Mobile Navigation Patterns
1. **Collapsed navigation**: Links hidden behind a toggle button, revealed inline
2. **Slide-out drawer**: Panel slides in from off-screen, covers page content

### Slide-Out Drawer Requirements
```html
<button aria-expanded="false" aria-controls="nav-drawer" aria-label="Open navigation menu">
  <!-- hamburger icon -->
</button>

<div id="nav-drawer" hidden>
  <nav aria-label="Site">
    <button aria-label="Close navigation menu"><!-- X icon --></button>
    <ul>...</ul>
  </nav>
</div>
```

**Critical accessibility behaviors:**
- `aria-expanded` on the toggle button
- Use `hidden` or `display:none` to hide drawer (not just visual positioning)
- Use `inert` attribute on page content when drawer is open (prevents interaction with background)
- **Focus management**: Move focus into the drawer when opened; return focus to trigger when closed
- **Esc key**: Close drawer, return focus to trigger

### Hiding Technique Choice
- Use `display: none` or `hidden` (fully hides from all users and AT)
- Avoid `visibility: hidden` alone (takes up space)
- Avoid off-canvas positioning alone (keyboard focus can still reach hidden content)

---

## Chapter 14 — Page-Level Accessibility: Page Title

### Why Page Titles Matter
- SC 2.4.2 Page Titled (Level A): Every page must have a `<title>` that describes its topic or purpose.
- Screen readers announce the page title when a page loads — first orientation cue.
- Browser tabs display the title.

### Best Practices for `<title>`
```html
<!-- Pattern: [Page Name] — [Site Name] -->
<title>Contact Us — Acme Corporation</title>
<title>Shopping Cart (3 items) — My Store</title>
```

- Should be **unique** per page.
- Should **describe the page topic/purpose**.
- Should **match or closely match** the `<h1>` of the page.
- For SPAs: Update `<title>` dynamically on route changes.

### 📚 Key Resources
- [Page Title in WCAG](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)

---

## Chapter 14.1 — Page Language

### Why Language Matters
- Screen readers use text-to-speech with specific pronunciation rules per language.
- Wrong language = wrong accent/pronunciation = incomprehensible content.
- SC 3.1.1 Language of Page (Level A): The default language must be programmatically determinable.
- SC 3.1.2 Language of Parts (Level AA): Language changes within the page must be identified.

### Setting Page Language
```html
<html lang="en">
<html lang="fr">
<html lang="ar">  <!-- Arabic — also triggers RTL in some browsers -->
<html lang="zh-Hans">  <!-- Simplified Chinese -->
```

### Language of Parts
```html
<p>In French, "hello" is <span lang="fr">bonjour</span>.</p>
<blockquote lang="de">Das ist ein deutsches Zitat.</blockquote>
```

### 📚 Key Resources
- [Language tags in HTML and XML — W3C](https://www.w3.org/International/articles/language-tags/)
- [BCP 47 Language Subtag Registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)

---

## Chapter 15 — Accessible Images: Alt Text

### WCAG Requirement
- SC 1.1.1 Non-text Content (Level A): All non-text content must have a text alternative that serves an equivalent purpose.

### The `alt` Attribute
```html
<img src="photo.jpg" alt="A baby bird resting on a person's hand.">
<img src="decorative.png" alt="">  <!-- empty = decorative -->
```
- `alt` attribute must **always be present** on `<img>` (even if empty).
- Without `alt`, some screen readers announce the file name.

### Five Types of Images

| Type | Alt Text Strategy |
|---|---|
| **Unessential (decorative/redundant)** | Empty `alt=""` |
| **Image of text** | Repeat the exact text in the image |
| **Complex images** (charts, infographics) | Short alt + extended description elsewhere |
| **Functional images** (in links/buttons) | Describe the **function**, not the image |
| **Informative images** | Describe the **information** the image conveys |

### Key Rules for Writing Alt Text

1. **Keep it short** — but as long as it needs to be. No character limit, but JAWS reads in 125-char chunks.
2. **End with a period** — creates a pause after announcement.
3. **Don't say "Image of" or "Photo of"** — screen readers already announce the role.
   - Exception: mention type if relevant (e.g., "Sketch of...", "Illustration of...")
4. **Context determines content** — why you're using the image guides what to describe.
5. **Emotion matters** — if an image conveys emotion, the alt text should too.
6. **Don't use the file name** as alt text.
7. **Don't use `title` attribute** as a substitute for `alt`.

### Functional Images in Links
```html
<!-- Logo in a link — describe destination, not image: -->
<a href="/"><img src="logo.png" alt="Acme Corp — Home"></a>

<!-- Icon next to text link — if redundant, empty alt: -->
<a href="https://twitter.com/sara"><img src="twitter.svg" alt=""> Follow Sara</a>

<!-- Icon that adds info (opens in new window): -->
<a href="..." target="_blank">
  How to meet WCAG <img src="external.svg" alt="Opens in new window">
</a>
```

### Complex Images — Extended Descriptions
```html
<figure role="group">
  <img src="chart.png" alt="Bar chart showing Q1 2024 revenue by product.">
  <figcaption>
    <h2>Revenue Data</h2>
    <table><!-- actual data table --></table>
  </figcaption>
</figure>
```

### `alt` vs `figcaption`
- `alt` = text alternative for when the image can't be seen (describes what it IS)
- `figcaption` = editorial caption that relates the image to its context (more narrative)
- `figcaption` does NOT replace `alt` — use both when appropriate.

### AI Cannot Replace Human Alt Text Writers
> "Quality image descriptions increase access to the visual world for me and many other people. Describing is a skill, an art, and should be by humans." — Haben Girma

AI cannot convey purpose, context, or emotion the way a human author can.

### Testing Alt Text
- **Web Developer Toolbar**: Disable images → view alt text in place of images.
- **Web Developer Toolbar**: Display Alt Attributes → see alt text overlaid on images.

### 📚 Key Resources
- [Alt-texts: The ultimate guide](https://www.sebastiangreger.net/2022/06/the-alt-text-question-ultimate-guide)
- [WAI Images Tutorial](https://www.w3.org/WAI/tutorials/images/)
- [Writing great alt text: Emotion matters — Eric Bailey](https://thoughtbot.com/blog/writing-great-alt-text)
- [Your image is probably not decorative — Eric Bailey](https://www.smashingmagazine.com/2021/06/img-alt-attribute-use-accessibility/)
- [Case Study: Implementing Accessible Data Charts for Khan Academy](https://www.sarasoueidan.com/blog/accessible-data-charts/)

---

## Chapter 16 — Accessible Forms: Grouping and Labelling

### Why Forms Are Critical
- 35.8% of form inputs on top 1M sites are not properly labeled (WebAIM 2023).
- Forms enable transactions — they're the gateway to accomplishing user goals.

### The `<label>` Element (Primary Labeling Mechanism)
```html
<!-- Explicit association (recommended): -->
<label for="email">Email address</label>
<input type="email" id="email">

<!-- Implicit association (inside label): -->
<label for="email">
  Email address
  <input type="email" id="email">
</label>
```

**Rules:**
- `for` value must match `id` value exactly.
- `<label>` can label only **one** control.
- `for` attribute only works on `<label>` — not on `<div>` or `<span>`.

### Labelable Elements
- `<button>`, `<input>` (except `type="hidden"`), `<meter>`, `<output>`, `<progress>`, `<select>`, `<textarea>`

### ARIA Labeling Fallbacks
```html
<!-- When label text exists but can't be a <label> element: -->
<span id="name-label">Full Name</span>
<input type="text" aria-labelledby="name-label">

<!-- When no visible label exists: -->
<input type="text" aria-label="Full Name">
```

### ❌ Don't Use `placeholder` as a Label
- Disappears when user types — violates SC 3.3.2
- Low contrast by default
- Not auto-translated
- Difficult for users with cognitive disabilities
- May look like pre-filled content

### Providing Additional Instructions
```html
<label for="pw">Create a password</label>
<input type="password" id="pw" aria-describedby="pw-requirements">
<ul id="pw-requirements">
  <li>At least 12 characters</li>
  <li>Mix of uppercase and lowercase</li>
  <li>At least one special character</li>
</ul>
```

### Grouping Related Controls: `<fieldset>` + `<legend>`
```html
<!-- Radio buttons group: -->
<fieldset>
  <legend>Choose a T-shirt color:</legend>
  <label><input type="radio" name="color" value="black"> Black</label>
  <label><input type="radio" name="color" value="blue"> Blue</label>
  <label><input type="radio" name="color" value="red"> Red</label>
</fieldset>

<!-- Multiple address groups: -->
<fieldset>
  <legend>Shipping Address</legend>
  <!-- address fields -->
</fieldset>
<fieldset>
  <legend>Billing Address</legend>
  <!-- address fields -->
</fieldset>
```

- `<legend>` must be a **direct child** of `<fieldset>`.
- `role="group"` + ARIA works but has worse mobile AT support — prefer `<fieldset>`.

### Visually-Hidden Labels (When Acceptable)
Context makes purpose clear (e.g., search input next to "Search" button):
```html
<label for="search" class="visually-hidden">Search</label>
<input type="search" id="search">
<button type="submit">Search</button>
```

### Useful Attributes for Better Forms

**`autocomplete` (SC 1.3.5 Level AA)**
```html
<input type="text" autocomplete="name">
<input type="email" autocomplete="email">
<input type="text" autocomplete="one-time-code">  <!-- SMS OTP autofill! -->
<input type="tel" autocomplete="tel">
```
51 possible values — enables browser autofill and AT customization.

**`inputmode`** (better mobile keyboards)
```html
<input type="text" inputmode="numeric">   <!-- number pad -->
<input type="text" inputmode="email">     <!-- email keyboard -->
<input type="text" inputmode="decimal">   <!-- decimal number pad -->
```

### 📚 Key Resources
- [Don't Use The Placeholder Attribute — Eric Bailey](https://www.smashingmagazine.com/2018/06/placeholder-attribute/)
- [Fieldsets, Legends, and Screen Readers — Adrian Roselli](https://adrianroselli.com/2022/07/use-legend-and-fieldset.html)
- [Build a better mobile input (tool)](https://better-mobile-inputs.netlify.app/)
- [W3C Forms Tutorial](https://www.w3.org/WAI/tutorials/forms/)

---

## Chapter 16.1 & 16.2 — Accessible Forms: Validation

### Key Principles for Accessible Form Validation

#### 1. Identify Required Fields
```html
<!-- Visual indicator + programmatic: -->
<label for="email">
  Email <span aria-hidden="true">*</span>
  <span class="visually-hidden">(required)</span>
</label>
<input type="email" id="email" required aria-required="true">
```
- Use `required` attribute (native HTML) — widely supported.
- `aria-required="true"` can supplement for custom widgets.
- Indicate required fields at the top of the form: "Fields marked with * are required."

#### 2. Inline Validation — Don't Validate Too Early
- **Don't** validate `onblur` (leaving a field) — frustrates users
- **Do** validate `onsubmit` — report all errors at once
- Or validate inline but only **after** the user has had a chance to complete input

#### 3. Error Identification (SC 3.3.1 Level A)
When errors are identified:
```html
<input type="email" id="email" 
       aria-invalid="true" 
       aria-describedby="email-error">
<p id="email-error" role="alert">
  Please enter a valid email address.
</p>
```
- `aria-invalid="true"` marks the field as invalid
- Error message associated with `aria-describedby`
- `role="alert"` or live region announces new error messages dynamically

#### 4. Error Suggestions (SC 3.3.3 Level AA)
- If an error is detected and suggestions are known, tell the user how to fix it.
- Not just "Invalid input" → "Please enter a date in MM/DD/YYYY format."

#### 5. Error Prevention for Important Actions (SC 3.3.4 Level AA)
For legal/financial transactions:
- Allow reversal, or
- Allow checking/confirming before submission, or
- Provide error checking with an opportunity to correct

#### 6. Focus Management on Validation
After form submission with errors:
- Move focus to the **error summary** at the top of the form, or
- Move focus to the **first field with an error**
```javascript
// After validation fails:
errorSummary.setAttribute("tabindex", "-1");
errorSummary.focus();
```

#### 7. Error Summary Component
```html
<div role="alert" aria-labelledby="error-heading" tabindex="-1">
  <h2 id="error-heading">There are 2 errors in this form</h2>
  <ul>
    <li><a href="#email">Email: Please enter a valid email address.</a></li>
    <li><a href="#phone">Phone: This field is required.</a></li>
  </ul>
</div>
```

### 📚 Key Resources
- [Form Validation Techniques — W3C](https://www.w3.org/WAI/tutorials/forms/validation/)
- [Inline Form Validation — Adrian Roselli](https://adrianroselli.com/2019/02/avoid-default-field-validation.html)

---

## Chapter 17.

## Chapter 17.1 — Accessible Notifications with ARIA Live Regions (Part 1)

### What Are ARIA Live Regions?
- A notification system targeted specifically at **screen reader users**.
- When content changes dynamically (without a page reload), live regions announce those changes automatically.
- Essential for Single Page Applications (SPAs), real-time updates, form validation, chat messages, etc.

### The Problem Live Regions Solve
Screen readers read content when a user moves focus to it. If content changes elsewhere on the page (e.g., a success message appears), the screen reader user won't know unless:
- Focus is moved to the new content, or
- The changed region is a live region

### Creating Live Regions

#### Method 1: ARIA `role` (Implicit Live Regions)
```html
<!-- role="alert" — assertive, interrupts current announcement -->
<div role="alert">Your session is about to expire in 2 minutes.</div>

<!-- role="status" — polite, waits for current announcement to finish -->
<div role="status">Your file has been saved successfully.</div>

<!-- role="log" — polite, ordered accumulation of messages (chat, logs) -->
<div role="log"><!-- log entries --></div>

<!-- role="timer" — time-sensitive countdown -->
<div role="timer">02:30</div>

<!-- role="marquee" — non-essential, constantly updating content -->
<div role="marquee"><!-- scrolling ticker --></div>
```

#### Method 2: `aria-live` attribute (Explicit Live Regions)
```html
<!-- aria-live="polite" — announce after current interaction -->
<div aria-live="polite" aria-atomic="true">
  Showing 1–10 of 45 results
</div>

<!-- aria-live="assertive" — interrupt immediately (use sparingly!) -->
<div aria-live="assertive">
  Critical error: Payment declined.
</div>

<!-- aria-live="off" — no announcements (default) -->
<div aria-live="off">...</div>
```

### Key Attributes for Live Regions

| Attribute | Values | Purpose |
|---|---|---|
| `aria-live` | `off`, `polite`, `assertive` | When to announce |
| `aria-atomic` | `true`, `false` | Whether to announce entire region or just changes |
| `aria-relevant` | `additions`, `removals`, `text`, `all` | What changes to announce |
| `aria-busy` | `true`, `false` | Suppress announcements while updating |

### `aria-atomic`
```html
<!-- aria-atomic="true": announce the whole region as one unit -->
<div aria-live="polite" aria-atomic="true">
  Page 3 of 10
</div>
<!-- Without atomic=true, might announce just "3" when number changes -->
```

### `aria-relevant`
```html
<!-- Only announce additions to this region: -->
<ul aria-live="polite" aria-relevant="additions">
  <!-- new messages are added here -->
</ul>
```

### Critical Implementation Rules
1. **Create live regions in the DOM before content changes** — don't inject the live region with the content.
```javascript
// ❌ Wrong — live region injected at same time as content:
container.innerHTML = '<div role="alert">Success!</div>';

// ✅ Correct — live region pre-exists, content is updated:
// HTML already has: <div role="status" id="status-region"></div>
document.getElementById('status-region').textContent = 'Success!';
```

2. **Start with empty live regions** — pre-populate in HTML, inject content via JS.

3. **Use `polite` by default** — only use `assertive` for critical, time-sensitive errors.

4. **Use `aria-atomic="true"`** when the full context of the region is needed (e.g., "3 of 10").

### Live Region Role Comparison

| Role | `aria-live` | `aria-atomic` | Use Case |
|---|---|---|---|
| `alert` | `assertive` | `true` | Critical errors, important warnings |
| `status` | `polite` | `true` | Success messages, status updates |
| `log` | `polite` | `false` | Chat messages, log entries |
| `timer` | `off` | `false` | Countdown timers |
| `marquee` | `off` | `false` | Non-essential scrolling content |

### HTML Native Live Regions
- `<output>` element — implicitly has `aria-live="polite"` and `role="status"`
```html
<output aria-live="polite">Results: 42 items found</output>
```

### 📚 Key Resources
- [ARIA Live Regions — MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions)
- [Using ARIA Live Regions — W3C](https://www.w3.org/TR/wai-aria-1.1/#live_region_roles)

---

## Chapter 17.2 — ARIA Live Regions (Part 2): Best Practices & Limitations

### When NOT to Use Live Regions

Live regions are **not suitable** for:
1. **Complex structured content** — descriptions are flattened to plain text; lists, headings, links inside live regions lose structure.
2. **Interactive content** — buttons, links inside live regions may not be reachable after announcement.
3. **Focus management situations** — when moving focus is the better approach (e.g., opening a dialog, navigating to a new "page" in a SPA).
4. **Content requiring user interaction** — live regions can't be "paused" to interact with.

### Prefer Focus Management Over Live Regions When Possible
- Opening a dialog → move focus into dialog
- SPA route change → move focus to main content / new `<h1>`
- Form validation → move focus to error summary
- Completing a multi-step process → move focus to confirmation

### Best Practices for Robust Live Regions

#### 1. Use a "Status Container" Pattern
```html
<!-- Keep live region in DOM from page load: -->
<div class="sr-only" role="status" aria-live="polite" aria-atomic="true" id="status"></div>
```
```javascript
function announceToScreenReader(message) {
  const status = document.getElementById('status');
  // Clear first to ensure re-announcement of same message:
  status.textContent = '';
  requestAnimationFrame(() => {
    status.textContent = message;
  });
}
```

#### 2. Clear and Re-set for Repeated Messages
If the same message is announced twice, some AT won't re-announce it. Clear the region first.

#### 3. Avoid Overusing `assertive`
Assertive live regions interrupt the user's current reading — use only for truly critical, time-sensitive messages (e.g., session timeout warnings, critical errors).

#### 4. Test Across Browser + AT Combinations
Live region support varies significantly. Always test with:
- NVDA + Firefox (Windows)
- JAWS + Chrome (Windows)
- VoiceOver + Safari (macOS/iOS)

#### 5. Don't Announce Too Much
Only announce what the user needs to know. Excessive announcements are annoying and degrade the experience.

### Example: Search Results Announcement
```html
<!-- Live region pre-exists in DOM -->
<div role="status" aria-live="polite" aria-atomic="true" class="visually-hidden" id="results-status"></div>

<!-- Search results container -->
<ul id="results">...</ul>
```
```javascript
// After search results load:
document.getElementById('results-status').textContent =
  `${results.length} results found for "${query}".`;
```

### Example: Cart Update Announcement
```javascript
announceToScreenReader('MacBook Pro added to cart. Cart now contains 3 items.');
```

### 📚 Key Resources
- [Testing ARIA Live Regions — Scott O'Hara](https://www.scottohara.me/blog/2022/02/05/this-is-fine.html)
- [Accessible notifications with ARIA Live Regions](https://www.smashingmagazine.com/2022/04/accessible-notifications-aria-live-regions/)

---

## Chapter 18.1 — Keyboard Accessibility: Designing Accessible Focus Indicators

### Why Focus Indicators Matter
- Focus indicators = the keyboard user's equivalent of a mouse cursor.
- Without visible focus, keyboard users don't know **where they are** on the page.
- SC 2.4.7 Focus Visible (Level AA): Any keyboard operable UI must have a visible focus indicator.
- SC 2.4.11 Focus Appearance (Level AA — WCAG 2.2): New, more specific requirements.

### The Problem: Default Focus Styles
Browsers provide default focus outlines, but:
- They're often visually removed with `outline: none` or `outline: 0` in resets.
- They vary significantly across browsers.
- They may lack sufficient contrast.

```css
/* ❌ Never do this: */
* { outline: none; }
button:focus { outline: none; }
```

### The Solution: `focus-visible`
```css
/* ✅ Remove default, style for keyboard users only: */
:focus { outline: none; }
:focus-visible {
  outline: 3px solid #005fcc;
  outline-offset: 3px;
}
```
- `:focus` fires for all input methods (mouse, keyboard, touch)
- `:focus-visible` fires only when focus should be visible (keyboard navigation)
- Provides better UX: no focus ring on click, but ring visible on keyboard navigation

### WCAG 2.2 SC 2.4.11 Focus Appearance Requirements (Level AA)
The focus indicator must:
1. **Enclose** the component (at minimum)
2. Have a **minimum area** of the perimeter of the unfocused component × 2 CSS pixels
3. Have a **contrast ratio of at least 3:1** between focused and unfocused states
4. Have a **contrast ratio of at least 3:1** between the focus indicator and adjacent colors

### Designing Good Focus Indicators

**Recommended approach — double indicator (works on any background):**
```css
:focus-visible {
  outline: 3px solid #005FCC;
  outline-offset: 2px;
  box-shadow: 0 0 0 5px #ffffff; /* white halo creates contrast */
}
```

**Or use `box-shadow` for rounded outlines:**
```css
:focus-visible {
  outline: none;
  box-shadow:
    0 0 0 3px #ffffff,   /* white gap */
    0 0 0 6px #005fcc;   /* colored outer ring */
}
```

### High Contrast Mode Considerations
- Focus indicators must also be visible in Windows High Contrast Mode / Forced Colors.
- Use `Highlight` or `ButtonText` system colors:
```css
@media (forced-colors: active) {
  :focus-visible {
    outline: 3px solid Highlight;
  }
}
```

### Tools for Testing Focus Indicators
- Manual keyboard navigation (Tab key)
- [Focus Indicator Checker — APCA](https://www.myndex.com/APCA/)
- [Who Can Use (contrast tool)](https://www.whocanuse.com/)

### 📚 Key Resources
- [A guide to designing accessible, WCAG-compliant focus indicators](https://www.sarasoueidan.com/blog/focus-indicators/)
- [WCAG 2.2 Focus Appearance Explained](https://www.tpgi.com/focus-appearance-explained/)
- [Focusing on Focus Styles — Eric Bailey](https://css-tricks.com/focusing-on-focus-styles/)
- [Stop trying to recreate the default focus outline — Sara Joy](https://www.accessible-colors.com/)

---

## Chapter 18.2 — Skip Links

### What Are Skip Links?
- Navigation links that allow users to **bypass repeated blocks** of content (navigation menus, headers).
- Required by SC 2.4.1 Bypass Blocks (Level A).
- Benefit: keyboard users and screen reader users can skip straight to main content.

### Basic Skip Link Implementation
```html
<!-- Place at the very top of <body>: -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<!-- Target element: -->
<main id="main-content" tabindex="-1">
  <!-- page content -->
</main>
```

```css
.skip-link {
  position: absolute;
  top: -100%;
  left: 0;
  z-index: 9999;
  padding: 0.5rem 1rem;
  background: #000;
  color: #fff;
  text-decoration: none;
}

/* Reveal on focus: */
.skip-link:focus {
  top: 0;
}
```

### Why `tabindex="-1"` on the Target?
- Allows programmatic focus on the target element when the skip link is activated.
- Without it, some browsers won't scroll to and focus the target after clicking the skip link.
- The element remains **not** in the natural tab order (only focusable via script or link activation).

### Multiple Skip Links (Advanced)
For content-heavy pages:
```html
<nav aria-label="Skip links">
  <a href="#main-content">Skip to main content</a>
  <a href="#main-nav">Skip to navigation</a>
  <a href="#search">Skip to search</a>
</nav>
```

### Section-Level Skip Links (Always Visible)
For very long pages, section skip links can help users skip between regions:
```html
<a href="#comments" class="visually-hidden">Skip to comments</a>
```

### 📚 Key Resources
- [Skip Navigation Links — WebAIM](https://webaim.org/techniques/skipnav/)
- [How–to: Use skip navigation links](https://www.a11yproject.com/posts/skip-nav-links/)

---

## Chapter 18.3 — Managing Keyboard Focus: Roving `tabindex`

### The Problem with Complex Widgets
Standard tab navigation moves through **every** focusable element. For widgets with many interactive items (toolbars, tab lists, radio groups), this is inefficient. Users expect arrow key navigation within the widget, then Tab to move out.

### What is Roving `tabindex`?
A technique to manage focus within a composite widget using `tabindex`:
- Only **one element** in the group has `tabindex="0"` at a time (the current/active item)
- All other items have `tabindex="-1"` (focusable programmatically, but not via Tab)
- Arrow keys move between items, updating which item has `tabindex="0"`

### Implementation Pattern
```html
<div role="toolbar" aria-label="Text formatting">
  <button tabindex="0" aria-pressed="false">Bold</button>
  <button tabindex="-1" aria-pressed="false">Italic</button>
  <button tabindex="-1" aria-pressed="false">Underline</button>
</div>
```

```javascript
const toolbar = document.querySelector('[role="toolbar"]');
const buttons = [...toolbar.querySelectorAll('button')];
let currentIndex = 0;

toolbar.addEventListener('keydown', (e) => {
  if (e.key === 'ArrowRight') {
    buttons[currentIndex].tabIndex = -1;
    currentIndex = (currentIndex + 1) % buttons.length;
    buttons[currentIndex].tabIndex = 0;
    buttons[currentIndex].focus();
    e.preventDefault();
  }
  if (e.key === 'ArrowLeft') {
    buttons[currentIndex].tabIndex = -1;
    currentIndex = (currentIndex - 1 + buttons.length) % buttons.length;
    buttons[currentIndex].tabIndex = 0;
    buttons[currentIndex].focus();
    e.preventDefault();
  }
  if (e.key === 'Home') {
    buttons[currentIndex].tabIndex = -1;
    currentIndex = 0;
    buttons[currentIndex].tabIndex = 0;
    buttons[currentIndex].focus();
    e.preventDefault();
  }
  if (e.key === 'End') {
    buttons[currentIndex].tabIndex = -1;
    currentIndex = buttons.length - 1;
    buttons[currentIndex].tabIndex = 0;
    buttons[currentIndex].focus();
    e.preventDefault();
  }
});
```

### Common Widgets Using Roving `tabindex`
- **Toolbars**: Arrow keys navigate between tools
- **Tab lists**: Arrow keys switch between tabs
- **Radio groups**: Arrow keys select options
- **Menu items**: Arrow keys navigate menu
- **Tree views**: Arrow keys navigate tree nodes

### Toggle Buttons with ARIA
```html
<button aria-pressed="false" onclick="this.setAttribute('aria-pressed', 
  this.getAttribute('aria-pressed') === 'true' ? 'false' : 'true')">
  Dark Mode
</button>
```
- `aria-pressed="true"` → button is active/pressed
- `aria-pressed="false"` → button is inactive
- Screen readers announce "toggle button" or "pressed/not pressed"

### Expected Keyboard Behavior by Widget Type

| Widget | Navigation | Activation |
|---|---|---|
| Toolbar | Arrow keys | Enter/Space |
| Tabs | Arrow keys | Automatic or Enter |
| Radio group | Arrow keys | Auto-selects on arrow |
| Menu | Arrow keys | Enter/Space |
| Tree | Arrow/Enter | Enter |

### 📚 Key Resources
- [Roving tabindex — web.dev](https://web.dev/articles/use-tabindex)
- [Managing Focus for Accessibility](https://www.smashingmagazine.com/2022/11/deep-dive-into-custom-focus-indicators/)
- [ARIA Toolbar Pattern — APG](https://www.w3.org/WAI/ARIA/apg/patterns/toolbar/)

---

## Chapter 19 — Adapting to Forced Colors Mode

### What is Forced Colors Mode?
- A system-level accessibility feature (e.g., **Windows High Contrast Mode / Contrast Themes**) that overrides all colors on a page with a limited system color palette.
- Helps users with low vision, light sensitivity, and other visual disabilities.
- Standardized in CSS as the `forced-colors` media feature.

### How It Works
- The OS replaces your CSS colors with a small set of system colors.
- Only certain properties are affected: `color`, `background-color`, `border-color`, `box-shadow`, `outline-color`, `text-decoration-color`, etc.
- Properties NOT affected: `background-image`, `opacity`, CSS transforms.

### Detecting Forced Colors in CSS
```css
@media (forced-colors: active) {
  /* styles for high contrast / forced colors environments */
}
```

### System Colors for Forced Colors
```css
@media (forced-colors: active) {
  .button {
    border: 2px solid ButtonText;
    color: ButtonText;
    background-color: ButtonFace;
  }

  .button:focus-visible {
    outline: 3px solid Highlight;
  }
}
```

#### Available System Color Keywords
| Keyword | Purpose |
|---|---|
| `ButtonFace` | Background of buttons |
| `ButtonText` | Text of buttons |
| `Canvas` | Page background |
| `CanvasText` | Page text |
| `Highlight` | Selected text background |
| `HighlightText` | Selected text foreground |
| `LinkText` | Unvisited links |
| `VisitedText` | Visited links |
| `GrayText` | Disabled text |
| `Field` | Input field background |
| `FieldText` | Input field text |

### Impact on HTML Elements

**Native elements** (buttons, links, inputs) → **automatically styled** by the OS with appropriate system colors. ✅

**Custom elements and ARIA widgets** → CSS colors are removed; must use system colors explicitly or native elements. ⚠️

**SVG images** → May lose fill/stroke colors; adapt using `currentColor` or system color keywords.

**Background images used for icons** → **Disappear** in forced colors mode (use inline SVG instead).

### CSS `forced-color-adjust`
```css
/* Opt out of forced colors for a specific element (use very sparingly): */
.custom-element {
  forced-color-adjust: none;
}
```

> Only use `forced-color-adjust: none` when you are providing your own high-contrast styles and the element would otherwise become inaccessible.

### Best Practices

1. **Use native HTML elements** → they inherit correct system colors automatically.
2. **Use inline SVG** for icons (not background images or icon fonts) → inline SVG uses `currentColor` which adapts.
3. **Use `currentColor`** for SVG fill/stroke → inherits from the text color.
4. **Use borders** instead of background colors for visual boundaries → borders are preserved; backgrounds may not be.
5. **Don't rely solely on color** to convey information → required by SC 1.4.1 anyway.
6. **Test in Windows High Contrast Mode** (or via browser DevTools forced colors emulation).

### Testing Forced Colors
- **Windows**: Settings → Accessibility → Contrast Themes (choose High Contrast Black or White)
- **Chrome DevTools**: Rendering tab → Emulate CSS media feature `forced-colors: active`
- **Edge DevTools**: Same as Chrome (Edge has best forced-colors support)

### ARIA and Forced Colors
- ARIA roles do **NOT** affect forced colors styling — the OS reads native HTML semantics.
- A `<div role="button">` will NOT get button colors in forced colors mode.
- Use native `<button>` to get automatic styling.

```html
<!-- ❌ Gets no system button colors in forced colors: -->
<div role="button">Click me</div>

<!-- ✅ Gets ButtonFace/ButtonText automatically: -->
<button>Click me</button>
```

### 📚 Key Resources
- [Forced colors explained — Polypane](https://polypane.app/blog/forced-colors-explained-a-practical-guide/)
- [Forced Colors Mode and High Contrast Mode — Melanie Richards](https://blogs.windows.com/msedgedev/2020/09/17/styling-for-windows-high-contrast-with-new-css-media-query/)
- [A guide to Windows High Contrast Mode — Sara Soueidan](https://www.smashingmagazine.com/2022/06/guide-windows-high-contrast-mode/)
- [Quick Note on ARIA and Windows High Contrast Mode — Scott O'Hara](https://www.scottohara.me/blog/2019/03/14/aria-high-contrast.html)
- [Polypane Forced Colors emulator](https://polypane.app/)

---

## Master Resources Reference

### W3C Standards & Specifications
- [WCAG 2.1](https://www.w3.org/TR/WCAG21/) — Primary accessibility standard
- [WCAG 2.2](https://www.w3.org/TR/WCAG22/) — Latest version
- [How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG21/quickref/) — Daily-use reference
- [ARIA Specification](https://www.w3.org/TR/wai-aria-1.1/)
- [ARIA in HTML](https://www.w3.org/TR/html-aria/) — Role mappings reference
- [HTML-AAM](https://www.w3.org/TR/html-aam-1.0/) — Accessibility API Mappings
- [Accessible Name Computation](https://www.w3.org/TR/accname-1.1/)
- [ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
- [Using ARIA](https://www.w3.org/TR/using-aria/)
- [WAI Tutorials (Forms, Images, etc.)](https://www.w3.org/WAI/tutorials/)
- [WCAG 3.0 Working Draft](https://www.w3.org/TR/wcag-3.0/)

### Testing Tools
- [WAVE Extension](https://wave.webaim.org/extension/) — Visual accessibility evaluation
- [Web Developer Toolbar](https://chrispederick.com/work/web-developer/) — Manual testing (headings, images, forms)
- [axe DevTools Extension](https://www.deque.com/axe/devtools/) — Automated issue detection
- [Assistiv Labs](https://assistivlabs.com/) — Remote screen reader testing
- [a11ysupport.io](https://a11ysupport.io/) — ARIA support tables
- [h123 Bookmarklet](https://hinderlingvolk.com/h123/) — Heading structure visualizer
- [APCA Contrast Tool](https://www.myndex.com/APCA/)
- [Build a better mobile input](https://better-mobile-inputs.netlify.app/) — Input type/mode explorer

### Screen Readers
- [NVDA (free)](https://www.nvaccess.org/) — Most popular free Windows SR
- [JAWS](https://www.freedomscientific.com/products/software/jaws/) — Most popular Windows SR (demo: 40 min)
- [Karabiner Elements (Mac)](https://karabiner-elements.pqrs.org/) — Remap Insert key on Mac
- [Deque Screen Reader Cheat Sheets](https://dequeuniversity.com/screenreaders/)

### Essential Community Resources
- [WebAIM](https://webaim.org/) — Articles, surveys, tools
- [The A11Y Project](https://www.a11yproject.com/) — Community-driven a11y resource
- [Smashing Magazine Accessibility](https://www.smashingmagazine.com/category/accessibility/)
- [Scott O'Hara's blog](https://www.scottohara.me/) — Deep dives into HTML/ARIA
- [Adrian Roselli's blog](https://adrianroselli.com/) — Practical accessibility research
- [Sara Soueidan's blog](https://www.sarasoueidan.com/blog/) — Accessible UI patterns
- [Tetralogical blog](https://tetralogical.com/blog/) — Foundations series, AT videos
- [Browsing with Assistive Technology (Video Series)](https://tetralogical.com/blog/2021/12/24/browsing-with-assistive-technology-videos/)
- [Course Toolkit Page](https://practical-accessibility.today/toolkit/)

---

## Quick Reference: Key WCAG Success Criteria

| SC | Level | Topic |
|---|---|---|
| 1.1.1 | A | Non-text content (alt text) |
| 1.3.1 | A | Info and relationships (semantic markup) |
| 1.3.5 | AA | Identify input purpose (autocomplete) |
| 1.4.1 | A | Use of color (not sole means) |
| 1.4.3 | AA | Contrast minimum (4.5:1 text) |
| 1.4.4 | AA | Resize text (200% without loss) |
| 1.4.5 | AA | Images of text (use real text) |
| 1.4.11 | AA | Non-text contrast (3:1 for UI) |
| 2.1.1 | A | Keyboard accessible |
| 2.4.1 | A | Bypass blocks (skip links) |
| 2.4.2 | A | Page titled |
| 2.4.6 | AA | Headings and labels (descriptive) |
| 2.4.7 | AA | Focus visible |
| 2.4.11 | AA | Focus appearance (WCAG 2.2) |
| 2.5.3 | A | Label in name |
| 3.1.1 | A | Language of page |
| 3.1.2 | AA | Language of parts |
| 3.3.1 | A | Error identification |
| 3.3.2 | A | Labels or instructions |
| 3.3.3 | AA | Error suggestion |
| 3.3.4 | AA | Error prevention (legal/financial) |
| 4.1.2 | A | Name, role, value |
| 4.1.3 | AA | Status messages (live regions) |

---

*Notes compiled from the Practical Accessibility course by Sara Soueidan — practical-accessibility.today*
*Course hashtag: #PracticalA11y*