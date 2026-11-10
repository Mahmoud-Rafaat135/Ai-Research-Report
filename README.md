# Ai-Research-Report
# 🤖 AI Research Report Generator — Multi-Agent System

> A multi-agent research pipeline built with **CrewAI** and a **local LLM (Ollama + Qwen2.5:3B)** that plans searches, analyzes evidence, and produces a professional Arabic research report — with **no paid API keys required**.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![CrewAI](https://img.shields.io/badge/CrewAI-Multi--Agent-orange)
![Ollama](https://img.shields.io/badge/Ollama-Local%20LLM-black)
![Gradio](https://img.shields.io/badge/Gradio-UI-yellow)
![Colab](https://img.shields.io/badge/Google%20Colab-Ready-F9AB00?logo=googlecolab&logoColor=white)

---

## 📌 Overview

This project demonstrates how a team of specialized AI agents can collaborate sequentially to turn a single research topic into a structured, source-grounded report.

The demo topic is:

> **Generative AI in Education: Opportunities, Risks, and Responsible Implementation**

Everything runs inside a Google Colab runtime using an open-source model served locally by Ollama, so there is **no dependency on OpenAI, Groq, or Gemini API keys** and **no payment card needed**.

> **Note:** This is a **Multi-Agent Web Research** workflow, not a RAG system — it does not use a vector database.

---

## 🏗️ Architecture

```
Topic
  │
  ▼
┌──────────────────────┐
│ Query Planner Agent  │  → generates 3 focused search queries
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ Web Research Agent   │  → organizes sources into an evidence pack
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ Evidence Analyst     │  → findings, opportunities, risks, recommendations
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ Report Writer Agent  │  → final Arabic report (Markdown → HTML)
└──────────┬───────────┘
           ▼
   Gradio App + Downloads (HTML / MD / CSV / JSON)
```

---

## ✨ Features

- **4 specialized agents** working in a sequential CrewAI process
- **100% local inference** with Ollama and `qwen2.5:3b` (multilingual, supports Arabic)
- **Keyless web search** via DDGS, with page text extraction using Requests + BeautifulSoup
- **Curated official-source fallback** (UNESCO, OECD, UNICEF) for stable and transparent results
- **Source tracking** with IDs (`[S1]`, `[S2]`, `[S3]`) attached to claims
- **Multiple export formats:** HTML, Markdown, Sources CSV, Sources JSON
- **Interactive Gradio interface** with a public share link and download buttons

---

## 🧰 Tech Stack

| Component | Purpose |
|---|---|
| [CrewAI](https://www.crewai.com/) | Agent and task orchestration |
| [Ollama](https://ollama.com/) | Local LLM runtime with an OpenAI-compatible API |
| Qwen2.5:3B | Lightweight multilingual language model |
| DDGS | Web search without an API key |
| Requests + BeautifulSoup | Web page text extraction |
| Markdown | Markdown → HTML conversion |
| Gradio | Web UI and report deployment |

---

## 🚀 Getting Started

### Option 1 — Google Colab (recommended)

1. Open `AI_Research_Report_CrewAI.ipynb` in Google Colab.
2. *(Optional)* Switch to a GPU: `Runtime → Change runtime type → GPU`.
3. Run the cells in order (`Runtime → Run all`).

### Option 2 — Local machine

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/ai-research-report-crewai.git
cd ai-research-report-crewai

# 2. Install Python dependencies
pip install -U "crewai>=1.15.0,<2.0.0" "ddgs>=9.0.0" "beautifulsoup4>=4.12.0" \
               "markdown>=3.6" "openai>=1.70.0" requests gradio

# 3. Install Ollama (https://ollama.com/download) and pull the model
ollama pull qwen2.5:3b

# 4. Start the Ollama server
ollama serve

# 5. Launch Jupyter and run the notebook
jupyter notebook AI_Research_Report_CrewAI.ipynb
```

---

## 📓 Notebook Walkthrough

| Step | Description |
|---|---|
| 00–01 | Setup and install Python libraries |
| 02–03 | Install and start the Ollama server |
| 04–05 | Download `qwen2.5:3b` and test the local API |
| 06 | Connect CrewAI to the local model |
| 07–08 | Define the topic and build the web research tool |
| 09–11 | Query Planner agent and search execution |
| 11.1 | Load curated official source summaries (fallback) |
| 12–14 | Research, Analyst, and Writer agents |
| 15 | Assemble and run the Crew |
| 15.1 | Fast report generation (no LLM call required) |
| 16 | Deploy the report with Gradio |

---

## 📂 Output Files

Generated inside `ai_agent_report_output/`:

```
ai_agent_report_output/
├── step_1_search_queries.txt      # Queries from the Planner agent
├── step_2_research_evidence.txt   # Evidence pack
├── step_3_evidence_analysis.txt   # Analytical brief
├── step_4_final_report.md         # Report written by the Writer agent
├── final_report.md                # Final Markdown report
├── final_report.html              # Styled HTML report
├── sources.csv                    # Source registry (CSV)
└── sources.json                   # Source registry (JSON)
```

---

## ⚠️ Transparency & Limitations

- The built-in source records for **UNESCO, OECD, and UNICEF** are **curated, paraphrased summaries** of the official pages. They are **not** verbatim quotations and **not** live scraping.
- The report is **not an exhaustive literature review**; always verify claims against the original sources linked in the report.
- `qwen2.5:3b` is a small model. Output quality and speed depend on the Colab runtime (CPU is noticeably slower than GPU).
- Some websites block automated page extraction; in that case only titles and search snippets are kept.

---

## 🔧 Customization

Change the research topic and report language in the notebook:

```python
REPORT_TOPIC = "Your research topic here"
REPORT_LANGUAGE = "Arabic"   # or "English"
```

You can also swap the model by changing `MODEL_NAME` (for example, `qwen2.5:7b` on a GPU runtime).

---

## 🗺️ Roadmap

- [ ] Add a user input field for custom topics in the Gradio UI
- [ ] Add PDF export
- [ ] Support larger models on GPU runtimes
- [ ] Add automated source quality scoring
- [ ] English / Arabic language toggle

