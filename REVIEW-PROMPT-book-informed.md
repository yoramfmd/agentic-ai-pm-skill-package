# Book-Informed Review Prompt: Agentic PM Skill Package

Use this prompt with a FRESH LLM instance (not the one that did the cold review). Share access to the four books and the seven SKILL.md files. Do NOT share the cold review.

The books:
- Book 1: *Agentic AI for Busy Product Managers* (the original framework; six-phase lifecycle slide originates here)
- Book 2: *Why Agentic AI Products Fail* (v4 manuscript; supervisory layer as primary product; the Dual Brief; Channel 2 four-dimension composition; Sealed Decision Artifact)
- Book 3: *The Agentic Team* (team roles, seams, handoffs)
- Book 4: *The Agentic AI Practitioner* (proficiency, deliberate practice, the practitioner's record)

The package is Stage 1 of three. It covers the PM lifecycle only. Team Collaboration (from Book 3) and Practitioner (from Book 4) will be Stage 2 and Stage 3 respectively. Do not flag missing team or practitioner content; that work is scoped out.

---

You are reviewing a Claude Cowork skill package built from the four books above. The package has seven skills: a router (`agentic-pm-lifecycle`), five lifecycle phase skills, and one portfolio-strategy skill (`agentic-pm-behavior-governance`).

Your job is canon consistency, not audience usability. A separate cold review handles whether the package works for a PM who has not read the books. You read with the books, looking for canon-level problems.

YOUR JOB:

For each skill, report the following, ordered by leverage (highest impact first):

1. **Canon drift.** Where does the skill say something inconsistent with the books. Quote the skill, quote the book passage, name the discrepancy. Distinguish between contradiction (the skill says X, the book says not-X) and dilution (the skill says X but the book's treatment is sharper).

2. **Framework name precision.** The author uses named constructs (Iceberg, Four Runtime Artifacts, Sealed Decision Artifact, Supervision Paradox, MVP House of Cards, etc.). Where does the skill use the wrong name, paraphrase a name, or invent a near-name. Quote the slip.

3. **Underused book content.** Where does the skill skim over a section the book develops more fully and where would the skill be materially stronger with a tighter paraphrase or a one-paragraph treatment of the book's depth. Cite the chapter and the topic. Do not propose lifting whole sections; the skills are working aids, not condensed books.

4. **v4 manuscript evolution.** Book 2 v4 in particular evolved past the original slide and the original Book 1. Where do the skills still reflect Book 1 framing where Book 2 v4 has moved on. Examples to look for: cost-model architecture multiplier (Book 2 Ch 3), the Dual Brief (Book 2 Ch 5b), audit surface temporal durability (Book 2 Ch 12 + Book 4 Ch 14), operational guardrails (Book 2 Ch 9), the constraint-vs-knowledge framing of constitutional rules (Book 2 Ch 17).

5. **Chapter reference precision.** Each skill closes with a Source section citing book chapters. Where are the citations wrong, missing, or imprecise (cites a whole book where a specific chapter would help).

6. **Cross-skill canon consistency.** Where does the same construct get treated differently across two skills (e.g., the audit surface appears in Design and Operate; if they disagree on what it is, flag the divergence).

7. **Specific edits.** Quote the original skill text and propose a replacement, with the book passage that supports the change. Maximum 10 edits.

DO NOT report:

Audience-usability issues. Teaching gaps, jargon without definition, first-timer confusion. The cold review handles that lens.

Praise for fidelity. The author already knows where the skills align with the books. Skip the "this faithfully captures Chapter X" sentences.

Suggestions to add Team or Practitioner content. Out of scope for Stage 1.

Style or voice suggestions. Voice is defined and intentional. Do not suggest softening or different framing.

Length cap: 1,500 words. Be precise. Quote both sides. The author wants to know where this is off-canon, not what it does well.
