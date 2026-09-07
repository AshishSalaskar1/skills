# HTML contract

Every guide is a complete HTML5 document encoded as UTF-8. Embed all CSS and JavaScript. The only external requests a reader should initiate are optional clicks on cited source links.

## Required structure

Use this structural contract while allowing the visual design to suit the topic:

```html
<!doctype html>
<html lang="en">
<head>...</head>
<body>
  <header>...<button class="theme-toggle" type="button">...</button></header>
  <nav class="tabs" role="tablist" aria-label="Topics">...</nav>
  <main>
    <!-- teach:section:<stable-id>:start -->
    <section id="<stable-id>" role="tabpanel" aria-labelledby="tab-<stable-id>">...</section>
    <!-- teach:section:<stable-id>:end -->
  </main>
  <script id="teach-manifest" type="application/json">...</script>
  <script>/* tab behavior only */</script>
</body>
</html>
```

The first panel is the overview. The last panel is Sources. Render all panels in document order so the guide remains readable if scripts fail or when printed.

## Manifest

Keep the manifest valid JSON with this minimum shape:

```json
{
  "schemaVersion": 1,
  "topic": "Vector databases",
  "slug": "vector-databases",
  "aliases": ["vector DBs"],
  "purpose": "Understand the subject end to end",
  "depth": "conceptual with practical context",
  "focus": [],
  "createdAt": "2026-09-07",
  "updatedAt": "2026-09-07",
  "revision": 1,
  "sections": [
    {"id": "overview", "title": "Overview"},
    {"id": "sources", "title": "Sources"}
  ],
  "sources": [
    {
      "id": "s1",
      "title": "Source title",
      "publisher": "Publisher",
      "url": "https://example.com/canonical-page",
      "tier": "primary",
      "publishedOrUpdated": "Not stated",
      "accessedAt": "2026-09-07"
    }
  ],
  "revisions": [
    {"revision": 1, "date": "2026-09-07", "summary": "Created the guide."}
  ]
}
```

Use real current dates obtained from the environment. Escape `<` as `\u003c` inside JSON string values if needed. The rendered Sources tab is the human-readable source ledger; the manifest is the machine-readable index. Keep them consistent.

## Navigation behavior

- Each tab is a `<button role="tab">` with stable `id`, `aria-controls`, and `aria-selected` attributes.
- Arrow Left and Arrow Right move between tabs; Home and End jump to the first and last tab; Enter or Space activates a focused tab.
- A URL hash matching a panel ID opens that panel, and activation updates the hash without causing a disruptive jump.
- With JavaScript enabled, hide inactive panels using the `hidden` attribute. Without JavaScript, show all sections.
- At narrow widths, allow the tab list to scroll horizontally or become a compact vertical list.

JavaScript must only support presentation and navigation. Theme selection may last for the current page session but must not use local storage, cookies, telemetry, or other persistent reader tracking.

## Light and dark themes

Every guide must provide polished light and dark themes rather than treating one as an inversion of the other.

- Define semantic CSS custom properties for canvas, surface, text, muted text, borders, links, accents, code, tables, focus rings, and illustration colors.
- Use `@media (prefers-color-scheme: dark)` as the initial default when JavaScript is unavailable or no in-page choice has been made.
- Add a keyboard-accessible button that switches between light and dark themes and exposes its current state with an accurate label and `aria-pressed` value.
- Apply the selected mode using a root attribute such as `data-theme="light|dark"`. Do not persist it beyond the current page session.
- Set `color-scheme: light dark` appropriately so native controls match.
- Avoid pure black on pure white for large reading surfaces. Check muted text, links, inline code, syntax colors, table borders, and source cards in both modes.
- Print using a clean light palette regardless of the active screen theme.

## Illustrations and images

Visuals are part of the explanation. Include them wherever they materially clarify a system, process, comparison, hierarchy, timeline, spatial relationship, or mental model.

Prefer, in order:

1. Original inline SVG illustrations created specifically for the explanation
2. Original HTML/CSS diagrams when they remain semantic and responsive
3. Clearly reusable source images with verified license terms and attribution

For original illustrations:

- Keep SVG inline so the guide remains standalone.
- Use a `viewBox` and responsive sizing; do not rely on fixed desktop dimensions.
- Draw colors from the guide's theme variables and verify legibility in both themes.
- Add a concise `<title>` and `<desc>` when the image conveys information.
- Provide a nearby text explanation or meaningful caption; visuals must not be the only way to access essential information.
- Use arrows, labels, grouping, and emphasis to explain a relationship, not merely decorate the page.

For third-party images:

- Use only when reuse or embedding is permitted by an explicit license or clear first-party media policy.
- Record creator or publisher, original URL, license, and any required attribution in the caption and Sources ledger.
- Download and embed the asset as a data URI only when the license permits it and its size is reasonable. Never hotlink, since the guide must work offline.
- Do not assume that public availability, popularity, a search result, or source citation grants permission to copy an image.
- Do not use screenshots containing private information, tracking URLs, or irrelevant interface chrome.

If licensing is unclear, recreate the underlying idea as an original diagram without copying the source's distinctive composition or artwork. Never fabricate a source-image license.

## Content and visual requirements

- Use one `<h1>` and a logical heading hierarchy.
- Include a short orientation in the header: what the guide explains and the assumptions used.
- Keep paragraphs readable, code blocks scrollable, tables responsive, and line length controlled.
- Make links visibly distinguishable and include `rel="noreferrer"` on external links opened in a new tab.
- Provide sufficient color contrast, visible `:focus-visible` styles, reduced-motion handling, and useful print styles.
- Prefer system fonts. Do not use external font or icon services.
- Use topic-appropriate styling rather than a generic dashboard aesthetic.
- Render code and factual notation exactly; never hide essential explanation in hover-only UI.

## Stable updates

Stable IDs and section markers are the update boundary. On extension:

- Keep existing section IDs unless the section itself is intentionally replaced.
- Give a subsequent related exploration its own section and tab unless it is only a correction, source refresh, or small elaboration.
- Insert or edit whole marked sections rather than applying fragile text substitutions.
- Keep source IDs stable and assign the next unused numeric ID to new sources.
- Preserve valid manual additions inside sections and styles.
- Increment `revision`, update `updatedAt`, and append one revision record.

If the manifest or markers are missing or malformed, preserve the original file and repair the structure conservatively. If a safe update is not possible, ask before rebuilding the guide.
