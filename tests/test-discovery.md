# Discovery Tests

The skill should activate for requests containing these intents:

- Review my resume from a recruiter's perspective.
- Would this resume get rejected?
- Simulate the 6-second recruiter scan.
- Is my resume ATS-friendly?
- Check my resume against Applicant Tracking Systems.
- What interview questions will they ask based on my resume?
- Find the gaps between my resume and this job description.
- Tailor my resume for this specific posting. (expects the coverage judgment from `tailor`; the finished rewrite hands off to job-lens when installed)
- Audit my LinkedIn profile for recruiters.
- How should I explain my employment gap?
- Is this a red flag on my resume?
- Can I use ChatGPT to write my resume?
- Strengthen my bullet points with impact.
- Review this cover letter for recruiter appeal.

The skill should NOT activate for:

- Finding, evaluating, or submitting job applications (use job-application-agent instead)
- Writing or editing non-job-search content (use wordsmith instead)
- Resume layout/design as a graphic artifact (use a design skill)
- Negotiating offers or compensation legal advice
- Company research unrelated to a specific application

Non-activation prompts that should route to job-lens (they ask for finished material):

- "Rewrite my resume bullets for this role."
- "Write five summary options for this job."
- "Rewrite my LinkedIn headline and About section."
- "Write my answers to the likely interview questions."
- "Make my resume better for this JD." (production; use `gap-analysis` first only if the user asks what is missing)

Ambiguous prompts, with expected routing:

| Prompt | Expected routing |
|---|---|
| "Improve my resume." (no JD) | `critique` first, then offer job-lens for the rewrite |
| "Tailor my resume to this JD." | `tailor` for coverage; job-lens mode 1 writes the tailored resume |
| "What will they ask me?" | `predict-questions`; offer job-lens for the answers |

The skill must never output precise metrics the candidate did not provide;
it must use candidate figures, explicitly framed approximations, or bracketed prompts.
