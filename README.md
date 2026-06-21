# Agentic AI PM Skill Package

Stage 1 of a skill package for product managers building agentic AI products in Claude Cowork. Seven skills covering the agentic PM lifecycle, from deciding whether to build through long-horizon governance, plus a portfolio-level strategic skill and a front-door router.

The skills are working aids. The reasoning lives in the four books they reference, all by Yoram Friedman, published at [agenticaiproductmanagement.com](https://agenticaiproductmanagement.com/):

- *Agentic AI for Busy Product Managers* ([Amazon](https://a.co/d/0dCz9Lbx))
- *Why Agentic AI Products Fail* ([Amazon](https://a.co/d/0cdvAyjn))
- *The Agentic AI Team* ([Amazon](https://a.co/d/0jhGrB91))
- *The Agentic AI Practitioner* (draft, online only)

The skills are designed to be invoked at the moment of need by a senior product manager working on a real agent.

## The package at a glance

| Skill | Phase | What it produces |
|---|---|---|
| `agentic-pm-lifecycle` | Router | Diagnoses the PM's situation and dispatches to the right specialized skill |
| `agentic-pm-discover-decide` | Phase 1 | Suitability record, context sufficiency map, distribution gap analysis, cost model, go-or-no-go memo. Includes a fully worked example for a refund agent. |
| `agentic-pm-design` | Phase 2 | Declared system type, four runtime artifacts (autonomy boundary, approval moment, audit surface, recovery workflow), Channel 2 composition, consequence classification, trust scaffold, adversarial defense plan, the two briefs (Human Brief and Executable Brief), Sealed Decision Artifact spec, step-level instrumentation requirement. |
| `agentic-pm-eval` | Phase 3 | Pass@K with worst-slice variance, compound probability projection, semantic-vs-state validation, coverage statement, adversarial suite, LLM-as-judge calibration, model-version policy, all-owner readiness memo. |
| `agentic-pm-observe` | Phase 4 | Six observation instruments, data-layer observation, operational guardrails (ceilings, kill switch, circuit breaker, burn-rate), supervised-vs-bypass report, supervisory engagement metrics, deployment-event log, stratified performance report. |
| `agentic-pm-operate` | Phase 5 | Drift detection (six vectors), Sealed Decision Artifact policy, instrument half-life, constitutional runtime rules, affected-person audit view, adaptive governance rule set, plus authority delegation audit, currency question, external audit on held-out sample. |
| `agentic-pm-behavior-governance` | Cross-phase | Portfolio maturity assessment, consolidation roadmap, three-stage governance arc (hand-built → control plane → platform primitive). |

Total: ~3,100 lines across seven skills.

## Who this is for

A senior product manager (10+ years) who is fluent in classical product management and is now building, evaluating, or operating an agentic AI product. The skills assume PM fluency on the conventional craft. Each phase skill includes a "first-timer foundations" section that teaches the constructs new to agentic work (golden datasets, Pass@K, the four runtime artifacts, drift vectors, the Sealed Decision Artifact, the constitutional runtime layer, and so on).

If you are an enterprise PM team adopting agentic AI and looking for a shared discipline, the package is designed to be invoked phase by phase as the team's work moves through the lifecycle. The router skill helps PMs find the right phase skill without needing to know the package structure.

## How to install

Each skill is a folder containing a single `SKILL.md` file. Cowork installs each one as a `.skill` zip. See the [Releases](https://github.com/yoramfmd/agentic-ai-pm-skill-package/releases) tab for the latest installable zips.

To install all seven:

1. Download the latest release archive.
2. In Cowork, go to Settings > Capabilities > Skills.
3. Drag each `.skill` file into the install area.
4. The skills appear in your available skills list and can be invoked by name or by natural-language trigger.

To install one skill at a time, download only the `.skill` zip for that skill.

## How to use

Each skill triggers on natural-language phrases described in its `description` block. For example:

- "I need to decide whether to build this as an agent." → `agentic-pm-discover-decide`
- "We are designing the approval moment for our refund agent." → `agentic-pm-design`
- "Is the agent ready to ship?" → `agentic-pm-eval`
- "Our agent has been live for six months; how do we tell if it has drifted?" → `agentic-pm-operate`
- "I'm not sure which phase I'm in." → `agentic-pm-lifecycle` (the router)

You can also invoke a skill by name explicitly.

Skills work independently. A PM whose agent is already in production can invoke `agentic-pm-observe` without having run `agentic-pm-discover-decide` first; each skill includes the anchors a PM coming in mid-flow needs.

## What is NOT in Stage 1

The package is the first of three planned stages. Two follow:

- **Stage 2 (planned): Team Collaboration.** Five skills built from *The Agentic AI Team*: the collaboration grid, seam audit, agent-as-team-member onboarding, fleet governance, team skill protection.
- **Stage 3 (planned): Practitioner.** Five skills built from *The Agentic AI Practitioner*: proficiency check, model dossier, configuration interview, deliberate-practice loops, first-month on-ramp.

Stage 1 covers the lifecycle. Stages 2 and 3 cover the team that ships it and the individual who must stay competent operating it. They will be released as separate skill bundles in this repo.

## Source

The skills are working condensations of the four books. Every named construct (the four runtime artifacts, the six drift vectors, the Sealed Decision Artifact, the supervision paradox, the Iceberg, the MVP House of Cards, the Enforcement Principle, the Currency Question, and so on) has its full treatment in the books. Each skill's `Source` section cites the canonical chapters.

If a skill omits depth you need on a specific construct, the book is where the depth lives. The skills are designed to be referenced quickly at a moment of need, not to substitute for the books.

## Editorial discipline

The package was built and reviewed against two lenses: a cold reader (without the books) and a book-informed reader (with the books). The cold review caught audience gaps. The book-informed review caught canon violations. Both reviews are reflected in the current state.

If you find a canon error or an audience gap, please open an issue.

## License

Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0).

You may share and adapt these skills for non-commercial purposes, with attribution to Yoram Friedman. Commercial repackaging requires written permission. See `LICENSE` for the full terms.

## Author

[Yoram Friedman](https://www.linkedin.com/in/yoram-friedman/) is a physician and senior product manager who has spent fifteen years building enterprise cloud, data, and platforms at SAP, Walmart, and Microsoft. He trained as a physician in anesthesiology and radiology and writes about healthcare AI, agentic systems, and what it actually takes for AI to move from pilots to production in regulated environments.
