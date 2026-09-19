# Pumpkin Studio — shared site specification

> **Frozen on 2026-08-13.** This file is byte-identical in all three learning repositories
> (`typo3-lernprojekt`, `astro-lernprojekt`, `wp-lernprojekt`). Change it only if the change
> is carried into **all three** — otherwise the sites drift apart and the system comparison
> is worthless.
>
> *Translated to English on 2026-09-19. The routes deliberately stay German: they are the
> URLs of a fictional German agency, and changing them would be a change to the sites
> themselves, not to their documentation.*

A fictional small agency called **"Pumpkin Studio"**. The same site, built three times: once
in TYPO3 v13, once as a WordPress block theme (FSE), once in Astro. The point is not the
site — the point is the direct comparison of three routes to the same result.

---

## Pages

```
/                    Home
/leistungen          Overview
/leistungen/[slug]   Detail
/blog                List
/blog/[slug]         Detail
/kontakt
/404
```

---

## Content types

### Service (4–5 of them) — `Leistung` in the UI

| Field | Type | Note |
|---|---|---|
| `title` | Text | |
| `slug` | Text | URL segment |
| `teaser` | Text | short, for the card in the grid |
| `icon` | Text | string key, not an upload |
| `order` | Number | sort order within the grid |
| `featured` | Bool | drives the home page grid |
| `body` | Rich text | |

### Blog post (5–6 of them)

| Field | Type | Note |
|---|---|---|
| `title` | Text | |
| `slug` | Text | |
| `date` | Date | |
| `teaser` | Text | |
| `cover` + `alt` | Image | Alt text is required, not optional |
| `tags[]` | List | |
| `author` | Relation | → Author |
| `draft` | Bool | |
| `body` | Rich text | |

### Author (2 of them)

| Field | Type |
|---|---|
| `name` | Text |
| `role` | Text |
| `avatar` | Image |

This type exists for exactly one reason: **to build one relation in every system.** TYPO3
solves it differently from WordPress and differently from Astro — that is the thing being
learned.

---

## Home page sections (fixed order)

1. **Hero**
2. **Service grid** — 3× `featured`
3. **Text/image with a left/right switch** ← comparison anchor
4. **Quote**
5. **CTA band**
6. **3 latest blog posts**

> **Section 3 is the comparison anchor.**
> TYPO3 = custom content element (Fluid + TCA/Content Blocks) ·
> WordPress = custom block (`block.json` + editor UI) ·
> Astro = `.astro` component with an `align` prop.
> The same visible result three times, three entirely different routes.

---

## Design tokens

Defined once, typed three times. Without identical tokens the sites drift apart visually
and the comparison loses its value.

```
Colours
  ink      #1A1614
  paper    #FDFBF7
  pumpkin  #E8590C
  muted    #6B625C
  line     #E5DED5

Typography
  Headings  Serif
  Body      System stack
  Sizes     fluid via clamp()

Spacing
  4  8  16  24  40  64  96

Layout
  contentSize  44rem
  wideSize     72rem
  Radius       4px / 16px
```

How each system implements them — part of the comparison too:

| System | Tokens live in |
|---|---|
| TYPO3 | SCSS map |
| WordPress | `theme.json` presets |
| Astro | CSS custom properties |

---

## Deliberately not part of the spec

No Tailwind, no UI framework, no headless setup, no multi-language, no shop. Hand-written
CSS in all three projects — anything else would make the systems incomparable.
