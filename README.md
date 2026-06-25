# Angela Kingdon — AI Career Agent

A persistent, git-backed job-search system run by Claude Code acting as Angela's executive search consultant. Goal: **maximize compensation × probability of interview, minimize her time.** Quality over quantity, always.

## How it works
Each session/day the agent reads `profile/angela-kingdon.md` + `AGENT.md`, searches the watchlist, scores new roles on the rubric, logs everything to `data/jobs.csv`, and writes a brief to `reports/`. Only roles scoring ≥ 8.0 are recommended.

## Structure
```
profile/angela-kingdon.md   # Candidate facts — source of truth (never fabricate beyond this)
AGENT.md                    # Operating spec: daily loop, scoring rubric, hard rules
data/jobs.csv               # Database of every role reviewed (NEW/SAVED/APPLIED/REJECTED/...)
reports/YYYY-MM-DD.md       # Daily briefs
resumes/masters/            # <-- DROP YOUR MASTER RESUME(S) HERE (currently empty)
resumes/tailored/           # Generated per-role tailored resumes
cover-letters/              # Generated bespoke cover letters
outreach/                   # Networking / LinkedIn message drafts
```

## To start a daily run
Open a Claude Code session in this repo and say: **"Run today's job search."** The agent will dedupe against `data/jobs.csv`, surface only new ≥8.0 roles, and update the database + a dated report.

## ⛔ Action needed from Angela
1. Add **master résumé(s)** to `resumes/masters/` — this unblocks tailored résumés and stronger cover letters.
2. Decide the **Anthropic Institute / relocation** question (see latest report).
3. Choose how you want **daily runs scheduled** (automated trigger vs. on-demand).

## Environment note
Direct job-board scraping (`curl`, and `WebFetch` on Greenhouse/Lever/Ashby/LinkedIn) is blocked in this environment. `WebSearch` is the live-data engine; verify comp/dates/live-status at each source URL before applying.
