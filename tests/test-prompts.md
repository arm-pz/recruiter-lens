# Test Prompts

Each prompt below should route to the named command and produce behavior
described in `references/commands.md`. Run these against a sample resume
(the synthetic one in `skills/recruiter-lens/examples/example.md` works)
and, where noted, a job description.

Global expectations for every command:

- No fabricated metrics. Any precise number must come from the candidate's
  input; otherwise use an explicitly framed approximation or a bracketed
  prompt like `[quantify: how many users?]`.
- Output follows the matching template in `references/output-formats.md`.
- Findings are prioritized; fixes are actionable.

## scan

**Input:** `/recruiter-lens scan` + resume text

**Expected:** 6-second first-impression simulation: what the recruiter
notices first (role fit, tenure, red flags), overall first-pass verdict
(pass / pass-with-questions / reject), and the 2-3 things that decide it.

## critique

**Input:** `/recruiter-lens critique` + resume text

**Expected:** Section-by-section review weighted by recruiter priorities
(summary, experience bullets, skills, education), specific rewrite
suggestions, and a top-5 fixes list ordered by impact.

## ats-check

**Input:** `/recruiter-lens ats-check` + resume text (or PDF path)

**Expected:** Parsing verdict against `references/ats-specs.md`: column
layout, fonts, special glyphs, headers/footers containing contact info,
section-header recognition, keyword coverage. Lists each failing item
with the fix.

## reject-reasons

**Input:** `/recruiter-lens reject-reasons` + resume text

**Expected:** Likely rejection triggers drawn from
`references/rejection-patterns.md`, each tied to the exact line/section
that causes it, plus the mitigation.

## linkedin-audit

**Input:** `/recruiter-lens linkedin-audit` + profile text or screenshot

**Expected:** Audit of headline, about, experience alignment with resume,
and recruiter-search keywords. If only a resume is provided, explicitly
downgrade to a resume-derived audit and request the profile text or a
screenshot.

## predict-questions

**Input:** `/recruiter-lens predict-questions` + resume text + job description

**Expected:** Likely interview questions derived from resume claims and
JD requirements, grouped by type (experience probe, gap challenge,
technical deep-dive, behavioral), each with what a good answer must cover.

## gap-analysis

**Input:** `/recruiter-lens gap-analysis` + resume text + job description

**Expected:** Required-vs-demonstrated matrix: matched skills, partially
evidenced skills, and true gaps — each gap labeled fatal, bridgeable, or
cosmetic with a bridging strategy.

## tailor

**Input:** `/recruiter-lens tailor` + resume text + job description

**Expected:** Restructured summary and reordered/rewritten bullets keyed
to the posting's priorities, using only the candidate's real experience;
missing-evidence keywords flagged rather than invented.

## ai-guidelines

**Input:** `/recruiter-lens ai-guidelines`

**Expected:** Rules for authentic AI-assisted job search: AI for structure
and language, never for fabricated experience or metrics; candidate must
verify and own every claim.

## format-fix

**Input:** `/recruiter-lens format-fix` + resume text

**Expected:** Concrete formatting corrections (dates, bullet style,
consistency, whitespace) presented as before/after pairs.

## keyword-match

**Input:** `/recruiter-lens keyword-match` + resume text + job description

**Expected:** Keyword table: term, present/absent in resume, where to add
it naturally — without keyword stuffing.

## impact-boost

**Input:** `/recruiter-lens impact-boost` + resume text

**Expected:** Weak bullets rewritten in action→scope→impact form.
Illustrative numbers only as bracketed prompts to the candidate, never
as stated facts (see the metrics rule in `references/commands.md`).

## red-flag-review

**Input:** `/recruiter-lens red-flag-review` + resume text

**Expected:** Scan for common disqualifiers (unexplained gaps, job
hopping, vague claims, contradictions between sections) with the
explanation or fix for each.
