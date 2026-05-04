# DAMA Hungary – Data Management Maturity Assessment Question Bank

This repository is the collection of questions used by **DAMA Hungary** for its **Data Management Maturity Assessment (DMMA)**. The question set is designed for structured interview settings and is intentionally evolving: questions are added, scored, and activated over time as the assessment methodology matures. The question bank also serves as an input for an agentic interview assessment.

---

## Purpose

The assessment helps organizations understand where they stand across key data management disciplines. Questions are posed to different personas (roles within an organization) and cover both organizational context and specific data management practices. The insights gathered could feed into a maturity scoring model aligned with the DAMA-DMBOK framework.

---

## Repository Structure

```
dama-dmma-questions/
├── dm_model.json       # Maturity model by aspect with phase descriptions
├── question_bank.json   # The full question bank
├── terms.json           # Data glossary with translations
└── README.md            # This file
```

---

## question_bank.json Schema

The question bank is a JSON object with three top-level category keys. Each category holds an array of question objects.

### Categories

| Key | Description |
|---|---|
| `persona` | Questions to understand the respondent's role, data experience, and attitude toward the assessment |
| `company` | Questions to understand the organization's structure, industry, and business context |
| `assessment` | Questions that directly evaluate data management maturity across DAMA knowledge areas |

### Question Object Fields

| Field | Type | Description |
|---|---|---|
| `id` | integer | Unique identifier for the question across the entire bank |
| `text` | string | The question text as it would be asked in an interview |
| `aspects` | string[] | One or more DMMA knowledge areas this question maps to |
| `terms` | string[] | Key data management terms surfaced by the question (references entries in `terms.json`) |
| `question_score` | integer | Relevance score (1–10); higher values indicate higher diagnostic value |
| `active` | 0 \| 1 | Whether the question is currently in active use (`1`) or retired/draft (`0`) |
| `source` | string | Origin of the question (e.g. `"generated"`) |
| `translations` | object | Translated question text keyed by language code (e.g. `{"hu": ""}`) |
| `persona` | string[] | Target respondent personas for this question (e.g. `["data", "business"]`) |

### Example

```json
{
  "id": 13,
  "text": "How aligned are your organization's data initiatives with its overall business strategy?",
  "aspects": ["Data Strategy"],
  "terms": [],
  "question_score": 10,
  "active": 1,
  "source": "generated",
  "translations": { "hu": "" },
  "persona": ["data", "business", "technology"]
}
```

---

## dm_model.json Schema

The model file is a flat array of maturity aspects. Each aspect defines the capability area, a short description, and the maturity phases from `1` to `7`.

### Model Object Fields

| Field | Type | Description |
|---|---|---|
| `aspect` | string | Canonical aspect name used by the assessment model |
| `description` | string | Short explanation of what the aspect measures |
| `phases` | object | Mapping of maturity levels `"1"` through `"7"` to descriptive phase texts |

### Example

```json
{
  "aspect": "Data Strategy",
  "description": "Alignment of data initiatives with business and IT strategies to drive organizational value from data.",
  "phases": {
    "1": "No data strategy",
    "2": "Analytics and data related improvements need to be aligned to a target",
    "3": "Data strategy is part of the IT strategy. Data is still not in focus, \"classic\" IT aspects are dominant.",
    "4": "Data related initiatives do not get priority, get delayed, expected results stay being a promise",
    "5": "Data Strategy is separated, it's focusing on business goals and it's in line with IT strategy",
    "6": "It's hard to keep strategies in synchron due to lack of \"interfaces\". Minor changes are not aligned or simply ignored that makes significant reworks also hard to implement. AI does not fit well into data strategy.",
    "7": "Data Strategy is integrated with business and IT strategies. AI has its own chapter within that or is developed as a separated one."
  }
}
```

The `aspect` values in this file serve as the reference vocabulary for the `aspects` arrays in `question_bank.json`.

---

## terms.json Schema

The terms file is a flat array of glossary entries. Each entry covers a key data management concept referenced across the question bank.

### Term Object Fields

| Field | Type | Description |
|---|---|---|
| `term` | string | The canonical English term |
| `definition` | string | Plain-language definition grounded in the DAMA-DMBOK2 framework |
| `translations` | object | Translated term and/or definition keyed by language code (e.g. `{"hu": ""}`) |

### Example

```json
{
  "term": "Data Management Maturity Assessment (DMMA)",
  "definition": "A structured evaluation of an organization's capabilities across data management disciplines, resulting in a maturity score that identifies strengths and improvement areas.",
  "translations": { "hu": "" }
}
```

