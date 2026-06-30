# 🔥 RoastCV — AI-Powered Resume Analyzer & ATS Checker

**Live App:** [roastcv.in](https://roastcv.in)

RoastCV is a multi-agent AI system that analyzes resumes the way a real hiring pipeline would — combining the perspectives of an ATS engine, an HR recruiter, a hiring manager, and a talent acquisition specialist into a single, brutally honest report. It doesn't just score your resume; it tells you exactly *why*, rewrites the weak parts, generates a tailored cover letter, and preps you for the interview that follows.

---

## ✨ What It Does

RoastCV runs **13 specialized AI agents** in a coordinated pipeline, each focused on one specific dimension of resume quality:

| # | Agent | Purpose |
|---|-------|---------|
| 1 | **Resume Reader** | Parses raw resume text into structured JSON (contact info, skills, experience, education, projects) |
| 2 | **Resume Audit** | Flags weak summaries, formatting issues, grammar problems, and low-impact bullet points |
| 3 | **ATS Review** | Estimates ATS compatibility — keyword optimization, structure, and formatting |
| 4 | **JD Analyzer** | Extracts required and preferred skills from the job description |
| 5 | **Gap Analysis** | Compares resume vs. job description to surface missing skills and keyword gaps |
| 6 | **HR Roast** | A brutally honest, recruiter-style critique — would this resume actually get shortlisted? |
| 7 | **Recruiter Review** | Evaluates the resume against current market and industry standards |
| 8 | **Resume Rewrite** | Rewrites weak sections using only real information — no fabricated experience |
| 9 | **Humanizer** | Strips AI-sounding buzzwords and clichés, making the resume read naturally |
| 10 | **Hiring Manager** | Evaluates practical team fit and project relevance from a hiring manager's lens |
| 11 | **Interview Coach** | Generates candidate-specific interview questions based on actual projects and experience |
| 12 | **Cover Letter Writer** | Produces a personalized, natural-sounding cover letter |
| 13 | **Final Decision Engine** | Aggregates every agent's score into one overall verdict and recommendation |

The result: a complete, end-to-end resume improvement workflow — from raw upload to a polished, downloadable resume, cover letter, and interview prep kit — powered entirely by AI.

---

## 🧠 Key Engineering Highlights

This project isn't just a wrapper around a single API call — it's built to be resilient, scalable, and production-ready:

- **Multi-Provider LLM Architecture with Automatic Fallback**
  Supports 6 LLM providers (Gemini, Groq, Cerebras, Mistral, GitHub Models, Azure OpenAI) behind a unified interface. If the primary provider fails or hits a rate limit, the system automatically retries with exponential backoff and falls back to the next configured provider — with zero downtime for the end user.

- **Concurrency-Safe Request Handling**
  Uses a semaphore-based concurrency limiter to safely handle multiple simultaneous users, thread-local provider tracking, and a timeout wrapper around every LLM call to prevent the app from ever hanging.

- **Robust JSON Parsing**
  LLM responses aren't always perfectly formatted JSON. A multi-stage cleaning and parsing pipeline (markdown fence stripping, regex extraction, trailing-comma repair) ensures structured output is reliably extracted even from imperfect model responses.

- **Defensive Score Aggregation**
  The final scoring engine explicitly validates every score (rejecting booleans, out-of-range values, and missing fields) before averaging — so a single failed agent or a hallucinated score never silently skews the overall result.

- **Document Generation Pipeline**
  Generates ATS-friendly **PDF** and **DOCX** resumes and cover letters from scratch using ReportLab and python-docx, with intelligent section parsing that correctly maps headings like "Technical Skills" or "Work Experience" to their canonical sections — preserving all links, contact details, and formatting.

- **Privacy-First Public Showcase**
  A "Wall of Roasts" feature publicly displays anonymized feedback (role, score, and excerpt only) with zero personally identifiable information ever stored — no name, email, phone, or resume text.

- **Production Deployment**
  Deployed on Render with a custom build step that patches Streamlit's static HTML to inject SEO meta tags, Google Analytics, and AdSense — solving the common problem of client-side-rendered apps being invisible to search engine crawlers.

---

## 🛠️ Tech Stack

- **Frontend / App Framework:** Streamlit
- **Language:** Python 3.11
- **LLM Providers:** Google Gemini, Groq, Cerebras, Mistral AI, GitHub Models, Azure OpenAI
- **Resume Parsing:** pdfplumber, python-docx
- **Document Generation:** ReportLab (PDF), python-docx (DOCX)
- **Deployment:** Render
- **Configuration:** python-dotenv, TOML

---

## 📂 Project Architecture

```
roastcv/
├── app.py                    # Main Streamlit application
├── config.py                 # Multi-provider configuration & validation
├── llm_client.py              # Unified LLM client with fallback chain
├── resume_parser.py           # PDF/DOCX text extraction
├── resume_reader.py           # Agent 1 — Resume → structured JSON
├── resume_audit.py            # Agent 2 — Resume quality audit
├── ats_review.py               # Agent 3 — ATS compatibility scoring
├── jd_analyzer.py              # Agent 4 — Job description analysis
├── gap_analysis.py             # Agent 5 — Resume vs JD gap analysis
├── hr_roast.py                  # Agent 6 — Brutally honest HR review
├── recruiter_review.py          # Agent 7 — Recruiter market evaluation
├── resume_rewrite.py            # Agent 8 — Resume rewriting
├── humanizer.py                  # Agent 9 — Natural tone humanizer
├── hiring_manager.py             # Agent 10 — Hiring manager evaluation
├── interview_coach.py            # Agent 11 — Interview question generator
├── cover_letter.py                # Agent 12 — Cover letter generation
├── final_decision.py              # Agent 13 — Final score aggregation
├── resume_pdf.py                   # PDF resume/cover letter generator
├── resume_docx.py                   # DOCX resume/cover letter generator
├── wall_of_roasts.py                 # Anonymous public feedback wall
├── patch_streamlit_html.py            # SEO/Analytics injection for deployment
├── requirements.txt
└── render.yaml                        # Render deployment configuration
```

---

## 🚀 Why This Project Matters

Most resume tools give you a single, generic score. RoastCV simulates an entire hiring panel — an ATS, an HR recruiter, a hiring manager, and a talent acquisition specialist — each with their own evaluation lens, and then combines their verdicts into one transparent, explainable decision. It's a practical demonstration of multi-agent AI system design, resilient LLM infrastructure, and end-to-end product thinking — from raw resume upload to a fully polished, recruiter-ready deliverable.

---

## 🔗 Links

- **Live Application:** [https://roastcv.in](https://roastcv.in)
- **GitHub:** [analyst-arbaz](https://github.com/analyst-arbaz)

---

*Built with a focus on reliability, real-world resilience, and genuinely useful feedback — not just another resume scorer.*
