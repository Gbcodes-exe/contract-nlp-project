# Contract Risk Analyzer & Supplier Similarity Matcher

This project automates contract analysis using Natural Language Processing (NLP). It extracts key clauses from procurement or service contracts, classifies their risk level, and suggests similar past supplier contracts for benchmarking and compliance.

---

## Features

- Clause Extraction from PDF contracts (e.g., payment, termination, jurisdiction, penalty, renewal)
- Risk Assessment using rule-based analysis (e.g., long payment terms, foreign jurisdiction)
- Supplier Similarity Matching using sentence embeddings (via `SentenceTransformer`)
- Visual Reports including similarity bar charts
- Fully customizable and extensible (add more clauses, smarter models)

---

## Tech Stack

| Component          | Technology                    |
|-------------------|-------------------------------|
| PDF Parsing        | `PyPDF`                       |
| NLP & Tokenization | `spaCy`, `re`                 |
| Embeddings         | `SentenceTransformer` (MiniLM)|
| Visualization      | `matplotlib`                  |
| Data               | JSON format (clause dictionaries) |
| Optional UI        | (Add Streamlit or CLI wrapper) |

---

## How It Works

1. PDF Processing:
   - Extracts full text from each contract page
   - Splits into separate contracts using signatures (e.g., “Signed,”)

2. Clause Extraction:
   - Scans each contract block for key phrases
   - Pulls first matching sentence for each clause

3. Risk Assessment:
   - Flags issues like:
     - Payment terms > 60 days
     - Termination notice > 60 days
     - Foreign jurisdiction
     - Missing penalties
     - Auto-renewal clauses

4. Supplier Matching:
   - Uses semantic embeddings to find most similar past contracts
   - Ranks based on cosine similarity across clause vectors

5. Visualization:
   - Outputs top suppliers with similarity bar chart

---

## Example Output

```json
{
  "overall_risk": "Medium",
  "reasons": [
    "No penalty clause found",
    "Auto-renewal clause present"
  ]
}

Most similar suppliers:
Infospark Ltd.: similarity 0.876
NeuralEdge Solutions: similarity 0.733
Datacube Corp.: similarity 0.614


