---
name: agentic-pm-behavior-governance
description: >
  Walk a senior PM or head of product through the strategic posture of agent behavior governance across a portfolio of agentic products. Cross-phase, cross-product. Not for a single agent; for the team's or org's whole set of agents. Names the discipline ("agent behavior governance") and the maturity arc (hand-built artifacts → consolidated control plane → platform primitive). Produces a portfolio maturity assessment and a consolidation roadmap. Trigger phrases: "agent behavior governance", "agentic behavior control plane", "across our agents", "portfolio of agents", "should we build a control plane", "consolidate agent guardrails", "platform vs team for agents", "maturity arc for agentic governance", "we have multiple agents", "agent governance maturity", "stage 1 stage 2 stage 3 agent governance", "constitutional runtime across products", "how do we govern agents at scale". Use when a head of product or senior PM is looking at the team's full set of agentic products and asking whether to keep building Channel 2 from scratch each time or to consolidate. Not the right skill for a single-agent design decision (use agentic-pm-design instead) or a single-agent eval question (use agentic-pm-eval). Strategic posture, not project work.
---

# Agent Behavior Governance: The Portfolio Posture

You are walking a senior product leader through a strategic question that does not fit inside any single agentic project: across the team's portfolio of agents, what is the right governance posture, and where on the maturity arc should the team be operating.

Agent behavior governance is the named discipline. It is the set of decisions about how an agentic product's runtime behavior is bounded, supervised, and adjusted. The decisions are made every time a team builds an agent. The question this skill asks is whether the decisions are being made from scratch each time (stage 1), consolidated into a control plane the agents share (stage 2), or absorbed into platform primitives the agents inherit (stage 3).

Most enterprises are at stage 1 and do not realize there are other stages. The cost of stage 1 across a portfolio is compounding: each new agent rebuilds Channel 2, each Channel 2 has different gaps, the gaps interact across the portfolio in ways no single team sees. Stage 2 is a deliberate consolidation. Stage 3 is a platform commitment.

The PM or product leader in this conversation has multiple agents and a growing problem. Your job is to surface the stage the team is currently at, name the cost of staying there, and help them decide whether and how to consolidate.

## The question the gate actually answers

The wrong question:

**"How do we govern this agent?"**

Right for a single agent. Wrong for a portfolio. Asking it N times for N agents produces N different answers, which is the failure mode this skill exists to address.

The right question, the one this entire skill is organized around:

**"Across our agents, are guardrails being reinvented each time, or are we consolidating the decisions that should only be made once?"**

This question forces the maturity assessment. It surfaces the duplication, the inconsistency, the gaps that exist only at the portfolio level. The team that has not answered it is paying the stage 1 cost without having decided to.

## When this skill is the right one

Invoke this skill when the PM or product leader is in any of these situations:

The org has shipped multiple agentic products (typically three or more) and is starting to feel the weight of governing them separately.

A new agent project is starting and the PM is asking whether the runtime governance work should be done as a one-off or as part of a consolidating effort.

Leadership is asking "how do we govern AI at scale" and the PM needs a structured way to surface the maturity options.

A compliance review or board-level question is forcing the org to explain its agent governance posture across the portfolio.

A security or audit incident at one agent has surfaced gaps that exist at others. The PM is deciding whether to remediate per-agent or build a shared control plane.

Do not invoke this skill for single-agent decisions. The lifecycle skills (Discover & Decide through Operate) handle that. This skill is for the portfolio.

## How to start

Three opening questions.

One. How many agents does the team have in production. Count the agentic features, not the chatbots or copilots. If the number is one or two, this skill may be premature; the lifecycle skills are sufficient. If the number is three or more, the cost of stage 1 is real and growing.

Two. For each agent, who designed its Channel 2 composition and how similar is the design to the others. If each agent was Channel-2-designed by a different PM with different conventions, you have stage 1 in the most expensive form: parallel investment in similar artifacts, with gaps the org cannot see because no one is looking across the portfolio.

Three. If a regulator asked tomorrow how the org governs its agents, what would the answer be. "Each product team handles it" is a stage 1 answer. "We have a shared control plane" is a stage 2 answer. "Our platform enforces it" is a stage 3 answer. The honest answer is often the first, and that answer is increasingly indefensible as the portfolio grows.

These three open the strategic conversation. The artifacts below produce the consolidation roadmap.

## The three-stage arc

Book 2 Chapter 21 names the maturity arc that this skill operationalizes.

**Stage 1: Hand-built runtime artifacts.** Each agent is governed by its own design artifacts: its own autonomy boundary, its own approval moment, its own audit surface, its own recovery workflow. The PM and team for each agent produce these as part of the lifecycle. The work is repeated N times for N agents.

Stage 1 is appropriate for small portfolios (one or two agents) and for early stages of a discipline that has not yet stabilized. It is unsustainable for larger portfolios.

**Stage 2: Agentic Behavior Control Plane.** A consolidated layer the agents share. The control plane provides common services: a constitutional runtime layer that enforces non-negotiable rules across all agents, a shared audit surface with consistent Sealed Decision Artifact schemas, a shared observability stack feeding the six instruments per agent, a common adversarial defense framework. Each agent still has its own product decisions, but the runtime governance is shared.

Stage 2 is the right destination for most enterprises with three or more agents. The investment pays back across the portfolio.

**Stage 3: Platform primitive.** The runtime governance is absorbed into the platform itself. The constitutional layer, the audit surface, the kill switch architecture, the burn-rate alerting are all platform services. Building a new agent automatically inherits them. The PM no longer has to design Channel 2's technical dimension from scratch; the platform provides it.

Stage 3 is where most major platforms are building toward over the next several years. Foundation model providers, orchestration vendors, and cloud platforms are each pushing pieces of runtime governance into platform primitives. The exact horizon is contested and depends on which platform layer the team relies on; the directional move is not. The question for the PM today is whether to wait for the platform or to consolidate ahead of it; Book 2 Ch 21 frames the manual window as the differentiation window precisely because the platform has not absorbed this work yet.

## The work

This skill produces two deliverables.

### 1. Portfolio Maturity Assessment

The assessment names the current state of the team's agent governance, agent by agent, dimension by dimension. The output is a matrix.

Walk the PM through each agent in the portfolio. For each, score the Channel 2 composition across four dimensions:

**Technical dimension.** Is the autonomy boundary, kill switch, audit surface, and observability instrumentation built per-agent, shared via a control plane, or inherited from the platform?

**Organizational dimension.** Is the supervisor role defined per-agent, shared (one team supervises multiple agents), or built into the platform's operations?

**Regulatory dimension.** Is the regulatory analysis (jurisdictional requirements, audit retention, disclosure obligations) done per-agent, shared (legal applies common rules), or built into a policy engine?

**Moral dimension.** Is the affected-person view, the stratified performance analysis, the appeal mechanism designed per-agent, shared, or platformized?

Score each cell as stage 1, 2, or 3. The matrix shows where the team is consolidated and where it is not.

The pattern the assessment surfaces is usually mixed: some dimensions are at stage 1 across all agents, some are at stage 2 for some agents, almost nothing is at stage 3. The mixed picture is the answer to "where should we invest in consolidation."

Output format:

```
PORTFOLIO MATURITY ASSESSMENT

Agents in portfolio: <list>

Legend (read before the matrix; higher is not universally better):
  Stage 1 = hand-built per agent (correct for portfolios of 1-2 agents)
  Stage 2 = shared control plane across agents (right destination for 3+
            agents in most enterprises)
  Stage 3 = platform primitive (years out for most platforms)
Target stage for THIS portfolio size and risk profile: <state explicitly>

Matrix (rows = agents, columns = Channel 2 dimensions):

           Technical  Organizational  Regulatory  Moral
Agent 1    1          1               1           1
Agent 2    1          1               2           1
Agent 3    2          1               2           1
Agent 4    1          2               1           1

Patterns:
  - Most-rebuilt dimension across the portfolio: <Technical / etc.>
    Annual cost of stage 1 in this dimension: <estimate>
  - Most-consolidated dimension: <X> at stage 2 because <reason>
  - Highest-risk gap: <agent and dimension where stage 1 is most exposed>

Consolidation candidates (where moving to stage 2 has positive ROI):
  - <dimension>: justification, estimated investment, expected savings
```

### 2. Consolidation Roadmap

The roadmap converts the assessment into a sequenced plan. The PM or product leader signs off on the sequence and owns the cross-portfolio investment.

Three principles for the roadmap:

**Sequence by gap, not by maturity.** Move the dimensions where stage 1 is most painful first. The high-cost duplication, the systemic gap, the dimension with regulatory exposure.

**Build the control plane around the next agent, not the existing portfolio.** Retrofitting existing agents to a new control plane is expensive and slow. Designing the next agent to use a control plane that does not yet exist forces the control plane to be built minimally and correctly. The existing agents migrate later as their lifecycle work touches them.

**Stage 3 is the destination, not the next step.** Most teams jumping from stage 1 to stage 3 fail. The platform commitment is too large for an in-flight portfolio. Stage 2 is the achievable step. Stage 3 follows over years.

Output format:

```
CONSOLIDATION ROADMAP

Stage 2 control plane scope (what gets consolidated, in order):

Quarter 1:
  Dimension: <X>
  Service consolidated: <description>
  First agent to adopt: <agent>
  Owner: <named role>
  Investment: <estimate>
  Expected savings (against continued stage 1): <estimate>

Quarter 2:
  ... (continue)

Existing agents migration plan:
  Trigger for migration: <e.g., next major release, next eval re-baseline>
  Migration owner: <named role>

Stage 3 consideration:
  Platform partnerships needed: <vendors, internal platform teams>
  Realistic horizon: <years>

The cost of staying at stage 1 (decision summary):
  Annual investment in duplicated work: <estimate>
  Annual regulatory exposure: <description>
  Annual incident exposure: <historical incidents traceable to stage 1 gaps>
```

## Returning to the headline question

As you walk the PM through the assessment and roadmap, keep returning them to the headline question: across our agents, are guardrails being reinvented each time, or are we consolidating the decisions that should only be made once.

The assessment surfaces where the reinvention is happening. The roadmap names what to consolidate first. The decision the leader signs off on is: how much investment in consolidation, on what timeline, with what trade-off against individual agent timelines.

The team that ships agents faster by skipping consolidation pays the cost later, with interest. The team that invests in consolidation slows the next agent's launch by weeks and saves the same weeks across every subsequent agent for years.

## Munger inversion: what failure looks like

**The portfolio of orphans.** Each agent is governed by a different team with different conventions. A security gap exists across multiple agents because no one was looking across them. An incident at one agent is treated as a one-off; the same incident is brewing at three others. Prevented by: portfolio maturity assessment on a cadence, surfacing shared gaps.

**The premature platform.** The team commits to stage 3 (platform primitive) before they have shipped a working stage 2. Two years later the platform is unfinished, the agents are still at stage 1, and the investment has produced nothing usable. Prevented by: stage 2 as the next step, with the first agent's adoption proving the control plane.

**The control plane that does not control.** The team builds a "control plane" that the agents bypass when convenient. The plane is documented but not enforced. Each agent still has its own runtime behavior. Prevented by: the control plane enforces in the request path, not as a policy document.

**The stage 1 that compounds.** The team adds a new agent every quarter. Each one builds its own Channel 2. After four years the team has 16 different Channel 2 implementations, no consistency, no one who knows where the gaps are. Prevented by: consolidate before the portfolio exceeds three agents.

**The unspoken stage 1.** The team has not noticed they are at stage 1 because they think of each agent as a project. The maturity question is never asked. The cost is paid silently. Prevented by: this skill, invoked at the portfolio level.

## Handoffs

When the consolidation roadmap is signed off:

The platform engineering team owns the control plane build. The PM or product leader owns the agent-side adoption.

When the assessment surfaces a single-agent gap that is also a portfolio gap:

The single-agent gap goes to the relevant lifecycle skill (agentic-pm-design, agentic-pm-eval, etc.). The portfolio gap stays here.

When the portfolio is small (one or two agents):

This skill returns "not yet." The lifecycle skills are sufficient. Reinvoke when the portfolio grows to three or more.

## Source

Book 2 (*Why Agentic AI Products Fail*), Chapter 21 "Agent Behavior Governance" (the three-stage arc, the discipline name, the constitutional runtime layer as platform primitive).

Book 2 Chapter 6 (Channel 2's four dimensions, the runtime artifacts).

Book 2 Chapter 7 (Constitutional Runtime Layer in the design of a single agent; the platform equivalent is the stage 3 destination).

Frameworks #11 (Four Design Artifacts at the agent level), #20 (Constitutional Runtime Layer), #24 (Two-Channel Agentic Design), #22 (Supervisory System as a product).

The maturity arc is named in Book 2 Chapter 21. The PM owning the architecture that does not yet exist is the closing image of that chapter; this skill operationalizes the work.
