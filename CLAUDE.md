# typo3-lernprojekt

**Lernprojekt, keine Produktivsite.** Baut dieselbe Site wie `astro-lernprojekt` und
`wp-lernprojekt` — Spezifikation in [docs/SPEC.md](docs/SPEC.md), eingefroren.

## Stack

TYPO3 **v13.4** (Composer-Distribution) · DDEV · apache-fpm · PHP 8.4 · MariaDB 11.8 ·
Docroot `public` · Sitepackage in `packages/sitepackage` (Extension-Key `sitepackage`,
Site Set `littlepumpkin/lernprojekt`).

## Startbefehl

```bash
ddev start
ddev launch
ddev launch typo3
ddev typo3 cache:flush
```

DB-Wiederherstellung nach einem Container-Unfall: `ddev import-db --file=db/seed.sql.gz`.

## Arbeitsweise

- **Jennifer schreibt allen Projektcode selbst** (TypoScript, Fluid, PHP, SCSS).
- **Erklären, nicht diktieren.** Konzept, Zusammenhang und das Warum erklären; keine
  fertigen Code-Blöcke zum Abtippen, keine Zeile-für-Zeile-Ansage. Sie setzt es selbst um,
  ich reviewe hinterher und gebe Feedback.
- Doku- und Config-Dateien (`SPEC.md`, `CLAUDE.md`, `.gitignore`, `.code-workspace`)
  schreibe ich. **`docs/JOURNAL.md` schreibt Jennifer selbst** — das ist Retrieval Practice.
- **Vor jeder Session die letzten zwei Einträge in [docs/JOURNAL.md](docs/JOURNAL.md) lesen.**
  Die Zeilen `NÄCHSTER SCHRITT` und `Startbefehl` sind der Wiedereinstieg.
- **Git macht Jennifer selbst** — ich führe kein `commit`/`push` aus, auch nicht am
  Session-Ende. Lesende Befehle (`status`, `log`, `diff`) sind okay.
- Eine Session gilt nur als fertig mit: sichtbarem Ergebnis im Browser + JOURNAL-Eintrag +
  Commit. Vor dem Commit `ddev export-db --gzip --file=db/seed.sql.gz` — Inhalte leben in
  der DB, nicht im Repo.
