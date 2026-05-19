## Rules

- Rule: An element's accessibility information has four parts — role, name, description, and state.
- Rule: Semantics should provide three main pieces of information — the role of the element (what it is/does), the name (identifies the element and its purpose), and the state (where applicable, the current state of the element).
- Rule: ARIA roles indicate what an element is, ARIA states indicate the current state of the element, and ARIA properties describe properties of the element (e.g., its name, description, current value, or relationship to other elements).
- Rule: Semantic HTML is the most powerful accessibility tool; ARIA is the second most powerful.
- Rule: ARIA supplements HTML semantics — it does not replace HTML and does not change HTML's behaviour.
- Rule: When an HTML element already has the semantic meaning needed, adding ARIA is redundant and discouraged.
- Rule: Treat ARIA as a last resort — "spackle, not rebar"; reach for native HTML elements first.
- Rule: There should be only one H1 per page.
- Rule: There are eight landmark regions defined by eight ARIA roles, each with an HTML element that implicitly maps to that role.
- Rule: Identifying landmarks is required to conform to WCAG SC 1.3.1 (Info and Relationships) and SC 2.4.1 (Bypass Blocks).
- Rule: Aim for only one banner landmark per site, and keep page-specific content out of it — the banner is for global, site-oriented content like the company logo, main site navigation, user login links, and a global search component.
- Rule: When using more than one navigation landmark, give each an accessible name via `aria-label` or `aria-labelledby`.
- Rule: Explicit `role="contentinfo"` on `<footer>` is no longer required in modern browsers (post-Safari 13).
- Rule: Complementary content should be related to the main content but also easily understood without it; content that does not fit this description belongs in another landmark type.
- Rule: When more than one complementary landmark exists, label each with a descriptive heading via `aria-labelledby`.
- Rule: Search is a separate landmark from form because it lets users find content on a site without navigating the site's structure.
- Rule: Multiple search landmarks are allowed; give each an accessible name (via heading + `aria-labelledby`, `aria-label`, `title`, or a hidden label referenced by `aria-labelledby`).
- Rule: A generic region must have an accessible name to be surfaced as a landmark, preferably referencing a visible heading via `aria-labelledby`.
- Rule: Let the visual design guide landmark choices so the visual and semantic structure align.
- Rule: Limit the number of landmarks on a page — too many landmarks reduce navigation efficiency and stop the truly important regions from standing out.
- Rule: Ensure all content on the page is contained within a meaningful landmark region, and use headings for fine-grained navigation within each region.
- Rule: Verify landmarks and heading structure using WebAIM's WAVE browser extension.
- Rule: What an element is determines how it can be used; semantics convey what an element is, and therefore how it can be used.
- Rule: Semantic information is vitally important to someone who isn't using the screen — choose HTML elements that describe what the component is so assistive technologies can expose those semantics.
- Rule: When creating a new component, the first thing to do is choose an HTML element that describes what it is to someone who can't see it.
- Rule: Using an element with the wrong semantics breaks user expectations of what will happen on interaction and can confuse users who try to operate the element a certain way but can't.
- Rule: Style an element according to its semantics — if it behaves like a button, style it like a button; if it is a link, avoid styling it to look like a button.
- Rule: Designers should define interactive behaviour in design mockups or specifications and annotate designs so developers know exactly what they are implementing.
- Rule: Buttons trigger actions on the page (e.g., submitting forms, opening dialogs, toggling navigation, showing/hiding content).
- Rule: Buttons and links have different semantics and are not interchangeable.
- Rule: Wire up a button's action via JavaScript or the HTML Invoker Commands API.
- Rule: Disable a native button using the HTML `disabled` attribute.
- Rule: Links do not require JavaScript to do what they do — they are inherently capable of redirecting the user to other places.
- Rule: Links can also download files (via `download`), open email apps (`mailto:`), or dial phone numbers (`tel:`).
- Rule: Links cannot be disabled with the HTML `disabled` attribute — that attribute applies only to form controls.
- Rule: Links expose unique browser affordances — most browsers show the `href` value in the status bar on hover, right-click reveals link-specific options, and a link can be opened in a new tab/browser window.
- Rule: The `role` attribute only changes the exposed role in the accessibility tree; it does not add behaviour or actually convert the element.
- Rule: Only enhance a link into a button as part of a deliberate progressive-enhancement strategy because of the manual work involved.
- Rule: Use `<nav>` for any navigation component — site-wide navigation, breadcrumbs, secondary navigations in a sidebar or footer, and tables of contents.
- Rule: Use links (not buttons) inside a navigation — links communicate to screen reader users that activating the item will take them places.
- Rule: Group navigation links into a list (`<ul>` or `<ol>`) so the number and order of items are conveyed semantically.
- Rule: Choose the element that semantically represents what you are creating even when multiple options map to the same role (e.g., `<ul>` vs `<ol>` both map to `list`).
- Rule: When CSS may strip list semantics (e.g., applying `list-style: none`), re-instate them by adding `role="list"` to the `<ul>` or `<ol>` so the list and its item count remain exposed.
- Rule: Use `aria-current="page"` (not `aria-current="true"`) on a navigation's current-page link so screen readers announce "link, current page".
- Rule: Use the `aria-current` attribute itself as the CSS styling hook (e.g., `a[aria-current="page"]`) rather than a dedicated `.current` class — the styling only applies when the accessible state is set.
- Rule: When HTML semantics fall short, supplement accessibility information using ARIA attributes (e.g., state information like indicating the current item within a set).
- Rule: ARIA is a Web standard (WAI-ARIA) that defines attributes extending HTML to add semantic roles, states, and properties so elements can be better understood by assistive technologies.
- Rule: ARIA is finite — you cannot make up your own role values or attribute values; only roles and values documented in the ARIA specification are valid.
- Rule: ARIA roles only affect the accessibility tree; they have no effect on the DOM and do not add interactive behaviour, focusability, or keyboard handling.
- Rule: Interactive ARIA widget roles (button, checkbox, searchbox, radio, switch, tab, etc.) indicate that elements are supposed to be interactive but do not make them interactive — you must implement focus, keyboard support, and the activation behaviour yourself in JavaScript.
- Rule: ARIA is a promise — every time you consider using an ARIA attribute, ask what promise you are making to the user and whether you are fulfilling it; "is there an HTML element I can use instead?" — if yes, use that.
- Rule: A role is a promise — applying an interactive role like `<div role="button">` is a binding contract that you, the author, have added the styles, focus, keyboard interactivity, and activation behaviour expected of that role; not fulfilling the promise breaks user expectations and often makes the component unusable.
- Rule: Add ARIA states using JavaScript and update them dynamically on user interaction; JavaScript is imperative for accessible custom interactive components.
- Rule: Without JavaScript to keep them current, ARIA state attributes are useless and can be actively confusing — apply ARIA with a progressive-enhancement mindset.
- Rule: Before using an ARIA role on an HTML element, check whether that role is permitted on the element via the "ARIA in HTML" specification.
- Rule: Composite ARIA roles must be used together with their associated roles to compose a UI widget (e.g., `tablist` with `tab` and `tabpanel`).
- Rule: Provide clear re-use documentation for design-system / pattern-library components that use ARIA so they aren't placed in conflicting contexts.
- Rule: Keep ARIA use to a minimum — if a component can be built with semantic HTML alone, or simplified to use fewer attributes with robust support, do so.
- Rule: There is no feature-detection for ARIA support — rely on native semantics as much as possible, use ARIA to the best of your knowledge, and test with various browser/AT combinations.
- Rule: Six categories of ARIA roles exist — Abstract (not for use in content), Landmark, Document Structure, Widget, Live Region, and Window.
- Rule: If you use semantic HTML for elements that have native mappings (document-structure and landmark roles), you do not need to also apply their equivalent ARIA roles.
- Rule: First Rule of ARIA — if you can use a native HTML element or attribute with the semantics and behaviour you need already built in, use it instead of repurposing an element with an ARIA role, state, or property.
- Rule: Exceptions to the First Rule of ARIA — (1) the HTML feature you need exists but isn't implemented or its accessibility support is missing; (2) visual design constraints rule out the native element because it can't be styled as required; (3) the feature is not available in HTML at all.
- Rule: Second Rule of ARIA — do not change native semantics unless you really have to (e.g., prefer `<div role="tab"><h2>Title</h2></div>` over `<h2 role="tab">Title</h2>`).
- Rule: Second Rule exception (fallback strategy) — it is OK to use native HTML elements that have similar semantics to the ARIA roles used, as a progressive-enhancement skeleton (e.g., HTML list elements for the skeleton of an ARIA-enabled, scripted tree widget).
- Rule: Third Rule of ARIA — all interactive ARIA controls must be usable with the keyboard; if a user can click, tap, drag, drop, slide, or scroll a widget, they must be able to perform the equivalent action with the keyboard, and the widget must be scripted to respond to standard keystrokes.
- Rule: Fourth Rule of ARIA — do not use `role="presentation"` or `aria-hidden="true"` on a focusable element (or an ancestor of one); doing so results in users focusing on "nothing".
- Rule: Fifth Rule of ARIA — all interactive elements must have an accessible name.
- Rule: ARIA does not remove behaviour from an already-interactive element — `aria-hidden="true"` on a `<button>` removes it from the accessibility tree but leaves it in the DOM, focusable, and operable.
- Rule: When using a non-interactive element (e.g., a heading) as the basis for an interactive component, you must add the semantics with ARIA AND the interaction behaviour with JavaScript.
- Rule: The less ARIA you use, the better — modifying the design or simplifying the pattern is almost always a better approach than rolling up your own custom ARIA widgets.
- Rule: Under-engineering design patterns will almost always result in a more accessible and more usable experience.
- Rule: Avoid pairing ARIA state attributes with their native HTML counterparts (e.g., `required` + `aria-required="true"`, `hidden` + `aria-hidden="true"`) — they are redundant and create a liability because the values can fall out of sync if not updated together.
- Rule: Avoid adding ARIA roles, states, or properties to long-implemented structural elements that already have good native support (e.g., `<h1 role="heading" aria-level="1">`).
- Rule: When you use ARIA, make sure you (a) know what the attributes do and don't do, (b) follow the rules of ARIA use, (c) implement the necessary accessibility behaviour, and (d) test the components using various browser and assistive-technology combinations.
- Rule: Prefer usability testing with disabled assistive-technology users to ensure components are actually usable, not just technically correct.
- Rule: No ARIA is better than bad ARIA — incorrect ARIA misrepresents the visual experience with potentially devastating effects on assistive-technology users.
- Rule: ARIA is a polyfill for HTML semantics — like a JavaScript polyfill, it is a last resort to fill missing features, not a tool to reach for by default; convey as much accessibility information as possible using HTML semantics and only reach for ARIA when HTML falls short.

## HTML Elements

- Element: `<header>` — implicit banner role; only exposed as a banner landmark when it is a direct child of `<body>`, not when nested in another sectioning element such as `<article>` or `<section>`.
- Element: `<nav>` — implicit navigation role; multiple navigation landmarks per page are allowed; preserves list semantics inside in Safari 16+ when default list markers are removed via CSS.
- Element: `<main>` — implicit main role; should be a direct child of `<body>`, with only one main landmark per page.
- Element: `<footer>` — implicit contentinfo role only when scoped directly to `<body>`; not exposed as contentinfo when nested in another sectioning element.
- Element: `<aside>` — implicit complementary role; should be a sibling or child of the main landmark.
- Element: `<form>` — only exposed as a form landmark when it has an accessible name.
- Element: `<search>` — maps to the search landmark role; preferred over legacy `role="search"` on a `<form>` or `<div>`.
- Element: `<section>` — does not affect the document outline, but its implicit region role is exposed as a landmark when it is given an accessible name — preferred element for custom regions; also commonly used with `role="tabpanel"` for tab panels.
- Element: `<div>` — no implicit landmark role; can be turned into a landmark by adding an explicit ARIA `role` attribute when markup cannot be changed; using `<div>` instead of `<nav>` loses the navigation landmark and (in Safari 16+) also strips list semantics from any list inside it; commonly used with `role="tablist"` since no native HTML element maps to tablist.
- Element: `<button>` — implicit button role with semantics and behaviour baked in; does nothing on its own except inside a `<form>`, where it may submit the form; focusable by default (no `tabindex="0"` needed); keyboard operable via Space and Enter; can be disabled with the HTML `disabled` attribute; ARIA roles permitted on `<button>` are `checkbox`, `link`, `menuitem`, `menuitemcheckbox`, `menuitemradio`, `option`, `radio`, `switch`, and `tab` — other roles (like `heading`) are not permitted.
- Element: `<a>` — has an implicit link role only when it has an `href` attribute; without `href` it represents a placeholder for a link, maps to the generic ARIA role, is not exposed in the accessibility tree, and is removed from the tab order (not even focusable in most browsers); when it has `href` it is focusable by default (no `tabindex="0"` needed) and is activated by the Enter key only.
- Element: `<ul>` — maps to the `list` role; conveys the number and order of items to screen readers; older Safari versions and Safari 16+ outside a navigation landmark remove list semantics when `list-style: none` is applied; can be safeguarded with `role="list"`.
- Element: `<ol>` — maps to the `list` role; semantically appropriate when order matters (e.g., breadcrumbs); shares the same Safari list-semantics caveats as `<ul>`.
- Element: `<li>` — list item element used inside `<ul>` or `<ol>`.
- Element: `<span>` — frequently used with the HTML `hidden` attribute to create a visually-hidden text label referenced from another element via `aria-labelledby`.
- Element: `<svg>` — can be excluded from the accessibility tree (hidden from screen readers) by adding `aria-hidden="true"` when decorative.
- Element: `<summary>` — maps to the `button` role and is subject to the same Children Presentational rule that suppresses descendants' semantics.
- Element: `<input>` — form control; requires an accessible name supplied programmatically via `<label for>` (preferred), `aria-label`, or `aria-labelledby` — visible-only labels (e.g., an adjacent `<span>` with no association) leave the input without an accessible name.
- Element: `<label>` — programmatically associates with a form control via its `for` attribute matching the control's `id`; the label text becomes the control's accessible name.

## ARIA Roles

- Role: `banner` — landmark for site-wide header content like the company logo, main site navigation, user login links, and a global search component; ideally only one per site.
- Role: `navigation` — landmark for a collection of navigational elements (usually links) for navigating within a website.
- Role: `main` — landmark designating the primary content of the page; only one per page.
- Role: `contentinfo` — landmark for information about the parent document; typically the page footer with copyright, privacy and accessibility links.
- Role: `complementary` — landmark for secondary information related to the main content yet understandable without it (e.g., sidebars, call-out boxes, list of related articles).
- Role: `form` — landmark for a form; only exposed when the form has an accessible name.
- Role: `search` — landmark for a collection of elements that together create a search facility (search of the site, of the current page, or an Internet-wide search).
- Role: `region` — generic landmark for a perceivable section of content important enough that users will likely want to navigate to it and see it listed in a page summary; requires an accessible name.
- Role: `button` — exposes an element as a button in the accessibility tree; widget role with a Children Presentational property that suppresses descendants' semantics; only changes the exposed role, not behaviour.
- Role: `link` — exposes an element as a link in the accessibility tree (used to reinstate link semantics after removing `href`).
- Role: `generic` — what an `<a>` without an `href` (and a `<div>`/`<span>` by default) maps to; not exposed in the accessibility tree.
- Role: `list` — implicit role of `<ul>` and `<ol>`; can be re-instated with `role="list"` when CSS strips list semantics.
- Role: `tablist` — composite widget role that owns child `tab` roles; no native HTML element maps to tablist; used together with `tab` and `tabpanel` to compose a Tabs widget.
- Role: `tab` — child widget role within a `tablist` that toggles a tab panel; MUST be contained in or owned by an element with `role="tablist"`.
- Role: `tabpanel` — widget role for the panel content associated with a `tab`.
- Role: `menu` — composite widget role; expects `menuitem` children.
- Role: `menubar` — composite widget role; expects `menuitem` children.
- Role: `menuitem` — widget role that must be a child of an element with `menu` or `menubar` role; may not contain interactive children (no nested `<button>`, no `<a>`, and no elements with implicit button or link roles).
- Role: `menuitemcheckbox` — widget role; allowed on `<button>`.
- Role: `menuitemradio` — widget role; allowed on `<button>`.
- Role: `checkbox` — widget role; allowed on `<button>`.
- Role: `radio` — widget role; allowed on `<button>`.
- Role: `option` — widget role; allowed on `<button>`.
- Role: `switch` — widget role; allowed on `<button>`.
- Role: `searchbox` — interactive widget role.
- Role: `heading` — document-structure role; pairs with `aria-level` to indicate heading level; not permitted on `<button>`.
- Role: `presentation` — suppresses an element's semantics in the accessibility tree; descendants of certain roles are treated as if they had `role="presentation"`; on a focusable element (e.g., a link), screen readers no longer announce the role but still announce the element's contents.

## Attributes

- Attribute: `role` — ARIA attribute that exposes an element's type in the accessibility tree (e.g., `button`, `link`, `banner`, `navigation`, `main`, `contentinfo`, `complementary`, `form`, `search`, `region`, `list`, `tablist`, `tab`, `tabpanel`, `menu`, `menubar`, `menuitem`, `presentation`); changes only the exposed role, not behaviour.
- Attribute: `aria-label` — Provides an accessible name; the attribute's value is used directly as the label.
- Attribute: `aria-labelledby` — Provides an accessible name by referencing another element (typically a heading or a hidden `<span>`) on the page as the label.
- Attribute: `aria-describedby` — Property that references one or more elements on the page to provide an accessible description for the element it is used on.
- Attribute: `aria-disabled` — Conveys disabled state to assistive technologies, e.g., `aria-disabled="true"`.
- Attribute: `aria-current` — Used on a link to indicate it is the current item in a set; supports values such as `true` and `page` — `page` causes screen readers to announce "link, current page" instead of just "link, current".
- Attribute: `aria-pressed` — State on a button-like element indicating whether the toggle is currently pressed (`true`) or not (`false`); changes must be managed via JavaScript.
- Attribute: `aria-expanded` — State indicating whether the thing the control controls is expanded (`true` / "open") or collapsed (`false` / "closed"); update via JavaScript on user interaction.
- Attribute: `aria-controls` — Property that creates a relationship between the element it is on and the controlled element referenced by id; note: no longer exposed by most screen readers.
- Attribute: `aria-hidden` — Property; when `true`, the element is excluded from the accessibility tree and hidden from screen readers — but it remains in the DOM and tab order, so applying it to a focusable element or an ancestor of one results in users focusing on "nothing".
- Attribute: `aria-valuetext` — Property holding a textual value for an element (e.g., an HTML range slider); should change as the user changes the element's value.
- Attribute: `aria-valuenow` — Property holding the current numeric value of an element; should change as the user changes the element's value.
- Attribute: `aria-level` — Property paired with the `heading` role to indicate heading level.
- Attribute: `aria-required` — ARIA state for required form controls; equivalent to HTML `required`; using both is redundant and can fall out of sync.
- Attribute: `href` — Required on `<a>` for it to be a hyperlink; defines the link's destination as a URL or in-page fragment.
- Attribute: `disabled` — HTML attribute that disables form controls including `<button>`; does not apply to links.
- Attribute: `required` — HTML boolean attribute on form controls; native equivalent of `aria-required="true"`; prefer it over the ARIA equivalent.
- Attribute: `download` — `<a>` attribute that triggers a file download instead of navigation.
- Attribute: `tabindex` — Controls focusability and tab order; `tabindex="0"` makes an otherwise non-focusable element focusable.
- Attribute: `hidden` — HTML boolean attribute that hides an element from rendering and from the accessibility tree; also used on a `<span>` to create a visually hidden text label referenced by `aria-labelledby`; pairing `hidden` with `aria-hidden="true"` is redundant.
- Attribute: `title` — Can be used to indicate the purpose of a landmark such as a `<search>` element when no visible label is available.
- Attribute: `for` — `<label>` attribute referencing an input's `id` to programmatically associate the label with the input and expose its text as the input's accessible name.
- Attribute: `id` — HTML attribute used to be referenced by `<label for>`, `aria-labelledby`, or `aria-describedby` for programmatic association.

## WCAG Success Criteria

- WCAG: SC 1.3.1 Info and Relationships — "Information, structure, and relationships conveyed through presentation can be programmatically determined or are available in text." Using the appropriate semantic elements to identify key areas of the page is required to meet this criterion.
- WCAG: SC 2.1.1 Keyboard (Level A) — "All functionality of the content is operable through a keyboard interface without requiring specific timings for individual keystrokes, except where the underlying function requires input that depends on the path of the user's movement and not just the endpoints." The baseline keyboard-accessibility requirement for any interactive component, including custom ARIA widgets.
- WCAG: SC 2.1.3 Keyboard (No Exception) (Level AAA) — "All functionality of the content is operable through a keyboard interface without requiring specific timings for individual keystrokes." The stricter, no-exception version of SC 2.1.1.
- WCAG: SC 2.4.1 Bypass Blocks — exists to ensure assistive technology users have a way to bypass repeated content and facilitate page navigation; using proper landmark elements is one way to meet this criterion.
- WCAG: SC 4.1.2 — referenced as being violated when an ARIA role conflicts with the nature of the element it is applied to (e.g., `role="heading"` on a `<button>`), because the semantic mismatch may prevent users from interacting with the element as announced.

## Patterns & Recipes

- Pattern: Name a navigation landmark — give the `<nav>` an `aria-label` describing its purpose (e.g., "Site", "Breadcrumbs"); or use `aria-labelledby` to reference an on-page heading or a visually-hidden `<span hidden>` placed inside the `<nav>`; do not include the word "navigation" in the label.
- Pattern: Label an `<aside>` — add a descriptive heading inside the `<aside>` and reference it from the `<aside>` via `aria-labelledby`.
- Pattern: Label multiple complementary landmarks — give each `<aside>` a descriptive heading and reference it via `aria-labelledby`.
- Pattern: Create a search landmark — wrap the search controls in `<search>`; give it an accessible name via a heading + `aria-labelledby`, `aria-label`, `title`, or a hidden text label (e.g., a `<span hidden>`) referenced by `aria-labelledby`.
- Pattern: Create a custom region — wrap content in `<section>` (or use a `<div>` with `role="region"`) and give it an accessible name, preferably referencing a visible heading via `aria-labelledby`.
- Pattern: Retrofit landmarks onto an existing site — apply ARIA role values (banner, navigation, main, contentinfo, complementary, form, search, region) to existing elements like `<div>` when the markup cannot be changed; you can also use heading roles with `aria-level` to fix an inefficient document outline.
- Pattern: Disable a link — remove its `href` so the browser no longer provides link interactive behaviour; reinstate link semantics with `role="link"`; convey the disabled state to screen readers with `aria-disabled="true"`.
- Pattern: Enhance a link into a button — override link semantics with `role="button"`; attach a click handler that calls `e.preventDefault()` and triggers the action; implement full button keyboard behaviour by firing on keydown for Enter (keyCode 13) and on keyup for Space (keyCode 32); add styles targeting Forced Colors modes (e.g., Windows High Contrast Mode) so it appears as a button.
- Pattern: Build an accessible site/breadcrumb navigation — wrap links in `<nav>` and give it an accessible name; group links inside `<ul>` (unordered) or `<ol>` (ordered, for breadcrumbs) with each link in an `<li>`; add `role="list"` to safeguard list semantics when CSS removes default markers; mark the current-page link with `aria-current="page"` and style it via `a[aria-current="page"]`.
- Pattern: Preserve list semantics across CSS changes — add `role="list"` to the `<ul>` or `<ol>` whenever default list markers are removed (e.g., `list-style: none`) so the list count remains exposed to screen readers.
- Pattern: Indicate the current page in a navigation — set `aria-current="page"` on the current-page link and reuse it as the CSS styling hook (`a[aria-current="page"]`) so the visual highlight only applies when the accessible state is set.
- Pattern: Hide decorative content from screen readers — add `aria-hidden="true"` to an element (e.g., a decorative `<svg>`) so it is excluded from the accessibility tree.
- Pattern: Provide an accessible description — give the descriptive element (e.g., a help paragraph) an `id` and reference it from the described element via `aria-describedby`.
- Pattern: Polyfill missing semantics — when HTML provides no equivalent element (e.g., a `tablist`), apply the appropriate ARIA role on a generic element such as `<div>` to expose the semantics in the accessibility tree; back the role with JavaScript-driven interactivity since the role itself adds no behaviour.
- Pattern: Provide an accessible name for an input — preferred: `<label for="user_name">User name</label>` paired with `<input type="text" id="user_name">`; alternative when a `<label>` cannot be used: `aria-labelledby` on the input pointing to the `id` of a text element (e.g., `<span id="uname">user name</span><input type="text" aria-labelledby="uname">`).
- Pattern: Build a custom button on a non-button element — add `role="button"` for semantics; make the element focusable (e.g., `tabindex="0"`); script Enter and Space to activate the action, mindful of the keydown/keyup difference between the two keys; style it like a button (including Forced Colors styles); test with keyboard and assistive tech to confirm the "role is a promise" contract is fulfilled.

## Complex Components

- Tabs: Composite structure — uses three ARIA roles together — `tablist` (container), `tab` (each tab control), and `tabpanel` (each panel of content).
- Tabs: Markup — wrap the set of tabs in an element with `role="tablist"` (no native HTML element maps to tablist); each tab is typically a `<button role="tab">`; each panel is typically a `<section role="tabpanel">`.
- Tabs: ARIA parent-child constraint — elements with `role="tab"` MUST be contained in or owned by an element with `role="tablist"`; `role="tab"` placed inside a `<nav><ul><li><a>` structure (without tablist) is invalid.
- Tabs: Behaviour — ARIA roles add no interactive behaviour; tab activation, panel switching, focus, and keyboard support must be implemented in JavaScript.
- Disclosure: Markup — a control (typically a `<button>`) sits adjacent to or above the panel it toggles.
- Disclosure: ARIA — set `aria-expanded="false"` on the control when collapsed and `"true"` when expanded; optionally use `aria-controls` to reference the controlled element's id (note: no longer exposed by most screen readers).
- Disclosure: State management — JavaScript must update `aria-expanded` on user interaction; without JavaScript the value is stale and can confuse screen-reader users.
- Toggle button: ARIA — use `<button aria-pressed="true|false">` to indicate whether the toggle is on or off.
- Toggle button: State management — JavaScript must flip `aria-pressed` when the user activates the button.
- Accordion: Markup — place a `<button aria-expanded="false">` inside the heading (e.g., `<h2><button aria-expanded="false">…</button></h2>`) rather than putting the role/state on the heading itself, preserving heading semantics for screen-reader navigation.
- Menu / Menubar: Structure — `role="menu"` or `role="menubar"` for the container with `role="menuitem"` children.
- Menu / Menubar: Children constraint — `menuitem` may not contain interactive children (no nested `<button>`, no `<a>`, no elements with implicit button/link roles).
- Menu / Menubar: Keyboard — Arrow keys navigate menu items; Space and Enter activate them; Esc closes the menu.
- Carousel: No native ARIA role — `role="carousel"` is invalid because ARIA is finite; the spec includes no carousel role.
- Breadcrumb: No native ARIA role — `role="breadcrumb"` is invalid; use `<nav aria-label="Breadcrumb">` so screen readers announce "Breadcrumb, Navigation" — role + name communicate everything that's needed.
- Modal dialog: ARIA category — modal dialogs fall under the "Window roles" category of ARIA roles, which describe windows within the browser.

## Anti-Patterns

- Anti-pattern: Exposing a form as a landmark when the form is the page's primary content — adds unnecessary noise.
- Anti-pattern: Surfacing too many landmarks on a page — decreases the user's efficiency in finding important areas; truly important regions stop standing out.
- Anti-pattern: Using `href="#"` (a meaningless `href`) on an `<a>` — a signal you should be using a button instead.
- Anti-pattern: Including the word "navigation" in a navigation's accessible name — screen readers end up announcing "Navigation" twice (once for the landmark role and once for the label).
- Anti-pattern: Using `<div>` to create a navigation instead of `<nav>` — loses the navigation landmark and (in Safari 16+) also strips list semantics from any list inside it.
- Anti-pattern: Adding ARIA when the HTML element already provides the semantics — redundant and discouraged; can introduce confusion or break behaviour.
- Anti-pattern: Using `role="heading"` on a `<button>` — the `heading` role is not permitted on `<button>`; the semantic-vs-functional mismatch creates usability problems and violates WCAG SC 4.1.2.
- Anti-pattern: Making up ARIA roles — invented roles like `role="carousel"` or `role="breadcrumb"` are invalid because ARIA is finite.
- Anti-pattern: Placing semantic descendants (e.g., an `<h3>`) inside `<button>`, `<summary>`, or `<div role="button">` — the button role's Children Presentational property suppresses descendants' semantics in the accessibility tree.
- Anti-pattern: Applying an interactive ARIA role without implementing the corresponding behaviour — you make a promise to screen-reader users you don't fulfil, creating a usability barrier.
- Anti-pattern: Adding ARIA state attributes without JavaScript to keep them in sync — stale state attributes are useless and can be actively confusing.
- Anti-pattern: Using key combinations users are unfamiliar with on a custom widget — screen readers won't announce them so users can't discover how to operate the widget.
- Anti-pattern: Expecting ARIA to change how Forced Colors / WHCM renders an element — WHCM uses inherent HTML semantics, not the accessibility tree, so a `<div role="button">` will render as plain text in WHCM regardless of ARIA.
- Anti-pattern: Using `role="tab"` outside a `tablist` — invalid markup; tab's parent must have `role="tablist"`.
- Anti-pattern: Repurposing `<div>` as a button with `role="button"` when `<button>` is available — violates the First Rule of ARIA and takes on the burden of focus, keyboard activation, and styling that `<button>` provides for free.
- Anti-pattern: Overriding meaningful element semantics with ARIA roles (e.g., `<h2 role="tab">`) — the heading semantics are lost from the accessibility tree; instead nest the heading inside an element bearing the role (e.g., `<div role="tab"><h2>…</h2></div>`).
- Anti-pattern: Making a heading itself an interactive control (`<h2 role="button" aria-expanded="false">`) — instead nest the interactive element inside the heading (`<h2><button aria-expanded="false">…</button></h2>`).
- Anti-pattern: `aria-hidden="true"` on a focusable element (e.g., `<button aria-hidden="true">`) — the element remains in the DOM and tab order, but screen readers don't announce it, so users focus on "nothing".
- Anti-pattern: `role="presentation"` on a focusable element (e.g., `<a href=".." role="presentation">`) — the element's semantics are suppressed; screen readers no longer announce the role even though the element is still focusable and active.
- Anti-pattern: `aria-hidden="true"` on an ancestor of a focusable element — the descendant inherits the hidden state from assistive technologies while remaining focusable and interactive.
- Anti-pattern: Interactive control without an accessible name (e.g., `<input>` with only a visually adjacent `<span>` label and no `for`/`id` association) — sighted users see the label, but the input has no accessible name in the accessibility tree.
- Anti-pattern: Redundant ARIA roles on native elements (`<button role="button">`, `<h1 role="heading" aria-level="1">`) — duplicates implicit semantics; explicit redundancy is wasted effort and a maintenance liability.
- Anti-pattern: Mirroring HTML state attributes with ARIA equivalents (`required` + `aria-required="true"`, `hidden` + `aria-hidden="true"`) — redundant and creates a sync liability if updated independently.

## Decision Rules

- Decision: Button vs link — if a control takes the user to another page or a section within the page (the URL changes when the element is clicked), use a link; if it changes something on the current page (layout, dialog, new view), use a button.
- Decision: Links take users places — that is their core difference from buttons.
- Decision: Is it really a link? — if you cannot right-click an element to open it in a new window, it is probably not a link.
- Decision: Is it really a button? — if an element does nothing without JavaScript, it is probably a button.
- Decision: Generic region vs specific landmark — reserve the generic region role for content that does not fit any other landmark type; prefer the specific HTML landmark element when one fits.
- Decision: `<ul>` vs `<ol>` — use `<ul>` when the order of items doesn't matter (e.g., a site navigation); use `<ol>` when order matters (e.g., breadcrumbs).
- Decision: `aria-current="page"` vs `aria-current="true"` — in navigation, use `page` so screen readers announce "link, current page" instead of just "link, current".
- Decision: When to reach for ARIA — first ask "is there an HTML element I can use instead?"; if yes, use that. Reach for ARIA only when HTML semantics fall short (e.g., to polyfill missing semantics like `tablist`, to override native ones, to convey state like `aria-pressed`, or to fix accessibility in legacy code you can't change).
- Decision: When to break the First Rule of ARIA — only when (1) the HTML feature isn't implemented or its accessibility support is missing, (2) visual design constraints prevent styling the native element as required, or (3) the feature doesn't exist in HTML at all.
- Decision: Custom widget keyboard keys — avoid unfamiliar key combinations because screen readers will not announce them.

## Keyboard Behaviour

- Key: Tab on native `<button>` — focusable by default; no `tabindex="0"` needed.
- Key: Tab on native `<a>` with `href` — focusable by default; no `tabindex="0"` needed.
- Key: Enter on native `<button>` — fires on keydown and continues firing while held.
- Key: Space on native `<button>` — fires on keyup; if Space is held and the user tabs away without releasing, the action will not fire.
- Key: Enter on native `<a>` — links are activated by the Enter key only.
- Key: Enter on a link-enhanced-as-button — fire the action on keydown (keyCode 13).
- Key: Space on a link-enhanced-as-button — fire the action on keyup (keyCode 32).

## Screen Reader & AT Behaviour

- AT: Accessibility tree as the source — accessibility information in the accessibility tree is shaped by HTML semantics, applied styles, and any ARIA attributes used; screen readers get their information about the page from this tree.
- AT: Landmark navigation availability — every screen reader provides at least one command or gesture for navigating between landmarks; per WebAIM's 9th screen reader user survey more than 25% of screen reader users use landmarks very often.
- AT: Beneficiaries of landmarks — primarily useful for screen reader users, but also benefit keyboard users who use browser extensions that enable landmark navigation via keyboard or a pop-up menu.
- AT: `<a>` without `href` — maps to the generic ARIA role, is not exposed in the accessibility tree, and is removed from the tab order.
- AT: Disabled link announcement — an `<a>` without `href` plus `role="link"` and `aria-disabled="true"` is announced by screen readers as a disabled/dimmed link, while the absence of `href` ensures it cannot be activated.
- AT: `role` attribute scope — changes only the exposed role in the accessibility tree; does not add behaviour or actually convert the element.
- AT: Not all ATs use the accessibility tree — Forced Colors modes such as Windows High Contrast Mode (now Contrast Themes in Win 11, standardised under `forced-colors` in CSS) use inherent HTML semantics rather than the accessibility tree; a native `<button>` picks up system colors because of its direct mapping, but a `<div role="button">` is treated as plain text — so an enhanced link-as-button or ARIA-button needs styles targeting Forced Colors modes to appear as a button.
- AT: Link-in-list announcements — when a link sits in a list inside a navigation, screen readers announce the link's position within the list and the total number of items, giving users a sense of how many links the navigation contains.
- AT: Safari and `list-style: none` — older versions of Safari on macOS remove list semantics (and item count) when default list markers are removed; Safari 16+ preserves list semantics only when the list is contained within a navigation landmark.
- AT: Link URL announcement — some screen reader users configure their screen reader to announce the URL of a link so they get an idea of where it will take them.
- AT: Current-page announcement — `aria-current="page"` causes screen readers to announce the link as "link, current page", conveying the same stateful information sighted users get from visual styling.
- AT: Browser-added interactivity — the browser adds focus and keyboard behaviour to native interactive elements (e.g., `<button>`) but NOT to elements that only have an interactive ARIA role; you must add focus, keyboard handling, and activation behaviour yourself.
- AT: Screen-reader instructions — when a screen reader encounters an element that invites interaction beyond reading, it typically provides instructions on how to interact with it based on the announced role.
- AT: Custom-key gap — if a custom widget uses non-standard key combinations, the screen reader will not surface those keys to the user.
- AT: Children Presentational — when an ARIA role's "Children Presentational" property is true (e.g., for the `button` role), browsers treat all descendants as if they had `role="presentation"`, suppressing their semantics in the accessibility tree.
- AT: `aria-controls` exposure — most screen readers no longer expose the `aria-controls` relationship to users.
- AT: ARIA support varies — ARIA support and behaviour varies between platforms, accessibility APIs, browsers, and assistive technologies; some parts may be fully supported, partially supported, or buggy. There is no feature-detection for ARIA — test with multiple browser/AT combinations.
- AT: `aria-hidden="true"` on a focusable element — the element is removed from the accessibility tree and not announced by screen readers, but it remains in the DOM and tab order; pressing Tab still moves focus to it, so the user focuses on "nothing".
- AT: `role="presentation"` on a link — suppresses the link's role in the accessibility tree; screen readers do not announce that it is a link when focused, but they still announce its text content.
- AT: ARIA does not affect the DOM or visual styles — adding an interactive role (e.g., `role="button"`) does not make the element interactive, focusable, or visually styled like a button; it only changes how the element is exposed in the accessibility tree.

## Tools

- Tool: WebAIM WAVE browser extension — evaluates web content for accessibility issues directly within the browser; the Structure tab provides a structural representation of the page including all landmarks and the heading structure within each landmark.
- Tool: a11ysupport.io — high-level overview of ARIA attributes and their expected support across browser/screen-reader combinations; the tests may not always be up-to-date, so always perform your own testing.

## Glossary

- Term: WCAG — Web Content Accessibility Guidelines.
- Term: Landmark region — a recognisable key area of a page or application that helps users orient themselves on a page and navigate easily to its different areas.
- Term: Semantics — what an element is, and therefore how it can be used.
- Term: Hyperlink — per the HTML living standard, an `<a>` element with an `href` attribute that represents a hypertext anchor labelled by its contents.
- Term: Navigation (component) — a component providing links to specific pages on the website or to sections of content within the same page; helps users determine their current position on the site and go to other locations.
- Term: WAI-ARIA / ARIA — Web Accessibility Initiative - Accessible Rich Internet Applications; a Web standard defining attributes that extend HTML to add semantic roles, states, and properties so elements can be better understood by assistive technologies.
- Term: Affordance — the quality or property of an object that defines its possible uses or makes clear how it can or should be used.
- Term: ARIA role — an attribute that describes what an element is; an indication of how it is meant to be used.
- Term: ARIA state — an attribute that expresses the current state of an element (e.g., `aria-pressed`, `aria-expanded`, `aria-current`).
- Term: ARIA property — an attribute that describes a property of an element such as its name, description, current value, or its relationship to other elements; less likely to change throughout an element's lifecycle than a state.
- Term: Composite role — an ARIA role that must be used in conjunction with other roles to compose one UI widget (e.g., `tablist` with `tab` and `tabpanel`).
- Term: Children Presentational — a property of certain ARIA roles; when true, browsers treat all descendants as if they had `role="presentation"`, suppressing their semantics in the accessibility tree.
- Term: Redundant ARIA — explicitly adding ARIA roles, states, or properties to an element that already maps to those semantics implicitly via HTML; wasted effort and a sync liability when state attributes diverge from their HTML counterparts.
- Term: ARIA polyfill — using ARIA as a last-resort gap-filler for missing or insufficient HTML semantics, not as a default authoring tool.
