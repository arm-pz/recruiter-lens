# recruiter-lens

An agent skill that evaluates job-search materials from a recruiter's perspective — evidence-based screening behavior, not generic career advice.

## What it does

- **6-second resume scan** — simulates a recruiter's first impression
- **Deep resume critique** — strengths, weaknesses, red flags with specific fixes
- **ATS compatibility check** — formatting and parsing failures before they silently reject you
- **Rejection-reason analysis** — the common triggers (gaps, job-hopping, generic summaries) and how to mitigate each
- **Interview question prediction** — likely questions derived from resume gaps + job description
- **Gap analysis & tailoring** — requirement coverage vs. a specific role
- **LinkedIn profile audit** — discoverability and credibility for recruiter searches
- **AI usage guidelines** — green/yellow/red-light rules for using AI authentically in a job search

## Core principle

Optimize presentation of real experience, never fabricate it. The skill refuses to invent achievements, skills, or metrics — numbers only ever come from the candidate.

## Install

Place the `recruiter-lens/` folder in your skills directory:

- Qoder CLI: `~/.qoder/skills/recruiter-lens/`
- Or any agent that reads `SKILL.md`

## Usage

```
/recruiter-lens scan        # 6-second recruiter impression
/recruiter-lens critique    # deep resume review
/recruiter-lens ats-check   # ATS parse verification
/recruiter-lens reject-reasons
/recruiter-lens predict-questions
/recruiter-lens gap-analysis
/recruiter-lens tailor
/recruiter-lens linkedin-audit
/recruiter-lens ai-guidelines
```

Natural language works too: "Why would this resume get rejected?" routes to `reject-reasons`.

## Structure

```
recruiter-lens/
├── SKILL.md                      # command routing, workflow, safety rules
└── references/
    ├── commands.md               # per-command behavior specs
    ├── recruiter-criteria.md     # what recruiters actually weigh
    ├── ats-specs.md              # ATS parsing rules by platform
    ├── rejection-patterns.md     # 10 rejection patterns + mitigations
    ├── output-formats.md         # standardized report templates
    └── quality-checklist.md      # pre-submission checklists
```
