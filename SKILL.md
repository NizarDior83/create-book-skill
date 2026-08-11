---
name: book-prompt-forge
description: >-
  Interview the user about a book they want to illustrate, then generate every page's
  Gemini image prompt in one markdown file, with the recurring character locked to a
  fixed identity across all pages. Use when the user wants a coloring book (adult or
  children's), a children's story book, an activity book, a picture book, or a
  KDP/Amazon book interior — and whenever they ask for "all the pages", "30 pages",
  "the whole book", "page prompts", "a book about the same character", or "keep the
  character consistent". Trigger on the book noun rather than on the word "prompt" —
  a request for one image, one scene, or a prompt from an uploaded photo belongs to a
  single-image prompt skill instead.
---

# Book Prompt Forge

Produce a complete, page-by-page prompt set for an illustrated book, ready to paste into Gemini one page at a time.

A book is not a pile of images. The reader turns thirty pages and must see the same girl, the same line weight, the same world. Individually good prompts written page by page drift — by page fifteen the character has a different face and the book is unsellable. This skill exists to stop that drift, and every rule below serves it.

---

## The two axes

Book *type* is the wrong question. Ask two questions instead, because they vary independently:

| | **Recurring character** | **Standalone scenes** |
|---|---|---|
| **Line art** (coloring) | Same bear on 30 pages, uncolored | Mandalas, botanicals, patterns |
| **Full color** (illustrated) | Children's story book | Wordless art book, scene collection |

All four cells are real books. An adult coloring book about "the same girl in different cities" is line art + recurring character — it needs the identity lock exactly as much as a children's story does.

**Character work applies whenever the subject axis is "recurring", regardless of format.** Skip Phase 2 entirely for standalone books.

---

## Phase 1 — Interview

Ask these before writing anything. The answers drive every downstream decision, and guessing at them produces a book the user did not ask for.

Ask in **two batches** so the user is not facing twelve questions at once.

**Batch A — what the book is**
1. What is the book about? (one sentence)
2. Coloring book (black line art to be colored in) or fully illustrated (finished color art)?
3. Who is it for — adults, or children of what age?
4. Does one character recur through the book, or is each page a standalone scene?
5. How many interior pages?

**Batch B — how it looks and reads**
6. Visual style? Offer 3–4 concrete options drawn from `references/style-library.md` and matched to their answers, rather than asking them to invent one.
7. If a character recurs: describe them — age, hair, clothes, anything fixed.
8. Does the book carry story text, or is it images only?
9. If it carries text: what language? Story text is written in the user's chosen language; **image prompts stay in English**, because image models are trained predominantly on English captions and non-English prompts degrade quality.
10. Trim size and orientation, if they know it. If not, default per `references/book-formats.md`.

When an answer is missing and the book cannot proceed without it, ask again. When an answer is missing but a sane default exists, take the default and state it in one line.

---

## Phase 2 — Lock the character

Run this phase only for recurring-character books. Its output is the single source of truth for the character; every page prompt copies from it.

### Write the DNA block

Fill every field. A field left vague is a field the image model improvises differently on each page.

```
CHARACTER DNA — [name]
Age & build: [e.g. 7 years old, small and round, large head-to-body ratio]
Face: [face shape, cheeks, nose, mouth, distinguishing marks]
Eyes: [shape, size, colour]
Hair: [colour, length, texture, exact style, how it sits]
Skin: [tone]
Outfit: [every garment, its colour, its pattern — this never changes between pages]
Footwear: [colour and type]
Signature prop: [one memorable object she always carries — the single strongest anchor for recognition]
Expression default: [her resting face]
```

The signature prop earns its own field because it survives style drift better than any facial feature. A reader identifies the character by the red satchel three pages before they read the face.

### Generate the character sheet prompt

Output one prompt that produces a reference sheet: the character at front, three-quarter, side, and back view, in a neutral standing pose, on a plain white background, in the book's chosen style. Instruct the user to generate it first, pick the best result, and keep the image.

### State the two-lock method

Tell the user plainly:

- **Attach the character sheet image** to each page prompt in Gemini. This is the strong lock.
- **The DNA text travels in every prompt anyway.** It is the fallback for regenerating a single page later, or for any surface where the image cannot be attached.

Both, not either. The text lock alone drifts; the image lock alone fails the moment they regenerate page 12 in a fresh session.

---

## Phase 3 — Plan the pages

Write a one-line plan for every page before writing any prompt, and show it to the user for approval.

The plan exists because a book needs a shape a page-by-page process cannot produce. A story needs an arc. A coloring book needs difficulty that ramps and settings that vary. Planning first also surfaces repetition while it is still cheap to fix.

Each plan line carries: **page number — setting — what the character is doing — camera angle**. Include the front and back cover as their own lines at the top of the plan, so the user approves them alongside everything else.

Vary the camera angle deliberately across the plan. Thirty medium eye-level shots is thirty times the same picture, and this is the most common way an otherwise correct book comes out boring. Cycle through wide establishing, medium, close-up, low angle, high angle, over-the-shoulder.

For story books, hold the arc: setup, inciting moment, rising complication, climax, resolution. For coloring books, ramp complexity from simple early pages to dense later ones.

Get approval on the plan, then write prompts. Revising a rejected plan costs one message; revising thirty rejected prompts costs the session.

---

## Phase 4 — Write the page prompts

### The anti-drift rules

- **Paste the DNA block verbatim into every page prompt.** Copy the characters exactly. Paraphrasing it — "the same girl as before", "our young heroine in her usual outfit" — is what actually causes drift, because the model reconstructs the description from scratch each time and reconstructs it differently.
- **Restate the style descriptor verbatim in every prompt too.** Style drifts as readily as faces do.
- **Give every page a distinct action, setting, and camera angle**, taken from the approved plan.
- **Keep text out of the image.** Image models render letterforms unreliably, and the user's story text will be laid over the art in a layout tool. Say "no text, no lettering, no words in the image" in every prompt. This is a guardrail worth stating in the negative because there is no positive phrasing that reliably suppresses spurious signage.

### Format-specific requirements

**Coloring pages** must specify: pure black outlines on a plain white background; no shading, no grayscale, no hatching, no colour fill; clean closed line work so digital colouring does not leak; white background inside every enclosed shape. Line weight and detail density come from the age band — see `references/style-library.md`.

**Full-colour pages** must specify: the fixed palette, the lighting direction, and where to leave uncluttered copy space for text overlay.

### Output template

One markdown file. Per-page fields are conditional — a wordless coloring book gets the prompt and nothing else; a coloring book with a story gets the text fields too.

```markdown
# [Book Title]
**Format:** [coloring / full colour] · **Audience:** [age] · **Pages:** [n] · **Trim:** [size]
**Style:** [one-line style descriptor, reused verbatim in every prompt below]

## Character DNA
[the block from Phase 2]

## Character Sheet — generate this first
[reference sheet prompt]

---

## FRONT COVER
[full prompt — character large and simple, clear space for title and author]

## BACK COVER
[full prompt — quiet field, lower right corner light and empty for barcode]

**Spine:** [width] — flat colour, no art.

---

## Page 1
**Story text ([language]):** [only when the book carries text]
**Layout note:** [only when the book carries text — where the text sits and what stays clear]

**Prompt:**
[Full English prompt: scene, action, camera angle, composition, verbatim DNA block, verbatim style descriptor, format constraints, no-text instruction.]

---

## Page 2
...
```

### Long books

Past 20 pages, write the prompts in batches of 10 and check in between batches. Quality degrades across a long single generation, and the drift this skill exists to prevent will reappear in the skill's own output.

---

## Phase 4b — Covers

Every book gets a front and a back cover prompt. Produce them without being asked; a book without a cover is not a book.

Generate front and back as two separate images, never one wrap — a wrap puts the spine mid-generation and the model fills it with garbage. The front carries the character large and simple enough to read at thumbnail size, with clear space for title and author. The back stays quiet, and **keeps its lower right corner light and empty for the barcode**, because a barcode over dark art will not scan.

Both reuse the character DNA and style descriptor verbatim. See `references/book-formats.md` for spine width and barcode dimensions.

---

## Phase 5 — The agent brief

Produce a second file: a self-contained brief the user hands to whatever agent or assistant generates the images. Do this without being asked. The prompt file tells the agent *what* to draw; the brief tells it *how to work* — and the working method is what actually preserves consistency.

The brief must stand alone. The agent will not see this conversation, the page plan, or your reasoning, so anything left unwritten does not exist for it.

Follow `references/agent-brief.md` for the full template. The parts that carry the weight:

- **Always attach the original character sheet, never the previous page's output.** Chaining outputs compounds error and is the single most common way a book drifts.
- **Paste prompts verbatim.** A capable agent will otherwise compress the repeated DNA block, which is exactly the failure the repetition prevents.
- **A consistency check table** naming the specific wrong version of each trait, not just the right one.
- **The predicted failure** — every style has one thing models get wrong by default. Name it or the agent accepts it.
- **The hardest page, by number**, so the agent regenerates it without being told.
- **Every prompt inlined in full** — character sheet, both covers, and all pages. A brief that points at a separate prompt file has failed: the agent will either lose the prompts or work from them while ignoring the rules. Briefs run to thousands of words, and that is correct.

---

## Phase 6 — Deliver

Hand over **two files**: the prompt file and the agent brief. Then say, in three lines: generate the character sheet first; attach it to every page prompt; regenerate any page whose character looks wrong rather than accepting it, because one off-model page is visible to every reader.

Offer one revision pass — a different style, a different page count, or a re-plan.

---

## Reference files

- `references/style-library.md` — style vocabulary by audience and format, line weight and detail density by age band, palette guidance. Read when proposing style options in Batch B or writing format constraints in Phase 4.
- `references/agent-brief.md` — template for the handoff brief. Read in Phase 5b.
- `references/book-formats.md` — trim sizes, margins, bleed, page count rules, KDP specifics. Read when setting trim in Batch B or writing layout notes.
