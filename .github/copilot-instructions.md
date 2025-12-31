# AI Agent Instructions - The Matrix Prime

## Architecture Overview
Single-file Streamlit app (`app.py`) built for hackathon speed. No microservices, no database—pure stateful UI with session state management. PDF → AI → Structured Output pipeline in ~500 lines.

**Data Flow:**
1. PDF upload → PyMuPDF extraction with page tracking (`extract_pdf_text_with_pages`)
2. Formatted text → Groq API (Llama-3.1-8B-Instant) with `SYSTEM_PROMPT`
3. Markdown memo → Session state → Split-screen display + chat refinement
4. Export → python-docx or raw markdown download
5. Persistence → Local storage (data/ folder) with load/reload capability

## Critical Developer Workflows

**Local Development:**
```bash
# Always run from project root
streamlit run app.py

# API key setup (required before first run)
# Edit .streamlit/secrets.toml with GROQ_API_KEY
```

**Testing AI Prompts:**
- Modify `SYSTEM_PROMPT` constant (lines 25-63 in app.py)
- Changes require app restart (Ctrl+C, rerun)
- Test with sample 10-K PDFs; output must include `[Page X]` citations

**Deployment:**
Streamlit Community Cloud only. No Docker, no K8s. Push to GitHub → connect repo in share.streamlit.io → add `GROQ_API_KEY` to Secrets.

## Session State Pattern (Critical!)
Never use global variables. ALL state lives in `st.session_state`:
- `memo_content`: Generated markdown (editable via chat)
- `pdf_text`: Full extracted text with `--- PAGE X ---` markers
- `chat_history`: Refinement conversation log
- `pdf_doc`: Raw PDF bytes for viewer rendering

**Example:**
```python
if 'memo_content' not in st.session_state:
    st.session_state.memo_content = None
```

Always check existence before access to avoid Streamlit rerun errors.

## Groq API Integration
**Model:** `llama-3.1-8b-instant` (optimized for speed and compatibility)
**Temperature:** 0.3 (balances accuracy vs creativity for financial analysis)
**Token Limits:**
- Input capped at 15,000 chars (`pdf_text[:15000]`) to avoid API errors
- Output capped at 2,000 tokens (sufficient for structured memo)

**Two API Call Patterns:**
1. `generate_credit_memo()`: Initial generation from full PDF
2. `refine_memo()`: Updates based on chat input (includes current memo + new instructions)

## UI Layout Convention
Split-screen is non-negotiable (judges expect it):
- `col1, col2 = st.columns([1, 1])` creates equal split
- Left column: PDF viewer + Plotly chart
- Right column: Memo markdown + export buttons + chat interface

**PDF Rendering:**
PyMuPDF renders page as PNG via `page.get_pixmap(matrix=fitz.Matrix(2, 2))`. The `Matrix(2, 2)` doubles resolution for readability. Don't reduce—quality matters for page verification.

## Export Logic
**Markdown:** Direct string download (trivial)
**Word (.docx):** Custom formatter in `export_to_docx()`:
- Splits memo by `# ` and `## ` for heading hierarchy
- Preserves markdown structure as Word styles
- Returns `io.BytesIO()` buffer (never writes to disk)

## Prompt Engineering Rules
The `SYSTEM_PROMPT` is the app's brain. When modifying:
1. **Always include output format template** (lines 32-63)—LLM needs explicit structure
2. **Confidence tags are mandatory** (✅/⚠️/❌)—auditors require this
3. **Page citations must use `[Page X]` format**—regex-parseable for verification
4. **"Data Gap" messaging**—better than hallucinated numbers

## Common Pitfalls
1. **PDF file object exhaustion:** `pdf_file.read()` consumes stream. Store result in variable.
2. **Streamlit reruns:** Any widget interaction triggers full script rerun. Use session state liberally.
3. **API key not found:** App degrades gracefully but won't generate. Check sidebar input OR secrets.toml.
4. **Plotly dark theme:** Uses `template='plotly_dark'` to match Streamlit's aesthetic. Don't use default.

## Adding New Features
**New metric to Key Metrics table:**
1. Update `SYSTEM_PROMPT` output format (add table row)
2. No code changes needed—LLM adapts

**New refinement command:**
Just chat—no code changes. LLM interprets natural language ("simplify", "add detail", etc.)

**New export format (e.g., JSON):**
Add new function mimicking `export_to_docx()`, create button in right column export section.

## Dependencies
All pinned to stable versions (see `requirements.txt`). No auto-upgrades—hackathon stability > latest features.
- `pymupdf==1.24.14` (NOT `PyPDF2`—faster text extraction, has pre-built wheels for Python 3.13)
- `groq==0.4.2` (official client, not `openai` wrapper)
- `python-docx==1.1.0` (NOT `docx`—different package!)

## File References
- AI prompt: `SYSTEM_PROMPT` constant (app.py:25-63)
- PDF extraction: `extract_pdf_text_with_pages()` (app.py:75-90)
- Main UI: Lines 300-409 (split-screen + welcome screen)
- Session state init: Lines 65-73
