Build a local pipeline that converts a mixed-source archive into a compact, source-aware advisor corpus for a “Ramit Sethi bot.” We want to build this in a way that we can generalize it to other types of bots as well (but a Ramit Sethi like advisor will be the first use case). 

The pipeline must ingest txt, md, pdf, and note files; classify each source as primary, secondary, personal-note, or non-canonical influence; chunk sources by semantic boundaries; generate structured source summaries; extract canonical doctrine, tone, advice patterns, user archetypes, anti-patterns, and representative examples; preserve provenance for every major claim; and produce a short runtime context document plus a retrieval corpus for examples and edge cases.

Do not produce a single prose summary only. Build a reusable workflow with intermediate artifacts. Keep primary Ramit material separate from my notes and other bot chats until the final assembly stage. Label all outputs as source-derived, archive-derived, advisor-inferred, or thin/uncertain where applicable.

Final outputs should include: source registry, chunk index, per-source summaries, canonical doctrine file, style/voice file, pattern/archetype file, runtime context file, retrieval-ready evidence index, and a report describing token budgets and recommended runtime assembly strategy.

Optimize for faithfulness, compactness, and reuse in downstream model prompts. Remove repetition and fluff, but preserve decision-relevant nuance, contradictions, and boundary conditions. Prefer behavioral primitives over descriptive biography. At runtime, assume the model will receive the short runtime context plus a few retrieved chunks, not the whole archive.

This prompt will define end-to-end system architecture, source separation, output files, provenance rules, and runtime strategy.

I have current prompts that extract and compact the source documents to create a doctrine to use as context for a Ramit Sethi bot:
- `context compaction prompt.md`
- `ramit sethi compaction prompt addendum`

Some additional context on someone who has done this at scale for enterprises:
- https://www.reddit.com/r/AI_Agents/comments/1nf859k/i_made_60k_building_ai_agents_rag_projects_in_3/
- https://www.reddit.com/r/AI_Agents/comments/1nbrm95/building_rag_systems_at_enterprise_scale_20k_docs/