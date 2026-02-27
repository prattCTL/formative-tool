# Faculty Guide: Adding a Quiz to Your Canvas Course

## What students experience

Students see all questions grouped together with one **Check My Answers** button.
Correct answers highlight green with a checkmark; incorrect answers highlight red with an explanation.
Students can retry as many times as they like.
Their answers reset when they close the browser tab — nothing is saved or submitted to a grade book.

---

## Step 1: Add your questions (creating a CSV file)

### Option A: Edit using GitHub's web interface (recommended — no software needed)

1. Go to the repository on GitHub.
2. Navigate to the `questions/` folder → your department folder.
   (To create one: click **Add file → Create new file**, name it `foldername/.gitkeep`, and commit.)
3. Click **Add file → Create new file**.
4. Name the file: `coursename-quiztopic.csv`
   (use hyphens, no spaces, must end in `.csv` — for example, `bio101-cell-division.csv`)
5. Paste the header row, then add your question rows beneath it.
6. Refer to [`docs/CSV_FORMAT.md`](CSV_FORMAT.md) for the exact column format and examples.
7. Click **Commit changes → Commit directly to main**.

### Option B: Edit in Excel or Google Sheets

1. Download `questions/example/sample-quiz.csv` from the repository.
2. Open it in Excel or Google Sheets. Keep row 1 (the header row) exactly as-is.
3. Replace the example rows with your own questions.
4. Export as CSV — not `.xlsx`.
   - Excel: **File → Save As → CSV (Comma delimited)**
   - Google Sheets: **File → Download → Comma-separated values (.csv)**
5. On GitHub, navigate to `questions/[your-folder]/`.
6. Click **Add file → Upload files**, drag in your CSV, and commit.

---

## Step 2: Get your quiz URL

Your quiz URL follows this pattern:

```
https://[ORG].github.io/[REPO]/canvas-quiz/quiz.html?quiz=questions/[folder]/[filename].csv
```

Example:

```
https://myuniversity.github.io/canvas-quiz/canvas-quiz/quiz.html?quiz=questions/biology/bio101-week3.csv
```

Test this URL in your browser before embedding. The quiz should load and all questions should appear.

---

## Step 3: Embed in Canvas

See [`docs/EMBED_INSTRUCTIONS.md`](EMBED_INSTRUCTIONS.md) for exact steps.

---

## Updating your questions

1. Navigate to the CSV file on GitHub.
2. Click the **pencil icon** (Edit this file).
3. Make your changes.
4. Click **Commit changes**.

Changes are live within about 60 seconds — no cache to clear on the student side.

---

## Troubleshooting

| Problem | Solution |
|---------|---------|
| "Quiz file not found" | Check that the `?quiz=` path in your URL matches the actual file path exactly. Paths are case-sensitive. |
| Questions don't appear | Check your CSV for formatting errors — see [CSV_FORMAT.md Common Mistakes](CSV_FORMAT.md#common-mistakes). |
| A validation error message is shown | The error names the `question_id` — find and fix that row in your CSV. |
| `correct_order` error | Items in `correct_order` must exactly match the spelling in the `items` column. |
| Quiz is cut off in Canvas | Increase the iframe `height` value — see [EMBED_INSTRUCTIONS.md](EMBED_INSTRUCTIONS.md). |
| Changes not showing after commit | GitHub Pages rebuilds in about 60 seconds. Hard-refresh with Ctrl+Shift+R (or Cmd+Shift+R on Mac). |
