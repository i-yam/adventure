# Adventure Capitalism

A twelve-class entrepreneurship course, hosted as a plain static site on GitHub Pages. Students build a startup idea across the term and pitch it three times.

Read [`CLAUDE.md`](CLAUDE.md) before writing or editing any page. It holds the voice, the syllabus, the reading map, and the house HTML style. A page that gets the facts right and the voice wrong gets rewritten.

## Layout

One folder per class. Each class folder holds an `index.html`, so the public URL has no `.html` tail (`/class-01/` instead of `/class-01.html`). One shared `style.css` at the root is the single source of truth for the look; every page links it and defines no tokens inline.

```
.
├── index.html          course landing / index
├── style.css           the one shared stylesheet (source of truth)
├── _template.html      copy-to-start skeleton for a new class
├── CLAUDE.md           authoring rules — read first
├── README.md
├── .nojekyll           serve files as-is (see note below)
├── .gitignore
├── assets/             shared, cross-class files only (favicon, og-image, logo)
├── class-01/
│   └── index.html
├── class-02/
│   └── index.html
├── ...
└── class-12/
    └── index.html
```

Pitch days are `class-04`, `class-08`, `class-12`. They use the same page shape with `type=pitch` in the tags and `PITCH · SHARK TANK` in the kicker, and they carry no reading block.

### Naming

Class folders are zero-padded and hyphenated: `class-01` through `class-12`. The padding keeps them sorting in order everywhere (editor, git, GitHub), and it matches the numbering used throughout `CLAUDE.md`. Do not use `class1`, `class10`, and so on.

### Paths

A class page sits one level down, so it reaches up for anything shared:

- Stylesheet: `href="../style.css"`
- Course index: `href="../index.html"`
- Next class: `href="../class-05/"`
- Shared asset: `src="../assets/favicon.svg"`
- This class's own worksheet: `href="worksheet.pdf"` (same folder, no `../`)

The root `index.html` links classes without the `../`: `href="class-01/"`.

## Run it locally

No build step. Serve the folder with anything static:

```
python3 -m http.server 8000
```

Then open <http://localhost:8000/>. Opening `class-01/index.html` directly with `file://` also works, since fonts and the stylesheet load over relative and absolute URLs that resolve fine.

## Deploy

GitHub → repo **Settings → Pages** → Source: **Deploy from a branch**, Branch: `main`, Folder: `/ (root)`. GitHub serves the static files directly.

The `.nojekyll` file at the root turns off Jekyll. Without it, GitHub Pages would ignore anything starting with an underscore (so `_template.html` would 404) and could reprocess the site. It is safe to keep on a hand-written static site.

## Add a class

1. Copy `_template.html` into a new `class-NN/` folder as `index.html`.
2. Fill in the number, kicker, headline, tag rail, and the `meta ac:tags` line. Keep the two tag sources in sync.
3. Write the body and the work block. Mark the activity `[ NO AI ]` or `[ AI OK ]` and say why.
4. Add the one reading-block essay from the reading map in `CLAUDE.md` (build classes only; pitch days get none).
5. Wire the footer: previous and next class as `../class-NN/`.
6. Add the class to the list in the root `index.html`.
7. Run the HTML check at the foot of `CLAUDE.md` before you ship.

Never ship a page with `NN` or `...` placeholders still in it.

## Status of the pages

The twelve class pages were scaffolded from the syllabus: metadata, tags, reading links, and navigation are complete and correct. The body prose is a first draft in the house voice, meant as a running start for a human author to expand into the full lesson, not a finished class. `index.html`, `style.css`, and `_template.html` are ready to use as-is.
