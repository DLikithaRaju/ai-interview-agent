# AI Interview Agent

A backend-only AI technical interview agent built for the 24-Hour AI Agent Coding Challenge.

## Overview

The AI Interview Agent conducts a complete technical mock interview based on a target job role and required skills.

The agent:

1. Accepts a job role and required skills.
2. Generates 5 role-specific interview questions.
3. Collects candidate answers through the command line.
4. Evaluates all answers using Gemini.
5. Scores each answer across multiple dimensions.
6. Generates an overall candidate evaluation.
7. Saves the complete interview transcript as a JSON file.

The project is intentionally implemented as a lightweight Python backend/CLI without a frontend framework.

## Features

* Role-specific interview question generation
* Exactly 5 questions per interview session
* Candidate answer collection through CLI
* AI-powered answer evaluation
* Per-question scoring
* Technical accuracy assessment
* Relevance assessment
* Problem-solving assessment
* Communication assessment
* Overall candidate score
* Strengths and skill gaps
* Skill-wise assessment
* Hiring recommendation
* Complete interview transcript saved as JSON
* Retry handling for temporary Gemini API failures

## Tech Stack

* Python 3
* Google Gemini API
* Google GenAI Python SDK
* JSON
* Python Standard Library

## Architecture

The agent uses Gemini for two main AI tasks.

### 1. Question Generation

Gemini receives:

* Job role
* Required skills

It generates exactly 5 interview questions covering fundamentals, practical application, problem solving, scenarios, and technical depth.

### 2. Batch Answer Evaluation

After the candidate answers all five questions, the answers are sent to Gemini together.

Gemini evaluates each answer on:

* Technical Accuracy — 0 to 10
* Relevance — 0 to 10
* Problem Solving — 0 to 10
* Communication — 0 to 10

Python then calculates the final overall score deterministically.

This approach reduces unnecessary API calls and keeps the application simple and efficient.

## Project Flow

```text
Job Role + Skills
       |
       v
Gemini Question Generation
       |
       v
5 Interview Questions
       |
       v
Candidate Answers
       |
       v
Gemini Batch Evaluation
       |
       v
Per-Question Scores
       |
       v
Python Score Calculation
       |
       v
Final Evaluation
       |
       v
JSON Transcript
```

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/ai-interview-agent.git
cd ai-interview-agent
```

Install the required dependency:

```bash
pip install -r requirements.txt
```

Or:

```bash
pip install google-genai
```

## Gemini API Key

Open `interview_agent.py` and configure your Gemini API key:

```python
API_KEY = "YOUR_GEMINI_API_KEY"
MODEL_NAME = "gemini-3.6-flash"
```

Replace `YOUR_GEMINI_API_KEY` with your actual API key.

### Important Security Note

Never upload your real Gemini API key to GitHub.

For a public repository, use an environment variable or `.env` file instead of hardcoding the key.

If an API key is accidentally exposed, revoke it and generate a new one.

## Running the Agent

Run:

```bash
python interview_agent.py
```

The application will ask for the job role:

```text
Enter the job role: Data Analyst
```

Then enter the required skills:

```text
Enter required skills (comma-separated): Python, SQL, Excel, Pandas, Data Visualization
```

The agent will generate 5 questions and start the mock interview.

After all answers are submitted, the agent produces the final evaluation.

## Example

```text
AI INTERVIEW AGENT
Role-specific technical mock interview

Enter the job role: Data Analyst
Enter required skills (comma-separated): Python, SQL, Excel

INTERVIEW CONFIGURATION
Role: Data Analyst
Skills: Python, SQL, Excel
Questions: 5

Generating 5 role-specific questions...
```

After the interview:

```text
FINAL RESULT

Overall Score: 7.6/10
Performance: Strong
Recommendation: Hire

Strengths:
- Good understanding of Python fundamentals
- Strong analytical reasoning
- Clear explanation of solutions

Gaps:
- SQL optimization needs improvement
- Limited discussion of edge cases
- Could provide more detailed examples
```

## Output

After the interview, a complete transcript is saved in:

```text
data/interview_<id>.json
```

The transcript contains:

* Interview ID
* Timestamp
* Job role
* Required skills
* Questions
* Candidate answers
* Individual question scores
* Feedback
* Improvement suggestions
* Overall score
* Performance level
* Strengths
* Gaps
* Skill assessment
* Hiring recommendation

## Scoring

Each question is evaluated using four dimensions:

| Dimension          | Score |
| ------------------ | ----: |
| Technical Accuracy |  0–10 |
| Relevance          |  0–10 |
| Problem Solving    |  0–10 |
| Communication      |  0–10 |

The question score is calculated as:

```text
Question Score =
(Technical Accuracy +
 Relevance +
 Problem Solving +
 Communication) / 4
```

The final score is the average of the five question scores.

The calculation is performed in Python to keep the numerical result deterministic.

## Performance Levels

|  Score | Performance       |
| -----: | ----------------- |
| 8.5–10 | Excellent         |
| 7–8.49 | Strong            |
| 5–6.99 | Moderate          |
| 3–4.99 | Needs Improvement |
| 0–2.99 | Weak              |

## Design Decisions

### Why Gemini?

Gemini is used for tasks requiring natural-language understanding:

* Generating contextual interview questions
* Understanding candidate responses
* Evaluating technical answers
* Providing qualitative feedback

### Why five questions?

The challenge requires support for at least five questions. Five questions provide a complete demonstration while keeping the interview efficient.

### Why batch evaluation?

Instead of making a separate API request for every question, all five answers are evaluated in one Gemini request.

This reduces:

* API calls
* Latency
* Token overhead
* Implementation complexity

### Why calculate scores in Python?

LLMs are well suited to qualitative evaluation but deterministic calculations are better handled by traditional code.

Therefore:

```text
Gemini → Evaluation
Python → Score Calculation
```

This makes the final scoring process more predictable.

### Why a CLI instead of a frontend?

The challenge states that a UI is optional. A clean backend/CLI implementation demonstrates the complete agent workflow without adding unnecessary frontend complexity.

## Project Structure

```text
ai-interview-agent/
│
├── interview_agent.py
├── README.md
├── requirements.txt
├── .gitignore
│
└── data/
    └── .gitkeep
```

## Challenge Requirements

| Challenge Requirement    | Implementation                                      |
| ------------------------ | --------------------------------------------------- |
| Role-specific questions  | Gemini generates questions based on role and skills |
| Candidate answers        | CLI input                                           |
| Answer scoring           | Four evaluation dimensions                          |
| At least 5 questions     | Exactly 5 questions                                 |
| Overall evaluation       | Score, strengths, gaps and recommendation           |
| Interview transcript     | JSON output                                         |
| End-to-end functionality | Complete CLI workflow                               |
| Backend/CLI              | Python                                              |
| Documentation            | README                                              |

## Future Improvements

Possible future enhancements include:

* Voice-based interview input
* Speech-to-text transcription
* Adaptive questioning based on previous answers
* Difficulty adjustment
* Resume-based question generation
* Interview history and analytics
* Web interface
* Authentication
* Database storage
* More detailed role-specific scoring rubrics

## License

This project was created as part of an AI Agent coding challenge and is intended for educational and portfolio purposes.
