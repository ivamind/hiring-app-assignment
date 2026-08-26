# Take-Home Assignment — Full Stack Developer

**What this is:** Some coding fun. Build at your own pace. All five parts below are required — we expect a working version of every one of them.

**How to submit:** Push the code to a public GitHub repository and email us the link by the deadline given to you.

**Need more time?** Just ask. Tell us before the deadline and we will extend it.

---

## About the product

We are building a hiring platform.

Resumes are hard to compare, and anyone can write anything in them. Our product replaces the resume with a **skills profile** — a fixed list of skills, each with a rating. The job has one, the candidate has one, and because both use the same list you can compare them directly.

Instead of a recruiter making 50 phone calls, our system runs the first interview round itself:

1. The recruiter says which skills the job needs.
2. An AI generates interview questions for those skills.
3. The candidate gets a link, opens it, and **answers by speaking**.
4. The system converts the speech to text and scores the answers.
5. The recruiter sees a score, a short summary, and the full transcript.

**Your assignment is to build a small working version of all five steps.** Parts 1 to 5 below map onto these steps one for one, and all five are part of the assignment — not a menu to choose from.

---

## What to build

There are five parts. **Complete all five.** They build on each other, so the order below is also the order we suggest you work in.

### Part 1 — Create a job with skills

A recruiter logs in and creates a job. The job has a title and a list of required skills.

Every skill has two things:

- a **dimension** — one of `knowledge`, `applied_skill`, `tool`, `responsibility`, `context`, `attribute`
- a **required rating** from 1 to 5

Do not invent your own skill list — use the attached `skills_seed.json`, which has around 40 skills already grouped by dimension.

*Example:* Job = "Backend Developer". Skills = Python (rating 4), PostgreSQL (rating 3), REST API design (rating 4).

### Part 2 — Generate interview questions

Add an endpoint like `POST /jobs/{id}/interview`. It should use an AI model to create **5 interview questions** from the job's skills.

Important: **save which skill each question is testing.** If you cannot tell us which skill a question came from, that is a bug.

Generate the questions once and save them. Do not call the AI again on every page load.

### Part 3 — The candidate link

Generating an interview should produce a **shareable link containing a token**:

```
http://localhost:3000/interview/8f3a9c2e-....
```

The candidate opens this link and:

- **does not create an account and does not log in**
- sees the 5 questions, one at a time
- **records an audio answer in the browser** for each question
- the audio is uploaded and saved
- the audio is converted into text (a transcript)

Rules for the link:

- It should work only once, and it should stop working after some time. You decide how long.
- Whoever holds this link is a stranger on the internet. The token must not expose any other data in your system.

> **About the AI and speech-to-text:** Use any provider — OpenAI, Claude, Gemini, Whisper, a local model. If you do not want to spend money on API calls, put the AI and speech-to-text behind an interface and commit a fake version returning fixed text. We are looking at your design, not your API bill.

### Part 4 — Scoring

After all 5 answers are recorded, score the interview:

- a **rating from 1 to 5 for each skill** that was tested
- an **overall Fit Score: High, Medium or Low**
- a **3-line summary** of the candidate

The score for a skill must come from what the candidate actually said in the transcript. Explain in your README how you decided High vs Medium vs Low.

### Part 5 — Recruiter screen

A simple React UI:

- a list of jobs
- for each job, the interviews and their status (not started / in progress / completed)
- an interview detail page showing the Fit Score, the rating for each skill, the summary, each question with its transcript, and an audio player for each answer

Keep the UI simple. We are **not** judging the design or the CSS.

---

## Technology

| Part | What to use |
|---|---|
| Backend | Python — FastAPI preferred. Django or Flask is also fine. |
| AI | **LangChain or LangGraph** (see below) |
| Frontend | React |
| Database | PostgreSQL, Supabase or SQLite — your choice |
| Running it | Must run on our laptop using the commands in your README. No deployment needed. |

### Please use LangChain or LangGraph

Build the AI parts — question generation and scoring — with **LangChain or LangGraph**. This is what we use, so we want to see how you work with it.

Two things we want to see:

- **Structured output.** The AI returns text, but your database needs proper fields. Use the framework's structured-output support so a question or score comes back in a fixed shape.
- **A clear chain or graph.** The steps — take the skills, generate questions, read the transcript, produce a score — should be visible as a chain or graph in your code, not one giant prompt inside a function.

Never used them before? That is fine — learning is part of the assignment. Say so in your DECISIONS.md and tell us what you found confusing.

---

## Using AI assistants — please read

**You are allowed to use AI coding assistants.** Claude Code, Cursor, Copilot, ChatGPT — whatever you normally use. We use them every day ourselves and are not trying to catch you.

**But there is one condition: you must fully understand every line of code in your repository.**

In the next round we will open your repository, ask you to change your own code while we watch, and ask why you built it that way.

So please do not paste in code you have not read. If an assistant gives you something you do not understand, either understand it or write it yourself in a simpler way.

---

## What we will look at

- **The candidate link.** Is the token limited to that one interview? Does it expire? Can it be used to read someone else's data?
- **AI output you can rely on.** What happens when the model returns something broken or in the wrong format?
- **Traceability.** Can we see which skill each question came from, and which part of the transcript each score came from?
- **The boring failure cases.** A silent 30-second recording. An upload that fails halfway. A candidate who closes the tab after question 2.
- **Clean code, a sensible database design, and commits we can follow.**

## What your repository must contain

1. **README.md** — how to run the project, and an honest account of anything that is not working. We are expecting all five parts; where something is incomplete, saying so plainly is far better than leaving us to find it.
2. **DECISIONS.md** — half a page. Three or four decisions and why. Include one thing you would do differently with more time.
3. **Real commit history.** Commit as you go. One big commit tells us nothing about how you work, and we will ask about it.

## Things we have deliberately not told you

Where to store the audio, how long the link stays valid, what to do with an empty or off-topic answer. Decide these yourself, and be ready to explain your choice.

## If you run short of time

**Ask for more time — do not quietly drop a part.** All five parts are expected, and the deadline is the flexible piece, not the scope. Tell us before the deadline and we will extend it. We would far rather work with an engineer who speaks up early than one who quietly ships something broken.

Two things are genuinely up to you, and neither counts as skipping a part:

- **Depth over polish.** A part that works simply beats a part that is half built. The recruiter UI in Part 5 can be a rough page — we are not judging CSS.
- **Typed answers as a fallback.** If browser audio recording defeats you, let the candidate **type** the answer instead, and say so in your README. The rest of Part 3 and all of Part 4 still apply, and the scoring logic is the same either way.

If something still ends up unfinished, write it down in your README and tell us how you would have done it. Handing us a gap you have explained is recoverable; handing us one you have not is what costs you.

---

If anything here is unclear, please email us. Asking a question is not a negative mark.

---

© 2026 IITM Pravartak Technologies Foundation.
