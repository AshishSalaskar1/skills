---
name: teach-me-tech
description: Create an in-depth, engineer-focused HTML course with technical diagrams and linked sources.
disable-model-invocation: true
argument-hint: "Topic, optional background, scope, and output directory"
---

Create a complete technical course the user can open once and read independently. Engineering understanding is the primary goal: build intuition, explain mechanisms, and connect theory to implementation. Interview preparation is a secondary benefit, not the structure of the course.

## 1. Establish scope

Use the requested topic, background, constraints, and depth. When only a topic is supplied, assume general engineering and programming literacy, but introduce the topic's own foundations before relying on them.

Clarify only ambiguity that materially changes the course, such as conflicting meanings of a topic or an unspecified target platform that changes the mechanisms. Otherwise choose a coherent, bounded scope and state prerequisites, coverage, and exclusions on the index. A broad topic should become a complete course within that scope, not a shallow survey or an outline awaiting later lesson requests.

Use an explicit output directory when supplied; otherwise use `./<topic-slug>-course/`, relative to where the skill was invoked. Inspect an existing destination before writing and preserve unrelated files and user edits. The format-document links below resolve from this skill's folder, not the output directory.

## 2. Design and ground the whole course

Plan all chapters and their conceptual dependencies before authoring. Group related concepts into substantial chapters, ordered from foundations to deeper engineering consequences. Each chapter should develop a coherent subject far enough that an engineer can reason about it, rather than deliver a tiny lesson or a single quick win.

Research the mechanisms and consequential claims using high-trust sources. Follow [RESOURCES-FORMAT.md](./RESOURCES-FORMAT.md) for source selection, citations, verification status, and the course-wide references page. Separate documented guarantees from implementation-specific behavior and your own illustrative examples.

This step is complete when the scoped topic has a full chapter plan, prerequisites are accounted for, and the sources and diagrams needed for the explanations are identified. Keep planning internal; the deliverable is the readable course.

## 3. Author substantial engineering chapters

Build explanations around a concrete problem, the model that explains it, and the mechanism that makes the model work. Move between intuition and precision: trace an example, show the relevant implementation or mathematics, then explain the consequences. Connect new concepts to earlier chapters through links instead of repeating their full explanations.

Use the following where they advance understanding, not as a repetitive checklist of headings:

- **Mechanisms:** what happens internally, why each step exists, and which assumptions or invariants it depends on.
- **Worked examples:** realistic code, execution traces, calculations, or scenarios, with the reasoning and outcome explained in the text.
- **Engineering decisions:** alternatives, tradeoffs, costs, scaling behavior, and the circumstances that make an approach appropriate.
- **Failure modes:** edge cases, broken assumptions, operational consequences, and commonly confused concepts.
- **Connections:** how the subject relates to surrounding systems and when its model stops being useful.

Depth follows the topic, not a fixed word count. Split at meaningful conceptual boundaries, not to manufacture bite-sized lessons. Avoid padding, unexplained jargon, and step-by-step handholding for ordinary engineering tasks. Define unfamiliar topic-specific terms on first use; for terminology-heavy courses, follow [GLOSSARY-FORMAT.md](./GLOSSARY-FORMAT.md).

Code should be internally consistent and identify its language, relevant version assumptions, and whether it is runnable or illustrative. Explain why the code works and its limitations rather than merely presenting a snippet. Make the core explanation self-contained; external reading is optional.

When useful, end a chapter with a short **Interview relevance** note about the reasoning worth communicating or a common misconception. Keep it secondary to the technical explanation.

This is a reading course, not an interactive tutor. Exclude question banks, Q&A sections, quizzes, recall prompts, answer-required exercises, mock interviews, learning logs, progress tracking, and reminders to return to the agent. Worked examples include their explanation and result without asking the reader to respond.

### Readability and content balance

Every substantial chapter should combine explanatory prose with purposeful structured elements. Use paragraphs to develop intuition, causal reasoning, and nuance; use structure to make relationships and important points easy to scan. Organize long explanations into descriptive sections and subsections, keeping each paragraph focused on one idea.

- **Bulleted lists:** parallel properties, assumptions, failure modes, or takeaways. Use numbered lists when order matters, such as an execution flow. Explain the reasoning in surrounding prose rather than compressing the whole chapter into bullets.
- **Tables:** genuine comparisons across shared dimensions, such as alternatives, guarantees, costs, and use cases. Introduce the comparison and explain its implications; keep lengthy explanations outside cells.
- **Notes and callouts:** concise, labeled notes, warnings, or key insights for an important invariant, caveat, or consequence. Keep the main explanation in the reading flow.
- **Important points:** selectively emphasize decisive terms or conclusions with bold text. Reserve emphasis for what deserves attention.
- **Quotes:** short, accurately attributed source quotations when the original wording adds value. Link the source and explain the quotation's relevance. Use a labeled note for your own insight rather than presenting it as a quotation.

Choose the format for the content, not to meet a quota. Balance sustained explanation with scannable structure: avoid both walls of paragraphs and fragmented, bullet-only summaries. Not every section needs every element, and callouts should highlight exceptional points rather than repeat the surrounding text.

## 4. Build the static reading site

Generate every planned HTML page and its assets in the same run before handing off the course:

- `index.html`: course overview, scope, prerequisites, and the complete reading order.
- `chapters/01-<chapter-slug>.html`, and subsequent numbered chapters.
- `reference/resources.html`: annotated sources linked to the chapters they support.
- `reference/glossary.html`: when a shared glossary is useful.
- `assets/course.css`: shared presentation.
- `assets/diagrams/*.svg`: local diagrams when not embedded directly in HTML.

Include the same course sidebar on the index, every chapter, and every reference page. Link all chapters and reference pages, mark the current page with `aria-current="page"`, and provide previous/next chapter links and a local table of contents for long chapters. Use ordinary relative HTML links with correct paths from each page's directory. The reader opens `index.html` once and navigates the whole course from there.

Keep navigation in the HTML itself, so it works through `file://` without JavaScript, a development server, or fetching shared fragments. All required styles, fonts, diagrams, and other assets must be local; use system fonts by default. External resources are links, not dependencies for rendering or understanding the course.

Use semantic HTML, a consistent heading hierarchy, readable typography, comfortable line lengths, and restrained styling. Keep the sidebar persistent on wide screens and usable without covering the content on narrow screens. Make code blocks scroll horizontally, diagrams scale without clipping labels, and print styling prioritize the chapter content over navigation. Share styling rather than duplicating it in each page. Add no application features or learner-state storage.

Give sections, lists, tables, callouts, and quotations consistent spacing and shared styles. Use proper table headers and captions where useful, keeping wide tables usable on narrow screens. Label callouts in text rather than relying on color alone; render source quotations with `blockquote` and visible attribution.

### Technical diagrams

Use rendered diagrams wherever relationships, transitions, or ordering would otherwise be difficult to follow. Choose the notation that explains the mechanism: state machines for transitions, flowcharts for decisions, sequence diagrams for interactions over time, and architecture or data-flow diagrams for structure and movement.

Author SVG directly or render diagram notation into local SVG assets during generation. The final HTML must contain or reference the rendered diagram, not leave ASCII art, raw diagram notation, or a runtime renderer as the explanation.

Label states, actors, arrows, conditions, and important boundaries. Use consistent visual conventions, readable text, and enough spacing for labels. Accompany diagrams with captions explaining what to notice and how they relate to the prose. Provide descriptive image alt text, or a title and description for inline SVG. Diagrams must agree with the code and explanation; prefer technical accuracy over decoration.

## 5. Validate and hand off

Before reporting completion:

- Confirm every planned chapter and reference page exists with substantive content, not placeholders or deferred sections.
- Review each chapter for a healthy mix of explanatory prose and useful structure, with clear sections, selective emphasis, and readable comparisons or callouts where warranted. Check that formatting preserves technical depth rather than replacing explanations.
- Check every local link, fragment target, stylesheet, image, and referenced asset resolves from its referring file, including local assets referenced by CSS. Confirm all pages are reachable from the sidebar.
- Check HTML structure, parse generated SVGs, and verify diagram labels, arrows, and ordering against the explanations. Validate runnable examples with appropriate available tools; clearly state anything not executed.
- Confirm the course has no required network resources, runtime imports, or server-dependent navigation.
- If browser tooling is available, inspect the index, a representative chapter, and a diagram-heavy page at wide and narrow widths using local files. Check sidebar usability, readable content, and unclipped diagrams. If unavailable, report that visual rendering was not checked rather than claiming it was.

Use available validation tools; do not add a build system merely to serve static HTML. If a generation limit or unresolved failure prevents the full course, report it as incomplete and identify the missing parts. A chapter outline is not a completed course.

Hand off the path to `index.html`, the scope delivered, and any material validation or source-access limitations. There is no required learner-facing Markdown, mission file, notes file, or learning record.

## Content updates

When the user requests an addition or correction, read the affected course files first. Modify only the relevant content and directly dependent navigation, citations, glossary entries, and diagrams. Preserve unrelated chapters, stable filenames and anchors where possible, and user-authored changes. Revalidate the affected pages and links; a change to the chapter list requires updating the sidebar on every page. Updating the course is document maintenance, not a new learning session.
