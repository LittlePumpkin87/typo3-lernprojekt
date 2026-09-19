# Design decisions — TYPO3 build

Why this repository looks the way it does. Decisions that apply to all three builds live in
[SPEC.md](SPEC.md); this file covers the TYPO3 side only.

New decisions are recorded in the closing comment of the issue they belong to and labelled
`decision`. `is:issue is:closed label:decision` lists them. The ones worth keeping are
summarised here.

---

## Site Sets instead of template records

**Decision:** The sitepackage ships its TypoScript through a v13 **site set**
(`Configuration/Sets/SitePackage/config.yaml`), activated from
`config/sites/lernprojekt/config.yaml` via `dependencies`.

**Considered instead:** The classic route — a template record on the root page, editable in
the backend, with TypoScript pasted into a textarea.

**Why:** A template record lives in the database. It is invisible to Git, it does not travel
with a clone, and a change to it leaves no trace in the history. With a site set the whole
configuration is a file. `git log` answers what changed and when.

**Consequence:** Nothing about the rendering configuration can be fixed "quickly in the
backend". Every change goes through the editor, a commit, and `ddev typo3 cache:flush`.
That is the intended trade.

---

## Composer distribution, not an unpacked release

**Decision:** TYPO3 is installed as a Composer project.

**Why:** Core and extension versions are pinned in `composer.lock` and reproducible from a
fresh clone. The alternative — downloading a release and committing the whole core — puts
tens of thousands of foreign files under version control and makes updates a manual diff.

**Consequence:** `ddev composer install` is a required step after cloning. The core is not
in the repository.

---

## No generator, no boilerplate kit

**Decision:** The sitepackage is written by hand. No sitepackage builder, no
`bootstrap_package`, no starter theme.

**Why:** This is a learning project. A generator produces a working result while leaving
every question it answered invisible — which is precisely the part worth learning. A
sitepackage is small enough to write out in full.

**Consequence:** Progress is slower and the early commits are unglamorous. Accepted.

---

## Content lives in the database, not in the repository

**Decision:** Page content ships as `db/seed.sql.gz` and is imported with
`ddev import-db`. The repository tracks the sitepackage and the environment.

**Why:** In TYPO3, content is database rows, not files. Exporting it into the repository
would mean maintaining a second, artificial representation that drifts from the real one.
A dump is honest about what it is.

**Consequence:** The seed has to be re-exported when the demo content changes materially.
Content and code can fall out of sync between commits; the journal notes when a fresh dump
is needed.

---

## Local only, no hosting

**Decision:** The site runs on DDEV and is never deployed. Evidence for the portfolio comes
from the public repository, README screenshots, and `ddev share` when a live look is needed.

**Considered instead:** A small VPS, or the Synology NAS that already carries the portfolio.

**Why:** A permanently hosted CMS means updates, backups and security patches. None of that
adds anything to the learning goal here, and an unpatched CMS on the open internet is a
real risk, not a theoretical one. The NAS is also out of RAM.

**Consequence:** No live URL in the README. This is the same decision as in the WordPress
build; the Astro build deploys to GitHub Pages, because a static site has none of these
problems.
