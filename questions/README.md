# Adding Your Questions

Each CSV file in this folder is one quiz. Students see it by visiting:

```
https://<your-github-username>.github.io/<repo-name>/quiz.html?quiz=questions/your-file.csv
```

## Quick start

1. Click **Add file → Create new file** in GitHub.
2. Name it `questions/my-topic/my-quiz.csv` (create subfolders freely).
3. Paste the header row, then add one row per question.
4. Commit directly to `main`.
5. Wait ~60 seconds for GitHub Pages to rebuild, then share the URL.

## Header row (copy this exactly)

```
type,question_id,set_title,set_description,question_text,option_a,option_b,option_c,option_d,correct_option,accepted_answers,items,correct_order,feedback_correct,feedback_incorrect,hint,case_sensitive,partial_credit,shuffle_options
```

## Supported question types

| `type` value | What it does |
|---|---|
| `MultiChoice` | Radio-button question with up to 4 options |
| `FillBlank` | Student types into an inline blank; use `{{blank}}` in the question text |
| `DragDrop` | Student drags items into the correct order |

## Working examples

- `questions/example/sample-quiz.csv` — one of each type
- `questions/example/multichoice-only.csv` — three MultiChoice questions

## Full authoring reference

See [`docs/CSV_FORMAT.md`](../docs/CSV_FORMAT.md) for every column explained in detail.
