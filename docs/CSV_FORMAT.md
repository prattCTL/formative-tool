# CSV Format Reference

## Overview

One CSV file = one question set. All rows share the same title and description.
Row 1 is always the **header row** — copy the exact column names below. Do not rename or reorder them.

```
type,question_id,set_title,set_description,question_text,option_a,option_b,option_c,option_d,correct_option,accepted_answers,items,correct_order,feedback_correct,feedback_incorrect,hint,case_sensitive,partial_credit,shuffle_options
```

---

## Column Reference

| Column Name | Used By | Required? | Description | Example |
|---|---|---|---|---|
| `type` | All | **Yes** | Question type. Exactly one of: `MultiChoice`, `FillBlank`, `DragDrop` | `MultiChoice` |
| `question_id` | All | **Yes** | Unique identifier within the file. Recommended prefixes: `MC-`, `FB-`, `DD-` | `MC-001` |
| `set_title` | All | **First row only** | Quiz title shown at the top of the page. Only the first data row's value is used. | `Cell Biology Check` |
| `set_description` | All | No | Short subtitle below the title. Leave blank if not needed. Only the first row's value is used. | `Test your knowledge of cell organelles.` |
| `question_text` | All | **Yes** | The question prompt. For FillBlank, include `{{blank}}` where each input goes. | `Which organelle produces ATP?` |
| `option_a` | MultiChoice | **Yes** | Text for option A | `Nucleus` |
| `option_b` | MultiChoice | **Yes** | Text for option B | `Mitochondria` |
| `option_c` | MultiChoice | No | Text for option C (leave blank for 2-option questions) | `Ribosome` |
| `option_d` | MultiChoice | No | Text for option D (leave blank for 2- or 3-option questions) | `Golgi apparatus` |
| `correct_option` | MultiChoice | **Yes** | Must be exactly `A`, `B`, `C`, or `D`, matching a column that has text | `B` |
| `accepted_answers` | FillBlank | **Yes** | Accepted spellings per blank. Use `\|` between synonyms; use `;` between blanks | `photosynthesis\|photo synthesis` |
| `items` | DragDrop | **Yes** | Pipe-delimited list of items in the scrambled display order students see | `Anaphase\|Prophase\|Telophase\|Metaphase` |
| `correct_order` | DragDrop | **Yes** | The same items in the correct sequence. Must contain identical elements to `items` | `Prophase\|Metaphase\|Anaphase\|Telophase` |
| `feedback_correct` | All | No | Message shown when the student answers correctly. Default: `Correct!` | `Right — mitochondria produce ATP.` |
| `feedback_incorrect` | All | No | Message shown when the student answers incorrectly. Default: `Review this topic and try again.` | `Think about which organelle makes energy.` |
| `hint` | FillBlank | No | Extra hint shown below the question after an incorrect submission. Leave blank to omit. | `Think about what "photo" means in Greek.` |
| `case_sensitive` | FillBlank | No | `TRUE` or `FALSE`. Whether the blank matching is case-sensitive. Default: `FALSE` | `FALSE` |
| `partial_credit` | FillBlank | No | `TRUE` or `FALSE`. When `TRUE`, each blank is scored independently. Only affects multi-blank questions. Default: `FALSE` | `TRUE` |
| `shuffle_options` | MultiChoice | No | `TRUE` or `FALSE`. Randomizes option order on each page load. Default: `FALSE` | `FALSE` |

---

## Question Type Examples

### Multiple Choice

**4-option example**

| Column | Value |
|---|---|
| `type` | `MultiChoice` |
| `question_id` | `MC-001` |
| `set_title` | `Cell Biology Check` |
| `set_description` | `Test your knowledge of cell organelles.` |
| `question_text` | `Which organelle is known as the powerhouse of the cell?` |
| `option_a` | `Nucleus` |
| `option_b` | `Mitochondria` |
| `option_c` | `Ribosome` |
| `option_d` | `Golgi apparatus` |
| `correct_option` | `B` |
| `feedback_correct` | `That's right — mitochondria produce ATP through cellular respiration.` |
| `feedback_incorrect` | `Not quite. Think about which organelle produces energy for the cell.` |
| `shuffle_options` | `TRUE` |

*What students see:* A question with four radio buttons. After submitting, option B highlights green with ✓; any wrong selection highlights red with ✗.

**2-option example**

| Column | Value |
|---|---|
| `type` | `MultiChoice` |
| `question_id` | `MC-002` |
| `question_text` | `Does DNA replication occur in the nucleus?` |
| `option_a` | `Yes` |
| `option_b` | `No` |
| `option_c` | *(leave blank)* |
| `option_d` | *(leave blank)* |
| `correct_option` | `A` |

*What students see:* A true/false-style question with two radio buttons.

---

### Fill in the Blank

**Single blank, one accepted answer**

| Column | Value |
|---|---|
| `type` | `FillBlank` |
| `question_id` | `FB-001` |
| `question_text` | `The powerhouse of the cell is the {{blank}}.` |
| `accepted_answers` | `mitochondria` |
| `case_sensitive` | `FALSE` |

*What students see:* `The powerhouse of the cell is the` _____ `.`
Accepts: `mitochondria`, `Mitochondria`, `MITOCHONDRIA` (case-insensitive). Also accepts close misspellings (`mitocondria`) via fuzzy matching.

---

**Single blank, multiple accepted answers (pipe-delimited)**

| Column | Value |
|---|---|
| `type` | `FillBlank` |
| `question_id` | `FB-002` |
| `question_text` | `Plants convert sunlight to chemical energy through {{blank}}.` |
| `accepted_answers` | `photosynthesis\|photo synthesis\|photosythesis` |
| `hint` | `Think about what "photo" means in Greek.` |

*What students see:* One blank. Any of the three spellings (or a fuzzy match) counts as correct. The hint appears only after an incorrect submission.

---

**Two blanks with partial credit**

| Column | Value |
|---|---|
| `type` | `FillBlank` |
| `question_id` | `FB-003` |
| `question_text` | `Photosynthesis takes in {{blank}} and releases {{blank}}.` |
| `accepted_answers` | `carbon dioxide\|CO2;oxygen\|O2` |
| `partial_credit` | `TRUE` |
| `case_sensitive` | `FALSE` |

*What students see:* Two inline blanks. With `partial_credit TRUE`, getting one blank right shows "(1 of 2 blanks correct)" and both blanks are individually colour-coded.

The semicolon (`;`) separates the answer group for blank 1 from blank 2. The pipe (`|`) separates accepted synonyms within a group.

---

### Drag/Drop Ordering

**4-item example**

| Column | Value |
|---|---|
| `type` | `DragDrop` |
| `question_id` | `DD-001` |
| `question_text` | `Arrange the stages of mitosis in the correct order:` |
| `items` | `Anaphase\|Prophase\|Telophase\|Metaphase` |
| `correct_order` | `Prophase\|Metaphase\|Anaphase\|Telophase` |
| `feedback_correct` | `Perfect! You correctly ordered all four stages of mitosis.` |
| `feedback_incorrect` | `Not quite — review the sequence: Prophase → Metaphase → Anaphase → Telophase.` |

*What students see:* A draggable list showing the items in the scrambled `items` order. After submitting, items in the correct position highlight green; items out of position highlight red. The correct order is shown below.

**`items`** is the scrambled display order — this is what students see first.
**`correct_order`** is the answer — it must contain exactly the same items, just in the right sequence.

---

## Common Mistakes

| Mistake | What happens | Fix |
|---|---|---|
| Using semicolons instead of commas as the CSV delimiter | The file fails to parse; all columns appear as one | Use commas to separate columns. Only use semicolons inside the `accepted_answers` field to separate blank groups. |
| Extra spaces around pipe characters (`a \| b`) | `" b"` doesn't match `"b"` | Write pipes without surrounding spaces: `a\|b` |
| `correct_order` items don't exactly match `items` spelling | Validation error: "items and correct_order must contain the same elements" | Copy-paste items from one field to the other, then reorder |
| Blank rows between questions | Parser skips empty rows — questions still load, but avoid gaps for clarity | Delete any blank rows between data rows |
| Field contains a comma | Parser splits the field incorrectly | Wrap the entire field value in double quotes: `"Smith, John"` |
| `{{blank}}` typed incorrectly | The placeholder renders as literal text; no input appears | Use exactly `{{blank}}` — double curly braces, lowercase, no spaces |
