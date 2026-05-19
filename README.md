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
- Rule: Don't work around implicit ARIA role mappings — you rarely have to, and doing so (e.g., forcing `role="button"` on `<summary>`) tends to break state exposure and cross-platform announcements.
- Rule: Add controls and ARIA attributes that require JavaScript from inside your script, not hard-coded into the markup — so users aren't left with broken controls and hidden content if JavaScript fails to load.
- Rule: Apply progressive enhancement to interactive components — start with a working static version, then enhance with JavaScript, so the content remains accessible if the script fails for any reason (spotty connection, browser-extension interference, data-saver mode, reader mode, etc.).
- Rule: To hide content from all users, use the HTML `hidden` attribute, CSS `display: none`, or CSS `visibility: hidden`.
- Rule: Always place a content panel directly after its trigger in the DOM (source order), even when `aria-controls` is used — so screen-reader users can continue navigating into the revealed content and keyboard users can quickly move focus to interactive elements within the panel.
- Rule: Use `aria-label` only as a last resort — prefer `aria-labelledby` referencing a visible heading or a hidden text node.
- Rule: When a text node only exists to supply an `aria-labelledby` target (not as page content), hide it with the HTML `hidden` attribute rather than a visually-hidden CSS class — `hidden` removes it from the accessibility tree as content while `aria-labelledby` still exposes it as the accessible name, avoiding a double announcement.
- Rule: Visually grouping disclosure widgets to look like an accordion is not enough — also convey the relationship semantically (group or region) and, when the accordion is exclusive, implement the group behaviour.
- Rule: A group needs an accessible name to identify its purpose — without one, it is just an unidentified collection of items.
- Rule: Not all that's accessible is necessarily usable — usability matters beyond technical accessibility; usability test with disabled and AT users.
- Rule: A group of `<input type="radio">` elements sharing the same `name` is automatically exclusive — at most one can be selected, and browsers expose group size via `aria-setsize` and position via `aria-posinset`.
- Rule: Headings are text elements and cannot be activated — they are meant to contribute to the page's heading hierarchy and be navigated to via screen reader shortcuts.
- Rule: To make a heading control a disclosure, wrap the heading around the `<button>` — not the other way around — so the heading semantics are retained and the trigger is interactive.
- Rule: The HTML `name` attribute does not work on custom (button-based) disclosure widgets; if the accordion is exclusive, implement the group behaviour in JavaScript.
- Rule: When using `hidden="until-found"`, apply padding/borders/backgrounds to a child container inside the hidden element rather than to the hidden element itself — under until-found the browser uses `content-visibility: hidden` and the element still generates a box.
- Rule: When using `hidden="until-found"`, audit reset stylesheets for `[hidden] { display: none !important; }` — that declaration overrides find-in-page reveal; replace with `[hidden]:not(:is([hidden="until-found"])) { display: none !important; }` so plain `hidden` keeps strong specificity while until-found still works.
- Rule: Use `hidden="until-found"` only as a progressive enhancement — ensure the content remains usable in browsers that don't yet support it.
- Rule: The end markup is key — regardless of the starting semantic skeleton (sections-with-headings, description list, etc.) you progressively enhance from, the final markup should semantically represent a meaningful grouping of accessible disclosure widgets.
- Rule: Why you are hiding an element determines which technique is most appropriate; the technique you choose determines who, if anyone, will have access to the element.
- Rule: Before hiding an element, ask — why are you hiding it (UX vs aesthetic), who are you hiding it from, who do you want to expose it to, who benefits from the hidden element, and what type of element is it (interactive vs static text).
- Rule: Aim for parity between keyboard and screen-reader experiences — if an element is keyboard-accessible, it should also be screen-reader-accessible.
- Rule: An element that is not visually accessible should not be focusable, unless it is un-hidden when it receives focus; when an element receives keyboard focus it should be clearly visible so users know what they are focusing on.
- Rule: Avoid hiding interactive/focusable elements using `aria-hidden` — modern browsers (e.g., Chrome) expose focusable elements to assistive technologies even when paired with `tabindex="-1"`, so focus can land on an element that isn't announced.
- Rule: To re-expose an element previously hidden with `aria-hidden`, remove the attribute altogether — `aria-hidden="false"` is inconsistent across browsers.
- Rule: `tabindex` cannot make an element non-focusable — only `disabled` or `inert` can.
- Rule: Test new CSS properties (e.g., `display: contents`, `content-visibility`) across browsers and screen readers before relying on them — implementation gaps may affect accessibility.
- Rule: Dim or obscure inert content to provide a visual cue that it is not currently accessible to anyone.
- Rule: Style disabled controls so the browser's default low-contrast grey doesn't compromise visual accessibility; usability-test disabled controls.
- Rule: Inside a `content-visibility: auto` container, hide descendants from screen readers via HTML or ARIA — CSS hides (`display: none`, `visibility: hidden`) aren't applied while rendering is postponed.
- Rule: Use the `visually-hidden` utility class only for textual content (and specific link cases like skip links).
- Rule: Prefer the class name `visually-hidden` over `sr-only` — the content is exposed via accessibility APIs to more than just screen readers.
- Rule: Prefer `role="none"` over `role="presentation"` — they are synonymous; `none` is less likely to be confused with `aria-hidden="true"`.
- Rule: Test every hiding choice with a screen reader and a check of the accessibility tree — different browser/AAPI combinations announce differently, and some browsers correct misuse by exposing content that "should" be hidden.
- Rule: Don't use the `visually-hidden` utility class on interactive elements — only static textual content; touch screen-reader users exploring by haptics won't reach a 1px-clipped interactive element.
- Rule: Don't hide an interactive element by moving it off-canvas (outside the viewport) — touch screen-reader users dragging their finger across the screen won't find it.
- Rule: When visually replacing a native form control with an image, keep the native control within the viewport in its natural position so touch screen-reader users can locate it via haptics.
- Rule: Don't shrink a replaced form control to 1px — it becomes very difficult to find by touch.
- Rule: Hide the visual replacement (e.g., an inline `<svg>`) with `aria-hidden="true"` so the native control remains the source of truth in the accessibility tree.
- Rule: Place the `<input>` AND its visual replacement (e.g., an inline `<svg>`) inside the control's `<label>` to enlarge the interactive area.
- Rule: Prefer inline `<svg>` over external/`<img>` when you need CSS access to the SVG's inner shapes, animations, or Forced Colors adaptation.
- Rule: Render every native state on the visual replacement — checked, unchecked, disabled, focus, hover, and (where applicable) indeterminate.
- Rule: Optimise custom-styled form controls for Forced Colors modes via a `@media (forced-colors: active)` block.

## HTML Elements

- Element: `<header>` — implicit banner role; only exposed as a banner landmark when it is a direct child of `<body>`, not when nested in another sectioning element such as `<article>` or `<section>`.
- Element: `<nav>` — implicit navigation role; multiple navigation landmarks per page are allowed; preserves list semantics inside in Safari 16+ when default list markers are removed via CSS.
- Element: `<main>` — implicit main role; should be a direct child of `<body>`, with only one main landmark per page.
- Element: `<footer>` — implicit contentinfo role only when scoped directly to `<body>`; not exposed as contentinfo when nested in another sectioning element.
- Element: `<aside>` — implicit complementary role; should be a sibling or child of the main landmark.
- Element: `<form>` — only exposed as a form landmark when it has an accessible name.
- Element: `<search>` — maps to the search landmark role; preferred over legacy `role="search"` on a `<form>` or `<div>`.
- Element: `<section>` — does not affect the document outline, but its implicit region role is exposed as a landmark when it is given an accessible name — preferred element for custom regions; also commonly used with `role="tabpanel"` for tab panels; can serve as a grouping element for a disclosure content panel when stronger semantics or landmark exposure is needed; named `<section>` is the preferred container for an accordion when the accordion's content is important enough to surface as a page landmark.
- Element: `<article>` — grouping element suitable for a disclosure content panel when its semantics are appropriate.
- Element: `<div>` — no implicit landmark role; can be turned into a landmark by adding an explicit ARIA `role` attribute when markup cannot be changed; using `<div>` instead of `<nav>` loses the navigation landmark and (in Safari 16+) also strips list semantics from any list inside it; commonly used with `role="tablist"` since no native HTML element maps to tablist; default grouping element for a disclosure content panel; with `role="group"` and an accessible name, becomes a non-landmark logical group (useful for accordion containers that shouldn't appear in the page outline).
- Element: `<button>` — implicit button role with semantics and behaviour baked in; does nothing on its own except inside a `<form>`, where it may submit the form; focusable by default (no `tabindex="0"` needed); keyboard operable via Space and Enter; can be disabled with the HTML `disabled` attribute; does not come with a built-in way to communicate expanded/collapsed state (use `aria-expanded`); ARIA roles permitted on `<button>` are `checkbox`, `link`, `menuitem`, `menuitemcheckbox`, `menuitemradio`, `option`, `radio`, `switch`, and `tab` — other roles (like `heading`) are not permitted.
- Element: `<a>` — has an implicit link role only when it has an `href` attribute; without `href` it represents a placeholder for a link, maps to the generic ARIA role, is not exposed in the accessibility tree, and is removed from the tab order (not even focusable in most browsers); when it has `href` it is focusable by default (no `tabindex="0"` needed) and is activated by the Enter key only.
- Element: `<ul>` — maps to the `list` role; conveys the number and order of items to screen readers; older Safari versions and Safari 16+ outside a navigation landmark remove list semantics when `list-style: none` is applied; can be safeguarded with `role="list"`.
- Element: `<ol>` — maps to the `list` role; semantically appropriate when order matters (e.g., breadcrumbs); shares the same Safari list-semantics caveats as `<ul>`.
- Element: `<li>` — list item element used inside `<ul>` or `<ol>`.
- Element: `<span>` — frequently used with the HTML `hidden` attribute to create a visually-hidden text label referenced from another element via `aria-labelledby`; when used purely as an `aria-labelledby` target, prefer `hidden` over a visually-hidden CSS class to avoid double announcement.
- Element: `<svg>` — can be excluded from the accessibility tree (hidden from screen readers) by adding `aria-hidden="true"` when decorative; preferred over CSS pseudo-elements for state-marker icons (e.g., on a disclosure trigger) because it offers more styling control and adapts better to Forced Colors modes. Inline `<svg>` (vs external/`<img>`) is animatable and lets CSS reach the SVG's inner shapes; when placed directly after a form control inside its `<label>`, the SVG can be styled via adjacent-sibling selectors (`input:focus-visible + svg`, `input:disabled + svg`, `input:checked + svg`) to mirror the control's states.
- Element: `<summary>` — child of `<details>`; has no implicit ARIA role in the ARIA-in-HTML spec but gets a meaningful computed role only when it is the first child of its `<details>` parent (otherwise treated as a generic `<div>`); may be exposed as "Push Button", "Button", "Summary", or "disclosure triangle" depending on platform/browser/AAPI; interactive element with browser-baked keyboard support (operable via Space and Enter); activating it toggles the `open` attribute on its `<details>` parent; comes with implicit expanded/collapsed state exposed to screen readers; subject to the Children Presentational rule.
- Element: `<details>` — implicit `group` role; native disclosure-widget container; the first `<summary>` child is the trigger and everything after it inside `<details>` is the controlled content; the browser toggles the `open` attribute to show/hide the content; can only have one trigger (extra `<summary>` elements are ignored as triggers); if no `<summary>` is provided, the browser supplies a generic "Details" label; supports a `name` attribute that, when shared across a group of `<details>`, makes them mutually exclusive (at most one open at a time) without JavaScript; Dragon voice software deprioritises `<details>` compared to buttons/links, making them harder for Dragon users to activate.
- Element: `<p>` — technically usable as the content panel of a disclosure widget; prefer a grouping element when the panel may contain more than a single paragraph.
- Element: `<input>` — form control; requires an accessible name supplied programmatically via `<label for>` (preferred), `aria-label`, or `aria-labelledby` — visible-only labels (e.g., an adjacent `<span>` with no association) leave the input without an accessible name. Browsers ship default state styling (checked/selected/disabled) and adjust colors for Forced Colors modes; these styles can be visually replaced by an inline `<svg>` while keeping the native input as the source of truth for assistive tech.
- Element: `<input type="checkbox">` — checkbox form control with built-in browser state styling for checked, unchecked, disabled, and Forced Colors; can be visually replaced by an inline `<svg aria-hidden="true">` placed after it inside the `<label>`, while the input itself remains interactive and screen-reader-accessible via the inclusive-hide technique (`position: absolute; opacity: 0`).
- Element: `<input type="radio">` — radio button; a group of radio buttons sharing the same `name` attribute becomes mutually exclusive (only one can be selected); browsers expose group size via `aria-setsize` and the focused item's position via `aria-posinset`, so screen readers can announce "radio button, 1 of 3" or similar. Like checkboxes, ships default checked/disabled/Forced Colors styling and can be visually replaced by an inline `<svg>` using the same inclusive-hide technique.
- Element: `<label>` — programmatically associates with a form control via its `for` attribute matching the control's `id`; the label text becomes the control's accessible name. Wrapping the `<input>` AND its visual replacement (e.g., an inline `<svg>`) inside the `<label>` enlarges the control's interactive area.
- Element: `<h2>` — visible heading commonly used as the accessible name source for a group or region via `aria-labelledby`.
- Element: `<fieldset>` — form-grouping element; applying `disabled` disables the fieldset and all of its descendant controls; applying `inert` makes the region and its descendants inert (rendered but inaccessible).
- Element: `<dialog>` — native HTML dialog element; when used in modal mode, the browser provides built-in inert-outside behaviour, sparing you from DOM-traversal + `aria-hidden` plumbing.
- Element: `<select>` — form control that can be disabled with the `disabled` attribute (no keyboard focus, no mouse events, no tab key).
- Element: `<img>` — applying `role="none"`, `aria-hidden="true"`, or `alt=""` to an `<img>` all hide it equivalently from screen readers (suitable for decorative images).
- Element: `<table>` — applying `role="none"` suppresses the table's own role AND the semantics of its required children (`<tr>`, `<td>`, etc.) because those children are required and semantically tied; useful for layout tables in legacy codebases.

## ARIA Roles

- Role: `banner` — landmark for site-wide header content like the company logo, main site navigation, user login links, and a global search component; ideally only one per site.
- Role: `navigation` — landmark for a collection of navigational elements (usually links) for navigating within a website.
- Role: `main` — landmark designating the primary content of the page; only one per page.
- Role: `contentinfo` — landmark for information about the parent document; typically the page footer with copyright, privacy and accessibility links.
- Role: `complementary` — landmark for secondary information related to the main content yet understandable without it (e.g., sidebars, call-out boxes, list of related articles).
- Role: `form` — landmark for a form; only exposed when the form has an accessible name.
- Role: `search` — landmark for a collection of elements that together create a search facility (search of the site, of the current page, or an Internet-wide search).
- Role: `region` — generic landmark for a perceivable section of content important enough that users will likely want to navigate to it and see it listed in a page summary; requires an accessible name.
- Role: `button` — exposes an element as a button in the accessibility tree; widget role with a Children Presentational property that suppresses descendants' semantics; only changes the exposed role, not behaviour; doesn't convey expanded/collapsed state on its own.
- Role: `link` — exposes an element as a link in the accessibility tree (used to reinstate link semantics after removing `href`).
- Role: `generic` — what an `<a>` without an `href` (and a `<div>`/`<span>` by default) maps to; not exposed in the accessibility tree.
- Role: `list` — implicit role of `<ul>` and `<ol>`; can be re-instated with `role="list"` when CSS strips list semantics.
- Role: `group` — represents a set of UI elements forming a logical collection of items in a widget; the implicit role of `<details>`; principal difference from `region` is that a group is **not** included in the page summary, outline, or table of contents by assistive technologies; needs an accessible name to identify its purpose.
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
- Role: `presentation` — suppresses an element's implicit semantics in the accessibility tree; the element no longer maps to its native role UNLESS the element is focusable (natively or via `tabindex`) OR it has a global ARIA state/property (e.g., `aria-label`); descendants of certain roles are treated as if they had `role="presentation"`; on a focusable element (e.g., a link), screen readers no longer announce the role but still announce the element's contents. ARIA 1.1 introduced `role="none"` as a synonym — `presentation` is often confused with `aria-hidden="true"`; prefer `role="none"`.
- Role: `none` — synonym of `presentation`; preferred wording because it is less likely to be misread as "hide this element"; same suppression rules and exceptions apply.

## Attributes

- Attribute: `role` — ARIA attribute that exposes an element's type in the accessibility tree (e.g., `button`, `link`, `banner`, `navigation`, `main`, `contentinfo`, `complementary`, `form`, `search`, `region`, `list`, `group`, `tablist`, `tab`, `tabpanel`, `menu`, `menubar`, `menuitem`, `presentation`); changes only the exposed role, not behaviour.
- Attribute: `aria-label` — Provides an accessible name; the attribute's value is used directly as the label; recommended only as a last resort — prefer `aria-labelledby` referencing a visible heading or a hidden text node.
- Attribute: `aria-labelledby` — Provides an accessible name by referencing another element (typically a heading or a hidden `<span>`) on the page as the label.
- Attribute: `aria-describedby` — Property that references one or more elements on the page to provide an accessible description for the element it is used on.
- Attribute: `aria-disabled` — Conveys disabled state to assistive technologies, e.g., `aria-disabled="true"`.
- Attribute: `aria-current` — Used on a link to indicate it is the current item in a set; supports values such as `true` and `page` — `page` causes screen readers to announce "link, current page" instead of just "link, current".
- Attribute: `aria-pressed` — State on a button-like element indicating whether the toggle is currently pressed (`true`) or not (`false`); changes must be managed via JavaScript.
- Attribute: `aria-expanded` — State indicating whether the element, or another grouping element it controls, is currently expanded (`true`) or collapsed (`false`); when used on a `<button>`, also communicates that the control is a disclosure button controlling the visibility of something; update via JavaScript on user interaction.
- Attribute: `aria-controls` — Property that identifies the element(s) whose contents or presence are controlled by the current element, via the controlled element's `id`; optional and effectively only supported by JAWS (poorly) — most screen readers no longer expose this relationship.
- Attribute: `aria-hidden` — Property that determines whether the element is included in the accessibility tree; when `true`, the element is excluded from the tree and hidden from screen readers — but it remains in the DOM and tab order, so applying it to a focusable element or an ancestor of one results in users focusing on "nothing"; modern browsers (e.g., Chrome) inconsistently still expose focusable elements even with `aria-hidden="true"` + `tabindex="-1"`. Setting `aria-hidden` with no value is equivalent to not setting it at all — the browser ignores it and determines visibility from other factors. `aria-hidden="false"` should re-expose the element but cross-browser support is inconsistent — to re-expose, remove the attribute entirely. Commonly used to hide decorative content (e.g., an SVG icon next to an equivalent text label).
- Attribute: `aria-valuetext` — Property holding a textual value for an element (e.g., an HTML range slider); should change as the user changes the element's value.
- Attribute: `aria-valuenow` — Property holding the current numeric value of an element; should change as the user changes the element's value.
- Attribute: `aria-level` — Property paired with the `heading` role to indicate heading level.
- Attribute: `aria-required` — ARIA state for required form controls; equivalent to HTML `required`; using both is redundant and can fall out of sync.
- Attribute: `aria-setsize` — ARIA property exposing the total number of items in a set (e.g., a `name`-grouped radio button group); auto-set by browsers for grouped radio buttons today and expected to be auto-set for `name`-grouped `<details>` in the future.
- Attribute: `aria-posinset` — ARIA property exposing an item's position within its set; auto-set by browsers for `name`-grouped radio buttons today and expected for `name`-grouped `<details>` in the future.
- Attribute: `href` — Required on `<a>` for it to be a hyperlink; defines the link's destination as a URL or in-page fragment.
- Attribute: `disabled` — Boolean HTML attribute that disables an interactive element — typically a form control such as `<button>`, `<input>`, `<select>`, or `<fieldset>` (cascades to all descendants); any value (or no value) disables the element because `disabled` is boolean. When set, the element no longer receives keyboard focus or mouse events and is removed from the tab order; it remains in the accessibility tree and screen readers announce the disabled state. Does not apply to links. Browsers often render disabled controls in low-contrast grey — author styles must restore visual accessibility.
- Attribute: `required` — HTML boolean attribute on form controls; native equivalent of `aria-required="true"`; prefer it over the ARIA equivalent.
- Attribute: `download` — `<a>` attribute that triggers a file download instead of navigation.
- Attribute: `tabindex` — Controls focusability and tab order; `tabindex="0"` makes an otherwise non-focusable element focusable; a negative integer (e.g., `tabindex="-1"`) on an interactive element removes it from the page's tabbing order while keeping it focusable programmatically and via mouse; cannot be used to make an element non-focusable — only `disabled` or `inert` can.
- Attribute: `inert` — Boolean HTML attribute on a region; the region and all descendants are visually rendered but are NOT exposed to accessibility APIs, are completely non-interactive (not keyboard-accessible), and are not targeted by any user-interaction events (mouse, touch included). Useful for the page content outside a custom modal dialog so that no interaction happens behind the backdrop. The `<dialog>` element provides this behaviour for free when used in modal mode.
- Attribute: `hidden` — HTML attribute that hides an element from rendering and removes it from the accessibility tree; when the hidden element is referenced via `aria-labelledby`, the browser still exposes its text as the accessible name for the referencing element — useful for providing a name without leaving the text node as a separate reading stop for screen readers; pairing `hidden` with `aria-hidden="true"` is redundant. Supports two states — the default (`hidden`) state applies `display: none`, while the "until-found" state (`hidden="until-found"`) keeps the content discoverable to browser find-in-page and fragment navigation by using `content-visibility: hidden` instead of `display: none`; in until-found the element still generates a box, so apply padding/borders/backgrounds to a child container; once revealed via find-in-page the content stays visible (no native way to recollapse); `display: none`, `display: contents`, or `display: inline` on the until-found element prevents reveal. Chromium-only support at the time of the lecture; part of the Interop 2025 project.
- Attribute: `open` — HTML boolean attribute on `<details>` that the browser toggles when the first `<summary>` is activated; controls whether the disclosure widget's content is visible; the browser also rewrites this attribute in the markup when `name`-based exclusive grouping is enforced.
- Attribute: `name` — HTML attribute; on `<input type="radio">`, groups radio buttons so only one in the group can be selected at a time; on `<details>`, when the same non-empty value is set on multiple elements, enforces that at most one `<details>` in the group is `open` at a time — the browser updates the `open` attributes in markup as it enforces exclusivity, offloading exclusive-accordion behaviour from JavaScript to the browser.
- Attribute: `title` — Can be used to indicate the purpose of a landmark such as a `<search>` element when no visible label is available.
- Attribute: `for` — `<label>` attribute referencing an input's `id` to programmatically associate the label with the input and expose its text as the input's accessible name.
- Attribute: `id` — HTML attribute used to be referenced by `<label for>`, `aria-labelledby`, `aria-describedby`, or `aria-controls` for programmatic association.

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
- Pattern: Hidden-label name source — add a `<span hidden id="x">…</span>` and reference it from the named element via `aria-labelledby="x"`; the browser exposes the span text as the accessible name while the screen reader does not encounter the text node again as page content.
- Pattern: Expose a logical group (no landmark) — wrap related items in `<div role="group">` and give it an accessible name via `aria-labelledby` (preferred — point to a visible or hidden heading/span) or `aria-label` as a last resort; the group is recognised by AT but does not appear in the page outline.
- Pattern: Expose a logical group as a landmark region — wrap related items in `<section>` with an accessible name via `aria-labelledby` pointing to a visible heading; this puts the group into the page's Landmarks list.
- Pattern: Build the `visually-hidden` utility class — selector `.visually-hidden:not(:focus):not(:active)` so interactive elements become visible on focus; shrink to a 1×1px box (`width:1px; height:1px`); hide overflow (`overflow: hidden`); clip with `clip-path: inset(50%)` plus `clip: rect(0 0 0 0)` for legacy IE; remove from page flow (`position: absolute`); prevent wrapping for proper announcement (`white-space: nowrap`).
- Pattern: Accessible name for an icon-only button — place a `<span hidden id="…">Menu</span>` inside the `<button>` and reference it via `aria-labelledby="…"` on the button; the browser exposes the hidden text as the button's accessible name (verifiable via Chrome/Edge DevTools accessibility panel).
- Pattern: Inert background behind a custom modal dialog — apply the `inert` attribute to the page content outside the dialog so it is rendered but inaccessible (no AAPI, no tab focus, no events); dim/obscure those regions visually. The native `<dialog>` element handles this for you when used in modal mode.
- Pattern: Remove layout-table semantics — apply `role="none"` to a `<table>` used purely for layout; the suppression cascades to required descendants (`<tr>`, `<td>`, etc.) so the entire table becomes presentation-only in the accessibility tree.
- Pattern: Inclusively hide a native form control replaced by an inline SVG — wrap `<input>` and `<svg aria-hidden="true">` inside the `<label>`; set the label/wrapper to `position: relative`; on the input set `position: absolute; opacity: 0; width: 1em; height: 1em` (relative units recommended; optional `z-index`); style the SVG via `input:focus-visible + svg`, `input:disabled + svg`, `input:checked + svg`; add a `@media (forced-colors: active)` block for Forced Colors adaptation.
- Pattern: Visible keyboard focus on a visually-replaced form control — target the adjacent SVG with `input[type="checkbox"]:focus-visible + svg { outline: 2px solid …; outline-offset: 4px; }`.
- Pattern: Animate an SVG-line-drawing checkmark on check — transition `stroke-dashoffset` on `input:checked + svg path` (e.g., `transition: stroke-dashoffset .4s linear; stroke-dashoffset: 0; stroke: currentColor`).

## Complex Components

### Accordion

- Definition — a group of collapsible, related sections of content; at its core, a grouping of disclosure widgets.
- Purpose — often used to save space by collapsing sections of content by default and expanding them on demand (e.g., product detail sections on e-commerce pages).
- Anatomy — a series of related disclosure widgets that can be identified as a group; in an exclusive accordion they additionally behave as a group.
- Exclusive variant — only one disclosure widget can be open at a time; opening one closes the others.
- Exact-exclusive variant — exactly one item is open at all times (zero open not allowed); the open item is "disabled" until another opens; requires JavaScript today; named in the OpenUI Accordion component explainer.
- Requirements — (1) create accessible disclosure widgets; (2) semantically group them; (3) give the group a name; (4) when exclusive, implement the group behaviour.
- Markup — start with a series of `<details>`/`<summary>` disclosure widgets and wrap them in a container.
- Container choice — use a named `<section>` when the accordion is important enough to be a page landmark, OR a `<div role="group">` when it's a logical group that shouldn't appear in the page outline.
- Naming — provide the container an accessible name via `aria-labelledby` pointing to a visible heading (preferred), `aria-labelledby` pointing to a hidden text node (use `hidden`, not visually-hidden, to avoid double announcement), or `aria-label` as a last resort.
- Native exclusive behaviour — give every `<details>` in the group the same non-empty `name` attribute value; the browser enforces "at most one open" and rewrites the `open` attributes in markup, with no JavaScript needed.
- Future name-attribute announcement — the `name` attribute on `<details>` is expected to expose group size and focused-item position to screen readers (mirroring `aria-setsize`/`aria-posinset` on radio button groups); not yet implemented in browsers — test with current ATs.
- Searchability — Chromium browsers (Chrome, Edge) auto-expand any `<details>` whose content contains the find-in-page search term, so accordion content remains discoverable through browser search.
- JavaScript is required when — implementing an exact-exclusive accordion, providing bulk expand/collapse (e.g., "Expand All"), needing finer control over opening/closing than `name` allows, or supporting custom behaviour/animations.
- Bulk expand/collapse UI — a checkbox above the accordion; checked = expand all, unchecked = collapse all, indeterminate = some but not all expanded.
- Heading-navigation gotcha — exclusive accordions break heading-based screen-reader navigation because not all content can be open at once; heading levels can also become "wonky" when headings are used inside the expand/collapse trigger.
- Dragon gotcha — Dragon voice software deprioritises `<details>` compared to buttons/links, making accordion sections harder for Dragon users to open.
- Reflow gotcha — content shifting as one section opens and another closes can disorient low-vision, mobile, and vestibular-disorder users; state also resets on page reload.
- Cognitive-load gotcha — exclusive accordions raise cognitive load because users cannot compare information between two sections and have difficulty scanning the overall content (per Eric Eggert's "Exclusive Accordions Exclude").
- Keyboard-fatigue gotcha — for keyboard users, comparing information across two sections of an exclusive accordion can take dozens of keystrokes (open one, navigate to the next, open it, navigate back, etc.).
- Lost-while-scrolling — in long accordions users easily lose their place (per Steven Hoober's "Designing for progressive disclosure"); fixing the accordion's visible size (per Adrian Roselli's fixed-size accordion demo) is one mitigation.
- HTML-standard caution — the HTML standard itself advises authors to consider whether grouping `<details>` into an exclusive accordion is helpful or harmful before using `name`; space savings can frustrate users who must open many items to find what they want, or compare multiple items.
- Default inclusivity — if the accordion doesn't need to be exclusive, it's more inclusive when it's not; reach for exclusive only when usability testing supports it.
- Custom-widget markup — group a series of `<div class="disclosure-widget">` blocks, each containing a `<button aria-expanded="false" aria-controls="…">` trigger and a panel `<div id="…" hidden>`, inside a named `<section>` (or a `<div role="group">`); ensure focus styles are present on the buttons.
- `name`-attribute incompatibility — the HTML `name` attribute only enforces exclusivity for native `<details>`; custom (button-based) disclosure widgets require JavaScript to implement exclusive behaviour.
- Initial markup for progressive enhancement — start from sections with headings, or a description list (`<dl>`/`<dt>`/`<dd>`) for question/answer content like FAQs; whatever skeleton you choose, the JavaScript-enhanced end markup must be a meaningful grouping of accessible disclosure widgets.
- Interactive-headings problem — accordion sections are typically preceded by headings, but headings are text elements and cannot be activated; you need an actual interactive element to expand/collapse.
- Wrong approach (heading-as-button) — `<h2 role="button">…` does not make the heading interactive and defeats the purpose of using a heading.
- Wrong approach (heading inside summary) — `<summary><h3>…</h3></summary>` risks suppressing the heading's semantics because the button role's Children Presentational property treats descendants as `role="presentation"`.
- Wrong approach (summary inside heading) — `<h3><summary>…</summary></h3>` makes `<summary>` no longer the first child of `<details>`, so it stops being the trigger.
- Correct approach (heading wraps button) — `<h3><button aria-expanded="…" aria-controls="…">…</button></h3>` keeps heading semantics intact while keeping the trigger interactive; this is the safe pattern for "interactive headings" in an accordion.
- AT support matrix for heading-in-`<summary>` — VoiceOver (macOS 15.3.1) exposes the heading with Safari 18.3, Firefox 136, and Edge 132; NVDA + Firefox v136 on Windows exposes it; Narrator + Chromium Edge exposes it; JAWS 2024 exposes it with Chromium but NOT with Firefox; older JAWS versions don't expose it anywhere — so the heading-wraps-button custom pattern is the most consistent.
- Find-in-page limitation on custom widgets — panels hidden via `display: none` or plain `hidden` are NOT discoverable through the browser's find-in-page functionality; the browser cannot search the hidden text and won't auto-expand the section.
- Find-in-page enablement — set the panel's hidden state to `hidden="until-found"` (e.g., `panel.setAttribute("hidden", "until-found")`); supporting browsers will search the hidden text and auto-expand the matching panel.
- hidden-until-found CSS gotcha — reset rules like `[hidden] { display: none !important; }` override `hidden="until-found"`; replace with `[hidden]:not(:is([hidden="until-found"])) { display: none !important; }` so plain `hidden` keeps strong specificity while until-found works.
- hidden-until-found generated-box gotcha — under until-found the browser uses `content-visibility: hidden` rather than `display: none`, so the element still generates a box; any margin/padding/borders/backgrounds on it render unexpectedly — move them to an inner container (e.g., `.panel__content`).
- hidden-until-found display gotcha — if the hidden element's computed `display` is `none`, `contents`, or `inline`, find-in-page will not reveal it.
- hidden-until-found persistence — once content is revealed via find-in-page, it stays visible after closing or starting a new search; there is currently no native way to recollapse it.
- hidden-until-found browser support — Chromium-only at the time of the lecture; expected to broaden via Interop 2025; use as a progressive enhancement only.

### Breadcrumb

- ARIA — no native `role="breadcrumb"` exists (ARIA is finite); use `<nav aria-label="Breadcrumb">` so screen readers announce "Breadcrumb, Navigation" — role + name communicate everything that's needed.

### Carousel

- ARIA — no native `role="carousel"` exists because ARIA is finite; the spec includes no carousel role.

### Custom-styled form control

- Use case — when CSS alone can't achieve the required visual / animation / Forced Colors adaptation for a native form control (e.g., a checkbox with an animated SVG-line-drawing checkmark).
- Markup — `<input>` and an inline `<svg aria-hidden="true">` both inside the control's `<label>`; the SVG is placed AFTER the input in the DOM so adjacent-sibling selectors can target it.
- Hide technique — label/wrapper `position: relative`; input `position: absolute; opacity: 0; width: 1em; height: 1em` (relative units recommended); optional `z-index`. Don't use `visually-hidden`; don't move the input off-canvas; don't shrink to 1px.
- ARIA — `aria-hidden="true"` on the visual replacement SVG so it isn't announced; the native control remains the source of truth in the accessibility tree.
- States to render — checked, unchecked, disabled, focus, hover, and (where applicable) indeterminate.
- State styling — `input[type="checkbox"]:focus-visible + svg { outline: …; outline-offset: … }`, `input[type="checkbox"]:disabled + svg { … }`, `input[type="checkbox"]:checked + svg { … }`; animate via SVG line-drawing (`stroke-dashoffset` transition) if desired.
- Forced Colors — add a `@media (forced-colors: active)` block that re-paints the SVG background/checkmark so the control stays visible in Windows Contrast Themes etc.
- Why inline SVG — full CSS control over inner shapes, supports animation, and adapts to Forced Colors more flexibly than an external `<img>`-embedded SVG.
- Why wrap input + SVG inside `<label>` — enlarges the interactive area of the control.
- Touch-SR gotcha — `visually-hidden` (1px clip) and off-canvas absolute positioning both make the native control unreachable for users exploring by touch (e.g., Android TalkBack); the inclusive-hide technique keeps the control inside the viewport in its natural position.
- Generalisation — the technique applies to any interactive form control you want to visually replace with an image (radio buttons, etc.), not just checkboxes.

### Disclosure

- Definition — an interactive control whose sole purpose is to reveal and hide content; typically a button that toggles a content panel.
- Anatomy — two parts: the trigger (the button) and the panel (the content controlled by the trigger).
- Building block — disclosure widgets are building blocks for several more complex patterns including accordions (a grouping of disclosure widgets), the toggle in a drop-down navigation, and the button that reveals a slide-out navigation; getting the foundations right prepares you for those patterns.
- Native markup — `<details>` is the container; the first `<summary>` child is the trigger; everything after `<summary>` inside `<details>` is the controlled content; the browser toggles the `open` attribute on `<details>` to show/hide.
- Native trigger constraint — `<details>` can only have one trigger; if multiple `<summary>` elements are present, only the first is treated as the trigger; if no `<summary>` is present, the browser supplies a generic "Details" label.
- Native built-ins — `<summary>` is operable via Space and Enter, browser toggles the `open` attribute on activation, the browser exposes expanded/collapsed state to AT, and the `<details>` panel is auto-expanded by the browser's find-in-page search if it contains the search term.
- Native role inconsistency — `<summary>` is exposed differently across platform/browser/screen-reader combinations — "disclosure triangle" (VoiceOver + Chrome v109 macOS), "Summary" (VoiceOver + Safari macOS), or "button" (NVDA + Firefox Windows, which also reads the triangle marker as part of the name); this is not a bug and should not be worked around.
- Don't override `<summary>` with `role="button"` — some browsers then treat `<summary>` as a standard `<button>`, which doesn't convey expanded/collapsed state, so the state is no longer announced; the ARIA in HTML spec specifically calls this unnecessary and cross-platform-problematic.
- Find-in-page caveat — once the browser auto-expands a `<details>` for in-page search, it stays expanded; this can enhance content accordions but is undesirable for tabs, drop-down navigations, and dialogs — those patterns need JavaScript to override or suppress this behaviour.
- Native gaps — `<details>` doesn't dismiss on Esc; patterns like drop-down navigations or dialogs that need Esc-to-close require JavaScript to add it.
- Native exclusive grouping — give multiple `<details>` the same non-empty `name` attribute value to make the browser permit at most one open at a time; this also rewrites the `open` attributes in markup.
- Dragon gotcha — Dragon voice software deprioritises `<details>` compared to buttons/links, making the native disclosure harder for Dragon users to open.
- Custom widget requirements — trigger exposed as a button; trigger operable via Space and Enter; activating the trigger toggles the panel; trigger communicates expanded/collapsed state to screen readers.
- Custom markup — wrap trigger + panel in a container (e.g., `<div class="disclosure-widget">`); use a `<button aria-expanded="false">` as the trigger (optionally with `aria-controls` referencing the panel's `id`); use a grouping element (`<div>` by default, or `<section>`/`<article>` if stronger semantics are needed) as the panel; place the panel directly after the trigger in the DOM.
- ARIA — set `aria-expanded="false"` on the trigger when collapsed and `"true"` when expanded; optionally use `aria-controls` to reference the controlled element's `id` (only JAWS exposes the relationship and even then support is poor).
- Source order — the content panel must follow the trigger in the DOM even when `aria-controls` is used, so screen-reader users can continue navigating into the revealed content and keyboard users can quickly tab into interactive elements inside the panel.
- State marker — visually indicate state via a marker (triangle, chevron, plus sign, or anything familiar) provided by a CSS pseudo-element or an inline `<svg>`; inline SVG is preferred for styling control and Forced Colors adaptation; hide the SVG from AT with `aria-hidden="true"`.
- Behaviour wiring — on trigger activation, JavaScript toggles `aria-expanded` and toggles panel visibility (e.g., add/remove `hidden`); optionally drive visibility entirely from CSS using `.disclosure-widget > button[aria-expanded="false"] + div { display: none; }` and animate the marker via `[aria-expanded="true"] > svg { transform: rotate(90deg); }`, so JavaScript only updates `aria-expanded`.
- Hiding the panel initially — when collapsed by default, set `aria-expanded="false"` and hide the panel from all users via the HTML `hidden` attribute, `display: none`, or `visibility: hidden`.
- State management — JavaScript must update `aria-expanded` on user interaction; without JavaScript the value is stale and can confuse screen-reader users.
- Progressive enhancement — start with a static version where the content panel is visible and there is no `<button>`; in JavaScript, create and prepend a `<button>` into the container, set initial ARIA attributes, hide the panel, and wire up the click handler — so if JS fails to load, the content remains accessible and the user isn't faced with a broken control.
- Native vs custom decision — use `<details>`/`<summary>` for simple disclosures where the semantics, behaviour, and find-in-page expansion fit (good starting foundation for content accordions); build a custom ARIA disclosure when you need consistent cross-browser/screen-reader announcements, want to avoid unwanted built-in behaviour, or the pattern requires different semantics (tabs, drop-down navigations, dialogs).
- Future native API — the OpenUI group is developing an "Openable API" (placeholder name) that will let you enhance native `<button>`s into disclosure buttons declaratively; not yet supported in any browser. The Popover API and Invoker Commands API proposals are related work in this area.
- Find-in-page on custom widgets — a custom `<button>` + `hidden` disclosure is invisible to browser find-in-page by default (the panel is hidden via `display: none`); switch the hidden state to `hidden="until-found"` to make the panel discoverable to find-in-page and fragment navigation in supporting (Chromium-only at lecture time, broadening via Interop 2025) browsers.
- hidden-until-found CSS interference — `[hidden] { display: none !important; }` reset rules block until-found's effect; use `[hidden]:not(:is([hidden="until-found"])) { display: none !important; }` instead so plain `hidden` still wins on specificity while until-found works.
- hidden-until-found generated-box — under until-found browsers use `content-visibility: hidden`, so the hidden element still generates a box; move padding, borders, and backgrounds to a child container (e.g., `.panel__content`) to avoid unexpected whitespace and borders.

### Menu / Menubar

- Structure — `role="menu"` or `role="menubar"` for the container with `role="menuitem"` children.
- Children constraint — `menuitem` may not contain interactive children (no nested `<button>`, no `<a>`, no elements with implicit button/link roles).
- Keyboard — Arrow keys navigate menu items; Space and Enter activate them; Esc closes the menu.

### Modal dialog

- ARIA category — modal dialogs fall under the "Window roles" category of ARIA roles, which describe windows within the browser.
- Native gaps — like drop-down navigations, dialogs built on `<details>` lack Esc-to-close and other expected behaviours; JavaScript must supply them, which is one reason to prefer custom ARIA dialogs over `<details>`.

### Tabs

- Composite structure — uses three ARIA roles together — `tablist` (container), `tab` (each tab control), and `tabpanel` (each panel of content).
- Markup — wrap the set of tabs in an element with `role="tablist"` (no native HTML element maps to tablist); each tab is typically a `<button role="tab">`; each panel is typically a `<section role="tabpanel">`.
- ARIA parent-child constraint — elements with `role="tab"` MUST be contained in or owned by an element with `role="tablist"`; `role="tab"` placed inside a `<nav><ul><li><a>` structure (without tablist) is invalid.
- Behaviour — ARIA roles add no interactive behaviour; tab activation, panel switching, focus, and keyboard support must be implemented in JavaScript.
- Don't reuse `<details>`/`<summary>` — Tabs have specific semantic, behaviour, and HTML-structure requirements that `<summary>` doesn't fulfil; visually styling `<details>` as tabs results in a confusing experience for screen-reader users.

### Toggle button

- ARIA — use `<button aria-pressed="true|false">` to indicate whether the toggle is on or off.
- State management — JavaScript must flip `aria-pressed` when the user activates the button.

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
- Anti-pattern: Multiple `<summary>` children inside a single `<details>` — the browser only uses the first one as the trigger; the rest are misleading.
- Anti-pattern: `<details>` with no `<summary>` — the browser supplies a generic "Details" label which is almost never what you want.
- Anti-pattern: `role="button"` on `<summary>` — some browsers then treat it as a standard `<button>` and the expanded/collapsed state announcement is lost; the ARIA in HTML spec explicitly calls this unnecessary and cross-platform-problematic.
- Anti-pattern: Building a Tabs widget out of `<details>`/`<summary>` — Tabs have specific semantic, behaviour, and HTML structure requirements that `<summary>` doesn't fulfil; results in a confusing experience for screen-reader users.
- Anti-pattern: Reaching for `<details>` just to write less JavaScript when the built-in behaviour (e.g., find-in-page auto-expansion) is unwanted — one feature you want doesn't justify the whole element if its other behaviour doesn't fit your pattern.
- Anti-pattern: Hard-coding the disclosure `<button>` and hiding the panel by default — if the JavaScript fails to load, the user is faced with a broken control and the content inside the panel becomes inaccessible.
- Anti-pattern: Visually grouping disclosure widgets to look like an accordion without semantic grouping — the relationship is invisible to screen-reader users.
- Anti-pattern: Using a visually-hidden CSS class for an `aria-labelledby` target that has no other purpose — screen readers announce the text twice (once as the accessible name, once as content); use the HTML `hidden` attribute instead.
- Anti-pattern: Defaulting to `aria-label` for naming an element — reserve it as a last resort; prefer `aria-labelledby` to a visible or hidden text node.
- Anti-pattern: Using the `name` attribute on `<details>` when you need bulk expand/collapse — the browser enforces "at most one open", breaking the feature.
- Anti-pattern: Defaulting to exclusive accordions — they raise cognitive load, frustrate comparing sections, disorient on content shifts, break heading navigation, and reset on reload; choose exclusive only when usability testing supports it.
- Anti-pattern: Placing `<summary>` inside its heading (`<h3><summary>…</summary></h3>`) — `<summary>` is no longer the first direct child of `<details>` and stops being the disclosure's trigger.
- Anti-pattern: Hiding accordion panels with plain `hidden` or `display: none` when find-in-page discoverability is wanted — the content becomes unsearchable and unreachable via fragment navigation; use `hidden="until-found"` as a progressive enhancement instead.
- Anti-pattern: Applying padding/borders/backgrounds directly to an element in the `hidden="until-found"` state — the element still generates a box (under `content-visibility: hidden`), so these styles render unexpectedly; move them to a child container.
- Anti-pattern: Hiding an interactive element by moving it off-screen via absolute positioning without un-hiding on focus — the element remains in the tab order, so keyboard users can focus an element they cannot see; a WCAG violation.
- Anti-pattern: `aria-hidden="true"` on a focusable element (even with `tabindex="-1"`) — modern browsers (e.g., Chrome) still expose them; focus may land on an unannounced element.
- Anti-pattern: `aria-hidden="false"` to re-expose a previously hidden element — support is inconsistent across browsers; remove the attribute entirely.
- Anti-pattern: Hiding descendants of a `content-visibility: auto` container with `display: none` / `visibility: hidden` to keep them out of screen readers — those styles aren't applied while rendering is postponed, so screen readers may still find them; hide them via HTML or ARIA instead.
- Anti-pattern: Disabling a control without restoring visual contrast — the default low-contrast grey can be hard for low-vision users to discern.
- Anti-pattern: Using `tabindex` to make an element non-focusable — only `disabled` or `inert` actually does that; `tabindex` only changes the tab order.
- Anti-pattern: Using `display: contents` on elements with meaningful semantics — early browser implementations stripped semantics; limit usage to elements without meaningful semantics (e.g., `<div>`) until target browsers behave per spec.
- Anti-pattern: Hiding an interactive form control (e.g., a checkbox you're replacing with an SVG) with the `visually-hidden` utility class — mobile screen-reader users exploring by touch won't reach the 1px-clipped control.
- Anti-pattern: Hiding a replaced form control by moving it off-canvas with absolute positioning — outside the viewport, touch screen-reader users dragging their finger across the screen can't find it.
- Anti-pattern: Shrinking a replaced form control to 1px — very hard to find by touch, even when within viewport bounds.

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
- Decision: Native `<details>` vs custom ARIA disclosure — use `<details>`/`<summary>` for simple disclosures where the semantics, behaviour, and find-in-page expansion fit (good fit for content accordions); build a custom ARIA disclosure when you need consistent cross-browser/screen-reader announcements, want to avoid the unwanted built-in behaviour (e.g., find-in-page sticking open, lack of Esc-to-close), or the pattern requires different semantics (tabs, drop-down navigations, dialogs).
- Decision: Disclosure content-panel element — use `<div>` by default; choose `<section>` or `<article>` only if the content warrants stronger semantics or landmark exposure; a single `<p>` is technically fine for trivial one-paragraph panels.
- Decision: Group (`role="group"`) vs region landmark for an accordion — use `role="group"` when the accordion is a logical collection that shouldn't appear in the page outline; use a named `<section>` (region) when the content is important enough that users would benefit from landmark navigation to it.
- Decision: Naming hierarchy — `aria-labelledby` pointing to a visible heading > `aria-labelledby` pointing to a hidden text node (use `hidden`, not visually-hidden) > `aria-label` as a last resort.
- Decision: Native accordion vs ARIA + JavaScript — use `<details>` + `<summary>` + `name` for a standard exclusive accordion (no JS); reach for ARIA + JavaScript when you need exact-exclusive behaviour, bulk expand/collapse, custom animations, finer control, or content types unsuited to `<details>`.
- Decision: Exclusive vs non-exclusive accordion — let usability testing with disabled and AT users decide; default to non-exclusive when in doubt because it is more inclusive.
- Decision: Heading inside `<summary>` vs heading wrapping `<button>` — prefer the custom (heading-wraps-button) markup when your users may be on AT pairings that don't expose headings in `<summary>` (e.g., JAWS prior to 2024, or JAWS + Firefox); `<details>` + heading-inside-`<summary>` is acceptable only when all target AT pairings reliably expose those headings.
- Decision: `hidden` vs `hidden="until-found"` — use `hidden="until-found"` when the content benefits from being discoverable via browser find-in-page and fragment navigation; use plain `hidden`, `display: none`, or `visibility: hidden` when full hiding from all access channels is desired.
- Decision: Which hiding technique to use — start from why (UX vs aesthetic), who you're hiding from, who you want to expose to, who benefits, and what type of element it is (interactive/focusable vs static text); the answers narrow the technique.
- Decision: `aria-hidden` vs `role="none"` — `aria-hidden="true"` removes the element AND its children from the accessibility tree; `role="none"` only suppresses the element's own role (and required or semantically-tied descendants), leaving other children's semantics intact.
- Decision: `inert` vs `hidden` — `hidden` removes the element's display entirely; `inert` keeps the element rendered but blocks all interaction, keyboard tabbing, mouse/touch events, and screen-reader access.
- Decision: `inert` vs `disabled` — both remove the element from the tab order; `inert` hides it from screen readers entirely (no AAPI exposure); `disabled` keeps it in the accessibility tree with the disabled state announced.
- Decision: `sr-only` vs `visually-hidden` class name — prefer `visually-hidden` because accessibility APIs expose the content to more than just screen readers.
- Decision: `role="presentation"` vs `role="none"` — synonyms; prefer `role="none"` because `presentation` is often confused with `aria-hidden="true"`.
- Decision: `visually-hidden` vs inclusive form-control hide — use `visually-hidden` for static textual content; use the inclusive hide (input overlaid on its visual replacement with `position: absolute; opacity: 0`) for interactive form controls being visually replaced by an image — the inclusive hide keeps the control reachable by touch.

## Keyboard Behaviour

- Key: Tab on native `<button>` — focusable by default; no `tabindex="0"` needed.
- Key: Tab on native `<a>` with `href` — focusable by default; no `tabindex="0"` needed.
- Key: Enter on native `<button>` — fires on keydown and continues firing while held.
- Key: Space on native `<button>` — fires on keyup; if Space is held and the user tabs away without releasing, the action will not fire.
- Key: Enter on native `<a>` — links are activated by the Enter key only.
- Key: Enter on a link-enhanced-as-button — fire the action on keydown (keyCode 13).
- Key: Space on a link-enhanced-as-button — fire the action on keyup (keyCode 32).
- Key: Space and Enter on native `<summary>` — both keys activate the `<summary>` and toggle the `open` attribute on its `<details>` parent; the browser bakes this interaction in.
- Key: Tab with `tabindex="-1"` on an interactive element — element is removed from the tab order; user cannot reach it via Tab, but it remains focusable programmatically and by mouse.

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
- AT: `aria-controls` exposure — effectively only JAWS exposes the `aria-controls` relationship to users, and even that support is poor; treat the attribute as optional.
- AT: ARIA support varies — ARIA support and behaviour varies between platforms, accessibility APIs, browsers, and assistive technologies; some parts may be fully supported, partially supported, or buggy. There is no feature-detection for ARIA — test with multiple browser/AT combinations.
- AT: `aria-hidden="true"` on a focusable element — the element is removed from the accessibility tree and not announced by screen readers, but it remains in the DOM and tab order; pressing Tab still moves focus to it, so the user focuses on "nothing".
- AT: `role="presentation"` on a link — suppresses the link's role in the accessibility tree; screen readers do not announce that it is a link when focused, but they still announce its text content.
- AT: ARIA does not affect the DOM or visual styles — adding an interactive role (e.g., `role="button"`) does not make the element interactive, focusable, or visually styled like a button; it only changes how the element is exposed in the accessibility tree.
- AT: Computed role and AAPI mappings — the role a browser exposes to assistive technologies is the "computed role" determined per the HTML Accessibility API Mappings (AAPI), and can depend on context (e.g., `<summary>` only gets a meaningful role when it is the first child of `<details>`); cross-platform announcement differences usually trace back to these mappings, not to bugs.
- AT: Group vs region in the page outline — named `<section>` regions are listed in the screen reader's landmark / page-outline view (e.g., VoiceOver Web Rotor's Landmarks list); named `role="group"` containers are recognised as a group with an accessible name but do **not** appear in the page summary/outline — this is the principal practical difference between the two.
- AT: Group start/end announcement — VoiceOver (with Safari on macOS) and similar screen readers (JAWS, NVDA on Windows) announce the start and end of a named group, including the group's accessible name; a named `<section>` is announced as a named region.
- AT: Double announcement of visually-hidden labels — when a `<span class="visually-hidden">` is both an `aria-labelledby` target AND visible to AT as content, screen readers read it twice (once as the accessible name, once as page content); hiding the span with the HTML `hidden` attribute removes the second announcement while `aria-labelledby` still exposes it as the name.
- AT: Radio-button group announcement — when radio buttons share a `name`, the browser exposes the group size via `aria-setsize` and the focused item's position via `aria-posinset`, so screen readers announce e.g. "radio button, 1 of 3".
- AT: Future `<details>` group announcement — browsers may, in future, expose group size and position for `name`-grouped `<details>` the same way they do for radio buttons; not yet implemented at the time of the lecture — perform your own testing.
- AT: VoiceOver + headings in `<summary>` — VoiceOver on macOS exposes the presence of a heading placed inside a `<summary>` when paired with Safari, Firefox, and Chromium-based browsers (tested macOS 15.3.1 / Safari 18.3 / Firefox 136 / Edge 132).
- AT: NVDA + headings in `<summary>` — NVDA with Firefox v136 on Windows exposes the presence of headings inside `<summary>`.
- AT: Narrator + headings in `<summary>` — Narrator paired with Chromium Edge exposes the presence of headings inside `<summary>`.
- AT: JAWS + headings in `<summary>` — JAWS 2024 announces a heading inside `<summary>` when paired with Chromium browsers, but currently does not when paired with Firefox; older JAWS versions don't expose them anywhere with any browser. Many AT users intentionally don't upgrade their software (per Eric Bailey's "truths about digital accessibility"), so pre-2024 JAWS users would miss those headings.
- AT: Custom heading-wraps-button — placing the `<button>` of a custom disclosure inside its heading exposes the heading's semantics consistently across all current browser/screen-reader pairings, regardless of AT version.
- AT: `opacity: 0` / `filter: opacity(0)` — element is visually transparent but semantics and accessibility info are unaffected; remains screen-reader- and keyboard-accessible, and still takes layout space.
- AT: `clip-path: inset(100%)` — visually clips the element out of view but does not affect semantics; element remains screen-reader- and keyboard-accessible and still takes layout space.
- AT: Off-screen `position: absolute` — moving an element out of the viewport doesn't remove it from the DOM or accessibility trees; the element remains in the tab order and is screen-reader-announced.
- AT: `visibility: hidden` — element is removed from the accessibility tree (inaccessible to all users), but still reserves its normal layout space.
- AT: `display: none` — element is removed from layout AND the accessibility tree; equivalent to the element not existing for any user; descendants are excluded too.
- AT: `display: contents` — per spec, the element generates no box but its children do, and semantics/accessibility are preserved; early browser implementations removed the element from the accessibility tree — mostly fixed now, but use cautiously on elements with meaningful semantics.
- AT: `content-visibility: auto` — prior to Chromium 90, descendant semantic elements (headings, landmarks) were not exposed to AAPIs; fixed in Chromium 90+. Caveat: while rendering is postponed, CSS hides (`display: none`, `visibility: hidden`) on descendants aren't applied — screen readers can still discover them; hide via HTML/ARIA instead.
- AT: `hidden` attribute any-value — any value (including `"false"`, `"invalid value"`, or no value at all) hides the element; invalid values default to the hidden state.
- AT: `disabled` controls — included in the accessibility tree; screen readers announce the disabled state and indicate the user cannot activate or interact.
- AT: `inert` regions — not exposed to accessibility APIs; non-interactive; not targeted for any user-interaction event (mouse, touch included).
- AT: `aria-hidden` with no value — the browser ignores the attribute; visibility is determined by other factors.
- AT: `aria-hidden="false"` — should re-expose the element to AAPIs but cross-browser support is inconsistent; remove the attribute entirely to re-expose.
- AT: `aria-hidden="true"` on a focusable element — partially/inconsistently hidden; Chrome and other modern browsers still expose them; focus may land on an unannounced element.
- AT: `role="none"` / `role="presentation"` — suppresses the element's implicit semantics so it no longer maps to its native role UNLESS the element is focusable (natively or via `tabindex`) OR has a global ARIA state/property; does not hide the element's content from screen readers.
- AT: `role="none"` on a heading — heading text is reported in the accessibility tree as a plain text string with no semantic meaning.
- AT: `role="none"` on a parent — children's semantics are preserved UNLESS the children are required by the element (e.g., `<td>`, `<tr>` inside `<table>`) or semantically tied (e.g., listitems require a list parent); only in those cases does the child semantics get suppressed too.
- AT: Hidden text referenced via `aria-labelledby` / `aria-describedby` — by default ATs don't relay hidden information, but the Accessible Name and Description Computation spec lets authors explicitly include hidden text as an accessible name or description; the browser exposes the hidden text accordingly.
- AT: Explore by touch on touch screen readers — touch-screen screen readers (e.g., Android TalkBack) let users drag a finger across the screen to hear the element directly underneath; an element hidden off-canvas or shrunk to 1px is unreachable via this navigation mode, even if it remains in the accessibility tree.

## Tools

- Tool: WebAIM WAVE browser extension — evaluates web content for accessibility issues directly within the browser; the Structure tab provides a structural representation of the page including all landmarks and the heading structure within each landmark.
- Tool: a11ysupport.io — high-level overview of ARIA attributes and their expected support across browser/screen-reader combinations; the tests may not always be up-to-date, so always perform your own testing.
- Tool: JAWS — Windows screen reader; effectively the only screen reader that currently exposes the `aria-controls` relationship to users (and even that support is poor, per Heydon Pickering's "aria-controls is poop").
- Tool: VoiceOver Web Rotor — macOS VoiceOver feature that provides a list/summary of items on a page, including a Landmarks list; named `<section>` regions appear in this list, but named `role="group"` containers do not.
- Tool: Edge / Chrome DevTools accessibility panel — inspect the accessibility tree to verify how content is exposed to screen readers (e.g., confirm an icon button's accessible name is derived from a referenced hidden `<span>`).
- Tool: Accessibility Insights for Windows — desktop application for inspecting how content is exposed in the accessibility tree (used in the lecture to demonstrate that a heading with `role="none"` is reported as plain text vs a heading exposed as a heading).
- Tool: Android TalkBack — Android touch-screen screen reader that supports "explore by touch" navigation: users drag their finger across the screen to hear what is directly underneath.

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
- Term: Disclosure — the act of disclosing or revealing something that is otherwise hidden.
- Term: Disclosure widget — an interactive control whose sole purpose is to reveal and hide content; typically a button that toggles a content panel.
- Term: Trigger (disclosure) — the button portion of a disclosure widget — the element the user activates to toggle visibility.
- Term: Panel / Content panel (disclosure) — the content (or container of content) that the disclosure trigger reveals and hides.
- Term: Progressive Enhancement — a design and development approach that ensures a usable minimum user experience by starting with a working static version and enhancing it with JavaScript, so the content remains accessible if the script fails to load or run.
- Term: AAPI — Accessibility API; the platform-level API a browser exposes accessibility information to; the HTML AAPI Mappings define which role browsers expose for each HTML element.
- Term: Computed role — the role the browser actually determines for an element based on context and AAPI mappings (e.g., `<summary>` gets a meaningful role only when it is the first child of `<details>`); may differ from the implicit role listed in ARIA-in-HTML.
- Term: Accordion — a group of collapsible, related sections of content; at its core, a grouping of disclosure widgets.
- Term: Exclusive accordion — an accordion in which only one disclosure widget can be open at a time.
- Term: Exact-exclusive accordion — an accordion where exactly one item is open at all times (zero open not allowed); the open item is "disabled" until another opens; requires JavaScript today; defined in the OpenUI Accordion component explainer.
- Term: Visually-hidden — a CSS utility (a set of CSS rules typically applied via a `.visually-hidden` class) that hides content visually while keeping it accessible to assistive technologies; preferred over the older name `sr-only` because accessibility APIs expose the content to more than just screen readers.
- Term: Inert — describes content (marked via the `inert` attribute) that is visually rendered but not exposed to accessibility APIs, completely non-interactive, and not targeted by any user-interaction event; conceptually like replacing the content with a static, non-interactive picture that has no alt text.
- Term: Icon button — a button containing only an icon and no visible accompanying text; needs a text alternative (e.g., via `aria-labelledby` referencing a hidden `<span>`) so screen-reader users can identify it.
- Term: Explore by touch — per the Material Design Accessibility Guidelines, "Touch interface screen readers allow users to run their finger over the screen to hear what is directly underneath. This provides the user with a quick sense of an entire interface."
- Term: Inclusive hide (for form controls) — visually hiding a native form control while keeping it within the viewport in its natural position (via `position: absolute; opacity: 0`, sometimes enlarged with relative width/height) so touch screen-reader users can still find it by haptics.
