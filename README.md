# typo3-lernprojekt

TYPO3 v13 Sitepackage, von Grund auf gebaut — ohne Generator, ohne Boilerplate-Kit.

Dies ist eines von **drei Lernprojekten**, die dieselbe fiktive Agentur-Website
„Pumpkin Studio" umsetzen: einmal in TYPO3, einmal als WordPress-Block-Theme, einmal in
Astro. Gleiche Seiten, gleiche Inhaltstypen, gleiche Design-Tokens — drei völlig
verschiedene Wege dorthin. Die gemeinsame, eingefrorene Spezifikation liegt in
[docs/SPEC.md](docs/SPEC.md).

| Repo | System |
|---|---|
| [typo3-lernprojekt](https://github.com/LittlePumpkin87/typo3-lernprojekt) | TYPO3 v13.4 |
| [wp-lernprojekt](https://github.com/LittlePumpkin87/wp-lernprojekt) | WordPress Block-Theme (FSE) |
| [astro-lernprojekt](https://github.com/LittlePumpkin87/astro-lernprojekt) | Astro (SSG) |

Der Systemvergleich wird fortlaufend in
[docs/COMPARE.md](https://github.com/LittlePumpkin87/astro-lernprojekt/blob/main/docs/COMPARE.md)
gesammelt.

## Stack

TYPO3 **13.4** (Composer-Distribution) · DDEV · Apache + PHP 8.4 · MariaDB 11.8 ·
Docroot `public`

## Was hier drin steckt

Das Sitepackage nutzt konsequent die **v13-Site-Sets** statt der alten
Template-Datensätze im Backend — die gesamte Konfiguration liegt damit im Code und in Git:

```
packages/sitepackage/
├── composer.json                                  Extension-Key "sitepackage"
├── Configuration/Sets/SitePackage/
│   ├── config.yaml                                Set "littlepumpkin/lernprojekt"
│   └── setup.typoscript                           page = PAGE → FLUIDTEMPLATE,
│                                                  menu-DataProcessor, lib.mainContent
└── Resources/Private/
    ├── Layouts/Default.html                       Seitengeruest, Navigation, Footer
    └── Templates/Default.html                     Content-Bereich

config/sites/lernprojekt/config.yaml               base, rootPageId, dependencies → Set
```

Der Weg eines Requests: Site-Config löst Domain und Seite auf → das per `dependencies`
aktivierte Site Set bringt sein TypoScript mit → `page = PAGE` rendert ein FLUIDTEMPLATE →
DataProcessor und `CONTENT` stellen Navigation und Seiteninhalte bereit → Fluid setzt
Layout und Template zusammen.

## Lokal starten

Voraussetzung: [DDEV](https://ddev.readthedocs.io/) und Docker.

```bash
git clone git@github.com:LittlePumpkin87/typo3-lernprojekt.git
cd typo3-lernprojekt
ddev start
ddev composer install
ddev import-db --file=db/seed.sql.gz   # Seiteninhalte — die leben in der DB, nicht im Repo
ddev launch                            # Frontend
ddev launch typo3                      # Backend
```

Nach jeder Änderung an TypoScript oder YAML: `ddev typo3 cache:flush`.

## Stand

- **S1** — Projektaufsetzung, Site-Konfiguration, Sitepackage als Site Set, Fluid-Grundgerüst.
  Frontend rendert Navigation und Content-Elemente end-to-end.
- **S2** — Projekt-Infrastruktur: eingefrorene Spec, Journal, DB-Seed.
- **Als Nächstes** — Header, Navigation und Footer in Fluid-Partials auslagern, weitere
  ViewHelper, danach das Text/Bild-Content-Element als Vergleichsanker zu den anderen
  zwei Systemen.

Die Site läuft bewusst nur lokal — ein dauerhaft gehostetes CMS bedeutet Updates,
Backups und Security-Patches ohne zusätzlichen Lerngewinn.

<!-- Screenshots von Frontend und Backend hier einfügen, sobald das Layout steht. -->
