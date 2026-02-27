# Embedding a Quiz in Canvas

## Option 1: Use Canvas's Embed dialog (simplest)

1. Edit a Canvas Page.
2. In the Rich Content Editor toolbar: **Insert → Media → URL**
   *(wording varies by Canvas version — look for "Embed" or "Media" in the toolbar)*
3. Paste your quiz URL:
   ```
   https://[ORG].github.io/[REPO]/canvas-quiz/quiz.html?quiz=questions/[path].csv
   ```
4. Set dimensions: width `100%`, height `600`.
5. Save, then use **Student View** to preview.

If that option isn't available in your toolbar, use Option 2.

---

## Option 2: Paste HTML directly

1. Edit a Canvas Page.
2. Click the **`</>`** (HTML Editor) button in the toolbar.
   *(In newer Canvas: click the three-dot menu → "Switch to HTML editor")*
3. Find where you want the quiz in the HTML and paste:

```html
<iframe
  src="https://[ORG].github.io/[REPO]/canvas-quiz/quiz.html?quiz=questions/[path].csv"
  width="100%"
  height="600"
  style="border: none;"
  title="[Your Quiz Title — describe it for screen readers]"
  allowfullscreen>
</iframe>
```

4. Replace the `src` URL with your actual quiz URL.
5. Replace the `title` attribute with a descriptive label (e.g., `"Cell Biology Check — Week 3"`).
6. Switch back to the visual editor to confirm it looks right.
7. Save, then preview with **Student View**.

---

## Adjusting height

600px works for most 2–4 question quizzes. Adjust as needed:

| Quiz length | Recommended height |
|---|---|
| Short quiz (2 questions) | `500` |
| Standard (3–4 questions) | `600`–`700` |
| Longer quiz (5+ questions) | `800`+ |

Preview in Student View to confirm nothing is cut off at the bottom.

---

## Checking it works

After publishing, use Canvas **Student View** to:

- Confirm the quiz loads inside the page (not a blank box)
- Interact with all questions and click **Check My Answers**
- Verify feedback highlights appear correctly
- Confirm the **Try Again** button resets the quiz

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Blank white box appears | Your institution may block iframes from external domains. Contact your Canvas admin to allowlist your GitHub Pages domain (e.g., `https://myuniversity.github.io`). |
| "Refused to connect" in browser DevTools | Same cause — Content Security Policy block. Ask your Canvas admin to add the GitHub Pages domain to Canvas Admin → Security → Allowed Domains. |
| Quiz is cut off at the bottom | Increase the `height` value in the iframe tag. |
| Quiz doesn't scroll inside the iframe | Increase `height` further, or add `overflow: auto;` to the iframe's `style` attribute. |
| Quiz loads in a new tab instead of inline | Remove `target="_blank"` if present, or try Option 2 (raw iframe HTML) instead of the Canvas embed dialog. |

### Note on Canvas iframe restrictions

Some Canvas instances block iframes pointing to external domains. If you run into this:

1. Ask your Canvas administrator to allowlist your GitHub Pages domain in **Canvas Admin → Security → Allowed Domains**.
2. Alternatively, share the quiz as a plain hyperlink — students click it and the quiz opens in a new tab. This works in any Canvas instance without any admin changes.
