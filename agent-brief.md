# Agent Brief Template

Read when producing the handoff brief in Phase 5b.

The brief is a **separate, self-contained file** the user hands to an image-generating agent. It must work with no other context — the agent will not see the conversation, the plan, or your reasoning. Anything not written in the brief does not exist.

Fill every bracket. Delete nothing.

---

```markdown
# Image Generation Brief — [BOOK TITLE] ([N] pages)

**For the image assistant. Read all of this before generating anything.**

You are generating [N] pages of [book type] for [audience]. The same [character] must appear on every page and be instantly recognisable as the same [character]. [N] individually good images are a failure; [N] pages of one character is the job.

[One sentence naming the single most distinctive thing about this book's look, and stating it must hold across every page.]

---

## Order of work

**Step 0 — Generate the character sheet FIRST.** Use the CHARACTER SHEET prompt below. Review all four views. Regenerate until [the two or three features most likely to drift] are clean and identical across the four. Do not start page 1 until you are satisfied.

**Step 1 — Save that image as `[name]-ref.png`.** It is the reference for the whole book.

**Step 2 — For each page, in order:**
1. Attach `[name]-ref.png`.
2. Paste the page prompt exactly as written. Change nothing.
3. Generate.
4. Run the consistency check below before starting the next page.

**Always attach the original `[name]-ref.png`.** Never use the previous page's output as the reference. Errors compound — chain them and by the final page you have a different character.

---

## Rules

**Paste every prompt verbatim.** Each prompt repeats the full character description and style block. This looks like redundancy you should tidy up. It is not — it is the entire consistency mechanism. Replacing it with "the same character as before" produces a different character.

[If the style block has a negative prompt:] **Keep the negative prompt.** Without it this style collapses into [the specific default it collapses into].

**Do not render text into the images.** Story text is laid over the art later in a layout tool.

[If the book carries text:] **Respect the layout note on each page.** It reserves quiet space where text will sit. Art filling that area makes the text unreadable and the page has to be redone.

**Generate one at a time and check each.** Catching drift on page 2 costs one regeneration. Catching it on the last page costs all of them.

---

## Consistency check — run on every image

Compare against `[name]-ref.png`:

| Check | Must be |
|---|---|
| **[Signature prop]** | [Exact description, and where it sits.] Present on every page. This is the primary anchor — check it first. |
| **[Hair or head feature]** | [Exact description, plus what it must NOT become — the specific wrong version the model defaults to.] |
| **[Face]** | [Exact description.] |
| **[Build / proportions]** | [Exact description.] |
| **[Format constraint]** | [Line weight and closure, or palette and background.] |
| **Text** | Zero letters or numerals anywhere. |
| [If applicable] **Copy space** | The area named in the layout note is quiet and uncluttered. |

**[Name the one or two checks that break first.]** [Say why, in one line.]

If a check fails, regenerate that page with the same prompt and the same reference. After three failures, stop and report which check is failing rather than accepting the image — the prompt needs adjusting, not another roll.

[If any trait deliberately varies:] **[That trait] is meant to differ on every page. That is by design, not drift.** Only the rows above stay fixed.

---

## Known risk

**Page [N] is the hardest.** [Why — usually a page where the character floats free of setting, appears from behind, or is very small in frame.] Expect extra regenerations there.

---

## CHARACTER SHEET PROMPT

[the full prompt]

---

# THE PAGE PROMPTS

**Every prompt is reproduced in full below. Copy them into this file in their entirety — character sheet, front cover, back cover, and every numbered page in order, each with its full DNA and style blocks, plus its story text and layout note where applicable.**

**Never replace this section with a pointer to another file.** A brief that says "the prompts are in the accompanying file" defeats the entire purpose: the agent loses the prompts, or opens a second file and generates without the rules. One file, everything in it, no cross-references.

## CHARACTER SHEET
[full prompt]

## FRONT COVER
[full prompt]

## BACK COVER
[full prompt]

## Page 1
[story text and layout note if applicable]
[full prompt]

## Page 2
[full prompt]

[...continue through every page. The brief is long. That is correct and expected — a 20-page book produces a brief of several thousand words. Do not abbreviate it.]
```

---

## What makes a brief work

**Name the specific wrong version, not just the right one.** "Chin-length bob, not shoulder-length, not wavy" catches drift that "chin-length bob" alone does not, because the agent needs to know what it is checking against.

**Predict the failure.** Every style has one thing models get wrong by default — grey shadows in a saturated palette, open line work in coloring pages, long hair on a short cut. Name it in the check table and the agent catches it. Leave it out and the agent accepts it.

**Flag the hardest page by number.** An agent told which page will fight it regenerates without being asked.

**Say why the repetition matters.** A capable agent will otherwise "helpfully" compress the repeated DNA block, which is precisely the failure the brief exists to prevent.

**Inline every prompt. Length is not a defect.** The strongest pull when writing a brief is toward tidiness — pointing at the prompt file instead of repeating thousands of words. Resist it. The brief and the prompts must travel together as one artifact, because an agent handed a rules file and told to fetch prompts elsewhere will either lose them or generate from the prompt file alone, ignoring every rule you just wrote.
