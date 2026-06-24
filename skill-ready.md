# Skill-Ready — A Practical Playbook for Adding Accessibility to Projects

> Status: **scaffold** — heading structure is locked; each sub-section below is a
> placeholder to be discussed and filled in depth, one topic at a time.

## How to Use This Guide

This guide is organized into three tiers. Apply them in order — each tier assumes
the previous one is already in place.

- **1. Minimum** — the non-negotiable foundation. Correct semantics, structure, and
  keyboard support that every project needs before anything else.
- **2. Basic** — state, ARIA, and communication. How the UI tells assistive
  technology what's happening (expanded/collapsed, current, selected, live updates).
- **3. Advanced** — component-specific patterns. The extra rules a particular
  component (modal, carousel, menu, tabs, …) needs beyond the generic foundation.

**How each sub-section is laid out** — every `###` section follows the same shape:

```
**What & why** — 1–2 lines on what it is and why it matters.
**Rules / Key points** — prescriptive bullets (Rule: …, Decision: …).
**Gotchas** — known traps (<name> gotcha — …).
**WCAG** — relevant Success Criteria.
```

Conventions: `backticks` for elements / ARIA attributes / CSS / JS; WCAG cited as
`SC 1.3.1 Info and Relationships`; em dashes for clause separation.

---

## 1. Minimum — The Foundation (do this on every project)

### 1.1 Semantic HTML

**What & why** — "Use semantic HTML" means using the right element for its correct
purpose. HTML is descriptive: each of its ~114 semantic elements already carries
meaning. Choosing the correct element is the single most powerful accessibility tool
you have — it hands assistive technology (AT) the element's **role** (what it is/does),
gives interactive elements **built-in keyboard behaviour** for free, and is a universal
language understood by every device, AT, reader mode, and forced-colors mode. ARIA is
only the *second* most powerful tool; it supplements HTML semantics and should be a last
resort, not a default.

**Rules / Key points**
- Rule: Semantics convey three things — the **role** of an element (what it is/does),
  its **name** (identifies it and its purpose), and its **state** where applicable.
- Rule: Semantic HTML is the most powerful accessibility tool; ARIA is the second. If a
  native element gives you the role and behaviour you need, use it — adding ARIA on top
  is redundant and discouraged.
- Rule: What an element *is* determines how it *can be used*. Picking the wrong element
  breaks user expectations and can leave a control that AT users cannot operate.
- Decision: When several elements map to the same role, still pick the one that best
  describes the content — e.g. `<ol>` and `<ul>` both expose the `list` role, but choose
  ordered vs unordered by meaning.
- Rule: Style an element according to its semantics — if it behaves like a button, make
  it a `<button>`; don't dress a link up as a button (and vice versa).
- Rule: `<div>` and `<span>` *are* semantic — they map to the `generic` role. They're
  fine for layout/styling hooks, but never use them for content that has a meaningful
  element available.
- Rule: When HTML semantics genuinely fall short, supplement with ARIA — but keep ARIA
  to a minimum and test across browser/AT combinations (there is no feature-detection
  for ARIA support).

**Gotchas**
- Contextual-role gotcha — some elements only expose a useful role in the right context:
  an `<a>` with no `href` is `generic` (not a link); a `<section>` is `generic` until it
  has an accessible name, only then becoming a `region` landmark; same idea for `<aside>`.
- No-role gotcha — not every element maps to a role. `<picture>` has no role mapping;
  it's the `<img>` inside it that matters for accessibility.
- Text-semantics gotcha — `<strong>` / `<em>` and other text-level semantics may not be
  announced unless the user has raised AT verbosity. Don't rely on them to convey meaning
  that must be perceived.
- CSS-breaks-semantics gotcha — CSS can strip semantics from otherwise-correct markup:
  - `list-style: none` on a `<ul>` removes list semantics in some Safari versions —
    re-instate with `role="list"` (or `list-style-type: ""`).
  - `display: flex`/`grid` historically dropped `<table>` semantics (largely fixed now,
    but test).
  - `display: none` / `visibility: hidden` remove the element from the accessibility tree
    entirely.
- ARIA-modifies-semantics gotcha — ARIA can override, supplement, or suppress native
  semantics (e.g. `aria-pressed` on a `<button>` exposes it as a toggle button). Powerful,
  but easy to misuse — changing native semantics is a last resort.

**Choosing the right element — quick checklist**
- Does it map to a meaningful ARIA role?
- Does it have the built-in keyboard behaviour I need?
- Does it need an accessible name (and does it have one)?
- Are any CSS styles inadvertently affecting its semantics?

**WCAG** — `SC 1.3.1 Info and Relationships` (Level A): information, structure, and
relationships conveyed visually must be programmatically determinable — which is exactly
what correct semantic markup provides.

### 1.2 Document Landmarks & Page Structure

_(header / nav / main / footer, one `main`, skip link)_

**What & why** — Landmarks are the key navigable regions of a page — the structural
equivalent of physical landmarks you orient by. Screen reader users use them to jump
straight to a region (25%+ navigate by landmarks regularly, per WebAIM). Using the right
sectioning element exposes each landmark for free; a skip link then lets keyboard users
bypass the repeated header/nav and get to the content. Together they answer "where am I,
and how do I get where I'm going" without forcing a linear read of the whole page.

**The eight landmarks and their native elements**

| ARIA role | HTML element | Notes |
|---|---|---|
| `banner` | `<header>` | Only when a direct child of `<body>` |
| `navigation` | `<nav>` | Each one should have a unique label |
| `main` | `<main>` | Only **one** per page |
| `contentinfo` | `<footer>` | Only when a direct child of `<body>` |
| `complementary` | `<aside>` | Sidebar / related content |
| `form` | `<form>` | Exposed as a landmark only when named |
| `search` | `<search>` | Native HTML element for search regions |
| `region` | `<section>` + name | Exposed only when given an accessible name |

**Rules / Key points**
- Rule: Prefer the **native element** over `role="…"` — `<header>`, `<nav>`, `<main>`,
  `<footer>`, `<aside>`, `<search>` give you the landmark with no extra ARIA.
- Rule: Exactly **one `<main>`** per page, and the `<h1>` should be its first child.
- Rule: **All page content should sit inside a landmark** — nothing orphaned between them.
- Rule: Use **as few landmarks as possible** — too many dilutes their navigation value.
- Decision: Let the **visual design guide landmark choice** so the visual and semantic
  structure line up.
- Rule: When there are **multiple landmarks of the same type**, give each a unique label
  via `aria-label` (e.g. `<nav aria-label="Site">`, `<nav aria-label="Breadcrumbs">`) or
  `aria-labelledby` pointing at a heading inside it.
- Rule: A `<section>` is `generic` until you give it an accessible name; name it (usually
  with `aria-labelledby` referencing its heading) to expose it as a `region`.
- Pattern: **Skip link** — first focusable element in `<body>`, `<a href="#main">Skip to
  main content</a>`, targeting `<main id="main" tabindex="-1">`. Visually hide it and
  reveal it on `:focus`.

```html
<a href="#main" class="skip-link">Skip to main content</a>
<!-- … header / nav … -->
<main id="main" tabindex="-1"><!-- h1 first --></main>
```

**Gotchas**
- Header/footer-scope gotcha — `<header>` and `<footer>` only map to `banner` /
  `contentinfo` when they are **direct children of `<body>`**. Nested inside an `<article>`
  or `<section>`, they're just generic headers/footers — that's fine, just don't expect
  the landmark.
- Skip-link-target gotcha — give the target `tabindex="-1"`. Without it, some browsers
  won't move focus to (or scroll to) the target after the link is activated. `-1` keeps
  it out of the natural Tab order while still allowing programmatic focus.
- Redundant-word gotcha — don't put "navigation" in a `<nav>` label; the role is already
  announced, so "Navigation navigation" is the result.
- Unnamed-form gotcha — a `<form>` only becomes a landmark when it has an accessible name;
  an unnamed form won't show up in the landmarks list.

**WCAG**
- `SC 1.3.1 Info and Relationships` (Level A) — structure conveyed visually (regions)
  must be programmatically determinable.
- `SC 2.4.1 Bypass Blocks` (Level A) — provide a way to skip repeated blocks of content;
  the skip link (and the landmarks themselves) satisfy this.

### 1.3 Heading Hierarchy

**What & why** — Headings are the primary way screen reader users navigate within a page.
Reading is linear by default, but users jump between sections using heading shortcuts (and
can pull up a list of all headings) — 85.7% find heading levels very/somewhat useful
(WebAIM). A correct heading hierarchy is effectively the page's table of contents: levels
must reflect the *actual* content structure, not how big the text looks.

**Rules / Key points**
- Rule: **One `<h1>` per page** — it describes the page's primary topic, should be the
  first child of `<main>`, and should match (or closely match) the page `<title>`.
- Rule: Build hierarchy with `<h2>`–`<h6>`: `<h2>` for major sections, `<h3>` for their
  subsections, and so on. **Do not skip levels** (no `<h2>` → `<h4>`).
- Rule: **If it looks like a heading, it must be a heading.** Marking visual headings up
  as plain styled text fails `SC 1.3.1`.
- Anti-pattern: Using heading elements **purely for their styling** (big/bold) when the
  text isn't a section heading — that injects phantom entries into the heading outline.
- Decision: For a **subheading / tagline** under a heading, use `<hgroup>` with one
  heading plus a `<p>` — never stack multiple headings inside `<hgroup>`.
- Rule: When you truly cannot use a native heading, you can synthesize one with
  `role="heading"` + `aria-level="n"` — but this is a fallback; prefer real `<h1>`–`<h6>`.

```html
<!-- Native (preferred) -->
<h2>This is a heading</h2>

<!-- Fallback only when a native heading isn't possible -->
<div role="heading" aria-level="2">This is a heading</div>
```

**Gotchas**
- Document-outline gotcha — the HTML "document outline algorithm" **does not exist** and
  never will; no browser implemented it. Multiple `<h1>`s nested in `<section>`s do **not**
  create nested outlines. Always pick the level that reflects real hierarchy.
- Styling-driven-level gotcha — choose heading level by **meaning, not appearance**. If a
  section heading needs to look smaller, style it down with CSS; don't drop to a lower
  heading level to get smaller text (and don't bump the level up for bigger text).
- Skipped-level gotcha — jumping levels (e.g. `<h1>` straight to `<h3>`) implies a missing
  section and disorients users navigating by structure.

**WCAG**
- `SC 1.3.1 Info and Relationships` (Level A) — visual headings must be marked up as
  headings programmatically.
- `SC 2.4.6 Headings and Labels` (Level AA) — headings must be **descriptive** of the
  content they introduce.
- `SC 2.4.10 Section Headings` (Level AAA) — provide section headings where content is
  organised into sections.

### 1.4 Lists, Tables & Grouping Semantics

**What & why** — Lists, tables, and grouping elements communicate **relationships** —
"these items belong together", "this many of them", "this cell relates to that header",
"these fields form one logical group". Sighted users read those relationships from layout;
AT users only get them if the right element exposes them. Used correctly, these elements
announce counts ("list, 5 items"), positions ("item 2 of 5"), and header/cell
associations for free.

**Lists**
- Rule: Group related items in a `<ul>` (unordered) or `<ol>` (ordered) so the **count
  and order** are conveyed; each item in its own `<li>`.
- Decision: Both `<ul>` and `<ol>` map to the `list` role — choose by meaning (sequence
  matters → `<ol>`, e.g. breadcrumbs, steps, pagination).
- Rule: Use `<dl>`/`<dt>`/`<dd>` (description list) for name–value pairs (metadata,
  glossaries, key–value detail rows).
- Gotcha: **`list-style: none` strips list semantics** in some Safari versions (notably
  outside a `<nav>` landmark). Re-instate with `role="list"` on the `<ul>`/`<ol>` whenever
  you remove the default markers, so the item count stays exposed.

```html
<ul role="list">          <!-- role="list" safeguards count after list-style: none -->
  <li>…</li>
</ul>
```

**Tables**
- Rule: Use `<table>` for **tabular data** — never for layout, and never fake a table
  out of `<div>`s.
- Rule: Give a data table a `<caption>` — it becomes the table's accessible name and
  helps users decide whether to explore it.
- Rule: Mark header cells as `<th>` and set `scope="col"` / `scope="row"` so AT can
  associate each data cell with its header(s).
- Pattern (legacy layout table): if you inherit a table used purely for layout, apply
  `role="none"` to the `<table>` — the suppression cascades to its required children
  (`<tr>`, `<td>`, …), making the whole thing presentational.

**Grouping**
- Rule: Group related **form controls** with `<fieldset>` + `<legend>` — the `<legend>`
  (first direct child) names the group. Covered in depth in §1.9 and §3.6.
- Decision: `group` vs `region` — both name a set of elements, but a `group` is **not**
  listed in the page outline/landmarks, whereas a named `<section>` (`region`) is. Use a
  `region` for major navigable areas; use `group` for smaller in-widget collections.
- Rule: Prefer the **native grouping element** over ARIA — `<fieldset>`/`<legend>` over
  `role="group"` + `aria-labelledby`, which has weaker mobile-AT support.

**Gotchas**
- Faked-structure gotcha — CSS grid/flex can make `<div>`s *look* like a list or table
  while exposing nothing. If it reads as a list or table, mark it up as one.
- `role="none"`-cascade gotcha — `role="none"` on a `<table>` removes the semantics of its
  required descendants too. Great for stripping a layout table; never do it to a real
  data table.

**WCAG** — `SC 1.3.1 Info and Relationships` (Level A): the relationships conveyed by
lists, tables, and groupings (count, order, header associations, grouping) must be
programmatically determinable.

### 1.5 Links vs Buttons

**What & why** — Links and buttons have **different semantics and are not
interchangeable**. A link's role promises navigation ("this takes me somewhere"); a
button's role promises an action ("this does something here"). Picking the wrong one
breaks user expectations — Enter vs Space stop working as expected, the right-click /
open-in-new-tab affordance disappears or appears wrongly, and AT announces a behaviour
the control doesn't deliver. Get this right and you also get the correct keyboard
behaviour for free.

**The core difference**
- **Link (`<a href>`)** → navigates to another place: a different page, a section within
  the page, a file, an email. The URL changes.
- **Button (`<button>`)** → triggers an action on the current page: open a dialog, submit
  a form, toggle UI, change a view. The URL does not change.

**How to choose** — ask:
1. Does it navigate to another page/section (URL changes)? → **Link**
2. Does it trigger an action on the current page? → **Button**
3. Does it (or should it) work without JavaScript? → likely **Link**
4. Can you sensibly right-click → open in new tab? → **Link**

**Behaviour you get for free**

| | `<button>` | `<a href>` |
|---|---|---|
| Implicit role | `button` | `link` |
| Focusable by default | Yes (no `tabindex`) | Yes (only with `href`) |
| Keyboard activation | **Space and Enter** | **Enter** only |
| Works without JS | No (except form submit) | Yes |
| Disable via | `disabled` attribute | remove `href` + `role="link"` + `aria-disabled="true"` |

**Rules / Key points**
- Rule: **Style to match semantics** — if it behaves like a button, style it as a button;
  if it's a link, don't disguise it as a button (and vice versa).
- Rule: A bare `<a>` without `href` is `generic` — **not** a link, and not focusable.
- Decision: Need an action but only have a link in the markup? Either switch to `<button>`,
  or progressively enhance the link into a button (below) — never leave a fake link.

**Enhancing a link into a button** (progressive-enhancement fallback)
```html
<a href="#" role="button">Do something</a>
```
You must also: (1) override semantics with `role="button"`; (2) `preventDefault()` on the
link's navigation; (3) handle both `keydown` (Enter fires immediately) **and** `keyup`
(Space fires on release) so it behaves like a real button.

**Gotchas**
- Fake-link gotcha — `href="#"` (a meaningless `href`) plus an `onclick` to fake a toggle
  is a smell that you should be using a `<button>`. Link semantics promise navigation, but
  the link goes nowhere — confusing for AT and broken for right-click/new-tab.
- Space-key gotcha — links don't activate on Space. If you've built an action out of an
  `<a>` and only wired up Enter, Space-key users are stuck — another sign it should be a
  `<button>`.

**WCAG**
- `SC 4.1.2 Name, Role, Value` (Level A) — the control's role must be correct and exposed;
  a link masquerading as a button (or vice versa) misreports its role.
- `SC 2.1.1 Keyboard` (Level A) — the control must be fully operable by keyboard with the
  keys its role implies.

### 1.6 Keyboard — Tab Flow & DOM Order

_(no positive `tabindex`, no keyboard traps)_

**What & why** — Many people operate the web entirely by keyboard (and switch devices,
voice control, and screen readers all build on the keyboard model). Everything you can do
with a mouse must be doable with a keyboard, in a **predictable order**. Tab order follows
**DOM/source order** — so if you get the markup order right and use native interactive
elements, correct keyboard flow comes for free. The job is mostly *not breaking* it.

**Rules / Key points**
- Rule: Use **native interactive elements** (`<button>`, `<a href>`, form controls). They
  are focusable, in the tab order, and keyboard-operable by default — no `tabindex` needed.
- Rule: **DOM order = tab order.** Make the source order match the logical/visual reading
  order so tabbing feels natural. Beware CSS (flex/grid `order`, absolute positioning)
  that reorders things visually but leaves the DOM — and therefore focus — out of sync.
- Rule: You only ever need two `tabindex` values:
  - `tabindex="0"` — add an otherwise non-focusable element into the tab order (in source
    position). Only for custom widgets built on non-interactive elements.
  - `tabindex="-1"` — focusable programmatically (`.focus()`) but **not** in the tab order
    (e.g. a skip-link target, an error-summary heading). All negative values behave as `-1`.
- Rule: **Never use positive `tabindex`** (`1`, `2`, …). It doesn't mean "after 0" — the
  browser walks *all* positive values first, in numeric order, before falling back to
  source order. That creates a tab-order/visual-order mismatch and easily fails SC 2.4.3.
- Anti-pattern: `tabindex="0"` on a native focusable element (redundant) or on a descendant
  of one (e.g. `<span tabindex="0">` inside a `<button>`) — creates two tab stops on one
  control.
- Rule: If it's focusable, it must be **visibly focusable** — when an element takes focus
  the user must be able to see it (see §1.7). Don't make off-screen/hidden things focusable
  unless they reveal on focus.
- Rule: For composite widgets (tabs, toolbars, radio groups, menus), make the group a
  **single tab stop** using roving `tabindex` — one item `tabindex="0"`, the rest `-1`,
  arrow keys move within. (Covered per-component in §3.)

**No keyboard traps**
- Rule: A user who tabs *into* anything must be able to tab *out* of it with the keyboard
  alone — no dead ends. The one legitimate "trap" is a modal dialog's intentional, fully
  managed focus loop (Esc closes it); see §3.1.
- Gotcha: Embedded widgets, custom date pickers, and third-party iframes/plugins are common
  accidental traps — test by tabbing all the way through the page.

**Gotchas**
- Visual-vs-DOM-order gotcha — reordering with CSS (`order`, `flex-direction: row-reverse`,
  absolute positioning) makes focus jump around unpredictably because focus still follows
  the DOM. Fix the source order instead.
- `tabindex`-can't-disable gotcha — `tabindex` **cannot** make an element non-focusable;
  only `disabled` or `inert` can. Don't reach for a negative `tabindex` to "remove" a
  control from interaction.
- `aria-hidden`-on-focusable gotcha — `aria-hidden="true"` on (or around) a focusable
  element doesn't remove it from the tab order; focus lands on something AT can't announce
  ("focusing nothing"). Use `inert`/`disabled`, or genuinely remove it.

**WCAG**
- `SC 2.1.1 Keyboard` (Level A) — all functionality available from the keyboard.
- `SC 2.1.2 No Keyboard Trap` (Level A) — focus can always move away with the keyboard.
- `SC 2.4.3 Focus Order` (Level A) — focus order preserves meaning and operability.

### 1.7 Visible Focus Indicators

**What & why** — A focus indicator is the keyboard user's cursor — it's how they know
*where they are* on the page. Without it, keyboard navigation is like using a mouse with
an invisible pointer. Browsers provide a default outline for free; the most common
accessibility regression is **removing it** (`outline: none`) in a CSS reset and never
replacing it. The rule is simple: never remove focus styling without providing a clearly
visible replacement.

**Rules / Key points**
- Anti-pattern: Globally killing the outline — `* { outline: none }` or `:focus { outline:
  0 }` with no replacement. This strands every keyboard user.
- Rule: Use **`:focus-visible`**, not `:focus`, for your custom ring. `:focus` fires for
  all input methods (including mouse click); `:focus-visible` fires only when the browser
  judges focus *should* be shown (keyboard) — so no ring on click, ring on Tab.
- Rule: Make the indicator **strong and high-contrast** — a thick outline (e.g. `3px`) with
  `outline-offset` so it doesn't crowd the control. Pair with a contrasting halo when the
  control may sit on varied backgrounds (double-indicator technique below).
- Rule: Support **Forced Colors / High Contrast Mode** — use system colors (`Highlight`,
  `ButtonText`) under `@media (forced-colors: active)` so the ring survives.
- Decision: Don't merely recreate the browser default — design an indicator that's *more*
  visible than the default, meeting the WCAG 2.2 appearance requirements.

```css
/* Remove the default, then provide a stronger keyboard-only ring */
:focus { outline: none; }

:focus-visible {
  outline: 3px solid #005FCC;
  outline-offset: 2px;
  box-shadow: 0 0 0 5px #ffffff; /* white halo → contrast on any background */
}

@media (forced-colors: active) {
  :focus-visible { outline: 3px solid Highlight; }
}
```

**WCAG 2.2 — what "good enough" means (`SC 2.4.11 Focus Appearance`)**
The indicator must:
1. **Enclose** the component (at minimum).
2. Be at least as large as the unfocused perimeter × 2 CSS px in area.
3. Have **≥ 3:1 contrast** between the focused and unfocused states.
4. Have **≥ 3:1 contrast** between the indicator and adjacent colors.

**Gotchas**
- `:focus`-vs-`:focus-visible` gotcha — styling plain `:focus` shows the ring on mouse
  click too, which designers dislike and then "fix" by removing it entirely. Style
  `:focus-visible` to get the best of both.
- Hidden-focus gotcha — an element that's focusable but visually hidden/clipped/off-screen
  means focus disappears. If something is focusable it must become visible on focus (ties
  back to §1.6).
- Forced-colors gotcha — a `box-shadow`-only indicator can vanish in Forced Colors mode
  (box-shadows are often dropped). Always include an `outline` fallback for that mode.

**WCAG**
- `SC 2.4.7 Focus Visible` (Level AA) — any keyboard-operable UI has a visible focus
  indicator.
- `SC 2.4.11 Focus Appearance` (Level AA, WCAG 2.2) — the indicator meets the size/contrast
  requirements above.

### 1.8 Images & Text Alternatives

_(`alt`, decorative vs informative)_

**What & why** — Non-text content needs a text alternative that serves an **equivalent
purpose**, so people who can't see the image still get its meaning. The `alt` attribute is
the primary mechanism — and the right alt text depends entirely on *why the image is
there*, not on what the picture literally contains. Crucially, `alt` must **always be
present** on an `<img>` (even if empty); omit it and some screen readers fall back to
reading the file name.

**The five types of image — and the alt strategy for each**

| Type | Strategy |
|---|---|
| Decorative / redundant | Empty `alt=""` — removes it from the accessibility tree |
| Image of text | Repeat the **exact text** shown in the image |
| Informative | Describe the **information** the image conveys |
| Functional (inside a link/button) | Describe the **function/destination**, not the picture |
| Complex (chart, infographic) | Short `alt` + an **extended description** nearby (§3 / data table) |

**Rules for writing alt text**
- Rule: Keep it **short** — as long as it needs to be, no longer. (JAWS reads in ~125-char
  chunks; long alt is fine when warranted, e.g. images of text.)
- Rule: **Don't write "image of" / "photo of"** — the role is already announced. (Exception:
  note the medium when it matters — "Sketch of…", "Illustration of…".)
- Rule: **Context determines content** — the same photo gets different alt depending on why
  it's used. If the image conveys **emotion**, the alt should too.
- Rule: End with a period (creates a natural pause in the announcement).
- Anti-pattern: Using the **file name** as alt, or the **`title`** attribute as a substitute
  for `alt`.

**Functional images** (image is the only content of a link/button)
- Rule: Describe the **action or destination**. A logo linking home → `alt="Acme Corp —
  Home"`, not `alt="Acme logo"`.
- Rule: If an icon sits **next to a text label** and is redundant, give it `alt=""` so it's
  not announced twice.
- Rule: If the icon **adds information** (e.g. "opens in new window"), put that in the alt.

```html
<a href="/"><img src="logo.png" alt="Acme Corp — Home"></a>          <!-- destination -->
<a href="…"><img src="x.svg" alt=""> Follow Sara</a>                  <!-- redundant → empty -->
<a href="…" target="_blank">WCAG <img src="ext.svg" alt="Opens in new window"></a>
```

**`alt` vs `<figcaption>`**
- `alt` — the text alternative for when the image *can't be seen*; describes what it **is**.
- `<figcaption>` — an editorial caption that relates the image to its surrounding context;
  more narrative.
- Rule: They are **not interchangeable** — a `<figcaption>` does not replace `alt`. Use both
  when appropriate, and don't have the figcaption merely repeat the alt.

**Gotchas**
- Missing-`alt` gotcha — no `alt` attribute ≠ decorative. Omitting it can make SRs read the
  file name; decorative requires an explicit empty `alt=""`.
- "Probably-not-decorative" gotcha — most images carry meaning. Default to describing;
  reserve `alt=""` for genuinely decorative or redundant images.
- AI-alt gotcha — auto-generated descriptions miss purpose, context, and emotion. Treat
  them as a starting point, not a finished alternative.
- SVG/icon-font gotcha — for icon *buttons*, the accessible name lives on the control, not
  a literal `alt` (see §3.10); decorative inline SVGs should get `aria-hidden="true"`.

**WCAG** — `SC 1.1.1 Non-text Content` (Level A): all non-text content has a text
alternative that serves an equivalent purpose (or is marked decorative).

### 1.9 Form Labels

_(every control has a programmatic label)_

**What & why** — Every form control needs a programmatically associated label so AT can
announce *what* the field is for, and so the label becomes a larger click/tap target.
This is the single most common form failure — 35.8% of inputs on the top 1M sites are not
properly labelled (WebAIM 2023). Get the label association right first; richer form
behaviour (validation, grouping logic, autofill) builds on top in §3.6.

**The `<label>` element — primary mechanism**
```html
<!-- Explicit (recommended): for matches id exactly -->
<label for="email">Email address</label>
<input type="email" id="email">

<!-- Implicit: control nested inside the label -->
<label>Email address <input type="email"></label>
```
- Rule: `for` must match the control's `id` **exactly**, and `for` only works on `<label>`
  (not `<div>`/`<span>`).
- Rule: A `<label>` labels **one** control only.
- Rule: Labelable elements are `<input>` (except `type="hidden"`), `<button>`, `<select>`,
  `<textarea>`, `<meter>`, `<output>`, `<progress>`. Anything else needs an ARIA fallback.

**ARIA fallbacks** (only when a `<label>` isn't possible)
```html
<span id="name-label">Full Name</span>
<input type="text" aria-labelledby="name-label">   <!-- visible text elsewhere -->

<input type="text" aria-label="Full Name">          <!-- no visible label at all -->
```
- Decision: Prefer a real `<label>` → then `aria-labelledby` (reuses visible text) →
  then `aria-label` (no visible text). A visible label helps everyone, not just AT.

**Rules / Key points**
- Anti-pattern: Using **`placeholder` as the label**. It disappears on input (fails
  `SC 3.3.2`), is low-contrast, isn't auto-translated, confuses cognitive-disability users,
  and can look like pre-filled content. A placeholder is a hint, never a substitute.
- Rule: Group related controls with **`<fieldset>` + `<legend>`** — the `<legend>` (a
  **direct child** of `<fieldset>`) names the group. Essential for radio/checkbox sets and
  multi-section forms (Shipping vs Billing). Prefer it over `role="group"` (weaker mobile
  AT support).
- Rule: A **visually-hidden label** is acceptable only when context makes purpose obvious
  (e.g. a search input beside a "Search" button) — hide the `<label>`, don't omit it.
- Rule: Provide extra instructions via **`aria-describedby`** (e.g. password requirements),
  not by overloading the label. (Detailed in §2.3.)

```html
<fieldset>
  <legend>Choose a T-shirt colour:</legend>
  <label><input type="radio" name="color" value="black"> Black</label>
  <label><input type="radio" name="color" value="blue"> Blue</label>
</fieldset>
```

**Helpful extras** (deeper coverage in §3.6)
- `autocomplete` (`SC 1.3.5`, Level AA) — `autocomplete="email"`, `"name"`, `"tel"`,
  `"one-time-code"` (SMS OTP autofill) enable browser autofill and AT personalisation.
- `inputmode` — surfaces the right mobile keyboard (`numeric`, `decimal`, `email`).

**Gotchas**
- `for`/`id`-mismatch gotcha — a typo'd or duplicated `id` silently breaks the association;
  the field then reads as unlabelled.
- Implicit-label gotcha — wrapping works, but some older AT pairings handle explicit
  `for`/`id` more reliably; prefer explicit when unsure.
- Placeholder-only gotcha — a field with only a placeholder *looks* labelled to sighted
  users but is unlabelled to AT once focused/typed-in.

**WCAG**
- `SC 1.3.1 Info and Relationships` (Level A) — the label↔control relationship is
  programmatic.
- `SC 3.3.2 Labels or Instructions` (Level A) — controls have labels/instructions; covers
  the placeholder-as-label failure.
- `SC 4.1.2 Name, Role, Value` (Level A) — each control exposes an accessible name.

### 1.10 Page Language, Title & Document Basics

**What & why** — A few document-level attributes set the stage for everything else. The
page **language** tells screen readers which pronunciation rules to use — get it wrong and
text-to-speech reads in the wrong accent, often becoming incomprehensible. The page
**title** is the first thing a screen reader announces on load and what labels the browser
tab — the user's first orientation cue. These are cheap to set and high-impact.

**Page language**
```html
<html lang="en">
<html lang="ar">       <!-- Arabic — also triggers RTL in some browsers -->
<html lang="zh-Hans"> <!-- Simplified Chinese -->
```
- Rule: Set a valid `lang` on the root `<html>` element — the default language must be
  programmatically determinable.
- Rule: Mark **inline language changes** with `lang` on the relevant element so AT switches
  pronunciation for that span:
  ```html
  <p>In French, "hello" is <span lang="fr">bonjour</span>.</p>
  ```
- Rule: Use valid **BCP 47** language tags (`en`, `en-GB`, `fr`, `zh-Hans`).

**Page title (`<title>`)**
```html
<!-- Pattern: [Unique page name] — [Site name] -->
<title>Contact Us — Acme Corporation</title>
<title>Shopping Cart (3 items) — My Store</title>
```
- Rule: Every page has a **non-empty `<title>`** that describes its topic/purpose.
- Rule: Make it **unique per page** so users can tell apart tabs, history, and search
  results — and it should make sense **out of context**.
- Rule: Put the **unique part first**, site name after (`Page — Site`), so the meaningful
  text shows in the truncated tab and is announced before the site name.
- Rule: It should **match or closely match the `<h1>`**. Keep it short and concise.
- Rule: For **SPAs**, update `<title>` on every route change (the browser won't do it for
  you).

**Other document basics**
- Rule: Set the document direction with `dir` when needed (`<html dir="rtl">` for RTL
  scripts; `lang="ar"`/`"he"` often imply it, but be explicit).
- Rule: Use a responsive viewport meta **without disabling zoom** — never set
  `user-scalable=no` or a low `maximum-scale`; users must be able to pinch-zoom
  (ties to `SC 1.4.4` / `1.4.10`, see §1.11).

**Gotchas**
- Wrong-`lang` gotcha — a template defaulting to `lang="en"` on a French page makes every
  word mispronounced. Verify it reflects the actual content language.
- Special-character gotcha — avoid characters like the vertical bar `|` in titles; some
  screen readers announce them awkwardly. Prefer a simple dash/en-dash separator.
- Zoom-blocking gotcha — `user-scalable=no` in the viewport meta silently blocks zoom for
  low-vision users; it's a common copy-paste regression.

**WCAG**
- `SC 3.1.1 Language of Page` (Level A) — default page language is set.
- `SC 3.1.2 Language of Parts` (Level AA) — inline language changes are identified.
- `SC 2.4.2 Page Titled` (Level A) — the page has a descriptive title.

### 1.11 Color & Contrast Basics

**What & why** — Text and UI must be perceivable by people with low vision and colour
blindness. Two foundational rules cover most cases: contrast must be **high enough** to
read, and colour must **never be the only way** information is conveyed. These are easy to
get wrong in design and easy to verify with a contrast checker, so they belong in the
baseline pass.

**Contrast minimums**

| What | Minimum ratio | SC |
|---|---|---|
| Normal text | **4.5:1** against its background | `1.4.3` (AA) |
| Large text (≥ 24px, or ≥ 19px bold) | **3:1** | `1.4.3` (AA) |
| UI components & graphical objects (borders, icons, control boundaries, focus rings) | **3:1** | `1.4.11` (AA) |

- Rule: Check **text against its actual background** (including over images/gradients —
  add a scrim if needed).
- Rule: Interactive boundaries (input borders, toggle states, focus indicators) need
  **3:1** as non-text contrast — see §1.7 for focus specifics.

**Don't rely on colour alone**
- Rule: Colour must **not be the only means** of conveying information, indicating an
  action, prompting a response, or distinguishing a visual element (`SC 1.4.1`).
- Rule: Pair colour with a **second cue** — text, an icon, underline, or shape. Classic
  cases: error fields (red **+** icon/text), required markers, links in body text
  (underline, not just colour), chart series, status badges.

```html
<!-- Error: colour PLUS icon PLUS text, not red alone -->
<p class="field-error"><svg aria-hidden="true">…</svg> Enter a valid email address.</p>
```

**Resize & real text**
- Rule: Text must **resize to 200%** without loss of content or function (`SC 1.4.4`) —
  don't block zoom (see §1.10), and avoid fixed pixel heights that clip enlarged text.
- Rule: Use **real text, not images of text** (`SC 1.4.5`) — images of text don't scale,
  recolour, or translate.

**Gotchas**
- Disabled-control gotcha — disabled controls are technically **exempt** from `SC 1.4.3`,
  but the browser's default low-contrast grey is still a real usability barrier. Style them
  to stay legible, and prefer not disabling controls at all (see §2.12).
- Placeholder-contrast gotcha — default placeholder grey usually fails contrast; another
  reason it's not a label (see §1.9).
- Color-only-state gotcha — toggles/tabs/selected states shown only by colour change fail
  for colour-blind users; add a shape, icon, underline, or text change.
- Contrast-over-imagery gotcha — text on photos can pass in one spot and fail in another;
  test the worst-case region or add an overlay.

**WCAG**
- `SC 1.4.3 Contrast (Minimum)` (Level AA) — 4.5:1 text / 3:1 large text.
- `SC 1.4.11 Non-text Contrast` (Level AA) — 3:1 for UI components and graphics.
- `SC 1.4.1 Use of Color` (Level A) — colour is never the sole means of conveying info.
- `SC 1.4.4 Resize Text` (Level AA) / `SC 1.4.5 Images of Text` (Level AA).

---

## 2. Basic — State, ARIA & Communication

### 2.1 ARIA-State-Driven CSS

_(style from `[aria-expanded]`, `[aria-current]`, `[aria-selected]`, …)_

**What & why** — This is the single most useful technique in the Basic tier: **style
directly from the ARIA state attribute** rather than from a parallel CSS class. When the
selector is `[aria-expanded="true"]` instead of `.is-open`, the visual state and the
accessible state are driven by **one source of truth** — they physically cannot drift
apart. Your JavaScript only has to toggle the ARIA attribute; the appearance follows for
free, and a forgotten class can never leave AT users with a control that *looks* open but
reads "collapsed" (or vice versa).

**The principle**
- Rule: Use the **ARIA state attribute itself as the CSS hook** — `a[aria-current="page"]`,
  `button[aria-expanded="true"]`, `button[aria-pressed="true"]`, `[aria-invalid="true"]`,
  `[aria-selected="true"]`, `[aria-disabled="true"]` — not a separate `.current` / `.open`
  / `.active` class.
- Rule: This makes the **accessible state the source of truth**: the style only applies
  when the state is actually set, so visuals and semantics stay in lockstep.
- Decision: JS toggles **one** thing (the attribute). Resist also toggling a class — that's
  the drift you're trying to eliminate.

**Common patterns**
```css
/* Current page in a nav — highlight only when the state is set */
a[aria-current="page"] { font-weight: 700; border-bottom: 2px solid; }

/* Toggle button — pressed look tracks aria-pressed */
button[aria-pressed="true"] { background: #ccc; box-shadow: inset 0 0 5px rgba(0,0,0,.2); }

/* Disclosure — rotate the chevron from the expanded state */
[aria-expanded="true"] > svg { transform: rotate(90deg); }

/* Optionally hide/show the panel from CSS, so JS only flips aria-expanded */
.disclosure > button[aria-expanded="false"] + .panel { display: none; }

/* Invalid field styling tracks the semantic state */
input[aria-invalid="true"] { border: 2px solid #b00020; }
```

**Rules / Key points**
- Pattern: **Disclosure / dropdown** — JS toggles `aria-expanded` on the trigger; CSS hides
  the adjacent panel (`button[aria-expanded="false"] + .panel { display: none }`) and
  rotates the marker. JS does nothing else visual.
- Pattern: **Current item** — `aria-current="page"` (or `step`/`true`) both communicates
  state to AT *and* serves as the highlight hook.
- Pattern: **Toggle button** — `aria-pressed` drives the pressed appearance (see §2.6).
- Pattern: **Validation** — `aria-invalid="true"` drives error styling (see §2.11).
- Rule: For **state-marker icons** (chevron, plus), prefer an inline `<svg aria-hidden="true">`
  over a CSS pseudo-element — more styling control and better Forced Colors behaviour — and
  drive its transform from the ARIA-state selector.

**Gotchas**
- Class-and-attribute-drift gotcha — toggling both a class *and* the attribute re-introduces
  exactly the desync you're avoiding; if one update is missed, they disagree. Toggle only
  the attribute.
- Missing-default-state gotcha — selectors like `[aria-expanded="false"]` only match when
  the attribute is **present**. Ship the initial attribute in the HTML (`aria-expanded="false"`),
  don't add it lazily on first interaction, or the initial styling won't apply.
- `aria-invalid="false"`-vs-absent gotcha — per spec, **remove** `aria-invalid` when a field
  becomes valid rather than setting `"false"` (with the one exception of suppressing the
  on-load invalid announcement on `required` fields). Your CSS should key off `="true"`.
- Decorative-marker gotcha — the icon you rotate must be `aria-hidden="true"`; the *state*
  is already conveyed by the ARIA attribute, so the glyph must not be announced too.

**WCAG** — Not a criterion in itself; it's an implementation technique that helps satisfy
`SC 4.1.2 Name, Role, Value` (Level A) by keeping the exposed **state** accurate and in
sync with the visual state.

### 2.2 Accessible Naming — `aria-label` vs `aria-labelledby`

**What & why** — The **accessible name** (accName) is the string AT announces to identify a
control — "Search, button", "Close, button". It is *not* the same as a visible label: a
label can be on screen yet have no programmatic association, leaving the control nameless
to AT. Every interactive element must have an accName; `aria-label` and `aria-labelledby`
are the ARIA tools for supplying one when native HTML can't. The skill is knowing which to
reach for, and in what order.

**The five sources of an accessible name** (and the priority that matters)
An accName can come from: (1) the element's **content**, (2) an **HTML attribute** (`alt`,
`value`, `title`), (3) **another element** (`<label>`, `<legend>`, `<caption>`),
(4) **`aria-labelledby`**, or (5) **`aria-label`**.

- Rule: In the computation algorithm, **`aria-labelledby` and `aria-label` win** over
  native HTML — native methods are only checked when both ARIA naming attributes are
  absent. `aria-labelledby` outranks `aria-label`.
- Rule (author's go-to priority — roughly the reverse): prefer **(1) visible HTML content**
  → **(2) native attribute/element** (`<label>`, `alt`) → **(3) `aria-labelledby`** pointing
  at on-page text → **(4) `aria-label` as a last resort**. Layer ARIA on only when HTML
  falls short.

**`aria-labelledby`** — reference visible (or intentionally hidden) text by `id`
```html
<button aria-labelledby="close-label">×</button>
<span id="close-label">Close dialog</span>

<!-- Compose a name from multiple ids; concatenated in the order listed -->
<button aria-labelledby="action item">×</button>
<span id="action">Remove</span> <span id="item">CSS</span>   <!-- → "Remove CSS" -->
```
- Rule: Prefer `aria-labelledby` over `aria-label` — it **reuses visible text** (so the
  name matches what's on screen) and it **translates** with the page.
- Rule: If the referenced text exists *only* to be a name (not page content), hide it with
  the HTML **`hidden`** attribute, not a visually-hidden CSS class — `hidden` keeps it out
  of the content flow while `aria-labelledby` still exposes it, avoiding a double
  announcement.

**`aria-label`** — supply a name string directly, when no visible text exists
```html
<button aria-label="Close">×</button>
```
- Rule: Use **only as a last resort** — there's no visible counterpart, and it's a string
  you must maintain separately.
- Rule: `aria-label` (and `aria-labelledby`) **override the element's content** — so if you
  put `aria-label` on a control that also has visible text, the visible text is no longer
  the name (an `SC 2.5.3` risk, below).

**Rules / Key points**
- Rule: A **visible label does not guarantee an accessible name** — you must create the
  programmatic association (`<label for>`/`id`, `aria-labelledby`, or `aria-label`).
- Rule: Check the **role permits a name first** — "name-prohibited" roles (`generic`
  `<div>`/`<span>`, `<p>`, `<em>`, `<strong>`, `<mark>`, `<time>`, `caption`, …) **cannot**
  take an accName; `aria-label` on a `<div>` is invalid and ignored.
- Rule: Don't use `aria-label` to provide a *description* — it replaces the name and hides
  the element's purpose. Descriptions belong in `aria-describedby` (see §2.3).
- Rule: When fixing an existing element's name without touching its markup, reach for a
  **higher-priority** method than the one already in play (e.g. add `aria-labelledby` when
  only an unassociated visible `<span>` exists).

**Gotchas**
- Label-in-Name gotcha (`SC 2.5.3`) — when a control has visible text, its accName must
  **contain** that visible text (ideally starting with it) so speech-control users can say
  what they see to activate it. An `aria-label` that doesn't include the visible words
  breaks voice control.
- Translation gotcha — automated translation tools typically **skip `aria-label`** content.
  Screen-reader users may hear the label in a different language than the page. Another
  reason to prefer `aria-labelledby` to real text.
- Name-prohibited gotcha — naming a `<div>`/`<span>` does nothing; if it needs a name, give
  it a real role first (or use the right element).
- Override gotcha — adding `aria-label`/`aria-labelledby` silently discards the element's
  own content as the name; double-check you didn't lose the visible wording.

**WCAG**
- `SC 4.1.2 Name, Role, Value` (Level A) — every interactive element exposes an accessible
  name.
- `SC 2.5.3 Label in Name` (Level A) — the accName contains the visible label text.

### 2.3 Accessible Descriptions — `aria-describedby`

**What & why** — Where the accessible *name* identifies a control ("Password"), the
accessible *description* (accDesc) supplies **supplementary** context — hints,
requirements, format rules, error text. It's announced **after** the name and role
("Password, edit, at least 12 characters"), is optional, and some AT/users may skip it.
`aria-describedby` is the workhorse: it points at one or more on-page elements by `id`, so
the description is the **same text sighted users see**. Keep it for *extra* info — never
stuff it into the name.

**Core usage**
```html
<label for="pw">Create a password</label>
<input type="password" id="pw" aria-describedby="pw-hint">
<p id="pw-hint">At least 12 characters, with one number and one symbol.</p>
```
- Rule: Use `aria-describedby` for hints/instructions/errors — and keep the **`<label>`
  short** by putting longer helper text outside it and associating via `aria-describedby`.
- Rule: It accepts **multiple ids**, concatenated in the order listed. For a field with
  **both an error and instructions**, list the **error id first** so it's announced before
  the hint:
  ```html
  <input id="email" aria-invalid="true"
         aria-describedby="email-error email-hint">
  ```

**Choosing the right attribute**
- Decision: Prefer **`aria-describedby`** (references DOM text) over `aria-description`
  (ARIA 1.3 inline string) when the text exists on the page — the announcement then matches
  what sighted users read, and it translates with the page (like the `aria-label` caveat).
- Decision: **`aria-details`** is *not* a description — AT announces only that extended info
  *exists* and doesn't read or focus it. Use it as a "heads-up" pointer to structured,
  navigable content (e.g. a `<details>` explaining a CVV), never as the accDesc.

**Rules / Key points**
- Anti-pattern: Using `aria-label` to carry a description — it **replaces the name** and
  hides the control's purpose. Name vs description are different jobs (see §2.2).
- Rule: For "**Opens in a new window**"–style link notes, a visually-hidden text node inside
  the link is more reliable than `title`/`aria-describedby`/`aria-description`, which aren't
  consistently announced for links.
- Rule: For dynamic-search inputs, a description like "Results will filter as you type"
  (via `aria-describedby`) is **less noisy and more robust** than making the results a live
  region (see §3.9).

**Gotchas**
- Flattening gotcha — `aria-describedby` content is **flattened to a plain string**;
  structure inside the referenced element (lists, links, headings) **loses its semantics**
  in the announcement (only an image's `alt` survives). Don't reference rich, navigable
  content and expect users to interact with it.
- Inconsistent-announcement gotcha — *whether and when* a description is read varies by
  browser/AT pairing and interaction type. Don't put **critical** information *only* in a
  description; ensure it's also perceivable in the visible content.
- `aria-details`-confusion gotcha — teams reach for `aria-details` expecting it to read the
  content. It doesn't. Use `aria-describedby` if you need the text announced.

**WCAG** — Supports `SC 1.3.1 Info and Relationships` (Level A) by programmatically tying
hints/errors to their field, and underpins accessible error handling for `SC 3.3.1` /
`SC 3.3.3` (see §2.11).

### 2.4 Disclosure State — `aria-expanded` / `aria-controls`

_(collapsed / expanded)_

**What & why** — A **disclosure widget** is the most reusable interactive pattern on the
web — a control (usually a button) that shows/hides content. It's the building block under
accordions, dropdown navs, off-canvas menus, "read more" toggles, and more. The job is to
tell AT whether the controlled content is currently **expanded or collapsed**: a plain
`<button>` has no built-in way to convey that, so you add `aria-expanded`. Master this one
pattern and a large slice of the Advanced tier becomes variations on it.

**Option 1 — native `<details>` / `<summary>`** (no JS)
```html
<details>
  <summary>Trigger label</summary>
  <p>Content revealed when the summary is activated.</p>
</details>
```
- `<summary>` is keyboard-operable (Space + Enter); the browser toggles the `open`
  attribute and exposes the expanded/collapsed state for free; content is found by **Find
  in Page** (auto-expands on match).
- Decision: Use it when you want zero-JS disclosure and the inconsistent cross-AT
  announcement ("button" / "summary" / "disclosure triangle") is acceptable. **Avoid** it
  for patterns that need specific semantics (Tabs, Menus) or where find-in-page
  auto-expand is unwanted (dialogs).

**Option 2 — custom ARIA disclosure** (when you need control)
```html
<div class="disclosure">
  <button aria-expanded="false" aria-controls="panel-1">Trigger label</button>
  <div id="panel-1" hidden><!-- content --></div>
</div>
```
```javascript
trigger.addEventListener("click", () => {
  const expanded = trigger.getAttribute("aria-expanded") === "true";
  trigger.setAttribute("aria-expanded", String(!expanded));
  panel.toggleAttribute("hidden");
});
```
- The trigger is a real `<button>` carrying `aria-expanded`; JS flips the state on
  activation. Style the chevron/panel from the state per §2.1.

**Rules / Key points**
- Rule: `aria-expanded` on a `<button>` does two things — communicates **expanded
  (`true`) / collapsed (`false`)** *and* signals that the button is a disclosure trigger.
- Rule: **Ship the initial state in the HTML** (`aria-expanded="false"`) and update it via
  JS on every toggle — don't add the attribute lazily.
- Rule: Always place the **content panel immediately after its trigger in the DOM** (source
  order), even when using `aria-controls` — so SR and keyboard users flow straight into the
  revealed content.
- Rule: **Progressive enhancement** — render content visible (no button) in the base HTML;
  let JS create the trigger, hide the panel, and manage `aria-expanded`. JavaScript can
  fail; content must be reachable without it.
- Rule: To make a **heading** the disclosure trigger, wrap the heading **around** the
  `<button>` (not vice versa) so the heading semantics survive and the button stays
  interactive.

**Gotchas**
- `aria-controls`-support gotcha — `aria-controls` is **optional and effectively only
  (poorly) supported by JAWS**; most SRs ignore the relationship. It doesn't replace
  good DOM order — keep the panel right after the trigger regardless.
- `<details>`-announcement gotcha — the way `<details>` is announced varies across AT;
  that's normal, not a bug. If you need consistent semantics, use the custom pattern.
- Dragon gotcha — Dragon voice software **deprioritises `<details>`** relative to
  buttons/links, making them harder to activate by voice. A custom button-based disclosure
  avoids this.
- State-marker gotcha — the chevron/icon must be `aria-hidden="true"`; the state is already
  conveyed by `aria-expanded`, so don't let the glyph be announced too (see §2.1).

**WCAG** — Supports `SC 4.1.2 Name, Role, Value` (Level A): the control's **state**
(expanded/collapsed) is exposed and kept in sync.

### 2.5 Current State — `aria-current`

**What & why** — Sighted users see "you are here" through styling — the highlighted nav
link, the active pagination number, today's date in a calendar. `aria-current` conveys that
same "current item in a set" information to AT, so a screen-reader user hears "link, current
page" instead of an undifferentiated "link". It's the right tool whenever one item in a
group is the active/current one, and (per §2.1) it doubles as the CSS highlight hook.

**Core usage**
```html
<nav aria-label="Site">
  <ul role="list">
    <li><a href="/products/" aria-current="page">Products</a></li>
    <li><a href="/team/">Team</a></li>
  </ul>
</nav>
```
```css
a[aria-current="page"] { font-weight: 700; border-bottom: 2px solid; }
```

**The six values**
- `aria-current` accepts: **`page`**, **`step`**, **`location`**, **`date`**, **`time`**,
  and **`true`** (`false` means "not current" and is usually just omitted). Any *unknown*
  value is treated by AT as `true`.

| Value | Use for |
|---|---|
| `page` | Current page in a site nav / breadcrumb |
| `step` | Current step in a multi-step process / wizard |
| `location` | Current location in a flow chart / visual progress |
| `date` / `time` | Current date/time in a calendar or schedule |
| `true` | Current item when none of the specific values fit |

**Rules / Key points**
- Rule: In navigation use **`aria-current="page"`, not `"true"`** — `page` makes SRs
  announce "link, current page"; `true` only yields the vaguer "current".
- Rule: Use the **attribute as the CSS hook** (`a[aria-current="page"]`), not a `.current`
  class — the highlight then only applies when the accessible state is set (see §2.1).
- Rule (nested nav): mark the **current page link** with `aria-current="page"` **and** the
  **active parent item** with `aria-current="true"` — so AT can convey "You are in Products;
  the current page is Kitchen."
- Pattern: Pagination — set `aria-current="page"` on the current page number (see §3.10).
- Rule: Only **one item per set** should carry `aria-current`.

**Gotchas**
- `page`-vs-`true` gotcha — defaulting to `aria-current="true"` in a nav loses the richer
  "current page" announcement. Pick the value that matches the set.
- Live-region-overkill gotcha — don't fire a live-region announcement for a current-item
  change; the state attribute already conveys it. Use `aria-current`, not an alert (see
  §2.7).
- Stale-current gotcha — in SPAs, update `aria-current` on route change and **remove it from
  the previously-current item**, or two items end up marked current.

**WCAG** — Supports `SC 4.1.2 Name, Role, Value` (Level A) by exposing the current-item
**state** that sighted users perceive from styling.

### 2.6 Selected / Pressed / Checked — `aria-selected`, `aria-pressed`, `aria-checked`

**What & why** — These three attributes all express a **binary on/off state** an element is
currently in — but each belongs to a *different role and interaction model*, and they are
not interchangeable. Picking the right one makes AT announce the correct thing ("toggle
button, pressed" vs "tab, selected" vs "checkbox, checked"). As with all state attributes,
JS toggles them and CSS styles from them (§2.1).

**Which one to use**

| Attribute | Use for | AT announces | Native alternative |
|---|---|---|---|
| `aria-pressed` | A **toggle button** (Bold, Mute, dark-theme) | "toggle button, pressed/not pressed" | — (no native toggle button) |
| `aria-checked` | A **checkbox / radio / switch** built in ARIA | "checkbox, checked" / "switch, on" | `<input type="checkbox\|radio">` |
| `aria-selected` | A **selected option** in a composite widget (tab, listbox option, grid cell) | "tab, selected" | — (composite widgets only) |

- Decision: **Prefer the native control first.** For checkable things, `<input
  type="checkbox">` / `type="radio"` give you state, keyboard, and focus for free —
  reach for `aria-checked` only when building a custom control.
- Decision: **Toggle button vs switch** — both are on/off. Use a **toggle button**
  (`aria-pressed`) for "activate/deactivate an action"; use a **switch**
  (`role="switch"` + `aria-checked`) for an explicit on/off setting that takes effect
  immediately.

**Toggle button** (`aria-pressed`)
```html
<button aria-pressed="false">Bold</button>
```
```javascript
btn.addEventListener("click", () => {
  const pressed = btn.getAttribute("aria-pressed") === "true";
  btn.setAttribute("aria-pressed", String(!pressed));
});
```
```css
button[aria-pressed="true"] { background: #ccc; box-shadow: inset 0 0 5px rgba(0,0,0,.15); }
```
- Rule: `aria-pressed` on a `<button>` **changes its mapping** to a *toggle button* in most
  accessibility APIs — so only use it when the control genuinely toggles.
- Rule: A toggle button supports a third value, **`mixed`**, for when it controls multiple
  items with differing values — most toggles only need `true`/`false`.

**`aria-selected`** (composite-widget selection)
- Rule: Only meaningful inside roles that define selection — `tab`/`tablist`,
  `option`/`listbox`, grid cells. Don't sprinkle it on arbitrary buttons. (Tabs detailed in
  §3.4.)

**Gotchas**
- Wrong-attribute gotcha — using `aria-selected` on a toggle button, or `aria-pressed` on a
  tab, makes AT announce the wrong role/state. Match the attribute to the role.
- Custom-checkbox gotcha — `role="checkbox"` + `aria-checked` does **not** give you keyboard
  or click behaviour; ARIA only relabels. You must wire up Space activation and focus
  yourself (`SC 2.1.1`). A native `<input>` avoids all of it.
- State-vs-label gotcha — don't *also* change the visible text to convey state (e.g.
  "Bold" → "Bold (on)") on top of `aria-pressed`; the state attribute already conveys it,
  and changing the accName can break voice control / `SC 2.5.3`.
- Live-region gotcha — don't announce the toggle via a live region; the state attribute
  conveys the change (see §2.7).

**WCAG**
- `SC 4.1.2 Name, Role, Value` (Level A) — the control exposes the correct state.
- `SC 2.1.1 Keyboard` (Level A) — custom ARIA controls must implement their own keyboard
  operation.

### 2.7 Live Regions & Announcements

_(`aria-live`, `role="status"` / `role="alert"`, polite vs assertive)_

**What & why** — Screen readers announce content when the user *moves to* it. When
something changes elsewhere on the page without a reload — a "Saved" toast, a results
count, a validation error, a new chat message — the SR user won't know unless you either
**move focus** to it or designate its container a **live region**. A live region is a
notification channel for AT: text that lands in it is announced automatically. Powerful,
but easy to overuse — they're transient (one-shot, gone forever) and announcements are
inconsistent across AT, so reach for them only when nothing more robust fits.

**There are only two ways to notify AT of a change**
- Rule: **Move focus** to the new content, **or** make its container a **live region**.
  There is no third option.
- Decision: If the new content contains **interactive elements**, **move focus** instead of
  using a live region — live regions flatten content and offer no way to navigate *into*
  them.

**Creating a live region**
```html
<!-- Implicit (a role with built-in live semantics) -->
<div role="status">File saved.</div>          <!-- polite + atomic -->
<div role="alert">Payment declined.</div>      <!-- assertive + atomic -->

<!-- Explicit (aria-live on any container) -->
<div aria-live="polite">Showing 1–10 of 45 results</div>
<div aria-live="assertive">Critical error.</div>   <!-- use sparingly -->
```
- `aria-live` values: **`polite`** (announce when the user pauses), **`assertive`**
  (interrupt immediately), **`off`** (default; same as omitting).
- Rule: **Default to `polite`.** Reserve `assertive`/`alert` for critical, time-sensitive
  messages (errors, session expiry) — it interrupts whatever the SR is saying.

**`role` vs plain `aria-live`**
- Rule: ARIA gives **five** live-region roles — `alert`, `status`, `log`, `marquee`,
  `timer`. Only **`alert`** (implicit `assertive`) and **`status`** (implicit `polite`)
  have good support; `log`/`marquee`/`timer` are poorly supported (`marquee`/`timer` may be
  removed from the spec).
- Rule: Live-region **roles add a spoken label** — some SRs prefix "Alert: …" / "Status:
  …"; plain `aria-live` does not. Roles also accept an **accessible name** (unlike a
  name-prohibited bare `<div aria-live>`), useful when several coexist ("Shopping cart, 5
  items").
- Note: `<output>` is the **only native HTML live region** (implicit `status`/polite,
  labelable) — but cross-AT announcement is inconsistent.

**Critical implementation rules**
- Rule: **Put the (empty) live region in the DOM at load**, then populate it via JS.
  Late-attached live regions may not be monitored.
  ```javascript
  // ✅ region pre-exists; update its text
  document.getElementById("status").textContent = "Saved.";
  // ❌ injecting the region together with its content often isn't announced
  ```
- Rule: **Empty the region before repopulating** it with a new message — improves the odds
  the SR notices the change.
- Rule: A live region works even when **visually hidden** — as long as it's not hidden in a
  way that removes it from the accessibility tree (so not `display:none`).
- Rule: When the message is **visible to everyone**, make that **same visible element** the
  live region rather than mirroring to a separate hidden one.

**Configuration attributes** (support is shaky — don't over-rely)
- `aria-atomic` — `true` announces the **entire** region (good for "Page 3 of 10", "Now
  Playing" where partial updates lose context); `false` (default) announces only the change.
- `aria-relevant` — which changes announce (`additions`, `removals`, `text`, `all`; default
  `additions text`); use `removals`/`all` sparingly.
- `aria-busy="true"` — tells SRs to ignore the region while you batch updates; flip to
  `false` when done so queued changes announce as one unit.
- Rule: Per real-world testing, `aria-relevant`/`aria-atomic`/`aria-busy` have **inconsistent
  cross-AT support** — don't depend on them.

**When NOT to use a live region**
- Anti-pattern: Using a live region **instead of a state attribute** — `aria-expanded`,
  `aria-pressed`, `aria-current` already convey their change (see §2.1, §2.4–2.6).
- Anti-pattern: Wrapping a **whole section** (rich text, links, controls) in a live region
  — it announces as one flat string and can't be navigated.
- Decision: **Filters** — add a persistent instructional cue ("Changing filters updates the
  results below") rather than a live region (§3.7). **Dynamic search** — an
  `aria-describedby` hint ("Results filter as you type") is less noisy than a live region
  (§3.9).
- Rule: Live regions are **transient** — if a persistent UI affordance will do, use that
  instead.

**Gotchas**
- Not-the-`region`-landmark gotcha — a "live region" and the `region` **landmark** are
  unrelated concepts; don't conflate them.
- Rich-content gotcha — headings/lists/links/buttons inside a live region **lose their
  semantics** in the announcement (flat string). Keep live-region content to plain text.
- Visual-chrome gotcha — for an empty pre-placed region, gate its padding/background on
  content: `[aria-live]:not(:empty) { … }`, so the chrome only appears when populated.
- Still-missed gotcha — even correct live regions are missed by some users/AT. Don't make a
  live region the **only** way critical info is perceived; test in your audience's
  browser/SR pairings.

**WCAG** — `SC 4.1.3 Status Messages` (Level AA): status messages can be programmatically
determined (announced) **without receiving focus**.

### 2.8 Hiding Content Correctly

_(visually-hidden vs `hidden` vs `aria-hidden` vs `display:none`)_

**What & why** — "Hiding" isn't one thing. Each technique hides from a *different audience*
— visually, from AT, from the keyboard, or some combination. The whole game is one
question: **who are you hiding from, and who should still have access?** Reach for the
wrong method and you either leak content you meant to hide, or strand AT/keyboard users on
something they can't see. Two cases dominate: hide *visually but keep for AT*
(visually-hidden) vs hide *from everyone* (`hidden` / `display:none`).

**What each technique actually does**

| Technique | Visually hidden? | In a11y tree? | Keyboard reachable? |
|---|---|---|---|
| `opacity: 0` / `clip-path` (still in flow) | Yes | **Yes** | Yes |
| Off-screen `position: absolute` | Yes | **Yes** | Yes (⚠️ bad for interactive) |
| `.visually-hidden` utility | Yes | **Yes** | (static text only) |
| `visibility: hidden` | Yes | No | No |
| `display: none` | Yes (no space) | No | No |
| `hidden` attribute | Yes (no space) | No | No |
| `inert` attribute | **No** (still visible) | No | No |
| `aria-hidden="true"` | **No** (still visible) | No | ⚠️ **still focusable** |

**Pick by intent**
- Decision: Hide from **everyone** (visually + AT + keyboard) → `hidden` attribute or
  `display:none` / `visibility:hidden`.
- Decision: Hide **visually only**, keep for screen readers → the **`.visually-hidden`**
  utility class (for *static text* — e.g. extra label context).
- Decision: Hide **from AT only**, keep visible → `aria-hidden="true"` (decorative icons,
  duplicate visual text) — **never on anything focusable**.
- Decision: Make a **visible** subtree non-interactive and AT-hidden (e.g. background behind
  a modal) → **`inert`** (see §3.1).
- Decision: Strip an element's **semantics only**, keep it visible and in flow →
  `role="none"`/`presentation` (e.g. a layout table, §1.4).

**The visually-hidden utility**
```css
.visually-hidden:not(:focus):not(:active) {
  position: absolute;
  width: 1px; height: 1px;
  overflow: hidden;
  clip-path: inset(50%);
  white-space: nowrap;
}
```
- Rule: Use it for **static supplementary text only** (e.g. a hidden "(opens in new
  window)" or a label for an icon button). The `:not(:focus):not(:active)` guard lets a
  skip link reveal itself on focus.

**Hidden text as an accessible name**
```html
<span id="menu-label" hidden>Menu</span>
<button aria-labelledby="menu-label"><svg aria-hidden="true">…</svg></button>
```
- Rule: When text exists **only** to be an `aria-labelledby` target (not page content),
  hide it with the **`hidden`** attribute, not `.visually-hidden` — `hidden` keeps it out
  of the content flow while `aria-labelledby` still exposes it, avoiding a double
  announcement (see §2.2).

**Gotchas**
- `aria-hidden`-on-focusable gotcha — the dangerous one: `aria-hidden="true"` hides from AT
  but **leaves the element focusable**, so keyboard focus lands on something that announces
  nothing ("focusing nothing"). Never put it on (or around) a focusable element — use
  `inert`/`disabled`, or genuinely remove it. (Ties to §1.6.)
- visually-hidden-on-interactive gotcha — don't apply `.visually-hidden` to interactive
  elements; a 1px-clipped control can't be found by touch SR users exploring by haptics,
  and off-screen positioning has the same problem.
- `display:none`-removes-from-AT gotcha — content hidden with `display:none`/
  `visibility:hidden` / `hidden` is gone from the a11y tree entirely — fine for genuinely
  hidden content, but it means a `display:none` skip link or live region **won't work**.
- `content-visibility:auto` gotcha — inside such a container, CSS hiding isn't applied while
  rendering is postponed; hide descendants from AT via HTML/ARIA instead.

**WCAG** — Supports `SC 1.3.1 Info and Relationships` and `SC 4.1.2 Name, Role, Value`
(Level A) — content exposed to AT must match what's perceivable/operable; hiding techniques
must not desync the two (e.g. hidden-but-focusable controls).

### 2.9 Focus Management Basics

_(move focus on view change, return focus)_

**What & why** — When the page changes in response to a user action — a dialog opens, a
view swaps in an SPA, a form fails validation — focus must go somewhere sensible.
Otherwise focus stays on a control that may have just disappeared, or resets to the top of
the document, leaving keyboard and SR users lost. Good focus management is often a *better*
notification than a live region: moving focus both tells the user where they now are and
puts them where they need to act.

**The two recurring moves**
- Rule: **Move focus** to new/relevant content as an immediate result of a user action.
- Rule: **Return focus** to the triggering control when a transient UI (dialog, drawer,
  menu) closes — so the user lands back where they were.

**When to move focus (prefer over a live region)**
- Open a dialog → move focus **into** the dialog (see §3.1).
- SPA **route change** → move focus to the main content / new `<h1>`.
- **Form validation** → move focus to the error summary's heading, or the first invalid
  field (see §2.11 / §3.6).
- Finishing a multi-step flow → move focus to the confirmation.
- Decision (the §2.7 rule restated): if newly added content contains **interactive
  elements**, **move focus** rather than making it a live region.

**How to move focus to non-interactive content**
```html
<main id="main" tabindex="-1"><h1>…</h1></main>
```
```javascript
// e.g. after an SPA route change
document.querySelector("#main").focus();
```
- Rule: Make a non-interactive target (a heading, an error summary, `<main>`)
  programmatically focusable with **`tabindex="-1"`**, then call `.focus()`. `-1` keeps it
  out of the natural Tab order while allowing scripted focus.
- Rule: Prefer moving focus to the **heading** that introduces the new content rather than a
  big container — focusing a large container makes some SRs (NVDA) read the *entire* thing,
  which is overwhelming.

**Composite widgets are a single tab stop**
- Rule: For tabs, toolbars, menus, radio groups, the group should be **one Tab stop** — Tab
  enters/leaves it, **arrow keys** move within. Native `<select>` and radio groups do this
  for free; custom widgets must replicate it with **roving `tabindex`** (one item
  `tabindex="0"`, rest `-1`; arrows move focus and shift the `0`). Detailed per-component in
  §3.

**Gotchas**
- Unsummoned-focus gotcha — only move focus as an **immediate response to a user action**.
  Don't yank focus to async/delayed UI the user didn't summon (a background toast, a
  late-arriving banner) — it disrupts whatever they were doing.
- Lost-focus gotcha — when you remove/replace the element that had focus (closing a dialog,
  deleting a row), focus falls back to `<body>` and the user is stranded at the top.
  Explicitly move focus to a sensible nearby element.
- Missing-`tabindex="-1"` gotcha — calling `.focus()` on a non-focusable element silently
  does nothing; add `tabindex="-1"` to the target first.
- Container-vs-heading gotcha — focusing the whole results/summary container can trigger a
  long unwanted readout; focus the heading instead.

**WCAG**
- `SC 2.4.3 Focus Order` (Level A) — focus moves in an order that preserves meaning and
  operability.
- `SC 3.2.1 On Focus` (Level A) — moving focus must not trigger an unexpected change of
  context.
- Supports `SC 4.1.3 Status Messages` when focus-move is the chosen notification method
  (see §2.7).

### 2.10 Reduced Motion — `prefers-reduced-motion`

**What & why** — Large or unexpected motion — parallax, big zoom/slide transitions,
auto-playing background video, spinning loaders — can trigger real symptoms for people
with **vestibular disorders** (nausea, dizziness, migraine) and is distracting for many
others. Operating systems expose a "reduce motion" setting; `prefers-reduced-motion` lets
your CSS/JS honour it. The baseline expectation: **respect the user's stated preference**
and never trap them in motion they can't stop.

**Core usage**
```css
/* Default: motion on. Pare it back when the user asks for less. */
.card { transition: transform .3s ease; }

@media (prefers-reduced-motion: reduce) {
  .card { transition: none; }

  /* Belt-and-braces global guard */
  *, *::before, *::after {
    animation-duration: .001ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: .001ms !important;
    scroll-behavior: auto !important;
  }
}
```
```javascript
const reduce = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
if (!reduce) { /* run the JS-driven animation */ }
```

**Rules / Key points**
- Decision: Two authoring styles — **(a)** animate by default and switch motion *off* under
  `reduce`, or **(b)** ship no motion and add it under `(prefers-reduced-motion: no-preference)`.
  Both are valid; (a) is most common, (b) is the safest default.
- Rule: Reduce ≠ remove everything. Often the right move is to **swap a large movement for a
  gentle fade/opacity change**, not strip all feedback. Keep the meaning, drop the
  vestibular trigger.
- Rule: Check the preference in **JS too** (`matchMedia`) for animations you drive with
  JavaScript, the Web Animations API, or libraries — CSS media queries don't cover those.
- Rule: For motion that **plays, auto-updates, or scrolls for more than 5 seconds** (carousels,
  tickers, auto-advancing slides), provide a **pause/stop/hide** control regardless of the
  motion preference (`SC 2.2.2`). See §3.2.

**Gotchas**
- All-or-nothing gotcha — a blanket "kill every animation" rule can break functional UI
  (e.g. an expanding panel that now snaps jarringly, or a loading indicator that vanishes).
  Reduce thoughtfully; keep essential state-change feedback.
- JS-animation gotcha — `prefers-reduced-motion` in CSS does **not** stop JS/library
  animations; you must gate those on `matchMedia` explicitly.
- Reflow gotcha — content that shifts as one section opens and another closes (accordions,
  reflowing layouts) can disorient low-vision, mobile, and vestibular users even without an
  explicit animation. Minimise layout jumps.
- `scroll-behavior`-gotcha — smooth-scroll (`scroll-behavior: smooth`) is motion too; set it
  to `auto` under `reduce`.

**WCAG**
- `SC 2.2.2 Pause, Stop, Hide` (Level A) — moving/auto-updating content lasting > 5s can be
  paused/stopped/hidden.
- `SC 2.3.3 Animation from Interactions` (Level AAA) — motion triggered by interaction can
  be disabled (the core `prefers-reduced-motion` use case).
- `SC 2.3.1 Three Flashes or Below Threshold` (Level A) — nothing flashes more than three
  times per second.

### 2.11 Error Messaging & Validation Basics

**What & why** — When a form rejects input, every user needs to know **what went wrong,
which field, and how to fix it** — and AT users need that conveyed programmatically, not
just with red colour. This section is the Basic-tier mechanics of communicating errors and
required state; the full per-field wiring and patterns live in §3.6. The throughline:
identify the error, associate the message with its field, suggest the fix, and put focus
where the user can act.

**Mark required fields**
```html
<label for="email">
  Email <span aria-hidden="true">*</span>
  <span class="visually-hidden">(required)</span>
</label>
<input type="email" id="email" required aria-required="true">
```
- Rule: Use the native **`required`** attribute (well supported); `aria-required="true"`
  supplements custom widgets.
- Rule: Don't rely on the `*` alone (colour/symbol) — pair it with text ("(required)" or a
  form-level "Fields marked * are required") so it's not colour-only (`SC 1.4.1`, §1.11).

**Don't validate too early**
- Rule: Avoid validating **on blur** (the moment a user leaves a field) — it nags people
  who haven't finished. Validate **on submit** (report everything at once), or inline only
  *after* the user has had a fair chance to complete the field.

**Identify the error programmatically** (`SC 3.3.1`)
```html
<input type="email" id="email" aria-invalid="true" aria-describedby="email-error">
<p id="email-error">Enter an email address like name@example.com.</p>
```
- Rule: Set **`aria-invalid="true"`** on the failing field (and use it as the CSS hook,
  §2.1); **remove** it when the field becomes valid rather than setting `"false"`.
- Rule: Associate the message with the field via **`aria-describedby`** so the error is read
  with the field (§2.3). If a field has both a hint and an error, list the **error id first**.

**Suggest the fix** (`SC 3.3.3`)
- Rule: Don't stop at "Invalid input." Say **how to fix it** — "Enter a date as
  DD/MM/YYYY", "Password needs at least 12 characters." Concrete suggestions help everyone,
  especially cognitive- and motion-impaired users.

**Move focus on failure** (and the error summary)
```html
<div role="alert" aria-labelledby="error-heading" tabindex="-1">
  <h2 id="error-heading">There are 2 problems with this form</h2>
  <ul>
    <li><a href="#email">Email: enter a valid email address.</a></li>
    <li><a href="#phone">Phone: this field is required.</a></li>
  </ul>
</div>
```
- Rule: On submit-with-errors, **move focus** to the error summary (or the first invalid
  field) — see §2.9. Prefer focusing the summary's **heading** over the container.
- Rule: Announce the summary by **moving focus** to it (best when it contains links), **or**
  by making it a live region (best when it doesn't) — not both.
- Rule: Each summary item **links to its field**; activating the link moves focus to the
  invalid input, where `aria-invalid` + `aria-describedby` then convey *that* it's invalid
  and *why*.

**Gotchas**
- Colour-only-error gotcha — a red border alone fails colour-blind users; pair it with an
  icon and text (`SC 1.4.1`, §1.11).
- `required`-announces-invalid gotcha — native `required` makes some browser/SR pairings
  announce a field as invalid **before** the user types. If that bites, set
  `aria-invalid="false"` initially (or prefer `aria-required`).
- Don't-disable-Submit gotcha — don't disable the submit button until the form is "valid";
  disabled buttons drop out of the tab order, go low-contrast, and confuse users. Let them
  submit and surface the errors (§2.12).
- Still-missed gotcha — even with `role="alert"`, some users miss inline errors; the error
  summary + focus move is the robust path. Test in your audience's browser/SR pairings.

**WCAG**
- `SC 3.3.1 Error Identification` (Level A) — errors are identified and described in text.
- `SC 3.3.3 Error Suggestion` (Level AA) — suggest a correction when one is known.
- `SC 3.3.4 Error Prevention` (Level AA) — for legal/financial actions, allow
  reverse/check/confirm before committing.
- `SC 3.3.2 Labels or Instructions` (Level A) / `SC 1.4.1 Use of Color` (Level A).

### 2.12 `disabled` vs `aria-disabled`

**What & why** — Both express "this control isn't available right now", but they behave very
differently. The native **`disabled`** attribute fully deactivates a control — but it also
**removes it from the tab order**, so keyboard and SR users can't reach it to discover *why*
it's unavailable. **`aria-disabled="true"`** marks the state for AT while leaving the
element **focusable and discoverable** (you suppress its action in JS). Knowing which to
reach for — and often *not* disabling at all — is the skill here.

**The difference**

| | `disabled` (HTML) | `aria-disabled="true"` (ARIA) |
|---|---|---|
| Where | Form controls (`<button>`, `<input>`, `<select>`, `<fieldset>`) | Any element (incl. custom widgets) |
| Focusable / in tab order | **No** — removed | **Yes** — stays reachable |
| Blocks interaction | Yes, natively | No — **you** must prevent the action in JS |
| Announced to AT | "dimmed/unavailable" | "dimmed/unavailable" |
| Contrast requirement | Exempt from `SC 1.4.3` | Not exempt (it's still "active") |

**Rules / Key points**
- Decision: Use native **`disabled`** for genuinely inert form controls where the user
  doesn't need to reach or understand them. Use **`aria-disabled`** when the control should
  remain **discoverable** — so users can focus it, read it, and learn what to do to enable
  it (then block the action in JS).
- Rule: **Links can't be disabled** with `disabled` (it only applies to form controls). To
  "disable" a link: remove `href`, restore `role="link"`, and add `aria-disabled="true"`.
- Rule: `disabled` on a **`<fieldset>`** cascades to all descendant controls (except those
  inside the first `<legend>`) — a quick way to disable a whole group.
- Rule: **Style disabled controls yourself.** Browsers default to low-contrast grey;
  restore enough contrast to keep them legible (the `SC 1.4.3` exemption is technical, not
  a licence to make them invisible).

**Prefer not disabling at all**
- Anti-pattern: **Disabling the Submit button** until the form is "complete/valid".
  Disabled buttons drop out of the tab order, go low-contrast, are invisible to many SR
  users, and confuse cognitive/learning-disabled users — they can't tell *why* they're
  stuck. Let the user submit, then surface errors (§2.11).
- Decision: When you must show "not yet available", an `aria-disabled` control with a clear
  explanation usually beats a hard `disabled` — the user can still find it and understand it.

**Gotchas**
- Unreachable-disabled gotcha — a `disabled` control can't be Tab-reached, so any tooltip
  /explanation attached to it is undiscoverable by keyboard users. Use `aria-disabled` if
  the *why* matters.
- `aria-disabled`-does-nothing-functionally gotcha — it only **announces** the state; the
  element stays clickable/operable unless you `preventDefault()`/return early in your
  handler. Forgetting this ships a "disabled" button that still fires.
- Contrast gotcha — don't lean on the `SC 1.4.3` exemption to justify unreadable grey;
  it's still a real usability barrier for low-vision users.

**WCAG**
- `SC 4.1.2 Name, Role, Value` (Level A) — the disabled **state** is exposed correctly.
- `SC 1.4.3 Contrast (Minimum)` (Level AA) — `disabled` controls are exempt, but
  `aria-disabled` ones are not; either way, aim for legibility beyond conformance.

---

## 3. Advanced — Component-Specific Patterns

### 3.0 A Repeatable Method for Any Component

_(native-first decision → anatomy → roles → keyboard model → focus management →
states → gotchas → what AT announces)_

**What & why** — The Minimum and Basic tiers give you the building blocks; the Advanced tier
is about assembling them correctly for a *specific* component. Rather than memorise every
widget, internalise one **repeatable method** and run any new component through it — modal,
slider, mega-menu, or something nobody's built before. Each §3.x mini-section below is just
this method pre-answered for a common pattern. The anchor reference for the whole tier is
the **W3C ARIA Authoring Practices Guide (APG)**, which documents the expected roles,
states, and keyboard model for each named pattern.

> **Two governing principles.** *"No ARIA is better than bad ARIA"* — the 2022 WebAIM
> Million found pages **with** ARIA had ~70% **more** detected errors. And *"a role is a
> promise"* — declaring a role commits you to delivering the entire behaviour that role
> implies. Both push you toward less custom work and more native HTML.

**The method — eleven steps**

**1. Native-first triage** *(Rule 1 of ARIA)*
Ask: can a **native element**, or a composition of natives, do this? `<button>`,
`<details>`, `<dialog>`, `<select>`, `<input type="…">` ship role, state, keyboard, and
focus for free. Only build custom when (a) the feature doesn't exist in HTML, (b) native
can't be styled as required, or (c) native a11y support is genuinely broken. This step
exists to help you *avoid* the next ten.

**2. Find the established pattern** *(don't invent)*
Map the component to a **named APG pattern** (dialog, tabs, combobox, disclosure, menu,
slider, …). Take its prescribed roles, states, and keyboard interactions as your spec.
Inventing a novel interaction model is itself an accessibility risk — users rely on
learned conventions.

**3. Map anatomy → roles** *(Rule 2 — don't change native semantics unless you must)*
Break the component into parts; assign each its role. Put ARIA roles on **wrapper**
elements, never on meaningful semantic ones — `<div role="tab"><h2>Title</h2></div>`, not
`<h2 role="tab">`. List the parts explicitly (trigger, panel, group, item…) so nothing is
left unnamed or unroled.

**4. Define the keyboard interaction model** *(Rule 3 — must be keyboard operable, `SC 2.1.1`)*
Spell out **every** key the pattern expects: **Tab** (enter/leave the widget), **arrows**
(move within), **Enter/Space** (activate — mind the keydown-vs-keyup difference), **Esc**
(dismiss), **Home/End**, and typeahead where relevant. Anything operable by click/tap must
be operable by keyboard. This is where most custom widgets fail — treat it as
non-negotiable.

**5. Plan focus management**
Decide what gets focus **on open, on action, and on close**. Composite widgets (tabs,
toolbars, menus) act as a **single tab stop** via roving `tabindex` (§2.9); overlays move
focus **in** on open and **return** it to the trigger on close (§3.1). *Rule 4:* never put
`aria-hidden`/`role="presentation"` on a focusable element — focus would land on "nothing".

**6. Wire states & properties — and drive visuals from them**
Identify which states apply (expanded / selected / pressed / checked / current / disabled /
invalid) and keep them in sync with reality. Style **from the attribute** (§2.1) so the
visual and accessible states can't drift apart.

**7. Name everything** *(Rule 5 — every interactive element has an accessible name)*
Each interactive part gets an accessible name (§2.2). Give composite widgets, dialogs, and
groups a **group/region name** too, so AT can announce the container's purpose.

**8. Decide dynamic announcements**
For anything that changes without a reload (results updated, item added, error shown),
choose deliberately: **move focus** *or* a **live region** (§2.7 / §2.9) — and prefer
focus-move when the new content is interactive. Don't reach for a live region by default.

**9. Build for resilience — progressive enhancement**
Make the component **work, or degrade gracefully, without JavaScript** where feasible;
content must stay reachable if scripts fail. Enhance a semantic baseline rather than
assembling the widget from inert `<div>`s.

**10. Visual & sensory robustness**
Confirm: visible focus indicator (§1.7), text/UI contrast (§1.11), Forced Colors / Windows
High Contrast Mode, reduced motion (§2.10), adequate touch-target size, and no loss at 200%
zoom / on reflow.

**11. Verify** *(the W3C "Custom Control" checklist)*
Run the component against:
- ☐ Focusable
- ☐ Keyboard operable (expected keys)
- ☐ Touch operable
- ☐ Expected key behaviour (matches the native/APG model)
- ☐ Visible focus indicator
- ☐ Accessible name (label)
- ☐ Correct role
- ☐ States and properties exposed
- ☐ Sufficient colour contrast
- ☐ Works in High Contrast / Forced Colors mode

Then: a **keyboard-only** pass, a **screen-reader** pass across the real browser/AT
pairings your audience uses, an **automated** check (axe/Lighthouse, §4), and — ideally —
**usability testing with disabled and AT users** (technically conformant ≠ actually usable).

**How the mini-sections use this** — each §3.x below answers steps 2–6 for a specific
component (its pattern, anatomy/roles, keyboard model, focus management, and states), then
calls out the component-specific gotchas. Steps 1 and 7–11 are largely the same every time
and live here.

### 3.1 Modal Dialog & Alertdialog

**What & why** — A **modal** dialog demands attention: while it's open, the rest of the page
is inert — you can't interact with anything behind it until you act on or dismiss the
dialog. That makes focus management the heart of the pattern: trap focus inside, return it
on close, and tell AT the background is unavailable. Get those wrong and a SR user "escapes"
into hidden page content, or a keyboard user is stranded. (`alertdialog` is the same machine
with an urgent message that *requires* a response.)

**Native-first** *(method step 1)*
- Decision: Prefer the native **`<dialog>`** element in **modal mode** (`.showModal()`). It
  provides the **inert backdrop**, Esc-to-close, focus entry, and the top layer for free —
  sparing you the DOM-traversal + `inert` plumbing a custom dialog needs. Reach for a custom
  `role="dialog"` only when `<dialog>` can't be styled/structured as required.

**Pattern, anatomy & roles** *(steps 2–3, per W3C APG)*
```html
<div role="dialog" aria-modal="true" aria-labelledby="dlg-title" aria-describedby="dlg-desc">
  <h2 id="dlg-title">Dialog title</h2>
  <p id="dlg-desc">Primary message / purpose of the dialog.</p>
  <!-- focusable content … -->
  <button>Cancel</button>
  <button>Confirm</button>
</div>
```
- `role="dialog"` (or `role="alertdialog"`) on the container.
- `aria-modal="true"` — tells AT the windows beneath are unavailable (inert). It **replaces**
  the older "`aria-hidden` everything else" technique.
- `aria-labelledby` → the dialog **title** (gives it an accessible name). Dialogs benefit
  from a name (§2.2).
- `aria-describedby` → static descriptive text **when there is some**; omit it for a
  form-only dialog (e.g. an "Add address" form) that has no descriptive prose.

**Keyboard model** *(step 4)*
| Key | Behaviour |
|---|---|
| **Tab** | Move to next focusable element; **wraps** from last → first |
| **Shift + Tab** | Move to previous; **wraps** from first → last |
| **Escape** | Closes the dialog |

Focus is **trapped** within the dialog while it's open.

**Focus management** *(step 5 — the crux)*
- Rule: **On open**, move focus to the **first focusable element** (often the first field).
  For a long dialog whose first control sits below the fold, instead focus the first
  paragraph by giving it `tabindex="-1"` — so the top of the content isn't hidden below the
  viewport.
- Rule: **While open**, trap focus — Tab/Shift+Tab cycle within the dialog; background
  content is not reachable.
- Rule: **On close**, **return focus to the trigger** that opened the dialog, preserving the
  user's point of regard.
- Rule: Make the background **inert** — native `<dialog>` modal mode does this for you; for a
  custom dialog, add the **`inert`** attribute to (or `aria-hidden` on) the rest of the page,
  and **dim/obscure** it visually as a cue (§2.8). Manually tab-test that focus can't reach
  anything behind the dialog.

**`alertdialog` variant**
- Decision: Use **`role="alertdialog"`** (a dialog + alert mashup) when an alert is
  **interactive** and must take focus and a response — e.g. "Discard unsaved changes?
  [Cancel] [Discard]". It replaces fragile toast-with-buttons patterns. Same keyboard/focus
  rules as a modal dialog; reference the alert message via `aria-describedby`.
- Rule: A plain `role="alert"` should **not** require dismissal or move focus — if focus must
  move, it's an `alertdialog`, not an `alert` (§2.7).

**Gotchas**
- Don't-focus-the-dialog-itself gotcha — don't put initial focus on the dialog *container*;
  some SRs then announce its entire contents, and the focus location is unclear. Focus the
  first control (or first paragraph via `tabindex="-1"`).
- Double-announce gotcha — if the first paragraph is both focusable and inside the
  `aria-describedby` target, some SRs announce it twice. Usually an acceptable trade-off.
- Weak-inert gotcha — CSS dimming alone does **not** make the background inert; keyboard/SR
  users still reach it. Use `inert` / `hidden` / `display:none`, and tab-test to confirm.
- `aria-modal`-support gotcha — `aria-modal` is relatively new (ARIA 1.1) and support varies;
  native `<dialog>` is the more robust route to true inert-background behaviour.
- Mobile-scroll gotcha — on touch, let the dialog fill the viewport (100%) so background
  movement isn't visible/scrollable behind it.

**WCAG** — `SC 2.4.3 Focus Order` (A), `SC 2.1.2 No Keyboard Trap` (A — the dialog's *managed*
trap with Esc is the legitimate exception), `SC 4.1.2 Name, Role, Value` (A); `alertdialog`
for errors is an advisory technique for `SC 4.1.3 Status Messages` (AA).

### 3.2 Carousel / Slider

**What & why** — A carousel cycles through a set of slides, often **auto-rotating**. That
auto-motion is the core accessibility problem: it's a moving target for screen-reader and
keyboard users, a vestibular trigger (§2.10), and it can advance content out from under
someone mid-read. The pattern is mostly about **giving the user control of the motion** and
**naming the parts** so they can navigate deliberately. Note: there is **no `role="carousel"`**
— ARIA is finite — so you compose it from a labelled group/region plus standard controls.

**Pattern, anatomy & roles** *(steps 2–3, per W3C APG)*
- Container: `role="region"` or `role="group"` + **`aria-roledescription="carousel"`** +
  `aria-label`/`aria-labelledby` (the label **omits** the word "carousel" to avoid
  doubling with the roledescription).
- **Rotation control** (play/pause) — a native `<button>`, **first in the tab order**, whose
  **label changes**: "Stop slide rotation" ↔ "Start slide rotation". No `aria-pressed`.
- **Previous / Next** — native buttons; activation **does not move focus** (so a user can
  press repeatedly).
- Slides (basic/grouped): `role="group"` + **`aria-roledescription="slide"`** +
  `aria-label` (e.g. "3 of 10"; label omits "slide").
- Optional **slide picker**: either the **tabs** pattern (slides become `role="tabpanel"`,
  picker is a `tablist`/`tab`, see §3.4) or a **grouped** button set (`role="group"`, current
  button `aria-disabled="true"`).

```html
<section aria-roledescription="carousel" aria-label="Featured articles">
  <button>Stop slide rotation</button>            <!-- rotation control, first -->
  <div aria-atomic="false" aria-live="off">        <!-- "off" while rotating; "polite" when stopped -->
    <div role="group" aria-roledescription="slide" aria-label="1 of 5">…</div>
    …
  </div>
  <button aria-label="Previous slide">‹</button>
  <button aria-label="Next slide">›</button>
</section>
```

**Auto-rotation requirements** *(the crux)*
- Rule: Provide a **play/pause button** to stop and restart rotation — critical for AT users
  in modes that move neither focus nor mouse (`SC 2.2.2 Pause, Stop, Hide`).
- Rule: **Stop rotation on mouse hover** over the carousel **and on keyboard focus entering
  any carousel element** — resume only by explicit user activation.
- Rule: Manage the live region: **`aria-live="off"` while auto-rotating** (so slides don't
  fire disorienting announcements), and **`aria-live="polite"` once stopped** (so the user
  can explore at their pace). Wrap the slides with `aria-atomic="false"`.
- Rule: Respect `prefers-reduced-motion` — consider **not auto-rotating at all** for users
  who've asked for reduced motion (§2.10).

**Keyboard model** *(step 4)*
- **Tab / Shift+Tab** move through the carousel's controls and content in DOM order — the
  rotation control comes first so it's easy to find.
- Prev/Next/rotation buttons follow the **button** pattern (Enter/Space); their activation
  **doesn't move focus**, allowing repeat presses.
- A **tab-based** slide picker follows the full **tabs** keyboard model (arrows to move, see
  §3.4).

**Focus management** *(step 5)*
- Rule: Auto-rotation **must pause** the moment focus enters the carousel, so focus never
  lands on a slide that then rotates away.
- Rule: Don't move focus on Prev/Next activation — keep it on the pressed control.

**Gotchas**
- Rotate-away gotcha — a SR user reading slide 1 loses context if rotation advances to slide
  2 between their commands. Pausing on focus/hover and `aria-live="off"` while rotating
  prevent this.
- Hidden-slides gotcha — off-screen/inactive slides that aren't properly hidden confuse SRs
  (they read content the user can't see). Manage slide visibility in the DOM (`hidden` /
  `display:none`), not just by positioning.
- Made-up-role gotcha — there is no `role="carousel"`/`role="slide"`; use
  `aria-roledescription` on a group/region instead. Inventing roles is invalid (ARIA is
  finite).
- Redundant-label gotcha — including "carousel"/"slide" in the label doubles with
  `aria-roledescription` ("carousel, Featured articles carousel"). Omit the pattern word.
- No-`setsize`/`posinset` gotcha — `group`-role slides can't use `aria-setsize`/
  `aria-posinset`; the "X of Y" label is the fallback for conveying position.

**WCAG** — `SC 2.2.2 Pause, Stop, Hide` (A — the headline requirement), `SC 2.3.3 Animation
from Interactions` (AAA, via reduced motion), `SC 4.1.2 Name, Role, Value` (A), `SC 2.1.1
Keyboard` (A).

### 3.3 Dropdown Navigation & Menu / Menubar

**What & why** — This is the section where picking the **wrong pattern** is the biggest
risk. "Dropdown menu" describes two very different things, and the ARIA `menu`/`menubar`
roles are **not** for site navigation. Choose the pattern by what the thing *does*, then
implement that pattern's full contract.

**The critical decision — navigation vs. action menu** *(method step 2)*

| If it… | Use… |
|---|---|
| Navigates to pages/sections (links) — a site nav dropdown / mega-menu | **Disclosure navigation** (Pattern A) |
| Performs **actions/commands** like a desktop app's File/Edit menu or a right-click context menu | **`menu`/`menubar`** (Pattern B) |

- Rule: Don't use `menu`/`menubar`/`menuitem` roles for site navigation. They describe
  **OS-style action menus**; they put SRs into application mode, **disable normal reading
  keys**, and commit you to the full arrow-key composite-widget contract that navigation
  doesn't need. Per APG: site nav "does not use the menu role because it does not provide
  the complex functionality that assistive technologies expect." Aligns with *"no ARIA is
  better than bad ARIA"* (§3.0).

---

#### Pattern A — Disclosure Navigation *(recommended for site nav, per W3C APG)*

**Anatomy & roles** *(steps 3, 6)*
- A `<nav>` landmark wrapping `<ul>`/`<li>`; **plain `<a>` links** (no `menuitem` roles).
- Each top-level item that opens a submenu is a real **`<button>`** carrying:
  - **`aria-expanded`** (`false`/`true`) — open/collapsed state.
  - **`aria-controls`** → the id of the submenu it controls.
- Current page link: `aria-current="page"` (§2.5).

```html
<nav aria-label="Main">
  <ul>
    <li>
      <button aria-expanded="false" aria-controls="sub-products">Products</button>
      <ul id="sub-products"> … <li><a href="…">Kitchen</a></li> … </ul>
    </li>
  </ul>
</nav>
```

**Keyboard model** *(step 4)* — it's just a disclosure (§2.4), so it stays in the **normal
tab order**:
- **Tab / Shift+Tab** — move among the buttons; into/through the links when a dropdown is open.
- **Enter / Space** — toggle the button's submenu.
- **Escape** — close the open dropdown and return focus to its controlling button.
- **Arrow keys** — *optional* enhancement only (supplement tabbing); not required.

**Focus management** *(step 5)*
- Rule: On expand, **focus stays on the button**; the user tabs into the links.
- Rule: **Escape** closes the dropdown and returns focus to the controlling button.
- Rule: Moving focus **out of the nav region closes** any open dropdown (needed for `SC
  1.4.13 Content on Hover or Focus`).
- Rule: If opening on **hover**, keep `aria-expanded` in sync, ensure Esc dismisses, make
  the dropdown hoverable, and add hover-intent so a passing pointer doesn't trigger it.

---

#### Pattern B — Menu / Menubar *(application action menus only, per W3C APG)*

**Anatomy & roles** *(steps 3, 6)*
- Trigger (menu button): a `<button>` with **`aria-haspopup="menu"`** + **`aria-expanded`**.
- Container: `role="menu"` (popup) or `role="menubar"` (persistent, usually horizontal,
  `aria-orientation` defaults horizontal); label via `aria-labelledby`/`aria-label`.
- Items: `role="menuitem"`, or `role="menuitemcheckbox"`/`menuitemradio"` (with
  `aria-checked`). A parent item with a submenu gets `aria-haspopup` + `aria-expanded`; the
  submenu `menu` is the **sibling immediately after** its parent item.

**Keyboard model** *(step 4 — a composite widget; Tab does NOT move within it)*
- **Arrow keys** move focus among items (Down/Up in a menu; Left/Right in a menubar;
  Right/Left open/close submenus).
- **Enter** activates an item (or opens a submenu + focuses its first item).
- **Space** — optional toggle for checkbox/radio items.
- **Home / End** — first/last item. **Character typeahead** — jump to the next item starting
  with that letter.
- **Escape** — close the menu and return focus to the menu button / parent item.
- **Tab / Shift+Tab** — exit the menu entirely (closing it).

**Focus management** *(step 5)*
- Rule: On open, focus the **first item**. Use **roving `tabindex`** (or
  `aria-activedescendant`) so the menu is a single tab stop (§2.9).
- Rule: On close (Esc/Tab/activation), **return focus** to the triggering button.
- Rule: Disabled items are **focusable but not activatable** (`aria-disabled="true"`).

**Gotchas**
- Wrong-pattern gotcha — the headline one: using `menu`/`menubar` for links breaks normal
  SR reading and burdens you with arrow-key handling navigation never needed. Default to
  disclosure for nav.
- Made-up-role gotcha — there's no `role="navigation-menu"`; compose nav from `<nav>` + lists
  + disclosure buttons.
- `menuitem`-on-`<li>` gotcha — if you *do* build a true menu, put `menuitem` on the
  interactive element (the link/button), **not** on the wrapping `<li>`.
- Hover-only gotcha — never open dropdowns **only** on hover; that excludes keyboard and
  fine-motor users. Wire a button + `aria-expanded` and treat hover as an enhancement.
- Focus-leaves-open gotcha — a dropdown that stays open after focus leaves the nav can
  obscure focused content elsewhere (risks `SC 2.4.11`); close it on focus-out and on Esc.

**WCAG** — `SC 4.1.2 Name, Role, Value` (A), `SC 2.1.1 Keyboard` (A), `SC 1.4.13 Content on
Hover or Focus` (AA — dismissible on Esc), `SC 2.4.11 Focus Not Obscured` (AA).

### 3.4 Tabs

**What & why** — Tabs show one panel at a time from a set, switched via a row of tab
controls. It's a **composite widget**: the tab row is a single tab stop you arrow within,
and there's no native HTML element for it — you compose it from three ARIA roles and supply
**all** the behaviour in JavaScript (the roles add none). The two things people most often
get wrong are the roving-focus keyboard model and the automatic-vs-manual activation choice.

**Anatomy & roles** *(steps 2–3, per W3C APG)*
- **`role="tablist"`** on the container (no native element maps to it; usually a `<div>`).
  Label it with `aria-label`/`aria-labelledby`; `aria-orientation="vertical"` for vertical
  tabs (default horizontal).
- **`role="tab"`** on each tab — typically a `<button role="tab">`. Each tab:
  - **`aria-selected="true"`** on the active tab, `"false"` on the rest.
  - **`aria-controls`** → its panel's id.
  - A `tab` **must** be inside a `tablist` (parent–child constraint).
- **`role="tabpanel"`** on each panel — typically a `<section role="tabpanel">` —
  **`aria-labelledby`** → its tab's id.

```html
<div role="tablist" aria-label="Account settings">
  <button role="tab" aria-selected="true"  aria-controls="p1" id="t1" tabindex="0">Profile</button>
  <button role="tab" aria-selected="false" aria-controls="p2" id="t2" tabindex="-1">Billing</button>
</div>
<section role="tabpanel" id="p1" aria-labelledby="t1" tabindex="0">…</section>
<section role="tabpanel" id="p2" aria-labelledby="t2" hidden>…</section>
```

**Keyboard model** *(step 4)*
- **Tab** moves focus **into** the tablist (landing on the **active** tab), then **out** to
  the panel (or its first focusable child) — it does **not** step through every tab.
- **Left/Right** (horizontal) or **Up/Down** (vertical) move focus between tabs, **wrapping**
  first↔last. A horizontal tablist must **not** hijack Up/Down (preserve page scroll).
- **Home / End** (optional) — first/last tab.
- **Delete** (optional) — close a removable tab + its panel, moving focus to an adjacent tab.

**Activation mode** *(key decision)*
- Decision: **Automatic activation** — the panel switches as focus moves with arrows.
  Recommended **when panels are preloaded** and switch with no latency (the common case).
- Decision: **Manual activation** — arrows move focus only; **Enter/Space** selects.
  Use when activating a tab is **expensive** (lazy-loads, network) so arrowing past tabs
  doesn't fire loads.

**Focus management** *(step 5)*
- Rule: **Roving `tabindex`** — the active tab is `tabindex="0"`, all others `tabindex="-1"`;
  arrows move focus and shift the `0` (§2.9). The tablist is one tab stop.
- Rule: Give the **tabpanel `tabindex="0"`** *only when it has no focusable children* — so
  it's still reachable by Tab. If it contains focusable content, leave it off.

**Gotchas**
- Don't-fake-tabs-from-`<details>` gotcha — visually styling `<details>`/`<summary>` (or a
  nav list) as tabs gives SR users a confusing experience; Tabs have specific semantics and
  behaviour `<summary>` doesn't fulfil. Use the real pattern.
- Tab-outside-tablist gotcha — `role="tab"` inside a `<nav><ul><li><a>` (no `tablist`) is
  **invalid**; the parent–child relationship is required.
- Every-tab-is-a-tab-stop gotcha — without roving tabindex, Tab walks through *every* tab,
  defeating the single-stop model. Implement the roving algorithm.
- Latency gotcha — automatic activation with slow-loading panels makes arrow navigation
  painful; switch to manual activation for expensive panels.
- Semantics-on-wrapper gotcha — prefer `<div role="tab"><h2>Title</h2></div>` over
  `<h2 role="tab">` so the heading semantics survive (Rule 2, §3.0).

**WCAG** — `SC 4.1.2 Name, Role, Value` (A), `SC 2.1.1 Keyboard` (A), `SC 2.4.3 Focus Order`
(A).

### 3.5 Accordion / Disclosure

**What & why** — An accordion is, at its core, a **group of disclosure widgets** (§2.4) —
collapsible related sections, used to save space. So §2.4 is the foundation; this section
adds what makes it an *accordion*: grouping it, naming the group, the "interactive heading"
markup, and the (often overused) exclusive variant. Keep `aria-expanded` driving both state
and CSS (§2.1).

**Anatomy & roles** *(steps 2–3, per W3C APG)*
- Each section = an **accordion header** (a `<button>` that toggles) + a **panel**.
- Rule: Wrap each header button in a **real heading** (`<h2>`–`<h6>`) at the level that fits
  the page's IA — so the accordion participates in heading navigation (§1.3).
- The button: **`aria-expanded`** (`true`/`false`) + **`aria-controls`** → its panel id.
- The panel: **`aria-labelledby`** → its header button's id; optionally `role="region"`
  (but **drop the region role past ~6 panels** to avoid landmark proliferation).
- Name the **group**: a named `<section>` (if it should be a page landmark) or a
  `<div role="group">` (logical group, not in the outline), named via `aria-labelledby` →
  a visible heading.

```html
<h3>
  <button aria-expanded="false" aria-controls="p1" id="h1">Shipping</button>
</h3>
<div role="region" id="p1" aria-labelledby="h1" hidden> … </div>
```

**Native vs. custom** *(step 1)*
- Decision: For a **non-exclusive** accordion, a series of `<details>`/`<summary>` in a
  named container is the no-JS baseline. For an **exclusive** accordion (one open at a
  time), give every `<details>` the **same non-empty `name`** — the browser enforces "at
  most one open", no JS required.
- Decision: Reach for the **custom button pattern** (above) when you need exact-exclusive
  behaviour, bulk expand/collapse, custom animation, or the most consistent heading
  exposure — `name` only works on native `<details>`, so custom widgets need JS for
  exclusivity.

**The interactive-heading problem** *(a headline accordion gotcha)*
A heading is text and can't be activated; you need an interactive element inside it.
- ✅ Correct: **heading wraps the button** — `<h3><button aria-expanded …>…</button></h3>`.
  Keeps heading semantics *and* an interactive trigger; most consistent across AT.
- ❌ `<h2 role="button">` — doesn't make the heading interactive; defeats the heading.
- ❌ `<summary><h3>…</h3></summary>` — the button role's Children-Presentational property
  can suppress the heading's semantics.
- ❌ `<h3><summary>…</summary></h3>` — `<summary>` is no longer `<details>`'s first child,
  so it stops being the trigger.

**Keyboard model** *(step 4)* — it's disclosures in the **normal tab order**:
- **Enter / Space** — toggle the focused header's panel.
- **Tab / Shift+Tab** — move between headers and into panel content (all focusable elements
  are in the page tab sequence).
- **Down/Up between headers** and **Home/End** are **optional** enhancements, not required.

**Focus management** *(step 5)* — none special: no trapping, no focus move on toggle. Just
keep `aria-expanded` accurate.

**Exclusive accordions — use sparingly**
- Decision: If it doesn't *need* to be exclusive, **don't make it exclusive** — it's more
  inclusive open-by-default. The HTML standard itself advises weighing this before using
  `name`.
- Why: exclusive accordions break heading-based navigation (not all content can be open),
  raise cognitive load (can't compare two sections), and cost keyboard users dozens of
  keystrokes to compare sections. Reach for exclusive only when usability testing supports
  it.

**Find-in-page**
- Native `<details>`: Chromium **auto-expands** a section when its hidden text matches a
  find-in-page search — content stays discoverable.
- Custom widgets: panels hidden with `display:none`/plain `hidden` are **not** findable. Use
  **`hidden="until-found"`** so supporting browsers can search and auto-expand them (a
  progressive enhancement; mind the reset-CSS and generated-box gotchas).

**Gotchas**
- Wonky-heading gotcha — putting headings inside triggers can scramble heading levels; keep
  levels reflecting real IA (§1.3) and use the heading-wraps-button markup.
- Reflow gotcha — content shifting as one section opens/another closes disorients low-vision,
  mobile, and vestibular users; state also resets on reload. Minimise jumps (§2.10).
- Dragon gotcha — Dragon deprioritises `<details>`; a custom button-based accordion is
  easier to activate by voice.
- `hidden="until-found"` reset gotcha — `[hidden]{display:none!important}` overrides it; use
  `[hidden]:not([hidden="until-found"]){…}` and move box styles to an inner container.

**WCAG** — `SC 4.1.2 Name, Role, Value` (A), `SC 1.3.1 Info and Relationships` (A — heading
structure), `SC 2.1.1 Keyboard` (A).

### 3.6 Forms & Form Validation

**What & why** — Forms are where users *do* things, and the most-failed area of the web
(35.8% of inputs unlabelled). The fundamentals live earlier — **labelling in §1.9**,
**error basics in §2.11**, grouping in §1.4, naming/descriptions in §2.2–§2.3, live regions
in §2.7, the disabled-submit anti-pattern in §2.12. This section assembles those into a
**component-level** view and adds the advanced parts: custom-styled native controls,
required-group nuances, input purpose & mobile ergonomics, native validation, the
end-to-end error flow, and multi-step forms. (Custom select/combobox → §3.9.)

#### Custom-styled native controls *(checkbox / radio / select)*
When CSS can't style a native control as needed (e.g. an animated checkmark, Forced-Colors
adaptation), **replace the visuals but keep the native control as the source of truth** —
the "inclusive-hide" technique.
- Rule: Put the `<input>` and an inline **`<svg aria-hidden="true">`** *both inside the
  `<label>`*, SVG **after** the input so adjacent-sibling selectors can target it (wrapping
  inside the label also enlarges the hit area).
- Rule: Hide the input *inclusively*, not with `.visually-hidden` and not off-canvas:
  ```css
  label { position: relative; }
  input[type="checkbox"] { position: absolute; opacity: 0; width: 1em; height: 1em; }
  input[type="checkbox"]:checked        + svg { /* checked look */ }
  input[type="checkbox"]:focus-visible  + svg { outline: 3px solid; outline-offset: 2px; }
  input[type="checkbox"]:disabled       + svg { /* dimmed */ }
  @media (forced-colors: active) { /* re-paint the SVG so it stays visible */ }
  ```
- Rule: Render **every native state**: checked, unchecked, disabled, focus, hover, and
  indeterminate where applicable.
- Gotcha: `.visually-hidden` (1px clip) or off-canvas positioning makes the real control
  **unreachable by touch SR** (TalkBack) — the inclusive-hide keeps it in place in the
  viewport.

#### Grouping & required groups
- Rule: Group radio/checkbox sets with **`<fieldset>` + `<legend>`** (§1.4/§1.9); prefer it
  over `role="group"` (weak mobile-AT support).
- Rule: To mark a **radio group required**, you can't use `required`/`aria-required` on a
  plain `<fieldset>`. Override its role: **`role="radiogroup"` + `aria-required="true"`** on
  the fieldset (note: `required` isn't valid on `radiogroup` either).

#### Input purpose & mobile ergonomics
- Rule: Set **`autocomplete`** to the field's purpose (`SC 1.3.5`) — `email`, `name`, `tel`,
  `street-address`, `one-time-code` (surfaces SMS codes on iOS) — from the fixed value list.
  Enables autofill and AT personalisation; a big help for motor-impaired users.
- Rule: Use the right **`type`** (`email`, `tel`, `url`, `number`, `date`) and **`inputmode`**
  (`numeric`, `decimal`, `email`) so mobile shows the correct keyboard; **`enterkeyhint`**
  (`go`, `search`, `next`) labels the on-screen Enter key.

#### Native input types & constraint validation
- Decision: Lean on native validation (`type`, `required`, `pattern`, `min`/`max`,
  `maxlength`) for free client-side checks — but **don't rely on the browser's native error
  bubbles**: their AT exposure and styling are inconsistent and they vanish on blur.
- Rule: Add **`novalidate`** to the `<form>` and run your own validation so you control the
  message, its association (`aria-describedby`), and focus — consistent across browsers/AT.

#### End-to-end validation flow *(ties §2.11 together)*
1. Mark required fields in text (not colour/`*` alone) — §2.11.
2. Validate **on submit** (or inline only after a fair chance) — §2.11.
3. On failure, render an **error summary** (`role="alert"` or focus-moved, `tabindex="-1"`)
   listing each error as a **link to its field**; **move focus** to the summary heading — §2.9.
4. On each invalid field set **`aria-invalid="true"`** + **`aria-describedby`** → its inline
   error (error id first if there's also a hint) — §2.11/§2.3.
5. Activating a summary link moves focus to the field, where its `aria-invalid` +
   `aria-describedby` announce *that* it's invalid and *why*.
6. Remove `aria-invalid` (don't set `"false"`) as fields become valid — §2.1.

#### Form-level concerns
- Rule: For **legal/financial/data-deleting** actions, meet `SC 3.3.4 Error Prevention` —
  make submissions **reversible**, **checked** for errors with a chance to correct, or
  **confirmed** before committing.
- Rule: **Don't disable the submit button** until "valid" (§2.12) — let users submit and
  surface errors.

#### Multi-step forms (wizards) *(general best practice — not from the source notes)*
- Rule: Make **progress perceivable** — a step indicator with the current step marked via
  **`aria-current="step"`** (§2.5), and announce the step in text ("Step 2 of 4: Payment")
  so it's not conveyed by styling alone.
- Rule: On advancing/going back (which is effectively an SPA view change), **move focus** to
  the new step's heading and update the page `<title>`/`<h1>` — don't leave focus on the
  now-removed "Next" button (§2.9/§1.10).
- Rule: Give each step a **clear heading** and treat each as its own labelled
  region/`<fieldset>`; keep the heading hierarchy sane across steps (§1.3).
- Rule: **Validate per step before advancing**, surfacing errors with the same flow above;
  don't silently lose data when navigating back.
- Rule: Don't rely on time limits; if one exists, meet `SC 2.2.1 Timing Adjustable`
  (warn + allow extension), and **preserve entered data** across steps and on back-nav.
- Rule: Provide a visible, **keyboard-reachable "Back"/"Previous"** control, and make the
  step indicator itself informative (not necessarily interactive — if steps are clickable,
  treat them as navigation).

**Keyboard / focus** *(steps 4–5)* — native form controls bring their own keyboard support;
the work is **focus management on submit/step-change** (move to error summary or next-step
heading) and not breaking tab order (§1.6).

**Gotchas**
- Native-error-bubble gotcha — relying on built-in validation popups gives inconsistent AT
  results; use `novalidate` + your own messaging.
- Required-on-`fieldset` gotcha — `required`/`aria-required` don't work on `<fieldset>`; use
  `role="radiogroup"` + `aria-required`.
- Lost-data gotcha — multi-step forms that drop input on back-navigation or timeout fail
  users with cognitive/motor disabilities hardest; persist state.
- Colour-only-required gotcha — a red `*` alone isn't enough (§1.11/§2.11).

**WCAG** — `SC 3.3.1` (A), `SC 3.3.2` (A), `SC 3.3.3` (AA), `SC 3.3.4` (AA), `SC 1.3.5`
(AA), `SC 4.1.2` (A), `SC 2.2.1` (A, for timed steps), `SC 1.4.1` (A).

### 3.7 Filter Component

**What & why** — A filter is UI that narrows a main content area based on user-selected
options (the WCAG Quick Reference sidebar is the canonical example). There's **no special
ARIA role** — a filter is a **group of native form controls** (§3.6) wired to a **results
region**. The interesting accessibility question isn't the controls; it's **how the result
change is communicated** without nagging the user — and here the counter-intuitive answer
is usually *not* a live region.

**Anatomy & roles** *(steps 2–3)*
- The filters: native **checkboxes / radios / `<select>`** grouped with `<fieldset>` +
  `<legend>` (or a named `role="group"`), labelled by what they filter (§3.6/§1.4).
- The results: a normal, **named** content region (e.g. a `<section aria-labelledby>` or a
  heading that introduces the results) that users navigate to when ready.

**The key decision — instructional cue vs live region** *(step 8)*
- Rule: **Prefer a persistent instructional cue** at the top of the filter group — e.g.
  *"Changing filters will change the listed results below."* It sets expectations for
  **everyone** (not just SR users), so no announcement is needed when results update.
- Decision: **Avoid a live region for the results.** Auto-announcing a re-rendered result
  list is noisy, flattens structure, and interrupts (§2.7). With the cue in place, SR users
  simply navigate to the results region when they're ready to explore.
- Rule (optional): a concise **result count** ("24 results") near the results heading helps
  orient everyone; if you must announce a change, keep it minimal and `polite`.

**Apply behaviour** *(step 5 — focus)*
- Decision: **Auto-apply** (filter on each change) vs an explicit **"Apply" button**.
  Auto-apply pairs naturally with the instructional cue. With an Apply button, on activation
  consider **moving focus to the results heading** (give it `tabindex="-1"`) so the user
  lands on the updated results (§2.9).
- Rule: Mark the current/active filters with state (`aria-pressed` on toggle-style filters,
  or checked state on inputs) and drive their styling from it (§2.1/§2.6).

**Keyboard model** *(step 4)* — native controls bring their own keyboard support; ensure the
filter group and results are in a sensible **tab/DOM order** (§1.6) and that nothing is a
keyboard trap.

**Gotchas**
- Live-region-noise gotcha — making the results container a live region announces the whole
  re-rendered list on every change; use the instructional cue instead.
- Focus-loss-on-rerender gotcha — if applying filters re-renders the DOM, focus can jump to
  `<body>`. Preserve focus on the control the user just changed (auto-apply), or move it
  deliberately to the results (Apply button).
- Hidden-results-count gotcha — conveying "how many results" only visually leaves SR users
  guessing; expose it in text near the results.
- Colour-only-active-filter gotcha — show active filters with more than colour (§1.11).

**WCAG** — `SC 4.1.2 Name, Role, Value` (A), `SC 1.3.1 Info and Relationships` (A), `SC
3.2.2 On Input` (A — don't trigger a surprising context change on input; the cue sets the
expectation), `SC 2.1.1 Keyboard` (A).

### 3.8 Toast / Notifications & Live Updates

**What & why** — A toast is a timely message (confirmation, status, alert) that usually
**auto-expires** after a few seconds. It's the visual cousin of a live-region announcement,
and it inherits live regions' biggest weakness: it's **transient** — once gone, it can't be
reviewed. The decision tree here is critical because the popular "toast with buttons" is an
accessibility trap. This section is really an applied extension of **§2.7 (live regions)**
and **§3.1 (dialog/alertdialog)** — pick the right vehicle for the message.

**Decision tree — which notification mechanism?** *(method step 8)*

| The message is… | Use… |
|---|---|
| A passive status ("Saved", "Copied") | `role="status"` (polite) live region — §2.7 |
| An urgent passive alert ("Connection lost") | `role="alert"` (assertive) live region — §2.7 |
| **Interactive** (has a button/link to act on) | **`role="alertdialog"`** (or a modal/non-modal dialog) + **move focus** — §3.1 |
| A confirmation the user must act on (cart, undo) | A **modal/non-modal dialog**, focus moved into it — §3.1 |

- Rule: **Toasts must not contain interactive elements.** When announced via a live region,
  the button/link semantics are **stripped**, focus doesn't move to the toast, there's no
  way to navigate *into* it, and it may **auto-dismiss before the user reaches it**. This
  hurts screen-reader, magnifier, **and** keyboard users — and typically fails multiple WCAG
  SCs.
- Rule: For an **actionable** notification, use **`role="alertdialog"`** (alert + dialog
  keyboard/focus behaviour, §3.1) and **move focus to it** as an immediate response to the
  user's action — this replaces the toast-with-buttons pattern.
- Rule: For an **"item added to cart"**–style confirmation, prefer a **modal overlay +
  focus-move** over a live-region announcement, so keyboard/SR users land in it with options
  to edit or check out.

**Implementation (passive toast as a live region)** *(per §2.7)*
- Rule: Place the **empty** live-region container in the DOM **at load**; populate it via JS
  when the toast fires. **Empty it before repopulating** so repeats re-announce.
- Rule: Use **`status`/polite** by default; reserve `alert`/assertive for genuinely urgent
  messages.
- Rule: Don't move focus to an **unsummoned** toast (one the user didn't trigger) — it
  disrupts their flow (§2.9). (Moving focus is for *interactive* notifications the user
  caused.)

**Persistence**
- Rule: Because toasts are **one-shot and gone**, offer a **persistent alternative** for
  anything important — a notifications centre / message log users can revisit. Don't make a
  transient toast the only way critical info is conveyed (§2.7).

**Keyboard / focus** *(steps 4–5)*
- Passive toast: **no focus change**; it's announced, not focused. If it has a dismiss
  button, that's a sign it should probably be a dialog.
- Interactive notification: it's an `alertdialog`/dialog — follow §3.1 (focus in on appear,
  Esc to dismiss, return focus on close).

**Gotchas**
- Toast-with-buttons gotcha — the headline trap: actionable toasts fail AT, magnifier, and
  keyboard users. Promote them to an `alertdialog`/dialog.
- Auto-dismiss gotcha — timing out a message before a slow reader/AT user perceives or acts
  on it; either don't auto-dismiss actionable messages, or give enough time / a persistent
  copy (`SC 2.2.1`).
- Transience gotcha — relying on a toast as the *only* record of something important; add a
  persistent affordance.
- `alert`-shouldn't-take-focus gotcha — a plain `role="alert"` should not move focus or
  require dismissal; if it must, it's an `alertdialog` (§2.7/§3.1).

**WCAG** — `SC 4.1.3 Status Messages` (AA — announce without focus), `SC 2.2.1 Timing
Adjustable` (A — for auto-dismiss), `SC 4.1.2 Name, Role, Value` (A); `alertdialog` for
errors is an advisory technique for `SC 4.1.3`.

### 3.9 Custom Select / Combobox / Dynamic Search

**What & why** — A combobox is an input with an associated popup of values to choose from
— the basis of custom selects, autocomplete, and type-ahead search. It is one of the
**most complex** ARIA patterns (a textbox + a managed popup + `aria-activedescendant` focus
juggling), which is exactly why **native-first matters most here**. Get it wrong and you
break the browser's own text-editing keys. The two faces of this section: the **combobox
widget** itself, and the lighter **dynamic-search** results pattern.

**Native-first** *(method step 1 — strongest here)*
- Decision: For a plain select-from-list, use a native **`<select>`** — full keyboard,
  focus, and mobile pickers for free. For text input with suggestions, **`<input list>` +
  `<datalist>`** gives native autocomplete with no ARIA. Only build a custom combobox when
  you need styling/behaviour neither can provide — and budget for the complexity.

#### Combobox widget *(per W3C APG)*

**Anatomy & roles** *(steps 2–3)*
- The input: **`role="combobox"`** + **`aria-expanded`** + **`aria-controls`** → the popup
  id + **`aria-autocomplete`** (`none` / `list` / `both`). Label it (`<label>` /
  `aria-label` / `aria-labelledby`). Add `aria-haspopup` when the popup isn't a listbox.
- The popup: usually **`role="listbox"`** with **`role="option"`** items; the active option
  carries **`aria-selected="true"`**.
- Optional **Open** button beside the input.

**Focus management — the defining trick** *(step 5)*
- Rule: **DOM focus stays on the combobox input.** You indicate the active option visually
  with **`aria-activedescendant`** (set to the focused option's id) rather than moving real
  focus into the listbox. The popup options never receive DOM focus.
- Rule: On open set `aria-expanded="true"`; on close set `"false"` and keep/return focus to
  the input.

**Keyboard model** *(step 4)*
- The combobox is in the **page tab sequence**; the popup and icon are **not**.
- **Down/Up** — open the popup and move the active option (via `aria-activedescendant`);
  selection follows focus.
- **Enter** — accept the active option, close the popup.
- **Escape** — close the popup (and optionally clear the input).
- **Home/End**, **Alt+Down/Up** (show/hide without moving), printable chars (type into the
  input in editable mode) — per APG.
- Rule: Don't capture the keys the browser uses for **native text editing** (arrows within
  text, Backspace) in a way that breaks typing.

**Autocomplete behaviours**
- `aria-autocomplete="none"` — fixed suggestions (e.g. recent searches).
- `aria-autocomplete="list"` — suggestions filter to what's typed (manual or auto-highlight
  first).
- `aria-autocomplete="both"` — list **plus** an inline completion string after the cursor.

#### Dynamic search results *(Scott O'Hara pattern — from the source notes)*
A search input that filters/shows results live as the user types — *not* necessarily a full
combobox.
- Rule: **Don't make the results container a live region** — announcing results on every
  keystroke is extremely noisy.
- Rule: Add an **instructional cue** via `aria-describedby` ("Results will filter as you
  type") so users know what to expect (visually-hidden is fine if you don't want it shown).
- Rule: Use an **assertive live region only for "No results found"** — an interrupt-worthy
  event the user needs to know immediately.
- Rule: **Enter** moves focus to the **heading that introduces the results** (the SR then
  announces the heading + result count); **Escape** returns focus to the input.

**Gotchas**
- Reinventing-`<select>` gotcha — custom comboboxes are a top source of broken widgets;
  exhaust `<select>` / `<datalist>` first.
- Captured-typing gotcha — intercepting arrow/Backspace keys breaks the input's native text
  editing; only handle the combobox keys, leave text editing alone.
- Real-focus-in-listbox gotcha — moving DOM focus into the options (instead of using
  `aria-activedescendant`) fights the textbox; follow the activedescendant model for
  listbox/grid/tree popups (a *dialog* popup is the exception — there focus does move in,
  per §3.1).
- Noisy-results gotcha — a live-region results list narrates every keystroke; use the cue +
  no-results-only announcement instead.
- `aria-owns`-legacy gotcha — use **`aria-controls`** (not the ARIA 1.0 `aria-owns`) to
  reference the popup.

**WCAG** — `SC 4.1.2 Name, Role, Value` (A), `SC 2.1.1 Keyboard` (A), `SC 4.1.3 Status
Messages` (AA — the no-results announcement), `SC 1.3.1` (A).

### 3.10 Smaller Controls

_(icon button, toggle button, breadcrumb, pagination, pill/chip, toolbar, skip link)_

**What & why** — A roundup of common smaller patterns. Each is mostly an application of
earlier tiers (semantic element + a name + the right state), so these entries are concise —
the recurring theme is **every control needs a clear, unique accessible name**, and several
"components" are just a labelled `<nav>` with no special role (ARIA is finite — there's no
`role="breadcrumb"`/`"carousel"`).

**Icon button** *(button whose only label is an icon)*
- Rule: It must be a real **`<button>`** wrapping an inline **`<svg>`** (SVG over icon
  fonts — resilient, can carry its own name). Unnamed, it announces only "button" and fails
  `SC 4.1.2`.
- Rule: Naming, in preference order — (1) visible text, (2) `.visually-hidden` text,
  (3) **`<span hidden id>` + `aria-labelledby`** (the go-to: translatable, reader-mode safe),
  (4) `aria-label` (last resort), (5) name via the SVG (`role="img"` + `aria-label`).
- Rule: If the button is named by anything **other than** the SVG, hide the SVG with
  `aria-hidden="true"` to avoid double announcement; if the **SVG is** the name, don't hide
  it (give it `role="img"` + a name).

**Toggle button** *(on/off action)* — `<button aria-pressed="true|false">`; JS flips it on
activation; style from `button[aria-pressed="true"]` (§2.6). `mixed` only for genuine
tri-state. Don't confuse with a switch or a tab (§2.6).

**Breadcrumb** — no `role="breadcrumb"`. Use **`<nav aria-label="Breadcrumb">`** wrapping an
**`<ol role="list">`** of links (ordered = the trail); mark the current page with
`aria-current="page"` (§2.5); re-instate list semantics if markers are removed (§1.4).

**Pagination**
- Rule: **`<nav>`** (named via `aria-labelledby` → a hidden label) containing an
  **`<ol role="list">`** of links; current page gets **`aria-current="page"`** (§2.5).
- Rule: Give each link a descriptive accName — "Page 1", "Page 2" — not a bare number
  (add "Page" via a visually-hidden span, or a shared hidden prefix referenced by
  `aria-labelledby`).
- Rule: Put the **"Next" link before** the page-number links in the DOM so keyboard users
  reach it without tabbing through every page.

**Pill / Chip** *(filter/selection tokens, often removable)*
- Rule: Each **remove button needs a UNIQUE name** saying *which* pill — "Remove CSS", not
  "Remove" — via `aria-labelledby="<pill>-remove <pill>"` (a hidden "Remove" span + the pill
  text). Hide the × icon with `aria-hidden="true"`.
- Gotcha: identical "Remove" names make VoiceOver's rotor/element list a wall of
  indistinguishable buttons.

**Toolbar** *(a visually grouped set of controls)*
- Rule: **`<div role="toolbar">`** (named via `aria-labelledby`) becomes **one tab stop**;
  **arrow keys** move among the controls via **roving `tabindex`** (first control
  `tabindex="0"`, rest `-1`; §2.9). Right/Left move + wrap, `preventDefault()` page scroll;
  a click also makes the clicked control the new tab stop.
- May mix `<button>`, `<button aria-pressed>`, `<select>`, checkboxes, radio groups.

**Skip link** — covered in §1.2; the first focusable element in `<body>`, visually hidden
until focused, targeting `<main id tabindex="-1">`. Also valid as in-page "skip" links for
long lists / before an `<iframe>` / "back to top" (§1.6).

**Gotchas (cross-cutting)**
- Made-up-role gotcha — no `role="breadcrumb"`/`"pagination"`/`"carousel"`; compose from
  `<nav>` + lists. (§3.0)
- Number-only-link gotcha — bare "2"/"3" pagination links lack out-of-context meaning; add
  "Page".
- Identical-name gotcha — repeated "Remove"/"Edit" icon buttons need disambiguating names.
- Toolbar-tab-stop gotcha — without roving tabindex a toolbar adds a tab stop per control,
  defeating its purpose.

**WCAG** — `SC 4.1.2 Name, Role, Value` (A — names/roles/states), `SC 2.1.1 Keyboard` (A),
`SC 2.4.1 Bypass Blocks` (A — skip link), `SC 1.3.1` (A — nav/list semantics).

---

## 4. Verification & Testing Checklist

**What & why** — Accessibility isn't done when the markup looks right — it's done when you've
*confirmed* it works for keyboard and assistive-tech users. Automated tools catch only a
fraction of issues (roughly a third); the rest need manual passes. The order below goes
cheap → thorough: automated first to clear obvious failures, then the manual passes that
actually prove the experience. Remember: **technically conformant ≠ usable** — usability-test
with disabled and AT users where you can.

**Automated pass** *(catches ~a third — necessary, not sufficient)*
- Run **axe** (axe DevTools) and/or **Lighthouse** for missing names, contrast, ARIA misuse,
  duplicate ids.
- Use **WAVE** to visualise landmarks and heading structure in context.
- Inspect the **accessibility tree** in Chrome/Edge DevTools to confirm an element's name,
  role, and state (and *where* the name came from).
- ⚠️ A clean automated report means "no detected errors", not "accessible." Always follow
  with the manual passes.

**Keyboard-only pass** *(unplug the mouse)*
- ☐ Every interactive element is **reachable** by Tab and **operable** with the expected keys
  (Enter/Space/arrows/Esc) — §1.6, §3.0.
- ☐ Tab order follows **DOM/visual order**; no positive `tabindex` surprises.
- ☐ **Visible focus** on every stop (§1.7); focused element never hidden behind sticky
  headers/overlays.
- ☐ **No keyboard traps** — you can always tab out (the only managed trap is an open modal,
  Esc-dismissible) — §1.6, §3.1.
- ☐ Composite widgets are a **single tab stop** with arrow-key navigation (§2.9).
- ☐ Tip: **Accessibility Insights "Tab Stops"** draws the focus path — a line into hidden
  content reveals a missing `inert`/`hidden`.

**Screen-reader pass** *(test real browser/AT pairings)*
- Test the pairings your audience uses — the common three: **NVDA + Firefox** (Windows),
  **JAWS + Chrome** (Windows), **VoiceOver + Safari** (macOS/iOS); add **TalkBack** for
  Android touch.
- ☐ Every control announces a clear **name + role + state** ("Products, link, current page";
  "Bold, toggle button, pressed").
- ☐ **Headings & landmarks** form a sensible outline (NVDA Insert+F7 elements list;
  VoiceOver rotor) — §1.2, §1.3.
- ☐ **Images** announce meaningful alt or are silent when decorative (§1.8).
- ☐ **Dynamic updates** announce as intended (live region) or move focus appropriately
  (§2.7, §2.9) — and don't over-announce.
- ☐ Don't assume one SR's behaviour generalises — `aria-controls`, `<summary>` exposure,
  `<output>`, and group roles differ across pairings (test, don't trust a support table).

**Visual / sensory pass**
- ☐ **Contrast** — 4.5:1 text, 3:1 large text & UI/non-text (§1.11); check focus rings and
  states too. Tools: contrast checkers, "Who Can Use".
- ☐ **Colour isn't the only cue** — errors, required, links, states (§1.11, §2.11).
- ☐ **Forced Colors / High Contrast Mode** — content, focus rings, and state icons survive
  (§1.7, §3.6).
- ☐ **Reduced motion** — animations respect `prefers-reduced-motion`; >5s motion has
  pause/stop/hide (§2.10, §3.2).

**Zoom & reflow pass**
- ☐ **200% text resize** with no loss of content/function (`SC 1.4.4`); zoom isn't blocked
  (§1.10).
- ☐ **400% / reflow** (≈320px-equivalent width) — content reflows to one column with no loss
  and no two-dimensional scrolling (`SC 1.4.10`).
- ☐ Layout doesn't clip enlarged text or trap content in fixed-height boxes.

**Beyond conformance**
- ☐ Where possible, **usability-test with disabled and AT users** — the surest signal, and it
  catches barriers no checklist does (§3.0).
