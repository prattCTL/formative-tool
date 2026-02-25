# Embedding in Canvas

There are two ways to get the quiz into Canvas. Both result in the quiz appearing inline on the page — no new tab required.

---

## Method 1 — External Tool / Redirect (simplest)

1. In your Canvas course, go to the module where you want the quiz.
2. Click **+** → **External URL**.
3. Paste your quiz URL:
   ```
   https://yourusername.github.io/repo-name/quiz.html?quiz=questions/week3/plant-cells.csv
   ```
4. Check **Load in a new tab** *or* leave it unchecked for inline embedding (behavior depends on your Canvas instance settings).
5. Save.

---

## Method 2 — HTML `<iframe>` in a Canvas Page (recommended for inline display)

This gives you full control over the embed and works in any Canvas instance.

### Step-by-step

1. Open or create a **Canvas Page** (Pages → + Page).
2. In the Rich Content Editor toolbar, click the `</>` (HTML editor) button
   *(in newer Canvas versions: click the three-dot menu → "Switch to HTML editor")*.
3. Paste this code, replacing the `src` URL with your quiz URL:

```html
<iframe
  src="https://yourusername.github.io/repo-name/quiz.html?quiz=questions/week3/plant-cells.csv"
  width="100%"
  height="600"
  style="border:none; border-radius:8px;"
  title="Formative Assessment"
  allowfullscreen>
</iframe>
```

4. Switch back to the visual editor to preview, then **Save**.

### Adjusting the height

- Most 3-question quizzes display well at `height="600"`.
- For 4 questions or long feedback text, try `height="750"` or `height="900"`.
- You can also set `height="800px"` in the `style` attribute instead of the `height` attribute — either works.

---

## Troubleshooting embeds

| Problem | Fix |
|---|---|
| Quiz shows a blank white box | Your institution may block iframes from external domains. Contact your Canvas admin to allowlist your GitHub Pages domain. |
| "Refused to connect" error in DevTools | Same as above — CSP/X-Frame-Options block. See note below. |
| Iframe too short, quiz is cut off | Increase the `height` value. |
| Quiz doesn't scroll inside iframe | Add `overflow: auto` to the iframe's style, or increase height. |

### Note on Canvas iframe restrictions

Some Canvas instances (especially those using strict Content Security Policies) may block iframes pointing to external domains. If your institution has this restriction, ask your Canvas administrator to add your GitHub Pages domain (`https://yourusername.github.io`) to the **Allowed Domains** list in Canvas Admin → Security.

Alternatively, you can host the repo under a custom domain (GitHub Pages supports this) and request that domain be allowlisted.

---

## Sharing as a direct link (no iframe)

If embedding is blocked, you can still share the quiz as a plain hyperlink in Canvas:

1. Open an Assignment, Discussion, or Announcement.
2. Highlight link text (e.g., "Click here for the Cell Biology Check").
3. Click the link icon and paste your quiz URL.

Students click the link and the quiz opens in a new tab.
