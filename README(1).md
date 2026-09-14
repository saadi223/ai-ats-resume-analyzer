# AI ATS Resume Analyzer

An AI-powered web application that compares a candidate's resume with a job description and provides an estimated ATS compatibility score, matching skills, missing keywords, improvement suggestions, formatting feedback, and an improved professional summary.

The application is built with **Python**, **Streamlit**, and the **Google Gemini API**. It supports selectable-text PDF, DOCX, and TXT resumes.

> **Important:** The ATS score is an AI-generated estimate. Real employers use different applicant tracking systems, evaluation rules, and hiring processes. This application does not guarantee an interview or job offer.

## Features

- Upload resumes in PDF, DOCX, or TXT format
- Paste any job description for role-specific analysis
- Generate an estimated ATS match score out of 100
- Identify skills already present in the resume
- Highlight missing keywords and job requirements
- Review resume strengths and weaknesses
- Receive practical ATS formatting feedback
- Generate an improved professional summary
- Download the improved summary as a TXT file
- Keep the Gemini API key protected with Streamlit Secrets

## How It Works

1. The user uploads a resume.
2. The app extracts text from the uploaded document.
3. The user pastes the target job description.
4. The extracted resume and job description are sent to Gemini for comparison.
5. Gemini evaluates the resume using a defined scoring rubric.
6. Streamlit displays the score and recommendations in a simple dashboard.

## ATS Scoring Rubric

| Evaluation area | Maximum score |
|---|---:|
| Relevant skills and keywords | 35 |
| Relevant experience and achievements | 25 |
| Education and certifications | 15 |
| ATS readability and structure | 15 |
| Professional summary and job alignment | 10 |
| **Total** | **100** |

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Application logic |
| Streamlit | Web interface and deployment |
| Google Gemini | AI-based resume analysis |
| Google Gen AI SDK | Connection with the Gemini API |
| PyPDF | PDF text extraction |
| python-docx | DOCX text extraction |

## Project Structure

```text
ai-ats-resume-analyzer/
├── app.py
├── requirements.txt
├── README.md
└── .gitignore
```

## Supported Resume Formats

| Format | Support | Notes |
|---|---|---|
| PDF | Yes | PDF must contain selectable text |
| DOCX | Yes | Paragraphs and tables are extracted |
| TXT | Yes | UTF-8 text is recommended |
| Scanned PDF | Not yet | OCR is required for image-based documents |

## Getting a Gemini API Key

1. Visit [Google AI Studio](https://aistudio.google.com/apikey).
2. Sign in with a Google account.
3. Select **Create API key**.
4. Select or create a Google Cloud project.
5. Copy the generated API key.
6. Keep the key private and never upload it to GitHub.

## Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/ai-ats-resume-analyzer.git
cd ai-ats-resume-analyzer
```

Replace `YOUR-USERNAME` with your GitHub username.

### 2. Create a virtual environment

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

macOS or Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install the dependencies

```bash
pip install -r requirements.txt
```

### 4. Create the Streamlit secrets file

Create this folder and file inside the project:

```text
.streamlit/
└── secrets.toml
```

Add the following content to `secrets.toml`:

```toml
GEMINI_API_KEY = "YOUR_ACTUAL_API_KEY"
```

The `.gitignore` file prevents `secrets.toml` from being uploaded to GitHub.

### 5. Start the application

```bash
streamlit run app.py
```

Streamlit will show a local address, usually `http://localhost:8501`.

## Deploy on Streamlit Community Cloud

### Step 1: Upload the project to GitHub

Make sure the repository contains:

- `app.py`
- `requirements.txt`
- `README.md`
- `.gitignore`

Do not upload `.streamlit/secrets.toml` or your API key.

### Step 2: Create the Streamlit app

1. Visit [Streamlit Community Cloud](https://share.streamlit.io/).
2. Sign in using GitHub.
3. Select **Create app**.
4. Choose the GitHub repository.
5. Select the `main` branch.
6. Enter `app.py` as the main file path.

### Step 3: Add the API key

Open **Advanced settings** or the app's **Secrets** settings and enter:

```toml
GEMINI_API_KEY = "YOUR_ACTUAL_API_KEY"
```

Select **Save** and then deploy or reboot the application.

## Requirements

The `requirements.txt` file should contain:

```text
streamlit
google-genai
pypdf
python-docx
```

The Gemini integration uses the current Google Gen AI SDK and the Interactions API:

```python
response = client.interactions.create(
    model="gemini-3.6-flash",
    input=prompt,
)
```

## How to Use the App

1. Open the deployed Streamlit application.
2. Upload a PDF, DOCX, or TXT resume.
3. Paste the complete job description.
4. Select **Analyze My Resume**.
5. Wait for the analysis to finish.
6. Review the ATS score, matching skills, missing keywords, and recommendations.
7. Download the improved professional summary if required.

For a meaningful result, always use the full job description instead of only the job title.

## Security and Privacy

- Never write the Gemini API key directly inside `app.py`.
- Never commit `.streamlit/secrets.toml` or `.env` files.
- Uploaded resumes are processed during the active Streamlit session.
- Avoid uploading documents containing unnecessary sensitive information.
- Before public or commercial use, review Gemini and Streamlit data-handling policies.

## Common Errors

### `GEMINI_API_KEY is missing`

Add the following entry to Streamlit Secrets:

```toml
GEMINI_API_KEY = "YOUR_ACTUAL_API_KEY"
```

Save the settings and reboot the application.

### `404 NOT_FOUND` or model unavailable

Confirm that `app.py` uses the model and API supported by your Gemini account:

```python
response = client.interactions.create(
    model="gemini-3.6-flash",
    input=prompt,
)
```

Also ensure that `requirements.txt` contains `google-genai` without an outdated pinned version.

### `IndentationError`

Python requires consistent indentation. Use four spaces inside each function or conditional block and do not mix tabs with spaces.

### `429 quota exceeded`

The Gemini API usage limit has been reached. Check the API quota in Google AI Studio or wait for it to reset.

### Very little text was extracted

The PDF may be a scanned image. Upload the original DOCX file or convert the document into a selectable-text PDF.

### `ModuleNotFoundError`

Check that the filename is exactly `requirements.txt`, all required packages are listed, and the file is located beside `app.py`.

## Limitations

- The score is an estimate rather than an official ATS result.
- AI output can occasionally be incomplete or inaccurate.
- Different employers prioritize different resume sections.
- Scanned PDFs cannot be processed without OCR.
- The app does not verify whether a candidate genuinely possesses a listed skill.
- Users should review every generated suggestion before changing their resumes.

## Future Improvements

- OCR support for scanned resumes
- Multiple resume comparison
- Role-specific keyword suggestions
- Resume section detection
- ATS-friendly resume rewriting
- Downloadable PDF analysis report
- Cover-letter generation based on the job description
- Analysis history for returning users

## Responsible Use

Only include skills, qualifications, experience, and achievements that are true. The application should improve how genuine experience is presented, not manufacture information.

## Contributing

Contributions and suggestions are welcome.

1. Fork the repository.
2. Create a new branch.
3. Make and test your changes.
4. Submit a pull request with a clear explanation.

## License

This project is provided for educational and portfolio purposes. Add a license file before allowing reuse or redistribution under specific terms.

## Author

**Muhammad Saad Hanif**

Mechanical Engineering graduate building AI, machine learning, agentic AI, and engineering automation projects.

If you find this project useful, consider starring the repository and sharing constructive feedback.
