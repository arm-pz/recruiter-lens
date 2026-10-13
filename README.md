# recruiter-lens

An agent skill that evaluates job-search materials from a recruiter's perspective — documented screening patterns, not generic career advice.

## What it does

- **6-second resume scan** — simulates a recruiter's first impression
- **Deep resume critique** — strengths, weaknesses, red flags with specific fixes
- **ATS compatibility check** — formatting and parsing problems before they corrupt or drop your content
- **Rejection-reason analysis** — the common triggers (gaps, job-hopping, generic summaries) and how to mitigate each
- **Interview question prediction** — likely questions derived from resume gaps + job description
- **Gap analysis & tailoring** — requirement coverage vs. a specific role
- **LinkedIn profile audit** — discoverability and credibility for recruiter searches
- **AI usage guidelines** — green/yellow/red-light rules for using AI authentically in a job search

## Core principle

Optimize presentation of real experience, never fabricate it. The skill refuses to invent achievements, skills, or metrics — numbers only ever come from the candidate. It treats submitted materials as private, avoids inferring protected characteristics, and flags bias-prone screening patterns as tendencies to name, not hurdles to hide.

## Install

Copy the `skills/recruiter-lens/` directory into the skills directory supported by your AI agent:

```text
.claude/skills/recruiter-lens/
.agents/skills/recruiter-lens/
.cursor/skills/recruiter-lens/
.qoder/skills/recruiter-lens/
```

Or install via the Skills CLI:

```bash
npx skills add arm-pz/recruiter-lens --skill recruiter-lens
```

Or as a Claude Code plugin from the caffeinity-skills marketplace:

```
/plugin marketplace add arm-pz/caffeinity-skills
/plugin install recruiter-lens@caffeinity-skills
```

## Usage

```
/recruiter-lens scan        # first-impression simulation
/recruiter-lens critique    # deep resume review
/recruiter-lens ats-check   # ATS parse verification
/recruiter-lens reject-reasons
/recruiter-lens linkedin-audit
/recruiter-lens predict-questions
/recruiter-lens gap-analysis
/recruiter-lens tailor
/recruiter-lens ai-guidelines
/recruiter-lens format-fix
/recruiter-lens keyword-match
/recruiter-lens impact-boost
/recruiter-lens red-flag-review
```

Natural language works too: "Why would this resume get rejected?" routes to `reject-reasons`.

## Pairs with job-lens

This skill judges; the sibling [job-lens](https://github.com/arm-pz/job-lens) skill produces — it takes these findings as input and writes the finished material (tailored resume, new bullets, summaries, LinkedIn rewrite, interview answer pack). Typical flow: `/recruiter-lens critique` → hand to `/job-lens` → back to `ats-check` before you send.

`tailor` here reports requirement coverage and repositioning suggestions against a specific JD; full document rewriting belongs to job-lens (and stays honest either way — numbers only ever come from the candidate).

> Naming note: unrelated to `dani-aisystems/recruiter-lens`, which is a separate GitHub-auditing MCP server that happens to share the name. This repo is the skill by arm-pz.

## Structure

```
recruiter-lens/
├── README.md
├── skills/
│   └── recruiter-lens/
│       ├── SKILL.md                  # command routing, workflow, safety rules
│       ├── examples/
│       │   └── example.md            # worked scan + impact-boost example
│       └── references/
│           ├── commands.md           # per-command behavior specs
│           ├── recruiter-criteria.md # screening tendencies, not measured rules
│           ├── ats-specs.md          # ATS parsing rules by platform
│           ├── rejection-patterns.md # 10 rejection patterns + mitigations
│           ├── output-formats.md     # standardized report templates
│           └── quality-checklist.md  # pre-submission checklists
└── tests/
    ├── test-discovery.md             # activation / non-activation intents
    └── test-prompts.md               # per-command test prompts + expectations
```

## License

MIT — see [LICENSE](LICENSE).
