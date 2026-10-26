# 🧭 AI CareerPilot – Intelligent Job Application Assistant

An AI-powered web app (Python + Streamlit) that helps job seekers prepare better applications.
Upload a resume, paste a job description, and get a match score, skill-gap analysis, honest resume
improvements, a cover letter, interview practice and downloadable reports.

> Built for the **AI Growth & Automation Associate – Work From Home** assessment.
> Works **without any API key** (clearly labelled *Demo / Fallback mode*) and uses a **real LLM**
> (Google Gemini or OpenAI) when a key is configured.

## ✨ Features

| # | Feature | What it does |
|---|---------|--------------|
| 1 | Resume analysis | PDF upload (validated) or pasted text → skills, education, experience, projects, completeness check |
| 2 | Job matching | Extracts required/preferred skills, compares with resume, **score out of 100 with an explanation** |
| 3 | Resume improvement | Rewrites *your existing* bullets; never invents employers, metrics or tools; flags anything suspicious |
| 4 | Cover letter | Personalised, editable, downloadable (.txt / .md) |
| 5 | Interview prep | Technical + HR questions with answers grounded in your resume; "Generate more" |
| 6 | Skill gap | **Verified** vs **inferred** vs **missing** skills + learning topics and mini-projects |
| 7 | Reports | Markdown, text and CSV downloads (score, matched/missing skills, recommendations) |
| 8 | AI + automation | Gemini/OpenAI integration, structured JSON prompts, retries, graceful fallback, no key leakage |

## 🧰 Tech stack

- **Python 3.10+** (tested on 3.12), **Streamlit** UI, **Pandas** tables, **pypdf** PDF text extraction
- **python-dotenv** for configuration, **requests** for the LLM HTTP calls (no vendor SDK to install)
- **LLM providers:** Google Gemini (default model `gemini-2.5-flash`) or OpenAI (`gpt-4o-mini`).
  Models are configurable in `.env`; if a provider retires a model name, change it there.
- **Git/GitHub** for version control, **Streamlit Community Cloud** for hosting

## 🚀 Quick start (Windows + VS Code + PowerShell)

Full beginner-friendly guide: [`docs/LOCAL_SETUP_WINDOWS.md`](docs/LOCAL_SETUP_WINDOWS.md)

```powershell
# 1. Open the extracted folder in VS Code, then open Terminal > New Terminal
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

Your browser opens at <http://localhost:8501>. Click **⚡ Load demo data** in the sidebar to try everything instantly.
Stop the app with `Ctrl + C` in the terminal.

> If PowerShell says *"running scripts is disabled"*, run once:
> `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned` and activate again.

## 🔑 Optional: enable live AI

1. Copy the template: `Copy-Item .env.example .env`
2. Put **one** key in `.env` (get a free Gemini key at <https://aistudio.google.com/app/apikey>):
   ```
   GEMINI_API_KEY=your_key_here
   ```
3. Restart the app. The sidebar badge changes from **DEMO MODE** to **LIVE AI**.

You can also paste a key in the sidebar (🔑 expander) – it is kept in the browser session only.
`.env` is listed in `.gitignore`, so it will never be committed.

## 🧪 Run the tests

```powershell
python -m pip install -r requirements-dev.txt
python -m pytest -v
```
Tests use fake HTTP responses, so no internet or API key is needed.

## 📁 Project structure

```
AI-CareerPilot/
├── app.py                      # Streamlit UI (sidebar navigation, 8 pages)
├── config.py                   # Settings from .env / environment / Streamlit secrets
├── requirements.txt            # Runtime dependencies
├── requirements-dev.txt        # + pytest
├── .env.example  .gitignore
├── .streamlit/config.toml      # Theme + upload limit
├── modules/
│   ├── resume_parser.py        # PDF validation/extraction + structured analysis
│   ├── job_analyzer.py         # JD parsing + match scoring (verified/inferred/missing)
│   ├── ai_service.py           # Gemini/OpenAI client, retries, typed errors
│   ├── prompt_templates.py     # All LLM prompts (documented in prompts/)
│   ├── resume_optimizer.py     # Bullet improvement + guardrails
│   ├── cover_letter.py         # Cover letter generation
│   ├── interview_generator.py  # Technical + HR questions and grounded answers
│   ├── skill_gap.py            # Learning recommendations
│   ├── report_generator.py     # Markdown / text / CSV reports
│   ├── skills_db.py            # Skill taxonomy, related skills, learning plans
│   └── text_utils.py           # Helpers + hallucination (grounding) checks
├── prompts/prompt_documentation.md
├── tests/test_basic.py
├── docs/                       # Report, video script, setup, deployment, GitHub, checklist, troubleshooting
└── sample_data/                # Fictional sample resume (.txt/.pdf) and job description
```

## 🛡️ Responsible-AI design

- **No invented facts.** Prompts forbid fabricating employers, degrees, projects, tools or metrics, and the app
  *checks* AI output: numbers or technologies that are not in your resume trigger a visible warning.
- **Verified vs inferred.** A skill is *verified* only if it appears on the resume. *Inferred* skills (related
  technology only) count partially in the score but are never claimed in generated letters or answers.
- **Honest labelling.** Every generated item is marked as a suggestion to review, and the app states whether it
  came from a live AI model or the rule-based fallback.
- **Privacy.** Nothing is stored on disk. With a live key, the text you submit is sent to the chosen AI provider.

## ⚠️ Known limitations

- Skill detection uses a built-in list of ~100 skills; niche skills will not be detected.
- Scanned (image-only) PDFs cannot be read – paste the text instead.
- Fallback mode produces templated text and outlines, not creative writing.
- Experience years are estimated from dated roles only.

## 📚 Documentation

| Doc | Purpose |
|-----|---------|
| [`docs/LOCAL_SETUP_WINDOWS.md`](docs/LOCAL_SETUP_WINDOWS.md) | Windows + VS Code setup, step by step |
| [`docs/GITHUB_SUBMISSION_GUIDE.md`](docs/GITHUB_SUBMISSION_GUIDE.md) | Publish on GitHub |
| [`docs/DEPLOYMENT_GUIDE.md`](docs/DEPLOYMENT_GUIDE.md) | Deploy on Streamlit Community Cloud |
| [`docs/SUBMISSION_CHECKLIST.md`](docs/SUBMISSION_CHECKLIST.md) | Deliverables, video, email template |
| [`docs/VIDEO_PRESENTATION_SCRIPT.md`](docs/VIDEO_PRESENTATION_SCRIPT.md) | 2–3 minute script |
| [`docs/PROJECT_REPORT.md`](docs/PROJECT_REPORT.md) | Full project report |
| [`prompts/prompt_documentation.md`](prompts/prompt_documentation.md) | Prompt engineering record |
| [`docs/TROUBLESHOOTING.md`](docs/TROUBLESHOOTING.md) | Fixes for common errors |

## 📄 License / data

Sample data is entirely fictional. No real personal information, resumes or API keys are included.
# AI-CareerPilot
# AI-CareerPilot
