# Keyword-Based Review Classifier (C++)

## Overview
This project implements a lightweight Natural Language Processing (NLP) system that evaluates written reviews and classifies them as **truthful**, **deceptive**, or **uncategorized** using a keyword-weight scoring approach.

The system processes a corpus of verified hotel reviews and assigns scores based on the presence and frequency of weighted keywords derived from prior linguistic analysis.

---

## Why this matters
Distinguishing truthful from deceptive reviews is difficult for humans and scales poorly. Even simple, interpretable NLP techniques—like keyword-weight models—can provide meaningful signal and serve as a foundation for more advanced classification systems.

This project focuses on **clarity, correctness, and reproducibility**, rather than black-box models.

---

## Tech Stack
- **Language:** C++ (C++11)
- **Core concepts:**  
  File I/O · String processing · Vectors · Modular design · Unit testing
- **Paradigm:** Rule-based NLP (keyword-weight scoring)

---

## Approach

### 1. Keyword-weight ingestion
- Read a verified keyword-to-weight mapping from a file
- Store keywords and weights in **parallel vectors** to preserve alignment

### 2. Review preprocessing
- Tokenize review text into individual words
- Normalize text by:
  - Lowercasing
  - Removing punctuation
  - Replacing numeric tokens with `<number>`

### 3. Scoring logic
- For each word in a review:
  - Look up its weight (if present)
  - Accumulate a total review score
- Words not found in the keyword list contribute `0.0`

### 4. Classification
Reviews are categorized using score thresholds:
- **Truthful:** score > 3.0  
- **Deceptive:** score < -3.0  
- **Uncategorized:** otherwise

### 5. Summary reporting
The program:
- Processes all available reviews
- Tracks highest- and lowest-scoring reviews
- Outputs a structured summary report to `report.txt`

---

## Example Output

review score category  
0 3.49 truthful  
1 3.33 truthful  
2 15.68 truthful  
...  
17 -21.61 deceptive  

Number of reviews: 20  
Number of truthful reviews: 9  
Number of deceptive reviews: 8  
Number of uncategorized reviews: 3  

Review with highest score: 6  
Review with lowest score: 17  

---

## Project Structure

├── reviews.h  
├── reviews.cpp  
├── evaluateReviews.cpp  
├── keywordWeights.txt  
├── reviewXX.txt  
└── report.txt  

---

## Limitations
- Keyword-based scoring does not capture context, negation, or sarcasm
- Performance depends heavily on the quality of the keyword-weight dataset
- Linear search over keywords is not optimized for large vocabularies

---

## Future Improvements
- Replace keyword lookup with a hash-based structure
- Add precision/recall evaluation
- Extend to n-grams or basic ML classifiers
- Apply to new, unseen review domains

---

## What this project demonstrates
- Modular C++ design
- Clean file I/O and preprocessing
- Interpretable NLP pipeline
- Engineering discipline over black-box complexity
