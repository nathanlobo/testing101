# 🔴 The Matrix Prime

**AI-Powered Credit Memo Generation for Financial Due Diligence**

Built for the **Orix McLaren Hackathon 2026**

---

## 🎯 Overview

The Matrix Prime transforms dense financial PDFs (Balance Sheets, 10-Ks, Annual Reports) into structured, audit-ready Credit Memos in **under 5 seconds**. Every claim is backed by source citations for full traceability.

### The Problem
Manual credit memo creation takes hours. Analysts manually extract metrics, cross-reference pages, and format reports. Error-prone. Slow. Painful.

### The Solution
Upload PDF → Get structured memo with:
- ✅ Executive Summary (5 key bullets)
- ✅ Key Metrics Table (Revenue, EBITDA, Debt Ratio with YoY comparison)
- ✅ Risk Analysis (Top 3 risks + mitigation strategies)
- ✅ Source Citations (Every fact links to [Page X])
- ✅ Interactive Refinement (Chat to adjust tone/detail)
- ✅ Export Ready (.md and .docx formats)

---

## 🚀 Features

### Split-Screen Interface
- **Left:** PDF viewer with page navigation
- **Right:** Generated Credit Memo in Markdown

### AI-Powered Analysis
- Powered by **Groq Llama-3** (llama3-8b-8192)
- Sub-5-second generation time
- Confidence tagging: ✅ Direct Match | ⚠️ Inferred | ❌ Missing

### Source Traceability
Every metric and claim includes a `[Page X]` citation for audit compliance.

### Interactive Refinement
Post-generation chat interface:
- "Simplify the risk section"
- "Add more detail to executive summary"
- "Find source for Debt Ratio"
- "Make tone more formal"

### Visual Analytics
Plotly-powered trend charts for key financial metrics.

### Export Options
- **Markdown (.md):** Clean, version-controllable format
- **Word (.docx):** Formatted document for stakeholders

---

## 🛠️ Technical Stack

| Component | Technology |
|-----------|-----------|
| **Frontend** | Streamlit 1.31.0 |
| **PDF Processing** | PyMuPDF (fitz) 1.23.21 |
| **AI Inference** | Groq API (Llama-3-8B-8192) |
| **Visualization** | Plotly 5.18.0 |
| **Export** | python-docx 1.1.0 |

---

## 📦 Installation & Setup

### Prerequisites
- Python 3.9 or higher
- Groq API Key ([Get one here](https://console.groq.com))

### Local Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd project-1
   ```

2. **Create virtual environment** (recommended)
   ```bash
   python -m venv venv
   
   # Windows
   venv\Scripts\activate
   
   # macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   
   Create a `.streamlit/secrets.toml` file:
   ```toml
   GROQ_API_KEY = "your_groq_api_key_here"
   ```
   
   **OR** set environment variable:
   ```bash
   # Windows PowerShell
   $env:GROQ_API_KEY="your_key_here"
   
   # macOS/Linux
   export GROQ_API_KEY="your_key_here"
   ```

5. **Run the application**
   ```bash
   streamlit run app.py
   ```

6. **Access the app**
   Open your browser to `http://localhost:8501`

---

## ☁️ How to Deploy (Streamlit Community Cloud)

### Step 1: Prepare Your Repository
1. Push your code to GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial commit - The Matrix Prime"
   git branch -M main
   git remote add origin <your-github-repo-url>
   git push -u origin main
   ```

### Step 2: Deploy on Streamlit Cloud
1. Go to [share.streamlit.io](https://share.streamlit.io)
2. Sign in with GitHub
3. Click "New app"
4. Select:
   - **Repository:** your-username/your-repo-name
   - **Branch:** main
   - **Main file path:** app.py
5. Click "Advanced settings" → "Secrets"
6. Add your secrets:
   ```toml
   GROQ_API_KEY = "your_groq_api_key_here"
   ```
7. Click "Deploy"

### Step 3: Access Your Live App
Your app will be live at: `https://your-app-name.streamlit.app`

---

## 🎬 3-Minute Demo Script

**Perfect for Hackathon Presentations**

---

### **0:00 - 0:30 | The Hook**
> *"Raise your hand if you've ever spent hours manually creating a credit memo."*
> 
> *[Pause for effect]*
> 
> *"Extracting metrics from 50-page PDFs. Cross-referencing page numbers. Formatting tables. It's brutal. What if we could do it in 5 seconds?"*
> 
> *"Meet The Matrix Prime—powerful, precise, and ready to scale financial analysis. SPEED."*

**[OPEN THE APP ON SCREEN]**

---

### **0:30 - 1:30 | The Live Demo**
> *"Let me show you. Here's a real 10-K filing from a tech company. 87 pages. I'm uploading it now."*

**[DRAG PDF INTO UPLOADER]**

> *"Watch this."*

**[CLICK "GENERATE CREDIT MEMO"]**

> *[Start counting out loud] "1... 2... 3... 4... 5... Done."*
> 
> *"Look at this. Split screen. PDF on the left. Structured memo on the right."*
> 
> **[SCROLL THROUGH MEMO]**
> 
> *"Executive Summary—5 bullets, each with a page citation. Key Metrics table—Revenue, EBITDA, Debt Ratio—compared to prior year. And look—confidence tags. Green check means 'Direct Match from the PDF.' Yellow warning means 'Inferred.' Red X means 'Data Gap.'"*

---

### **1:30 - 2:15 | The "Wow" Feature (Traceability)**
> *"Here's the game-changer for auditors and compliance teams. See this Debt Ratio? It says [Page 42]."*

**[CLICK ON PDF VIEWER, NAVIGATE TO PAGE 42]**

> *"Let me verify. Switching to page 42 on the left... There it is. Balance Sheet. Total Liabilities divided by Total Assets. The AI found it, extracted it, and cited it."*
> 
> *"But wait—what if I need to adjust the memo? Watch."*

**[TYPE IN CHAT: "Find the source for EBITDA"]**

> *[SEND MESSAGE]*
> 
> *"AI responds instantly with the page reference. Full traceability. No more 'Where did this number come from?'"*

---

### **2:15 - 3:00 | The Close (Export & Business Value)**
> *"And when you're done? Export it."*

**[CLICK "DOWNLOAD AS .DOCX"]**

> *"Word document. Ready for your stakeholders. Or Markdown for version control."*
> 
> **[PAUSE, LOOK AT JUDGES/AUDIENCE]**
> 
> *"Why does this matter? Investment banks process hundreds of deals a year. Private equity firms review dozens of targets per quarter. This tool saves 4+ hours per memo. That's $200K/year in analyst time for a mid-size firm."*
> 
> *"Plus—it's audit-ready on day one. Every claim has a source. Compliance loves it."*
> 
> **[FINAL SLIDE/GESTURE]**
> 
> *"The Matrix Prime. From upload to export in 30 seconds. Built for speed. Built for accuracy. Built for you."*
> 
> *"Thank you."*

---

## 📊 Sample Output

### Executive Summary
- Company achieved 23% revenue growth YoY, reaching $198.7M in FY2024 [Page 12] ✅
- EBITDA margin improved from 24.4% to 25.8%, indicating operational efficiency [Page 15] ✅
- Debt-to-equity ratio increased to 1.42 from 1.21, raising leverage concerns [Page 18] ⚠️
- Customer retention rate at 94%, above industry average of 89% [Page 31] ✅
- R&D spending decreased 8% YoY, potential innovation risk [Page 22] ⚠️

### Key Metrics
| Metric | Current Year | Prior Year | Change | Confidence |
|--------|-------------|-----------|--------|-----------|
| Revenue | $198.7M | $175.2M | +13.4% | ✅ |
| EBITDA | $51.3M | $42.8M | +19.9% | ✅ |
| Debt Ratio | 1.42 | 1.21 | +17.4% | ⚠️ |

### Risk Analysis
**Risk 1: Rising Leverage [Page 18]**  
**Description:** Debt-to-equity ratio jumped 17% due to $25M term loan.  
**Mitigation:** Monitor cash flow coverage ratio; consider deleveraging plan.

---

## 🐛 Troubleshooting

### "GROQ_API_KEY not found"
- Ensure `.streamlit/secrets.toml` exists with correct key
- OR enter API key directly in the sidebar

### PDF not rendering
- Check file size (Streamlit Cloud has limits)
- Ensure PDF is not password-protected

### Slow generation
- Verify internet connection (Groq API is cloud-based)
- Check Groq API rate limits on your account

---

## 🤝 Contributing

This is a hackathon project. Contributions welcome!

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

MIT License - see LICENSE file for details

---

## 🏆 Hackathon Credits

**Built for:** Orix McLaren Hackathon 2026  
**Team Role:** Senior Solutions Architect & Full-Stack AI Engineer  
**Technology Partner:** Groq (Ultra-fast LLM inference)

---

## 📞 Contact

For questions or demo requests, reach out via GitHub Issues.

---

**Built with 🔴 precision and ❤️ power**
