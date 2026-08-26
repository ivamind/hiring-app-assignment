# Hiring App — Take-Home Assignment

This repository holds the take-home assignment for the **Full Stack Developer** role at
IITM Pravartak Technologies Foundation.

## What is here

| File | What it is |
|---|---|
| [`iitmpravartak_take_home_assignment.md`](iitmpravartak_take_home_assignment.md) | The assignment brief — read this first. |
| [`skills_seed.json`](skills_seed.json) | The fixed skill list (~40 skills, grouped by dimension) your job and candidate profiles must use. Do not invent your own skills. |

## The short version

Build a small working version of a hiring platform that replaces the resume with a
**skills profile**. There are five parts and **all five are required**:

1. A recruiter creates a job with required skills and ratings.
2. An AI generates 5 interview questions from those skills.
3. The candidate opens a tokenised link — no login — and answers by speaking.
4. The audio is transcribed.
5. The recruiter sees a Fit Score, per-skill ratings, a summary, and the transcript.

Backend in Python (FastAPI preferred), AI parts in **LangChain or LangGraph**, frontend in
React, database of your choice. Full details, the build order, and what we will look at are
all in the assignment brief.

If the deadline is too tight to finish all five, tell us before it passes and we will extend
it — that is the piece we can move. Dropping a part is not.

## How to submit

1. Push your code to a **public GitHub repository** of your own.
2. Email us the link before the deadline you were given.

Your repository must contain a `README.md` (how to run it, and what you did not finish),
a `DECISIONS.md` (three or four decisions and why), and a real commit history.

## Questions

If anything is unclear, email us. Asking a question is not a negative mark. If the deadline
is too tight, tell us before it passes and we will extend it.

---

© 2026 IITM Pravartak Technologies Foundation.
