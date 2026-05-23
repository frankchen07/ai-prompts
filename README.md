# ai-prompts

This is a collection of prompts I've built and used — persona roles, project-specific builders, and notes on where AI can actually pull weight.

---

## persona prompts

These are role-based personalities you drop into a chat to get expert-mode responses:

- `therapy bot prompt.md` — LMFT therapist with IFS/DBT/somatic background
- `financial advisor prompt.md` — personal finance + investing advisor
- `dream psychologist prompt.md` — Jungian dream analyst
- `mechanic agent prompt.md` — car mechanic scoped to a 2003 Subaru WRX
- `youtuber agent prompt.md` — YouTube content helper agent
- `career product biz persona.md` — PM/brand/marketing job coach that tailors cover letters, resumes, and interview prep to Frank's specific background
- `dealmaker persona.md` — tactical negotiation advisor combining Chris Voss, Ury, and Ramit Sethi; gives exact words and scripts for high-stakes conversations
- `ramit sethi persona.md` — Ramit Sethi playing long-term advisor on career, finances, and life direction
- `writing editor persona.md` — expert writing coach and editor for non-fiction Substack content, grounded in Frank's archive and core craft books

## project prompts

Prompts used to actually build something:

- `boast coffee website prompt.md` — rebuild boastcoffee.com in HTML/CSS/JS
- `protonflow prompt.md` — ProtonMail wrapper with Gmail-style keyboard shortcuts
- `veterinarian specula prompt.md` — text-to-CAD prompt for a vet speculum in Zoo AI
- `trading bot prompt.md` — crypto trading pipeline reporting Minervini/O'Neil signals twice daily; no reasoning, no unauthorized actions
- `text to map prompt.md` — Telegram bot that generates Google Travel Maps from natural language, with layered categories (eat/drink/do) and automatic icon/color rules

## meta / reference

- `structured prompt templates.md` — reusable prompt structures (context, role, format, etc.)
- `idea list for ai applications.md` — running list of AI use cases, checked off as built
- `context compaction prompt.md` — extracts dense, decision-useful knowledge from source materials into a compressed advisor persona

### compaction workflow

A 4-step iterative process for building high-quality advisor personas to load into Claude Projects:

1. **Baseline extraction** — upload source materials + `context compaction prompt.md` to Claude → produces `[name] compacted output 1.md`
2. **Quality critique** — upload source materials + compaction prompt + output 1 to ChatGPT → ChatGPT identifies gaps and produces a `[name] compaction prompt addendum.md`
3. **Refined extraction** — back on Claude: source materials + compaction prompt + addendum → produces `[name] compacted output 2.md`
4. **Load into project** — output 2 goes into a Claude Project as the ready-to-use advisor

The addendum files are the reusable prompts (ChatGPT-generated quality critiques); the output files are generated artifacts. Four personas have the full compaction package:

- `career product biz compaction prompt addendum.md` — role-fit taxonomy, story bank, positioning playbook for job search
- `dealmaker compaction prompt addendum.md` — negotiation scripts, failure-mode intercepts, exact-words frameworks
- `ramit sethi compaction prompt addendum.md` — diagnostic patterns, anti-patterns, emotional reframes, conversational rhythm
- `writing editor compaction prompt addendum.md` — editorial checklist, Frank-specific voice calibration, craft-book frameworks

---

Fork anything. Adapt the persona prompts to your own context; they work best when you feed in personal documents or background at the top.
