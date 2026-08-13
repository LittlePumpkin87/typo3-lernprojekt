# Pumpkin Studio — gemeinsame Site-Spezifikation

> **Eingefroren am 13.08.2026.** Diese Datei liegt identisch in allen drei Lernprojekt-Repos
> (`typo3-lernprojekt`, `astro-lernprojekt`, `wp-lernprojekt`). Änderungen nur, wenn sie in
> **allen drei** Repos nachgezogen werden — sonst laufen die Sites auseinander und der
> Systemvergleich ist wertlos.

Fiktive kleine Agentur **„Pumpkin Studio"**. Dieselbe Site, dreimal gebaut: einmal in
TYPO3 v13, einmal als WordPress-Block-Theme (FSE), einmal in Astro. Der Sinn ist nicht die
Site — der Sinn ist der direkte Vergleich der drei Wege zum selben Ergebnis.

---

## Seiten

```
/                    Startseite
/leistungen          Übersicht
/leistungen/[slug]   Detail
/blog                Liste
/blog/[slug]         Detail
/kontakt
/404
```

---

## Inhaltstypen

### Leistung (4–5 Stück)

| Feld | Typ | Anmerkung |
|---|---|---|
| `title` | Text | |
| `slug` | Text | URL-Segment |
| `teaser` | Text | kurz, für die Kachel im Grid |
| `icon` | Text | String-Key, kein Upload |
| `order` | Zahl | Sortierung im Grid |
| `featured` | Bool | steuert das Startseiten-Grid |
| `body` | Rich Text | |

### Blogpost (5–6 Stück)

| Feld | Typ | Anmerkung |
|---|---|---|
| `title` | Text | |
| `slug` | Text | |
| `date` | Datum | |
| `teaser` | Text | |
| `cover` + `alt` | Bild | Alt-Text ist Pflicht, nicht optional |
| `tags[]` | Liste | |
| `author` | Relation | → Autor |
| `draft` | Bool | |
| `body` | Rich Text | |

### Autor (2 Stück)

| Feld | Typ |
|---|---|
| `name` | Text |
| `role` | Text |
| `avatar` | Bild |

Der Typ existiert aus genau einem Grund: **in jedem System einmal eine Relation bauen.**
TYPO3 löst das anders als WordPress und anders als Astro — das ist der Lerninhalt.

---

## Startseiten-Sektionen (fixe Reihenfolge)

1. **Hero**
2. **Leistungs-Grid** — 3× `featured`
3. **Text/Bild mit Umschalter links/rechts** ← Vergleichsanker
4. **Zitat**
5. **CTA-Band**
6. **3 neueste Blogposts**

> **Sektion 3 ist der Vergleichsanker.**
> TYPO3 = eigenes Content-Element (Fluid + TCA/Content Blocks) ·
> WordPress = eigener Block (`block.json` + Editor-UI) ·
> Astro = `.astro`-Komponente mit `align`-Prop.
> Dreimal dasselbe sichtbare Ergebnis, drei völlig verschiedene Wege.

---

## Design-Tokens

Einmal festgelegt, dreimal getippt. Ohne identische Tokens driften die Sites optisch
auseinander und der Vergleich verliert seinen Wert.

```
Farben
  ink      #1A1614
  paper    #FDFBF7
  pumpkin  #E8590C
  muted    #6B625C
  line     #E5DED5

Typografie
  Headings  Serif
  Body      System-Stack
  Größen    fluid via clamp()

Spacing
  4  8  16  24  40  64  96

Layout
  contentSize  44rem
  wideSize     72rem
  Radius       4px / 16px
```

Umsetzung pro System — auch das ist Teil des Vergleichs:

| System | Tokens leben in |
|---|---|
| TYPO3 | SCSS-Map |
| WordPress | `theme.json` Presets |
| Astro | CSS Custom Properties |

---

## Bewusst nicht Teil der Spec

Kein Tailwind, kein UI-Framework, kein Headless-Setup, keine Mehrsprachigkeit, kein Shop.
Handgeschriebenes CSS in allen drei Projekten — alles andere würde die Systeme
unvergleichbar machen.
