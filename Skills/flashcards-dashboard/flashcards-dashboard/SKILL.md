---
name: flashcards-dashboard
description: |-
  Creates an interactive HTML learning dashboard from a source file by extracting key concepts into validated flashcards with source links, hover-detail answers, filters, review tracking, shuffle, and progress tracking.

  Use when the user says:
    - "Create flashcards from this file"
    - "make an HTML learning dashboard"
    - "turn this deck into flip cards"
    - "Create an HTML dashboard with animated Flashcards that flip when clicked"
    - "help me learn the content in this file"
    - "make a study dashboard from this deck"
---
# Flashcards Dashboard

## When to use
Use this skill when the user wants to learn, revise, or review the content of a SharePoint/OneDrive file through an interactive HTML dashboard with animated flip flashcards.

Use it for PowerPoint decks, PDFs, Word documents, or other readable files where the goal is comprehension, training, revision, onboarding, or knowledge checks.

## Inputs
- Source file name, URL, selected file, or file reference.
- Optional preferences: audience/difficulty, number of cards, language, theme, destination, topics to emphasize/exclude.
- Modes to include by default: Study, Shuffle, Review missed. Do not include Quiz mode unless explicitly requested.

## Steps
1. Locate the source file.
   - If the user gives a filename, use SharePoint/OneDrive file discovery tools.
   - If exact search fails, retry broader keywords and semantic search.
   - If outside the current site, use tenant search as fallback.
   - If no file is found, say so plainly and ask for a link or selected file.

2. Read or digest the file content.
   - Use a file-reading tool when raw content is needed.
   - Use file digest only when a summary is enough.
   - For PowerPoint files with speaker notes, preserve slide content and presenter-note insights.
   - For long files, create cards from section summaries and say the dashboard is summary-based.

3. Extract cards using this schema:

```json
{
  "id": "Stable unique card id, e.g. c0",
  "category": "Short topic label",
  "question": "Question shown on the front",
  "answer": "Concise answer shown on the back",
  "detail": "Expanded answer for hover/focus detail panel",
  "hint": "Short clue or memory hook",
  "sourceAnchor": "Slide/page/section/table name, or Source file if unknown",
  "sourceUrl": "Clickable source document URL when available",
  "difficulty": "Easy | Medium | Hard"
}
```

   - Produce 12–25 cards unless the user requests another count.
   - Keep `answer` concise; put longer explanation in `detail`.
   - Do not fabricate source anchors, URLs, slide counts, page numbers, or facts.

4. Generate a self-contained HTML dashboard.
   - Use sandboxed code and store the full HTML as a data reference before file creation.
   - Include flip cards, category filters, difficulty filters, progress tracking, source anchors, source links, hover-detail answers, Study, Shuffle, and Review missed.
   - Cards flip on click and keyboard Enter/Space.
   - Hover-detail panels must also work on keyboard focus.
   - Detail panels must not be clipped: use visible overflow, high z-index on hovered/focused cards, and right-align panels for cards near the right edge.
   - Keep card widths consistent even when filters leave only one visible card. Use a fixed max card width such as `max-width:360px`, and grid columns like `repeat(auto-fill, minmax(280px, 360px))` with `justify-content:start`; don't use `1fr` in a way that lets a single card stretch across the dashboard.
   - Use inline CSS and JS only. No external scripts, stylesheets, fonts, images, or CSS URL dependencies.

5. Make source links work with one left-click in SharePoint.
   - Put source links only on the answer side.
   - Use a normal `<a>` element with `href`, `target="_blank"`, `rel="noopener noreferrer"`, and `data-interception="off"`.
   - Add pointer/mouse handlers to prevent card flipping from taking the click:

```html
<a class="sourceLink"
   href="SOURCE_URL"
   target="_blank"
   rel="noopener noreferrer"
   data-interception="off"
   onpointerdown="event.stopPropagation()"
   onmousedown="event.stopPropagation()"
   onclick="event.preventDefault(); event.stopPropagation(); if(event.stopImmediatePropagation){event.stopImmediatePropagation();} window.open(this.href, '_blank', 'noopener,noreferrer'); return false;">
  Open source document
</a>
```

   - Add CSS so the link remains clickable inside transformed cards:

```css
.sourceLink { pointer-events:auto; position:relative; z-index:1000; }
```

   - In the delegated card click handler, ignore `.sourceLink` before other card click logic:

```js
if (e.target.closest('.sourceLink')) return;
```

6. Apply the default refined dark design system.
   - Page background: `#0B1120` and `#0F172A`.
   - Card background: `#1E293B` to `#0F172A` subtle gradient.
   - Answer card background: `#065F46` to `#064E3B` subtle gradient.
   - Border: `1px solid #334155`.
   - Primary text: `#F1F5F9`; secondary/source text: `#94A3B8`.
   - Accent/progress/active filters: `#22D3EE` or `#67E8F9` at reduced brightness.
   - Difficulty colors: Easy `#67E8F9`, Medium `#34D399`, Hard `#FBBF24`.
   - Body text minimum 15–16px with 1.55–1.65 line-height.
   - Use visible card borders, soft shadows, and subtle top highlights.
   - Action buttons: “Got it” soft green; “Needs review” soft amber.

7. Implement Review missed and action buttons correctly.
   - Track cards by stable `data-id`, never array index alone.
   - Maintain `missed` as a set of card ids.
   - “Needs review” adds the card id to `missed`.
   - “Got it” removes the card id from `missed` and flips the current card back to the front side with `card.classList.remove('flipped')`.
   - In Study and Shuffle mode, clicking “Got it” should visibly flip the card back to the front side.
   - In Review missed mode:
     - Show only cards whose ids are in `missed`.
     - Hide “Needs review”; only “Got it” shows.
     - Clicking “Got it” removes that card from Review missed immediately and flips it to the front side.
   - Shuffle must reorder DOM/cards without changing card ids or breaking review tracking.

8. Validate before saving.
   - Confirm the HTML contains: grid, front/back faces, flip behavior, filters, progress, source anchors, hover/focus details, stable `data-id`, Review missed by id, and CSS/JS hiding “Needs review” in Review missed.
   - Confirm card layout uses fixed max card width and doesn't stretch a single filtered card to full dashboard width.
   - Confirm “Got it” removes `flipped` from the current card.
   - Confirm source links include `data-interception="off"`, `onpointerdown`, `onmousedown`, `stopImmediatePropagation`, `window.open(this.href, '_blank', ...)`, and `.sourceLink { pointer-events:auto; position:relative; z-index:1000; }`.
   - Confirm source links do not trigger card flipping.
   - Confirm no external `<script src>`, stylesheet links, or remote image/font dependencies.
   - If validation fails, fix and validate again before file creation.

9. Save the dashboard.
   - Create an `.html` file in SharePoint/OneDrive.
   - Prefer saving beside the source file when writable; otherwise use the current site’s primary Documents library.
   - If access is denied, retry in the current site’s primary document library or ask for a destination.
   - Use a descriptive filename like `<source topic> Flashcard Dashboard.html`.

## Output format
Respond with:

```markdown
Created the HTML flashcard dashboard:

[File name](file URL)

Includes clickable animated flip cards, category/difficulty filters, source links, hover-detail answers, Review missed, Shuffle, and progress tracking.
```

If the file couldn’t be created:

```markdown
I couldn’t create the dashboard because: <reason>.
```

## Quality checklist
- Real `.html` file saved in SharePoint/OneDrive.
- Every card has required fields and stable id.
- Source links open in a new browser tab on one left-click in SharePoint.
- Hover-detail panels are visible, not clipped, and keyboard accessible.
- Cards retain original width in filtered views and never stretch full dashboard width.
- “Got it” flips the card back to the front side in Study, Shuffle, and Review missed.
- Softer dark palette, improved hierarchy, card depth, calm accents, and difficulty colors are applied.
- Review missed hides “Needs review”; “Got it” removes the current card from review.
- Shuffle does not break review tracking.
- Quiz mode is not included by default.
- Content is grounded in the source file.
- If tools fail or return empty, say so plainly — don’t invent content.
