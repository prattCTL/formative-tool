# Faculty Guide

## What this tool does

Students visit a URL, answer 2–4 questions, click **Submit Answers**, and instantly see color-coded feedback with explanations. They can click **Try Again** as many times as they like. No login, no data collection, no servers.

You control the questions entirely through CSV files stored in this GitHub repository.

---

## One-time setup (done once per course or department)

1. **Fork or copy this repository** to your own GitHub account (or ask your IT/instructional design team to set it up).
2. In the repo's **Settings → Pages**, set the source branch to `main` and folder to `/ (root)`.
3. GitHub will give you a URL like `https://yourusername.github.io/repo-name/`. Save it.
4. That's it — the tool is live.

---

## Adding a new quiz

### Option A — Edit directly on GitHub (no software needed)

1. Go to your repository on GitHub.com.
2. Click **Add file → Create new file**.
3. Type the path in the filename box:
   `questions/week3/plant-cells.csv`
   (GitHub creates folders automatically when you include `/` in the name.)
4. Paste the header row, then add your question rows (see `docs/CSV_FORMAT.md`).
5. Click **Commit changes** at the bottom.
6. Wait about 60 seconds for GitHub Pages to rebuild.
7. Your quiz URL is:
   `https://yourusername.github.io/repo-name/quiz.html?quiz=questions/week3/plant-cells.csv`

### Option B — Upload a CSV you prepared locally

1. Create your CSV in Excel, Google Sheets, or a text editor.
   - In Excel/Sheets: **File → Download → CSV**.
   - Make sure the first row is the exact header row from `docs/CSV_FORMAT.md`.
2. On GitHub, navigate to the `questions/` folder.
3. Click **Add file → Upload files**.
4. Drag your CSV in, commit.

---

## Editing an existing quiz

1. Navigate to the CSV file on GitHub.
2. Click the **pencil icon** (Edit this file).
3. Make your changes.
4. Click **Commit changes**.

---

## Sharing with students

Post the quiz URL in Canvas. The easiest approach is to paste it as a link in a Page, Assignment, or Discussion:

```
https://yourusername.github.io/repo-name/quiz.html?quiz=questions/week3/plant-cells.csv
```

For an embedded iframe experience, see `docs/EMBED_INSTRUCTIONS.md`.

---

## Testing your quiz before sharing

You need a local server to test (browsers block `fetch()` on `file://` URLs).

**Quick option — Python (built into macOS and most Linux):**
```bash
cd /path/to/your/repo
python3 -m http.server 8080
```
Then open: `http://localhost:8080/quiz.html?quiz=questions/example/sample-quiz.csv`

**Quick option — Node.js:**
```bash
npx serve .
```
Then open the URL it prints, adding `?quiz=...`.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| "No quiz specified" message | URL is missing `?quiz=...` | Add the `?quiz=path/to/file.csv` parameter |
| "Quiz file not found" | Path in URL doesn't match the file location | Check spelling and folder names — they are case-sensitive |
| Quiz loads but question is missing | That row has a validation error | Open browser DevTools (F12) → Console to see the specific error |
| Blank appears as literal text `{{blank}}` | Typo in the placeholder | Verify it is exactly `{{blank}}` with double curly braces |
| Options display out of order | `shuffle_options` is `TRUE` | Normal behavior — set to `FALSE` to fix the order |
| Changes not showing | GitHub Pages hasn't rebuilt yet | Wait 1–2 minutes and hard-refresh (Ctrl+Shift+R) |
