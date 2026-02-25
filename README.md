# Canvas Formative Assessment Tool

A zero-server, zero-build quiz tool for Canvas LMS, hosted on GitHub Pages.
Faculty add questions by editing CSV files directly on GitHub. Students get instant, color-coded feedback with unlimited retries.

---

## How it works

```
quiz.html?quiz=questions/your-topic/your-quiz.csv
```

The single `quiz.html` file fetches any CSV at runtime and renders an interactive formative activity. No backend, no accounts, no build step.

**Supported question types:**

| Type | Student experience |
|---|---|
| Multiple Choice | Click a radio button; one correct answer |
| Fill in the Blank | Type into an inline blank; multiple accepted spellings |
| Drag to Reorder | Drag items into the correct sequence |

---

## One-time setup

1. **Fork this repository** (or have IT create it from this template).
2. Go to **Settings → Pages**, set source to `main` branch, root folder.
3. GitHub will publish the tool at:
   ```
   https://<your-username>.github.io/<repo-name>/
   ```
4. Done — share quiz URLs with students.

---

## Adding questions

1. Create or upload a `.csv` file in the `questions/` folder.
2. Use the header row from [`docs/CSV_FORMAT.md`](docs/CSV_FORMAT.md).
3. Commit to `main`.
4. Share the URL:
   ```
   https://<your-username>.github.io/<repo-name>/quiz.html?quiz=questions/your-file.csv
   ```

See [`questions/README.md`](questions/README.md) for a quick-start guide.

---

## Embedding in Canvas

Paste an `<iframe>` tag into any Canvas Page's HTML editor:

```html
<iframe
  src="https://<your-username>.github.io/<repo-name>/quiz.html?quiz=questions/your-file.csv"
  width="100%"
  height="600"
  style="border:none;"
  title="Formative Assessment">
</iframe>
```

Full instructions: [`docs/EMBED_INSTRUCTIONS.md`](docs/EMBED_INSTRUCTIONS.md)

---

## Repository structure

```
canvas-quiz/
├── quiz.html                        ← single-file quiz app (all HTML/CSS/JS)
├── questions/
│   ├── README.md                    ← how to add questions
│   └── example/
│       ├── sample-quiz.csv          ← one of each question type
│       └── multichoice-only.csv     ← three MultiChoice questions
├── docs/
│   ├── CSV_FORMAT.md                ← every column explained
│   ├── FACULTY_GUIDE.md             ← step-by-step faculty instructions
│   └── EMBED_INSTRUCTIONS.md        ← Canvas iframe guide
└── README.md                        ← this file
```

---

## Local development / testing

Browsers block `fetch()` on `file://` URLs, so you need a local server:

```bash
# Python (no install needed on macOS/Linux)
python3 -m http.server 8080

# Node.js
npx serve .
```

Then open:
```
http://localhost:8080/quiz.html?quiz=questions/example/sample-quiz.csv
```

---

## Documentation

- [`docs/CSV_FORMAT.md`](docs/CSV_FORMAT.md) — complete column-by-column reference
- [`docs/FACULTY_GUIDE.md`](docs/FACULTY_GUIDE.md) — authoring walkthrough and troubleshooting
- [`docs/EMBED_INSTRUCTIONS.md`](docs/EMBED_INSTRUCTIONS.md) — Canvas embedding instructions
