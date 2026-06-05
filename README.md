# Privacy Aware Computing: PII Sanitization & Utility Analysis

## Overview

This repository contains a Minimum Viable Product (MVP) demonstrating Natural Language Processing (NLP) data sanitization using Microsoft Presidio.

The project evaluates two models:

1. **Baseline MVP**: Uses Presidio's out-of-the-box Named Entity Recognition (NER) to detect standard PII (Dates, Persons, Locations).
2. **Improved MVP**: An enhanced engine featuring custom Regular Expressions (Regex) and dictionary hooks to detect domain-specific data that the baseline model misses (e.g., specific financial formats, custom server usernames, local street addresses, and targeted medical/corporate terminology).

---

## Key Features

- **Custom Pattern Recognizers**: Implements regex patterns to identify and redact exact financial amounts, custom IT usernames, partial street addresses, and student IDs.
- **Targeted Deny Lists**: Utilizes a custom dictionary to redact highly sensitive domain-specific quasi-identifiers (SENSITIVE_TERM).
- **Semantic Utility Scoring**: Uses the en_core_web_lg model from spaCy to calculate the Cosine Similarity between the original prompt and the sanitized output, mathematically proving how heavy redaction flattens a sentence's semantic vector.
- **Automated Data Visualization**: Generates a grouped bar chart (seaborn and matplotlib) comparing the utility scores of the Baseline and Improved models across a batch of sample inputs.

---

## Prerequisites and Installation

This script requires Python 3.7+ and several external libraries. You can install the required dependencies using pip.

```bash
# Install Microsoft Presidio components, spaCy, Pandas, Matplotlib, and Seaborn
pip install presidio-analyzer presidio-anonymizer spacy pandas matplotlib seaborn numpy

# Download the large English spaCy model (required for word vectors and cosine similarity)
python -m spacy download en_core_web_lg
```

---

## Usage

1. Simply run the Notebook! The pre-reqs are included when you run the notebook.

---

## What to Expect Upon Execution

The script processes a batch of 8 domain-specific test prompts (Medical, Business, HR, IT, Education, Real Estate, Personal, and Financial).

1. Console Output: The terminal will print a detailed side-by-side comparison for each sample, displaying:

- The Original Text
- The Baseline Output (Standard Presidio)
- The Improved Output (Custom Rules)
- The Baseline vs. Improved Cosine Similarity Scores
- The calculated Score Difference (Utility Drop)

2. Visualization Export:
   The script generates a visualization. This grouped bar chart clearly illustrates the utility drop associated with aggressive privacy redaction.

---

## Understanding the Metrics

1. Semantic Utility (Cosine Similarity)
   Calculated via spaCy, this metric represents how much of the original meaning is retained after sanitization. A score closer to 1.0 means the sentence structure and context are highly preserved.
