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

## critique then production (applicant-kit hand-off)

**Input:** "Critique my resume, then fix it." + resume with some bullets
lacking metrics

**Expected:** `critique` output first; then a hand-off to applicant-kit if
installed (or a rewrite under the never-invent rule if not), with open
metric slots marked for the user to fill.

**Fail:** invented numbers in the rewrite; the critique repeated inside
the rewrite.

## Trigger and boundary cases (recruiter-lens side)

Drafted by reading the tuned skill descriptions only — not a real
triggering run. "Flag" marks a case where the description alone does not
settle the answer. Duplicate check against this file and
`test-discovery.md`: no case table existed when these were written; R12
and R9 overlap the discovery intents "Audit my LinkedIn profile for
recruiters" and "Strengthen my bullet points with impact", and R8 overlaps
the non-activation prompt "Rewrite my resume bullets for this role."
Sibling: applicant-kit (writes the better version); partner IDs refer to
cases in `applicant-kit.test-prompts.md`.

### Clear triggers

| # | Message | Expected | Command | Pass condition | By hand |
| --- | --- | --- | --- | --- | --- |
| R1 | "I've sent 40 applications and got two replies. Look at my resume and tell me why." | recruiter-lens | reject-reasons | Findings ranked by impact, each with an exact fix on the candidate's own wording. No full rewrite. | pass |
| R2 | "Will this resume get through ATS for this job?" (JD pasted) | recruiter-lens | ats-check | Reads the ATS reference first. Says the result is a rubric judgment, not a real ATS score. | pass |
| R3 | "Give me a quick first impression of my resume." | recruiter-lens | scan | Simulates a first pass and calls the 6 to 8 second figure a heuristic. | pass |

### Implicit triggers

| # | Message | Expected | Command | Pass condition | By hand |
| --- | --- | --- | --- | --- | --- |
| R4 | "Recruiters never call me back after I apply. What am I doing wrong?" | recruiter-lens | reject-reasons | If no resume is attached, asks once for it. Does not guess. | pass |
| R5 | "Given the gaps in my CV, what would an interviewer press me on?" | recruiter-lens | predict-questions | Questions only, tied to gaps or the JD. Writes no answers; offers the answer pack in one line. | pass — see caveat |

### Near-misses

| # | Message | Expected | Pass condition | By hand |
| --- | --- | --- | --- | --- |
| R6 | "Polish the grammar in my blog post about Kubernetes." | neither (wordsmith if installed) | recruiter-lens does not trigger. | pass |
| R7 | "Turn my resume into a PDF." | file skills (pdf or docx) | recruiter-lens does not review; it only finishes content if asked. | pass |
| R8 | "Rewrite my bullets so they sound more senior." | applicant-kit, mode 2 | If both are installed, hands off. If only recruiter-lens is installed, rewrites under never-invent and mentions applicant-kit once. | pass |

### Boundary pairs (this side judges)

| # | Message | Expected | Command | Pass condition | Partner | By hand |
| --- | --- | --- | --- | --- | --- | --- |
| R9 | "Which of my bullets are the weakest, and what is each one missing?" | recruiter-lens | impact-boost | Quotes the weak bullets and names what each lacks (metric, scope, outcome). Asks for missing numbers. Rewrites nothing. Ends with one handoff-offer line. | A5 | pass — see caveat |
| R10 | "Which keywords from this JD am I missing?" | recruiter-lens | keyword-match | Reports supported, lacking, and gaps to leave alone. Inserts nothing. Ends with one handoff-offer line. | A6 | pass |
| R11 | "How well does my resume cover this JD, requirement by requirement?" | recruiter-lens | gap-analysis or tailor | A coverage report only. No rewritten resume. | A1 | pass |
| R12 | "Audit my LinkedIn profile." | recruiter-lens | linkedin-audit | Findings with fixes. No full rewrite. | A4 | pass |

### Alias check

| # | Message | Expected | Pass condition | By hand |
| --- | --- | --- | --- | --- |
| R13 | "Optimize my resume for this job." | applicant-kit most likely; recruiter-lens acceptable | If recruiter-lens fires (the `optimize` alias maps to `tailor` — [SKILL.md:81](file:///C:/Users/abdul/Downloads/Qoder/recruiter-lens/skills/recruiter-lens/SKILL.md#L81)), it gives a coverage report and a handoff offer, and does not rewrite uninvited. If applicant-kit fires, it starts with modes 1 and 3. | **flag** |

### Spanning case

| # | Message | Expected | Pass condition | By hand |
| --- | --- | --- | --- | --- |
| R14 | "Check my resume against this JD, then fix whatever is weak." | either skill first | Findings travel in the block from `references/findings-handoff.md`. The second skill doesn't re-derive the verdict. Gaps marked "not shown" are reported, never filled with invented experience. | pass — see caveat |

### Caveats (checked against the skill as it stands)

- R9: `impact-boost` rewrites by design — the command spec transforms weak
  bullets into impact statements
  ([commands.md:277-281](file:///C:/Users/abdul/Downloads/Qoder/recruiter-lens/skills/recruiter-lens/references/commands.md#L277-L281))
  and the `impact-boost` test above expects rewrites. "Rewrites nothing"
  is a spec change, not current behaviour; run R9 against the tuned
  descriptions or amend the command first.
- R5: the `predict-questions` test above expects each question with
  "what a good answer must cover". That is coverage guidance, not an
  answer script, so "writes no answers" holds only if the agent keeps
  that line terse; flag for the real run.
- R14: `references/findings-handoff.md` does not exist in either the repo
  (`skills/recruiter-lens/references/`) or the installed copy, and nothing
  in applicant-kit's references points at one. The pass condition is
  unverifiable until that file is written or the condition is reworded to
  the actual handoff mechanism (`applicant-kit/references/recruiter-lens-skill.md`).
