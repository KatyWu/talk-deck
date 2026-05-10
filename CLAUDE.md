# Project — Katy 大學演講 / "Global team brand designer experience sharing"

A 140-minute (~135 min) university guest lecture deck. Audience = UX / programming / bitcoin students. Tone = casual share + practical knowledge.

---

## ⚡ Before ANY deck.html edit

**Read `SLIDES.md` first.** It lists every slide's line number. Jump directly to the right line — do not scan the whole file.
After any add/delete/reorder, update `SLIDES.md` in the same commit.

---

## 🎯 Hard rules — do not violate

1. **Language: full English on slides** (speaker may mix 中文 verbally; speaker notes in English bullets).
2. **No serif fonts.** Display = `Archivo Black`. Body = `Space Grotesk`. Mono labels = `JetBrains Mono`.
3. **Palette: black + electric blue + neon green.**
   - `--black: #050607` · `--blue: #1538FF` · `--green: #CFFF3C` (accent / highlight only)
4. **Speaker notes = brief bullet prompts only.** Never full scripts. One short paragraph per slide max.
5. **Avoid AI-slop tropes.** No emoji, no rounded-corner-with-left-accent containers, no gradient backgrounds, no fake icon SVG. Placeholders are fine — better than bad attempts.
6. **Do NOT overwrite the main deck without copying it first.** Past mistake: I lost 100+ slides by overwriting `Talk.html`. Always copy → edit copy.

---

## 🗂 Files

- `deck.html` — the main deck (currently Ch.00 only, 6 slides). Authoritative.
- `deck-stage.js` — slide-deck shell (scaling, nav, speaker notes). Don't edit.
- `大綱.md` — full content outline, 106 slides, 5 chapters. **Source of truth for content.** User edits this directly between turns.
- `CLAUDE.md` — this file.

---

## 🧱 Chapter plan (per `大綱.md`)

| Ch | Topic | Slides | Time |
|---|---|---|---|
| 00 | Opening | 6 | 5m |
| 01 | Brand & UIUX Designer | 27 | 35m |
| 02 | Working Life — Foreign + Remote (merged) | 26 | 35m (incl. break) |
| 03 | Bitcoin | 13 | 15m |
| 04 | AI | 25 | 35m |
| 05 | 結尾 / Closing | 9 | 10m |
| **Total** | | **106** | **135m** |

User has finalized content for all chapters in `大綱.md`. **Always re-read `大綱.md` before editing — user updates it between turns.**

---

## 🎨 Style DNA (already in `deck.html`)

- Slide size: **1920×1080** via `<deck-stage>` web component.
- Three section variants: default (black) / `.blue` (chapter dividers, hero, signposts) / `.green` (Q breaks, recap moments).
- Chrome: top `<div class="hdr">` with mono uppercase labels + green tick `■`. Bottom `<div class="ftr">` with name + `XX / total`.
- Display sizes use `.display` (xl ~360px hero / sm ~180px section) with `.hl` neon-green inline highlight.
- Reusable layouts already styled in `<style>` block: `.cards.c2/c3/c4`, `.bullets`, `.numlist`, `.twocol`, `.weekgrid`, `.talkmap`, `.compare`, `.timeline`, `.stat`, `.quote`, `.divider`, `.tagrow`, `.eyebrow`, `.subtitle`. **Reuse these — don't invent new layouts unless content genuinely needs it.**
- Background textures: `.grid-tex` (for `.blue`) / `.grid-dark` (for default). Always include one.

---

## 🔁 Working flow with user

1. User edits `大綱.md` directly. They'll say "我改完了 / saved" to signal.
2. Always **read `大綱.md` first** before any deck edit — content may have changed.
3. Build/edit one chapter at a time. Show user. Wait for OK before next.
4. On large additions/restructures, **copy `deck.html` → `deck v2.html`** before destructive changes.
5. Speaker-notes JSON array in `<head>` must stay **positionally aligned** with slide order. When inserting/deleting/reordering slides, update the array in the same edit.
6. Footer counter `XX / total` must match total slide count — update when slide count changes.

---

## 📊 Slide content patterns from outline

- **Chapter dividers**: `.blue.divider` with big "01 / 02 / …" numeral + chapter title + scribbled English subtitle.
- **Q break slides**: `.green` background, simple "Q break — [chapter]" + 2–3 prompt questions.
- **Stakeholder cards (Ch.01)**: `Person 0X — Role` pattern, one card per person, single bold takeaway line at bottom.
- **Before/After AI examples (Ch.04)**: two-column compare layout.
- **Recap slides (every chapter)**: `.green` numbered list, 3 takeaways max.

---

## ⚠️ Things user has flagged as friction in past

- I once made the deck in **traditional Chinese with serif fonts and beige palette** — completely wrong. User had to re-state the rules. **Re-read this CLAUDE.md if uncertain.**
- I once duplicated work because I didn't re-read `大綱.md` after user edited it. **Always re-read before edits.**
- Validator findings about `<24px` text are usually false positives on chrome (header/footer mono labels at 14–18px are intentional). Ignore unless body text is genuinely small.

---

## 🛠 Tooling notes

- `<deck-stage>` auto-assigns `data-deck-slide` indices, posts `slideIndexChanged` for speaker notes, handles keyboard nav. Don't manually set indices.
- Section attrs needed: `data-label="…" data-screen-label="NN Title" data-om-validate="no_overflowing_text,no_overlapping_text,slide_sized_text"`.
- For batch slide edits, prefer `run_script` reading the file as a string and rewriting — avoids fragile multi-line `str_replace_edit` matches.

---

## 🔮 Current status (2026-05-09)

- ✅ `大綱.md` finalized through all 5 chapters
- ✅ `deck.html` rebuilt with 6 Ch.00 slides matching outline (cover · self intro · the work · map · what this isn't · what you get)
- ⏳ Next: Ch.01 (27 slides) — wait for user to confirm Ch.00 visual direction before building
