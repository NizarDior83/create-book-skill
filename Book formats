# Book Formats

Read when setting trim size during the interview, or writing layout notes into page entries.

---

## Common trim sizes

| Size | Use | Aspect ratio for prompts |
|---|---|---|
| 8.5 × 11 in | Adult coloring, activity books. The volume default. | 3:4 portrait |
| 8.5 × 8.5 in | Children's coloring, toddler books | 1:1 square |
| 8 × 10 in | Children's coloring, slightly cheaper to print | 4:5 portrait |
| 6 × 9 in | Text-led books with spot illustration | 2:3 portrait |
| 8.5 × 8.5 or 10 × 8 in | Picture books | 1:1 or 5:4 landscape |

Defaults when the user does not specify: **8.5 × 11 for adult coloring, 8.5 × 8.5 for children's coloring, 8.5 × 8.5 for picture books.**

State the aspect ratio inside every page prompt. Generating square art for a portrait book means every page gets cropped or letterboxed.

---

## Margins and safe zone

- **Outer margin:** 0.25 in minimum beyond trim, more is safer
- **Gutter (inner, spine side):** 0.375 in for books under 150 pages; add 0.125 in per additional 150 pages
- **Safe zone:** keep every element the reader must see 0.5 in inside the trim edge

Practical instruction for prompts: **compose with generous empty margin on all sides.** Subjects that touch the frame edge get cut by the trim.

The gutter matters most on spreads. If the character's face lands on the spine, it disappears into the fold — plan faces to sit left or right of centre on any double-page spread.

---

## Single-sided printing for coloring books

Coloring books are usually printed single-sided so markers do not bleed through onto the next image. That means alternating art page and blank page, and it doubles the physical page count.

Confirm this with the user, because it changes the count: a "30 page" coloring book usually means **30 images and a 60+ page book**.

---

## Page count rules

- Minimum for most print-on-demand: **24 pages**
- Page count must be **even**
- Front matter typically takes 2–4 pages: title page, copyright, optional dedication or test-color swatch page
- Adult coloring books commonly run 50–100 images
- Children's coloring books commonly run 25–50 images
- Picture books conventionally run **32 pages** total, which after front matter leaves about 28 pages of art — the standard trade format, worth honouring if the user intends traditional publishing

---

## Text overlay

Story text is laid over finished art in a layout tool, not rendered by the image model. So every page carrying text needs a **layout note** naming where the text sits and what the illustration must keep clear.

Reliable patterns:
- **Sky band** — text across empty sky at the top, art in the lower two thirds
- **Ground band** — text across the bottom third over simple ground or floor
- **Side panel** — art on one side, plain background on the other
- **Full-bleed with a quiet corner** — art fills the page, one corner kept low-contrast and uncluttered

Write the choice into the prompt: *"leave the upper third as open uncluttered sky for text overlay."*

Keep text off busy or high-contrast areas — it becomes unreadable, and a picture book that is hard to read fails at the only thing it does.

---

## Covers — always required

Every book needs a front and a back cover. Produce both without being asked. A book without a cover is not a book, and the cover is the only page that has to sell before it is read.

Generate the front and back as **two separate images**, never as one wrap. Wrap covers put the spine in the middle of the generation, where the model treats it as a design element and fills it with garbage. Assemble the wrap in a layout tool.

### Front cover

Reuse the character DNA and style descriptor verbatim, exactly as on interior pages — the cover is where consistency is most visible, because it sits next to the interior in every listing preview.

Requirements:
- The character large, centred, and unmistakable, in her single most appealing pose
- Simpler than any interior page. A busy cover fails at thumbnail size, which is how every online buyer first sees it.
- Reserve clear space at the top for the title and at the bottom for the author name
- Strong silhouette that still reads when shrunk to 100px

### Back cover

- Much simpler than the front — mostly quiet field, matching palette and style
- A small character motif or single decorative element, not a full scene
- **Leave the lower right corner completely clear and light-toned for the barcode.** Roughly 2 × 1.2 in. A barcode printed over dark art will not scan, and a book that will not scan does not sell.
- Reserve a calm central band for blurb text

### Spine

Spine width = page count × paper thickness.
- White paper: 0.002252 in per page
- Cream paper: 0.0025 in per page

So a 84-page white-paper book has a spine of about 0.19 in. Most print-on-demand services require a minimum page count before they will print spine text at all — commonly around 79 pages — so short picture books get a blank spine. Verify against the printer's own spine calculator before final layout; these figures move.

Do not generate spine art. Fill it with a flat colour drawn from the book's palette.
