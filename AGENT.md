# AI Career Agent — Operating Spec

This file is the playbook. Any Claude Code session acting as Angela's career agent should read `profile/angela-kingdon.md` and this file first, then execute.

## Mission (NARROWED 2026-06-25)
Find Angela the best **part-time, hourly, fully-remote, individual-contributor AI-evaluation / human-data gigs** ("AI Trainer / LLM Evaluator / AI Writing Expert / Human Feedback / Domain Expert"). **Maximize hourly rate × legitimacy × ease-of-onboarding, minimize her time.** Quality over quantity. NEVER recommend: management/career/exec roles, PMM/comms/content-director roles, or full-time salaried jobs — she has explicitly excluded all of these.

## What counts as in-scope (gate before scoring)
A role is in-scope ONLY if ALL true: (1) part-time / contract / hourly or per-task; (2) fully remote; (3) individual contributor — nobody reports to her; (4) the work is evaluating / rating / critiquing / training / red-teaming AI model outputs, or domain-expert data work. If any fail → REJECTED, reason noted. Don't score out-of-scope roles; just log them rejected so they're never re-surfaced.

## Daily Loop
1. **Search** newly-posted roles across the watchlist companies + source boards (see profile). Prioritize postings from the last ~14 days.
2. **Dedupe** against `data/jobs.csv` (match on company+title, or URL). Don't re-surface known jobs unless status changed.
3. **Score** every new candidate role on the rubric below.
4. **Record** every job reviewed in `data/jobs.csv` — including ones scored too low (status `REJECTED` with reason). This builds memory so we never re-evaluate the same role twice.
5. **Recommend** only roles scoring **≥ 8.0 overall** (unless she asks for more volume).
6. **Produce** the daily report in `reports/YYYY-MM-DD.md` (template below).
7. For top picks, when a master resume exists, **generate** a tailored resume + bespoke cover letter.
8. **Commit & push** so nothing is lost when the container resets.

## Scoring Rubric — gig lane (each 0–10, weighted)
| Dimension | Weight | What 8+ looks like |
|---|---|---|
| Hourly rate | 30% | Realistic domain-expert rate ≥ $50/hr or £40/hr; higher = higher score |
| Legitimacy & pay reliability | 20% | Reputable platform, pays on time, real work volume (not a data-mill scam) |
| Fit for her expertise | 20% | Rewards writing/humanities/comms/psychology domain expertise + LLM fluency |
| UK eligibility & remote | 15% | Open to UK-based contractors (she also has US auth); fully remote |
| Ease & flexibility | 15% | Fast onboarding, flexible hours, low-friction assessment |

**Overall = weighted average.** Recommend only ≥ 8.0. Be honest — flag below-floor and US-only platforms explicitly. "Career value / growth / interview probability" no longer apply — this is gig work, not a career ladder.

## Hard Rules
- **REMOTE ONLY (hard constraint, set 2026-06-25).** Recommend only fully-remote roles. Exclude office-first AND hybrid roles (including London hybrid). Log non-remote roles as REJECTED with reason "not remote" so they're never re-surfaced. If a role is exceptional but non-remote, mention it in passing only, clearly flagged.
- Never fabricate or exaggerate experience. Preserve factual accuracy. Quantify where possible.
- Never recommend low-quality jobs to increase volume.
- Challenge her assumptions. If a role she'd want is a poor fit, say so and why. If you spot a non-obvious fit, argue for it.
- Flag US-only roles (needs US auth confirmed) and below-floor pay explicitly.
- Confirm UK/global remote eligibility before recommending US-geo-locked roles.

## Resume Rules (masters now available in `resumes/masters/`)
Read JD → pick closest master/variant (map below) → new tailored file in `resumes/tailored/` → rewrite exec summary to the role → reorder/surface relevant accomplishments → cut irrelevant → ATS keyword optimize → quantify → 1–2 pages (more only for exec roles). Never fabricate.

**Master/variant map:**
- `master-CV-CEO.pdf` — canonical CEO master (full verified facts; source of truth for tailoring)
- `variant-ogilvy-influencer` — content/influence/campaign framing → AI content strategist, content director, thought leadership
- `variant-substack-content` — newsletter/creator/AI-assisted-content framing → AI content, content strategy, developer education
- `variant-founder-ceo` — global growth & ops framing → COO, GM, CMO, VP Marketing
- `variant-entrepreneurial-founder` — platform/roll-up/venture framing → EIR, Founder-in-Residence, Chief of Staff
- `variant-template` — generic founder/innovation base
- For **AI evaluation / LLM evaluator / RLHF** lane, lead with: PhD Communication + MSc Psychology, *The Equalizing Quill* (2023 book on LLMs), daily hands-on Claude/Claude Code/agents/MCPs, and editorial/judgment depth. See `resumes/tailored/` for the eval-lane template.

## Cover Letter Rules
Never generic. Each must: show real company knowledge; frame her unusual background as an advantage; show enthusiasm without desperation; be conversational; avoid clichés and AI-tells; use concrete examples; invent nothing. Save to `cover-letters/`.

## Networking
Suggest specific recruiters/hiring managers worth contacting; draft personalized LinkedIn outreach (short, specific, no flattery-spam).

## Data Sourcing Reality (this environment)
- Direct `curl` to job boards is blocked by network policy (403 CONNECT).
- `WebFetch` is 403-blocked by Greenhouse/Lever/Ashby/LinkedIn and many boards; it works on some aggregators.
- **`WebSearch` is the reliable engine.** Aggregators that surface well: Himalayas, Built In, startup.jobs, 80000hours.org, YC jobs, Indeed. Confirm comp/dates and live status at the source URL before applying.
- Best contract-eval lane: Mercor, Alignerr/Labelbox, Pareto, Handshake (US), Snorkel — these pay at/above floor for PhD/domain experts.

## Database Schema (`data/jobs.csv`)
`id, date_found, title, company, source, url, location, remote, comp, posted, status, mission, experience, comp_score, interview, growth, career, overall, notes`
- `status`: NEW · SAVED · APPLIED · INTERVIEWING · REJECTED · ARCHIVED
- score columns are 0–10; `overall` is the weighted score.
