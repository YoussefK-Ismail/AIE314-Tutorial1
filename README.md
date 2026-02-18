# AIE314 Tutorial 1: Preprocessing Unstructured Data for LLM Applications

## Team Members
- Youssef Khaled Ismail (ID: 22101260)

---

## Project Description
This project involves preprocessing unstructured data from various document types (PDF, Word, Excel) and preparing it for use in LLM / RAG applications. The pipeline extracts raw text, normalizes it, splits it into overlapping chunks, and generates semantic embeddings for each chunk — producing structured JSON files ready for downstream retrieval.

### Pipeline Steps
1. **Text Extraction** — detects file extension (`if .pdf` → `pypdf` / `elif .docx` → `python-docx` / `elif .xlsx` → `openpyxl`)
2. **Normalization** — Unicode NFKC, lowercase, remove noise, collapse whitespace
3. **Chunking** — overlapping word-level windows (300 words, 50-word overlap)
4. **Semantic Embedding** — TF-IDF vectors (128 features); upgrade to `sentence-transformers` on Colab for dense embeddings

---

## Repository Structure
```
AIE314-Tutorial1/
├── AIE314_Tutorial1_Preprocessing.ipynb      # Main notebook (Google Colab ready)
├── README.md
└── output/
    ├── computer_science_overview_pdf_processed.json
    ├── computer_science_overview_docx_processed.json
    └── ExcelSample_processed.json
```

---

## How to Run the Code

### Option A — Google Colab (recommended)
1. Open [Google Colab](https://colab.research.google.com/) and upload `AIE314_Tutorial1_Preprocessing.ipynb`
2. Upload your input files (`*.pdf`, `*.docx`, `*.xlsx`) via the 📁 Files panel on the left
3. Update the `FILES` list in **Step 8** with your file names
4. Run all cells: `Runtime → Run all`
5. Processed JSON files will be saved to the `output/` folder

### Option B — Local (Python 3.9+)
```bash
# 1. Clone the repo
git clone https://github.com/<your-username>/AIE314-Tutorial1.git
cd AIE314-Tutorial1

# 2. Install dependencies
pip install PyMuPDF python-docx openpyxl sentence-transformers scikit-learn jupyter

# 3. Launch Jupyter
jupyter notebook AIE314_Tutorial1_Preprocessing.ipynb
```

---

## Dependencies
| Library | Purpose |
|---|---|
| `PyMuPDF (fitz)` | PDF text extraction |
| `python-docx` | DOCX text extraction |
| `openpyxl` | XLSX text extraction |
| `scikit-learn` | TF-IDF embeddings |
| `sentence-transformers` | Dense semantic embeddings (optional upgrade) |

```bash
pip install PyMuPDF python-docx openpyxl scikit-learn sentence-transformers
```

---

## Output Format (JSON)
Each processed file produces a JSON with the following structure:
```json
{
  "source_file": "example.pdf",
  "file_type": "pdf",
  "total_chunks": 3,
  "embedding_method": "TF-IDF 128 features",
  "normalized_text_preview": "introduction to computer science ...",
  "chunks": [
    {
      "chunk_id": 0,
      "text": "normalized chunk text here ...",
      "word_count": 300,
      "embedding": [0.0, 0.134, 0.021, ...]
    }
  ]
}
```
