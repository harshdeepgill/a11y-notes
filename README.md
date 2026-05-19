## Rules

- Rule: An element's accessibility information has four parts — role, name, description, and state.
- Rule: Semantics should provide three main pieces of information — the role of the element (what it is/does), the name (identifies the element and its purpose), and the state (where applicable, the current state of the element).
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

## HTML Elements

- Element: `<header>` — implicit banner role; only exposed as a banner landmark when it is a direct child of `<body>`, not when nested in another sectioning element such as `<article>` or `<section>`.
- Element: `<nav>` — implicit navigation role; multiple navigation landmarks per page are allowed; preserves list semantics inside in Safari 16+ when default list markers are removed via CSS.
- Element: `<main>` — implicit main role; should be a direct child of `<body>`, with only one main landmark per page.
- Element: `<footer>` — implicit contentinfo role only when scoped directly to `<body>`; not exposed as contentinfo when nested in another sectioning element.
- Element: `<aside>` — implicit complementary role; should be a sibling or child of the main landmark.
- Element: `<form>` — only exposed as a form landmark when it has an accessible name.
- Element: `<search>` — maps to the search landmark role; preferred over legacy `role="search"` on a `<form>` or `<div>`.
- Element: `<section>` — does not affect the document outline, but its implicit region role is exposed as a landmark when it is given an accessible name — preferred element for custom regions.
- Element: `<div>` — no implicit landmark role; can be turned into a landmark by adding an explicit ARIA `role` attribute when markup cannot be changed; using `<div>` instead of `<nav>` loses the navigation landmark and (in Safari 16+) also strips list semantics from any list inside it.
- Element: `<button>` — implicit button role with semantics and behaviour baked in; does nothing on its own except inside a `<form>`, where it may submit the form; focusable by default (no `tabindex="0"` needed); keyboard operable via Space and Enter; can be disabled with the HTML `disabled` attribute.
- Element: `<a>` — has an implicit link role only when it has an `href` attribute; without `href` it represents a placeholder for a link, maps to the generic ARIA role, is not exposed in the accessibility tree, and is removed from the tab order (not even focusable in most browsers); when it has `href` it is focusable by default (no `tabindex="0"` needed) and is activated by the Enter key only.
- Element: `<ul>` — maps to the `list` role; conveys the number and order of items to screen readers; older Safari versions and Safari 16+ outside a navigation landmark remove list semantics when `list-style: none` is applied; can be safeguarded with `role="list"`.
- Element: `<ol>` — maps to the `list` role; semantically appropriate when order matters (e.g., breadcrumbs); shares the same Safari list-semantics caveats as `<ul>`.
- Element: `<li>` — list item element used inside `<ul>` or `<ol>`.
- Element: `<span>` — frequently used with the HTML `hidden` attribute to create a visually-hidden text label referenced from another element via `aria-labelledby`.

## ARIA Roles

- Role: `banner` — landmark for site-wide header content like the company logo, main site navigation, user login links, and a global search component; ideally only one per site.
- Role: `navigation` — landmark for a collection of navigational elements (usually links) for navigating within a website.
- Role: `main` — landmark designating the primary content of the page; only one per page.
- Role: `contentinfo` — landmark for information about the parent document; typically the page footer with copyright, privacy and accessibility links.
- Role: `complementary` — landmark for secondary information related to the main content yet understandable without it (e.g., sidebars, call-out boxes, list of related articles).
- Role: `form` — landmark for a form; only exposed when the form has an accessible name.
- Role: `search` — landmark for a collection of elements that together create a search facility (search of the site, of the current page, or an Internet-wide search).
- Role: `region` — generic landmark for a perceivable section of content important enough that users will likely want to navigate to it and see it listed in a page summary; requires an accessible name.
- Role: `button` — exposes an element as a button in the accessibility tree; only changes the exposed role, not behaviour.
- Role: `link` — exposes an element as a link in the accessibility tree (used to reinstate link semantics after removing `href`).
- Role: `generic` — what an `<a>` without an `href` maps to; not exposed in the accessibility tree.
- Role: `list` — implicit role of `<ul>` and `<ol>`; can be re-instated with `role="list"` when CSS strips list semantics.

## Attributes

- Attribute: `role` — ARIA attribute that exposes an element's type in the accessibility tree (e.g., `button`, `link`, `banner`, `navigation`, `main`, `contentinfo`, `complementary`, `form`, `search`, `region`, `list`); changes only the exposed role, not behaviour.
- Attribute: `aria-label` — Provides an accessible name; the attribute's value is used directly as the label.
- Attribute: `aria-labelledby` — Provides an accessible name by referencing another element (typically a heading or a hidden `<span>`) on the page as the label.
- Attribute: `aria-disabled` — Conveys disabled state to assistive technologies, e.g., `aria-disabled="true"`.
- Attribute: `aria-current` — Used on a link to indicate it is the current item in a set; supports values such as `true` and `page` — `page` causes screen readers to announce "link, current page" instead of just "link, current".
- Attribute: `href` — Required on `<a>` for it to be a hyperlink; defines the link's destination as a URL or in-page fragment.
- Attribute: `disabled` — HTML attribute that disables form controls including `<button>`; does not apply to links.
- Attribute: `download` — `<a>` attribute that triggers a file download instead of navigation.
- Attribute: `tabindex` — Controls focusability and tab order; `tabindex="0"` makes an otherwise non-focusable element focusable.
- Attribute: `hidden` — Used on an element (e.g., a `<span>`) to create a visually hidden text label that can still be referenced by `aria-labelledby` to name a landmark.
- Attribute: `title` — Can be used to indicate the purpose of a landmark such as a `<search>` element when no visible label is available.

## WCAG Success Criteria

- WCAG: SC 1.3.1 Info and Relationships — "Information, structure, and relationships conveyed through presentation can be programmatically determined or are available in text." Using the appropriate semantic elements to identify key areas of the page is required to meet this criterion.
- WCAG: SC 2.4.1 Bypass Blocks — exists to ensure assistive technology users have a way to bypass repeated content and facilitate page navigation; using proper landmark elements is one way to meet this criterion.

## Patterns & Recipes

- Pattern: Name a navigation landmark — give the `<nav>` an `aria-label` describing its purpose (e.g., "Site", "Breadcrumbs"); or use `aria-labelledby` to reference an on-page heading or a visually-hidden `<span hidden>` placed inside the `<nav>`; do not include the word "navigation" in the label.
- Pattern: Label an `<aside>` — add a descriptive heading inside the `<aside>` and reference it from the `<aside>` via `aria-labelledby`.
- Pattern: Label multiple complementary landmarks — give each `<aside>` a descriptive heading and reference it via `aria-labelledby`.
- Pattern: Create a search landmark — wrap the search controls in `<search>`; give it an accessible name via a heading + `aria-labelledby`, `aria-label`, `title`, or a hidden text label (e.g., a `<span hidden>`) referenced by `aria-labelledby`.
- Pattern: Create a custom region — wrap content in `<section>` (or use a `<div>` with `role="region"`) and give it an accessible name, preferably referencing a visible heading via `aria-labelledby`.
- Pattern: Retrofit landmarks onto an existing site — apply ARIA role values (banner, navigation, main, contentinfo, complementary, form, search, region) to existing elements like `<div>` when the markup cannot be changed.
- Pattern: Disable a link — remove its `href` so the browser no longer provides link interactive behaviour; reinstate link semantics with `role="link"`; convey the disabled state to screen readers with `aria-disabled="true"`.
- Pattern: Enhance a link into a button — override link semantics with `role="button"`; attach a click handler that calls `e.preventDefault()` and triggers the action; implement full button keyboard behaviour by firing on keydown for Enter (keyCode 13) and on keyup for Space (keyCode 32); add styles targeting Forced Colors modes (e.g., Windows High Contrast Mode) so it appears as a button.
- Pattern: Build an accessible site/breadcrumb navigation — wrap links in `<nav>` and give it an accessible name; group links inside `<ul>` (unordered) or `<ol>` (ordered, for breadcrumbs) with each link in an `<li>`; add `role="list"` to safeguard list semantics when CSS removes default markers; mark the current-page link with `aria-current="page"` and style it via `a[aria-current="page"]`.
- Pattern: Preserve list semantics across CSS changes — add `role="list"` to the `<ul>` or `<ol>` whenever default list markers are removed (e.g., `list-style: none`) so the list count remains exposed to screen readers.
- Pattern: Indicate the current page in a navigation — set `aria-current="page"` on the current-page link and reuse it as the CSS styling hook (`a[aria-current="page"]`) so the visual highlight only applies when the accessible state is set.

## Anti-Patterns

- Anti-pattern: Exposing a form as a landmark when the form is the page's primary content — adds unnecessary noise.
- Anti-pattern: Surfacing too many landmarks on a page — decreases the user's efficiency in finding important areas; truly important regions stop standing out.
- Anti-pattern: Using `href="#"` (a meaningless `href`) on an `<a>` — a signal you should be using a button instead.
- Anti-pattern: Including the word "navigation" in a navigation's accessible name — screen readers end up announcing "Navigation" twice (once for the landmark role and once for the label).
- Anti-pattern: Using `<div>` to create a navigation instead of `<nav>` — loses the navigation landmark and (in Safari 16+) also strips list semantics from any list inside it.

## Decision Rules

- Decision: Button vs link — if a control takes the user to another page or a section within the page (the URL changes when the element is clicked), use a link; if it changes something on the current page (layout, dialog, new view), use a button.
- Decision: Links take users places — that is their core difference from buttons.
- Decision: Is it really a link? — if you cannot right-click an element to open it in a new window, it is probably not a link.
- Decision: Is it really a button? — if an element does nothing without JavaScript, it is probably a button.
- Decision: Generic region vs specific landmark — reserve the generic region role for content that does not fit any other landmark type; prefer the specific HTML landmark element when one fits.
- Decision: `<ul>` vs `<ol>` — use `<ul>` when the order of items doesn't matter (e.g., a site navigation); use `<ol>` when order matters (e.g., breadcrumbs).
- Decision: `aria-current="page"` vs `aria-current="true"` — in navigation, use `page` so screen readers announce "link, current page" instead of just "link, current".
- Decision: When to reach for ARIA — when HTML semantics fall short (e.g., no native HTML attribute identifies the current element in a set), supplement with ARIA attributes.

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
- AT: Not all ATs use the accessibility tree — Forced Colors modes such as Windows High Contrast Mode use the inherent semantics of the element rather than the accessibility tree, so an enhanced link-as-button needs styles targeting those modes to appear as a button.
- AT: Link-in-list announcements — when a link sits in a list inside a navigation, screen readers announce the link's position within the list and the total number of items, giving users a sense of how many links the navigation contains.
- AT: Safari and `list-style: none` — older versions of Safari on macOS remove list semantics (and item count) when default list markers are removed; Safari 16+ preserves list semantics only when the list is contained within a navigation landmark.
- AT: Link URL announcement — some screen reader users configure their screen reader to announce the URL of a link so they get an idea of where it will take them.
- AT: Current-page announcement — `aria-current="page"` causes screen readers to announce the link as "link, current page", conveying the same stateful information sighted users get from visual styling.

## Tools

- Tool: WebAIM WAVE browser extension — evaluates web content for accessibility issues directly within the browser; the Structure tab provides a structural representation of the page including all landmarks and the heading structure within each landmark.

## Glossary

- Term: WCAG — Web Content Accessibility Guidelines.
- Term: Landmark region — a recognisable key area of a page or application that helps users orient themselves on a page and navigate easily to its different areas.
- Term: Semantics — what an element is, and therefore how it can be used.
- Term: Hyperlink — per the HTML living standard, an `<a>` element with an `href` attribute that represents a hypertext anchor labelled by its contents.
- Term: Navigation (component) — a component providing links to specific pages on the website or to sections of content within the same page; helps users determine their current position on the site and go to other locations.
