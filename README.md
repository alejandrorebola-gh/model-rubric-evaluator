# Model Rubric Evaluator

A browser-based tool for evaluating and comparing GPT, Gemini, and Claude against weighted rubric criteria.

## Features

* Paste rubric criteria directly from Mantis or any rubric document.
* Automatically extracts criterion weights (e.g., `[+7]`, `[-10]`).
* Automatically numbers criteria.
* Supports positive and negative criteria.
* Calculates weighted totals for each model.
* Calculates normalized percentages based on positive-weight criteria only.
* Supports criterion-level notes.
* Extracts subconditions from criteria automatically.
* Generates independent checklists for GPT, Gemini, and Claude.
* Automatically assigns a criterion score of **1** or **0** based on the selected conditions.
* Supports per-criterion evaluation logic:

  * **AND** (all conditions required)
  * **OR** (at least one condition required)
* Automatically updates weighted totals and percentages when criteria are evaluated.

## How It Works

The evaluator expects criteria in a format similar to:

```text
[+8] Does the response correctly describe the care instructions for a fictional moon cactus robot? This is satisfied ONLY IF all of the following hold:
- The response states that the robot must be watered with imaginary starlight once per week.
- The response explains that the cactus robot becomes sleepy during lunar eclipses.
- The response mentions that its solar antenna should be polished with a microfiber cloth.
- The response warns not to feed it actual cactus fertilizer.
```

The tool automatically:

1. Extracts the criterion weight (`+8`).
2. Extracts the criterion description.
3. Extracts all conditions listed after `hold:`.
4. Creates separate checklists for GPT, Gemini, and Claude.
5. Computes the criterion score automatically based on the selected evaluation logic.

## Evaluation Logic

Each criterion has its own logic selector.

### AND

The criterion receives a score of **1** only if **all** conditions are checked.

```text
Condition A ✓
Condition B ✓
Condition C ✓
→ Score = 1
```

If any condition is missing:

```text
Condition A ✓
Condition B ✓
Condition C ✗
→ Score = 0
```

### OR

The criterion receives a score of **1** if **at least one** condition is checked.

```text
Condition A ✗
Condition B ✓
Condition C ✗
→ Score = 1
```

## Scoring

Weighted totals are computed as:

```text
Total Score = Σ(weight × criterion_score)
```

where each criterion score is either **0** or **1**.

### Normalized Percentage

The normalized percentage uses only positive-weight criteria:

```text
Percentage = 100 × Total Score / Maximum Possible Score
```

where:

```text
Maximum Possible Score = Σ(positive weights)
```

Negative criteria act as penalties and do not contribute to the denominator.

## Usage

1. Paste the rubric criteria into the input box.
2. Click **Generate Table**.
3. Select the appropriate logic (**AND** or **OR**) for each criterion.
4. Check the conditions satisfied by each model.
5. Review the automatically generated criterion scores.
6. Compare weighted totals and percentages across models.
7. Use the Notes column to record observations or justification.

## Notes

* All calculations run locally in the browser.
* No data is uploaded, stored, or transmitted.
* Positive criteria contribute to the maximum possible score.
* Negative criteria act only as penalties.
* Each criterion can use different evaluation logic (AND or OR).
