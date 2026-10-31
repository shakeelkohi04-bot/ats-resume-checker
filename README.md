# ats-resume-checker# 📄 ATS Resume Checker

A Streamlit app that scores a resume for Applicant Tracking Systems (ATS) and tells you exactly how to improve it, powered by Google Gemini Flash.

## Features
- Upload a resume as **PDF or DOCX**
- Optional **job description** for role-specific scoring and keyword gaps
- Overall ATS score (0-100) plus breakdown: formatting, keywords, experience, education, readability
- Strengths, weaknesses, missing keywords
- Prioritised improvements and rewritten bullet points
- Download the report as JSON

## Project structure
```
.
├── app.py             # Streamlit app
├── requirements.txt   # Python dependencies
├── README.md
└── .gitignore
```

## Run locally
1. Get a free API key from [Google AI Studio](https://aistudio.google.com/apikey).
2. Install and run:
   ```bash
   python -m venv .venv
   source .venv/bin/activate        # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. Provide the key, either way:
   - Create `.streamlit/secrets.toml`:
     ```toml
     GEMINI_API_KEY = "your-key-here"
     ```
   - or set an environment variable (`export GEMINI_API_KEY=...` / `set GEMINI_API_KEY=...` on Windows)
   - or just paste it into the app's sidebar.
4. Start the app:
   ```bash
   streamlit run app.py
   ```

## Configuration
| Name | Purpose | Default |
|------|---------|---------|
| `GEMINI_API_KEY` | Your Gemini API key | none (required) |
| `GEMINI_MODEL` | Gemini model to use | `gemini-flash-latest` |

If you get a "model not found" error, set `GEMINI_MODEL` to a model listed in the [Gemini docs](https://ai.google.dev/gemini-api/docs/models).

## Deploy on Streamlit Community Cloud
1. Push this repo to GitHub (never commit your API key).
2. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
3. Click **Create app**, choose your repo, branch `main`, main file `app.py`.
4. Open **Advanced settings → Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```
5. Click **Deploy**.

## Notes and limitations
- Scanned or image-only PDFs have no readable text; ATS systems can't read them either. Use a text-based PDF or DOCX.
- The score is an AI estimate of ATS-friendliness, not the output of a real ATS. Use it as guidance.
- Resume text is sent to Google's Gemini API for analysis. Don't use it with documents you aren't allowed to share.
