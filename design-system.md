# Design System — Katy University Talk

Slide size: **1920 × 1080 px**. Body padding: **120 px** all sides.

---

## Colour Tokens

| Token | Value | Usage |
|---|---|---|
| `--black` | `#050607` | Default slide background |
| `--blue` | `#1538FF` | Chapter dividers, hero moments |
| `--green` | `#CFFF3C` | **Accent only** — `.hl`, labels, key markers |
| `--ink` | `#F6F6F4` | Primary text |
| `--muted` | `rgba(246,246,244,0.55)` | Secondary text on dark |
| `--muted-blue` | `rgba(255,255,255,0.65)` | Secondary text on blue |
| `--rule` | `rgba(246,246,244,0.18)` | Card borders, subtle dividers |
| `--rule-strong` | `rgba(246,246,244,0.35)` | Table rows, prominent dividers |

**`--green` is the only highlight/accent colour.** `--blue` is a background colour — it's not visible enough on black for text emphasis.

---

## Typography

| Role | Family | Size | Weight | Treatment |
|---|---|---|---|---|
| Display XL | Archivo Black | 280 px | 900 | Uppercase, `line-height: 0.92`, `ls: -0.025em` |
| Display LG | Archivo Black | 220 px | 900 | same |
| Display MD | Archivo Black | 170 px | 900 | same |
| Display | Archivo Black | 180 px | 900 | same |
| Display SM | Archivo Black | 130 px | 900 | same |
| Header chrome | JetBrains Mono | 24 px | 400 | Uppercase, `ls: 0.22em`, `--muted` |
| Mono label | JetBrains Mono | 26 px | 400 | Uppercase, `ls: 0.14–0.2em` |
| Body / subtitle | Space Grotesk | 36 px | 400 | `line-height: 1.4` |
| Bullets | Space Grotesk | 34 px | 400 | `line-height: 1.4` |
| Numlist | Space Grotesk | 38 px | 400 | Numbers in Archivo Black 60 px |
| Card title | Archivo Black | 36 px | 900 | Uppercase |
| Card body | Space Grotesk | 24 px | 400 | `--muted` |

**No serif fonts. No gradient text.**

---

## Slide Backgrounds

| Class | Colour | Texture | Use when |
|---|---|---|---|
| *(default)* | `--black` | `.grid-dark` (opacity 0.10) | All regular content slides |
| `.blue` | `--blue` | `.grid-tex` (opacity 0.20) | Chapter dividers, signpost moments |
| `.green` | `--green` | none | Q breaks, recaps, positive/interactive moments |

Always include one texture div as the first child of the section.

```html
<!-- dark slide -->
<div class="grid-dark"></div>

<!-- blue slide -->
<div class="grid-tex"></div>
```

---

## Chrome

### Header `.hdr`
Position: `top 58 px · left/right 96 px`

```html
<div class="hdr">
  <span class="mark">CH-LABEL — SECTION NAME</span>
</div>
```

Right-side label removed from all slides.

`.mark` prefix auto-renders the Bitcoin icon (green on dark/blue, black on green) via CSS `::before`.

### Footer `.ftr`
Position: `bottom 52 px · left/right 96 px`
Currently unused (removed from all slides). Available if needed.

---

## Components

### Cards `.cards.c2 / .c3 / .c4`
Grid layout with glass-morphism cards.

```html
<div class="cards c3">
  <div class="card">
    <div class="n">/ LABEL</div>
    <h4>Title</h4>
    <p>Optional body — keep short.</p>
  </div>
</div>
```

Style: `border-radius: 16px · backdrop-filter: blur(12px) · border: 1.5px solid --rule`

**Image placeholder inside card:**
```html
<div class="card" style="padding:0;overflow:hidden;">
  <div style="aspect-ratio:16/9;background:linear-gradient(135deg,#0d0d0d,#1a1a1a);
              position:relative;display:flex;align-items:flex-end;padding:22px;">
    <span style="font-family:'JetBrains Mono';font-size:18px;letter-spacing:.16em;
                 color:rgba(255,255,255,.35);text-transform:uppercase;">[ image placeholder ]</span>
  </div>
  <div style="padding:22px 26px 26px;">
    <div class="n">/ LABEL</div>
    <h4>Title</h4>
  </div>
</div>
```

---

### Bullets `.bullets`
Unordered list with green dash marker. Keep items to short phrases — no full sentences.

```html
<ul class="bullets">
  <li>Short phrase</li>
</ul>
```

---

### Numbered list `.numlist`
Large Archivo Black numbers as counters. Max 4–5 items.

```html
<ol class="numlist">
  <li>Short phrase</li>
</ol>
```

---

### Tag pills `.tagrow`
Pill-shaped tags. `.on` = active/highlighted (green fill).

```html
<div class="tagrow">
  <span class="tag on">#active-tag</span>
  <span class="tag">#inactive-tag</span>
</div>
```

---

### Two-column `.twocol`
50/50 split with 100 px gap.

```html
<div class="twocol">
  <div>Left content</div>
  <div>Right content</div>
</div>
```

---

### Compare `.compare`
Before/after or A vs B layout.

```html
<div class="compare">
  <div class="col good"><h3>Before</h3><ul><li>item</li></ul></div>
  <div class="col done"><h3>After</h3><ul><li>item</li></ul></div>
</div>
```

`.col.good h3` → green · `.col.done h3` → ink

---

### Week schedule `.weekgrid`
3-column grid: Day · Activity · Tag. Bordered rows.

```html
<div class="weekgrid">
  <div class="day">Mon</div>
  <div class="what">What happens</div>
  <div class="tag">Label</div>
</div>
```

---

### Timeline `.timeline`
7-step horizontal pipeline. Add `.highlight` to featured step.

```html
<div class="timeline">
  <div class="step highlight">
    <div class="s-n">01</div>
    <h5>Step Name</h5>
    <p>Short note</p>
  </div>
</div>
```

---

### Stat `.stat`
Full-bleed large number.

```html
<div class="stat">
  <div class="stat-num">42</div>
  <div class="small-note">Label</div>
</div>
```

---

### Quote `.quote`
Large Archivo Black quotation.

```html
<div class="quote">
  "This is the <span class="hl">key word.</span>"
</div>
<div class="quote-attr">— Attribution</div>
```

---

### Chapter divider `.divider.blue`

```html
<section class="blue divider">
  <div class="grid-tex"></div>
  <div class="hdr">...</div>
  <div class="body">
    <div class="big-ch">Chapter 01</div>
    <div class="big-num">01</div>
    <h2 class="big-ti">Chapter <span class="hl">Title</span></h2>
  </div>
</section>
```

`.big-num` = 520 px · `.big-ti` = 200 px

---

### Relationship map `.talkmap`
Absolute-positioned nodes around a centre circle.

```html
<div class="talkmap">
  <div class="me">ME</div>
  <div class="node n1"><span class="role">Role</span><span class="note">Note</span></div>
  <!-- n1 top · n2 top-right · n3 top-left · n4 bottom-right · n5 bottom-left · n6 bottom -->
</div>
```

---

## Image Placeholder Pattern

Use consistently for any image slot before real photos are inserted:

```html
<div style="aspect-ratio:16/9; background:linear-gradient(135deg,#0d0d0d,#1a1a1a);
            position:relative; display:flex; align-items:flex-end; padding:22px;">
  <span style="font-family:'JetBrains Mono'; font-size:18px; letter-spacing:.16em;
               color:rgba(255,255,255,.35); text-transform:uppercase; z-index:1;">
    [ image placeholder ]
  </span>
</div>
```

---

## Slide Section Template

Every `<section>` must include these attributes:

```html
<section
  class="blue"
  data-label="Short label"
  data-screen-label="NN Title"
  data-om-validate="no_overflowing_text,no_overlapping_text,slide_sized_text"
>
```

| Attribute | Purpose |
|---|---|
| `data-label` | Internal identifier |
| `data-screen-label` | Slide number + title shown in nav |
| `data-om-validate` | Runs 3 checks on every slide |

### Validation rules (`data-om-validate`)

| Rule | Checks |
|---|---|
| `no_overflowing_text` | No text exceeds slide bounds |
| `no_overlapping_text` | No elements overlap unintentionally |
| `slide_sized_text` | Body text is readable size (≥ 24 px) |

**Note:** Header/footer mono labels at 22–24 px are intentional — these validator warnings can be ignored. Only flag if actual body text is too small.

---

## Rules

1. **English only** on slides. Speaker notes in English bullets.
2. **No emoji**. No gradient backgrounds. No serif fonts. No fake icon SVGs.
3. **Green is the only accent** — `.hl`, `.n` labels. Blue is a background/decoration colour only — not readable as text on dark slides. Eyebrow elements not used on slides.
4. **No large text blocks**. Max one short sentence per bullet. No paragraph prose.
5. **Slide content must stay within padding** (120 px all sides). Large display type: test for overflow.
6. **Speaker notes** = brief bullet prompts only. Max one short paragraph per slide.
7. **Never overwrite `deck.html` directly** — copy to `deck v2.html` before destructive edits.
8. **`deck-stage.js`** — do not edit.
