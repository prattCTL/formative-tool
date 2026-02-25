# CSV Format Reference

One CSV file = one question set. All question types can coexist in the same file.
Row 1 is always the **header row** — copy it exactly.

## Header row

```
type,question_id,set_title,set_description,question_text,option_a,option_b,option_c,option_d,correct_option,accepted_answers,items,correct_order,feedback_correct,feedback_incorrect,hint,case_sensitive,partial_credit,shuffle_options
```

---

## Column reference

### `type` *(required)*

Exactly one of:

| Value | Question style |
|---|---|
| `MultiChoice` | Radio-button; up to 4 lettered options |
| `FillBlank` | Inline text input(s) embedded in the question sentence |
| `DragDrop` | Draggable list the student reorders |

All rows in a file must share the same `set_title` and `set_description` — only the **first data row** is read for those fields.

---

### `question_id` *(required)*

Unique identifier within the file. Recommended prefixes:

- `MC-001`, `MC-002` … for MultiChoice
- `FB-001`, `FB-002` … for FillBlank
- `DD-001`, `DD-002` … for DragDrop

---

### `set_title` *(required on first row)*

Display title shown at the top of the quiz. Only the first data row's value is used.

### `set_description` *(optional, first row only)*

Short subtitle shown below the title. Leave blank if not needed.

---

### `question_text` *(required)*

The question prompt shown to students.

- For **FillBlank**: use `{{blank}}` as a placeholder for each blank.
  Example: `The powerhouse of the cell is the {{blank}}.`
  Multiple blanks: `{{blank}} and {{blank}} are both organelles.`

---

### `option_a`, `option_b`, `option_c`, `option_d`

**MultiChoice only.** At least `option_a` and `option_b` are required; `option_c` and `option_d` are optional. Leave all four empty for FillBlank and DragDrop rows.

---

### `correct_option`

**MultiChoice only.** Must be exactly `A`, `B`, `C`, or `D`, matching an option that has text.

---

### `accepted_answers`

**FillBlank only.** Pipe-delimited list of accepted spellings/synonyms per blank.

**Single blank:**
```
mitochondria|mitochondrion|the mitochondria
```

**Multiple blanks** — separate groups with semicolons, answers within a group with pipes:
```
carbon dioxide|CO2;water|H2O
```

Leave empty for MultiChoice and DragDrop rows.

---

### `items`

**DragDrop only.** Pipe-delimited list of items shown to students in the *display* order (intentionally scrambled).

```
Anaphase|Prophase|Telophase|Metaphase
```

---

### `correct_order`

**DragDrop only.** Pipe-delimited list of the **same items** in correct sequence.

```
Prophase|Metaphase|Anaphase|Telophase
```

`items` and `correct_order` must contain identical elements — the quiz will show an error if they differ.

---

### `feedback_correct` *(optional)*

Text shown when the student answers correctly. Defaults to `Correct!`

### `feedback_incorrect` *(optional)*

Text shown when the student answers incorrectly. Defaults to `Review this topic and try again.`

---

### `hint` *(optional, FillBlank only)*

Shown below the question after any incorrect submission. Leave empty to show no hint.

---

### `case_sensitive` *(optional, FillBlank only)*

`TRUE` or `FALSE`. Defaults to `FALSE` (case-insensitive matching).

---

### `partial_credit` *(optional, FillBlank only)*

`TRUE` or `FALSE`. Applies when there are multiple blanks.

- `TRUE` — each blank is scored independently; partial feedback is shown.
- `FALSE` — all blanks must be correct for the question to count as correct.

Defaults to `FALSE`.

---

### `shuffle_options` *(optional, MultiChoice only)*

`TRUE` or `FALSE`. If `TRUE`, option display order is randomized each load. Defaults to `FALSE`.

---

## Tips

- Wrap any field containing commas or quotation marks in double quotes:
  `"Smith, John"` or `"She said ""hello"""`
- Keep each CSV to 2–4 questions for the best student experience.
- You can have as many CSV files as you like — each maps to a unique quiz URL.
- Test your CSV locally before sharing with students (see `docs/FACULTY_GUIDE.md`).
