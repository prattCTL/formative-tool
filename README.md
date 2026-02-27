# Canvas Formative Assessment Tool

Interactive formative quiz activities for Canvas LMS, hosted on GitHub Pages.
No servers. No accounts for students. No build steps.

## How it works

1. A faculty member adds a CSV file to the `questions/` folder
2. The quiz URL is:
   ```
   https://[ORG].github.io/[REPO]/canvas-quiz/quiz.html?quiz=questions/path/file.csv
   ```
3. That URL is embedded in a Canvas Page as an iframe
4. Students open the Page and take the quiz

## Question types

- **Multiple Choice** (2–4 options)
- **Fill in the Blank** (single or multiple blanks, typo-tolerant matching)
- **Drag/Drop Ordering**

## One-time admin setup

1. Fork or clone this repo into your institution's GitHub organization
2. **Settings → Pages → Source:** Deploy from branch → Branch: `main` → `/` (root) → Save
3. Wait ~60 seconds, then test:
   ```
   https://[ORG].github.io/[REPO]/canvas-quiz/quiz.html?quiz=questions/example/sample-quiz.csv
   ```
4. Share `docs/FACULTY_GUIDE.md` with faculty who want to add quizzes

## Repository structure

```
canvas-quiz/
└── quiz.html                  ← single-file quiz app (all HTML/CSS/JS)
docs/
├── CSV_FORMAT.md              ← complete column reference with examples
├── FACULTY_GUIDE.md           ← step-by-step guide for faculty
└── EMBED_INSTRUCTIONS.md      ← how to embed in a Canvas Page
questions/
├── README.md                  ← folder conventions and quick-start
└── example/
    ├── sample-quiz.csv        ← one of each question type
    └── multichoice-only.csv   ← three MultiChoice questions
README.md                      ← this file
```

## Local development

Browsers block `fetch()` on `file://` URLs, so you need a local server:

```bash
# Python (built into macOS/Linux)
python3 -m http.server 8080

# Node.js
npx serve .
```

Then open:
```
http://localhost:8080/canvas-quiz/quiz.html?quiz=questions/example/sample-quiz.csv
```

## Privacy

- No student data is collected or stored anywhere outside the student's browser
- Answers live in `sessionStorage` only — cleared when the browser tab closes
- No analytics, no tracking, no login required for students
- Do not put student names or any identifying information in CSV files

## Documentation

| File | Purpose |
|------|---------|
| [`docs/CSV_FORMAT.md`](docs/CSV_FORMAT.md) | Every column explained with complete examples |
| [`docs/FACULTY_GUIDE.md`](docs/FACULTY_GUIDE.md) | Adding questions and sharing quiz URLs |
| [`docs/EMBED_INSTRUCTIONS.md`](docs/EMBED_INSTRUCTIONS.md) | Embedding in a Canvas Page |
| [`questions/README.md`](questions/README.md) | Folder and file naming conventions |
