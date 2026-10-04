# Discovery Tests

The skill should activate for requests containing these intents:

- Review my resume from a recruiter's perspective.
- Would this resume get rejected?
- Simulate the 6-second recruiter scan.
- Is my resume ATS-friendly?
- Check my resume against Applicant Tracking Systems.
- What interview questions will they ask based on my resume?
- Find the gaps between my resume and this job description.
- Tailor my resume for this specific posting.
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

The skill must never output precise metrics the candidate did not provide;
it must use candidate figures, explicitly framed approximations, or bracketed prompts.
