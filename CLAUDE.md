# Project — Katy 大學演講 / "Global team brand designer experience sharing"

A 140-minute (~135 min) university guest lecture deck. Audience = UX / programming students. Tone = casual share + practical knowledge.

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

- `deck.html` — the main deck, **77 slides, all chapters complete**. Authoritative.
- `presenter.html` — presenter view with timer, speaker notes, next-slide preview, page-jump input (type number + Enter).
- `deck-stage.js` — slide-deck shell (scaling, nav, speaker notes). Don't edit.
- `style.css` — shared styles. Edit with care; changes affect all slides.
- `大綱.md` — full content outline. **Source of truth for content.** User edits this directly between turns.
- `SLIDES.md` — slide index (number → line → title → chapter). Regenerate with Python after any structural change.
- `assets/` — images and videos used in slides (freepik.png, freepik-space.mov, stitch.mov).

**GitHub Pages:**
- Presenter: `https://katywu.github.io/talk-deck/presenter.html`
- Projector: `https://katywu.github.io/talk-deck/deck.html`
- Both windows must be in the same browser on the same machine for BroadcastChannel sync.

---

## 🧱 Chapter plan (current — Bitcoin chapter removed)

| Ch | Topic | Slides | Time |
|---|---|---|---|
| 00 | Opening | 4 | 5m |
| 01 | Brand & UIUX Designer | ~23 | 35m |
| 02 | Working Life — Foreign + Remote (merged) | ~20 | 35m (incl. break) |
| 03 | AI & Tools | ~22 | 35m |
| 04 | Conclusion | ~8 | 10m |
| **Total** | | **77** | **~135m** |

**Always re-read `大綱.md` before editing — user updates it between turns.**

---

## 🎨 Style DNA (already in `deck.html`)

- Slide size: **1920×1080** via `<deck-stage>` web component.
- Three section variants: default (black) / `.blue` (chapter dividers, hero, signposts) / `.green` (Q breaks, recap moments).
- Chrome: top `<div class="hdr">` with mono uppercase labels + green tick `■`. Bottom `<div class="ftr">` with name + `XX / total`.
- Display sizes use `.display` (xl ~360px hero / sm ~180px section) with `.hl` neon-green inline highlight.
- Reusable layouts already styled in `<style>` block: `.cards.c2/c3/c4`, `.bullets`, `.numlist`, `.twocol`, `.weekgrid`, `.talkmap`, `.compare`, `.timeline`, `.stat`, `.quote`, `.divider`, `.tagrow`, `.eyebrow`, `.subtitle`. **Reuse these — don't invent new layouts unless content genuinely needs it.**
- Background textures: `.grid-tex` (for `.blue`) / `.grid-dark` (for default). Always include one.
- Cards/compare/twocol children: do NOT use `flex:1`. Parent `.body` div uses `justify-content:center;gap:36px`.

---

## 🔁 Working flow with user

1. User edits `大綱.md` directly. They'll say "我改完了 / saved" to signal.
2. Always **read `大綱.md` first** before any deck edit — content may have changed.
3. Build/edit one chapter at a time. Show user. Wait for OK before next.
4. On large additions/restructures, **copy `deck.html` → `deck v2.html`** before destructive changes.
5. Speaker-notes JSON array in `<head>` must stay **positionally aligned** with slide order. When inserting/deleting/reordering slides, update the array in the same edit.
6. Footer counter `XX / total` must match total slide count — update when slide count changes.

---

## 📊 Slide content patterns

- **Chapter dividers**: `.blue` with big chapter numeral + title + 48px bridge subtitle (rgba white 0.4).
- **Q break slides**: `.green` background, quote or prompt questions.
- **Stakeholder cards (Ch.01)**: `Person 0X — Role` pattern, one card per person.
- **Before/After AI (Ch.03)**: two-column `.compare` layout. Some columns have Figma/web links.
- **Video slides**: `<video src="assets/file.mov" controls muted playsinline>` with `max-width/max-height:100%;object-fit:contain`.
- **Image slides with links**: wrap image container in `<a target="_blank">` with `↗ Tool name` overlay div.

---

## ⚠️ Things user has flagged as friction in past

- I once made the deck in **traditional Chinese with serif fonts and beige palette** — completely wrong. **Re-read this CLAUDE.md if uncertain.**
- I once duplicated work because I didn't re-read `大綱.md` after user edited it. **Always re-read before edits.**
- Validator findings about `<24px` text are usually false positives (header/footer mono labels at 14–18px are intentional). Ignore unless body text is genuinely small.
- numlist font sizes are intentional: `li { font-size:38px }`, `li::before { font-size:60px }`. Don't increase them.

---

## 🛠 Tooling notes

- `<deck-stage>` auto-assigns `data-deck-slide` indices, posts `slideIndexChanged` for speaker notes, handles keyboard nav. Don't manually set indices.
- Section attrs needed: `data-label="…" data-screen-label="NN Title" data-om-validate="no_overflowing_text,no_overlapping_text,slide_sized_text"`.
- **For batch slide edits**, use Python to read/write the file as a string — avoids fragile multi-line Edit tool matches. Pattern for deletion:
  ```python
  # Delete slide N (comment + section block)
  pattern = r'\n<!-- ═+[^=]+ · LABEL[^>]*═+ -->\n<section[^>]*data-screen-label="N Title[^"]*"[^>]*>.*?</section>'
  html = re.sub(pattern, '', html, flags=re.DOTALL)
  # Pop speaker note at 0-indexed position (in reverse order if multiple)
  notes.pop(N - 1)
  # Renumber data-screen-labels after deletion
  for old, new in [(N+1, N), (N+2, N+1), ...]:
      html = html.replace(f'data-screen-label="{old} ', f'data-screen-label="{new} ')
  ```
- **SLIDES.md regeneration** (run after any structural change):
  ```python
  import re
  lines = html.split('\n')
  for i, line in enumerate(lines, 1):
      m = re.search(r'<section[^>]*data-screen-label="(\d+)\s+([^"]+)"', line)
      if m: rows.append((int(m.group(1)), i, m.group(2)))
  ```

---

## 🔮 Current status (2026-05-12)

- ✅ All 77 slides built and committed (latest: `5f2644d`)
- ✅ Speaker notes written for all slides (JSON array in `<head>`)
- ✅ presenter.html has page-jump input, timer, next-slide preview
- ✅ Video slides: freepik-space.mov (slide ~58), stitch.mov (slide ~61)
- ✅ Figma/web links on image slides (slides 9, 13, 56, 60)
- ✅ Contact slide (last): katy.wu@jan3.com · @katywuu · katy21.com
- ✅ Deployed to GitHub Pages
- ⏳ No pending changes — ready for talk
