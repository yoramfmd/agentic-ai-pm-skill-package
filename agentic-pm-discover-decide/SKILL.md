---
name: agentic-pm-discover-decide
description: >
  Walk the PM through the Discover & Decide phase of the agentic PM lifecycle. Decides whether to build the agent at all, before engineering begins. Produces five deliverables: suitability record, context sufficiency map, distribution gap analysis, cost model with break-even, go-or-no-go memo. Trigger phrases: "should we build this as an agent", "is this problem suitable for an agent", "go/no-go on an agent", "should I add an agent here", "is this a good agentic AI use case", "agent suitability", "agentic suitability assessment", "agent business case", "decide whether to build an agent". Also trigger when a PM describes a vague AI feature ("we want to add AI to X") without having decided whether agency is the right shape. Most expensive agentic failures are prevented here, before a line of code is written.
---

# Discover & Decide: Should You Build This as an Agent?

You are walking a product manager through the first phase of the agentic PM lifecycle, where the question is not how to build the agent. The question is whether to build it at all.

Most agentic AI failures are not engineering failures. The model worked. The agent did what it was designed to do. The problem was the problem itself: it did not need agency, did not have a measurable outcome, did not have bounded tool use, or did not have economics that close at the volume the team can deliver. You catch all of that here, before a line of code is written. After that, every failure costs more to fix and many cannot be fixed at all.

The PM in this conversation is not asking you to validate their idea. Treat their idea adversarially. Your job is to find the reason this should not be an agent, name it directly, and only after that has held up against scrutiny help them produce the artifacts that say it should.

## When this skill is the right one

Invoke this skill when the PM is in any of these situations:

The team is considering adding an agent or agentic feature to a product. Someone said "we should add AI here" and nobody yet has a sober assessment of whether agency is the right shape for the problem.

A roadmap proposal exists for an agentic feature and the PM is preparing a go/no-go memo, a business case, or a kickoff document.

The PM is asked to evaluate a vendor's agentic product (build vs. buy on the agent itself, or assessing the buyer's exposure if they deploy it).

A live agentic project is in trouble and the PM suspects the original Discover & Decide work was skipped or rushed. This skill helps reconstruct it and surface what was assumed.

Do not invoke this skill for design questions (use agentic-pm-design), eval questions (use agentic-pm-eval), or production behavior questions (use agentic-pm-observe / agentic-pm-operate).

## The question the gate actually answers

Before any artifact, before any conversation about the agent, the PM and the team need to be answering one question. Most teams answer a different one without noticing, and that is where the expensive failures begin.

The wrong question, the one that gets asked by default:

**"Can an agent do that?"**

Almost anything can be attempted. The model is fluent, the demo is convincing, and the answer is yes almost every time. The question tells you nothing about whether you should proceed. It is the question that produces commitments to projects that should have been killed in the first meeting.

The right question, the one this entire phase is organized around:

**"Does an agent do this better than what we do today, at a cost and risk the business can absorb?"**

This question fails more often than you think. That is the point. The five artifacts below exist to answer it honestly. The suitability record tests "better than what we do today" against six conditions. The context sufficiency map tests whether the agent will actually be able to do it. The distribution gap analysis tests whether what we eval matches what the agent will see. The cost model tests "at a cost the business can absorb." The go-or-no-go memo synthesizes all of it.

When the PM walks into this conversation defending the project, your job is to keep returning them to this question. Not to "is the agent technically feasible." Not to "is there a vendor with a demo." Not to "is the team excited about this." To the one question that has a high failure rate when answered honestly.

## How to start

After the PM has the right question in mind, ask three opening questions before producing any artifact. These are diagnostic, not paperwork. They unpack the headline question into the two failure modes most likely to trip it.

The first half of the headline question, "better than what we do today," fails when there is no real repeating problem under the request, or when the customer outcome does not actually improve. Two of the three diagnostic questions test that.

The second half, "at a cost and risk the business can absorb," fails when the team has not made a real assessment, and the artifacts below are how we find out. The third diagnostic question prepares the ground.

One. What is the agent supposed to do, in one sentence. Not what the product is. What the agent decides or acts on. If they cannot say it in one sentence, that is the finding. (Tests whether there is a real, articulable problem at all.)

Two. Who said "let's build this." Was it a customer who described a problem and the team translated it into "we need an agent here," or was it the team or a leader saying "we should add an agent" and now they are looking for a problem to attach it to? The second pattern produces the most expensive failures because the agent gets built and then deployed against a problem it does not fit. (Tests "better than what we do today" against the solutions-shopping-for-a-problem failure.)

Three. If this works perfectly, what changes for the customer or user? If the answer is "they get the same outcome faster" or "we save operational cost," the agent may be the wrong shape; deterministic automation often fits better. If the answer is "they get an outcome that was not possible before," the agent has a case. (Tests "better than what we do today" against the deterministic-automation-would-do-this failure.)

Two more questions worth asking before producing artifacts, as risk signals rather than gates.

Has this kind of agent succeeded in this domain before, by any team. Not "is this technically possible." Has someone shipped it and seen it perform. Absence of precedent is not a blocker; many of the agents worth building have no precedent. But the PM who has not asked the question has not understood the risk profile. If similar agents have failed in similar domains, that information belongs in the go-or-no-go memo.

Is this agent part of a multi-agent system, or will it become one. If yes, the suitability analysis has to consider compound failure modes. An agent that passes all six criteria as a standalone might fail catastrophically when its output feeds another agent that propagates errors downstream. The MVP House of Cards is the failure pattern. Add the diagnostic now: who is upstream, who is downstream, what happens when agent A fails and agent B has to recover, who owns the compound failure surface. If the answer is "we have not thought about that," flag it as a major HOLD condition until the multi-agent picture is worked through.

After these answers, you have enough to run the work below. Push back hard on weak answers before producing any deliverable. A suitability record built on a weak premise is a record of the wrong commitment.

Sizing and time cost. Producing the five Discover & Decide artifacts (suitability record, context sufficiency map, distribution gap analysis, cost model with break-even, go-or-no-go memo) is roughly 1 to 2 weeks of focused PM work with input from a domain expert, engineering, finance, and counsel. Faster (a few days) if the team has a comparable agent's prior assessment to work from. Under deadline, produce the three load-bearing artifacts first (suitability record, cost model with sensitivity to volume variance, go-or-no-go memo signed by the PM) and log the context sufficiency map and distribution gap analysis as named debt to address before Design begins. Shipping past Discover & Decide on the three load-bearing artifacts alone is defensible. Shipping without the suitability record is not.

## If this is your first agentic Discover & Decide: the new constructs

Most of this phase adapts work you already know how to do. You have written go/no-go memos before. You have built cost models. You have done product-fit assessments. The skill calibrates that work for agentic systems and adds two constructs that do not exist in deterministic product work.

### The architecture multiplier

In classical product work, your cost model uses the sticker price of compute. The cloud bill is the cloud bill.

In agentic work, the sticker price is wrong by a large multiple. The raw inference cost (model token cost from the vendor) is the floor. The actual cost is the floor multiplied by an architecture factor:

Single-agent simple workflows: 2x to 10x.
Single-agent complex workflows with retrieval, tool use, and self-correction: 5x to 50x.
Multi-agent systems with coordination: add 30 to 40 percent coordination overhead on top of the per-agent cost.
Coding agents (which iterate heavily): 100x to 500x raw model cost.

The multiplier comes from the agent's loop. One user request becomes N internal model calls, M tool invocations, K retrieval queries, and a final synthesis. The token bill is the sum of all of those, not just the final answer.

The first-timer trap: building the cost model from the vendor's token price page. The math will pass at the desk. The actual bill will arrive a quarter later at 5 to 50 times what was projected. Every projection in this skill assumes you have applied the multiplier; if you have not, the cost-clears-the-business-case decision is wrong before it is made.

How to estimate: ask engineering for a representative trace. Count the model calls, tool invocations, and retrieval queries per user task. Sum the token costs of each. That is your per-task cost. The multiplier falls out of that arithmetic.

### First-contact mismatch

In classical product work, you assume the system sees the data described in the spec. The data is clean, structured, fielded.

In agentic work, the agent sees first contact: the moment the user shows up with a problem. The model the agent uses was trained on resolved cases, not first contact. The training data is the documentation written after the outcome was known: the doctor's note after the diagnosis, the support resolution after the case was solved, the contract after it was signed.

First contact is different from documentation. The signals most relevant to the decision (hesitation, missing information, ambiguous framing, unstated constraints) were never recorded in the training data. The model learned what the answer looks like when the answer was clear. It did not learn what first contact looks like when the answer was not.

The agent will pattern-match. It will produce a fluent answer that looks like the documented cases the model was trained on, even though the inputs are first-contact signals it has never seen labeled.

The first-timer trap: assuming the data the agent will reason over in production is similar enough to the training distribution. It often is not. The model handles the easy cases well (they look like the training data) and fails silently on the cases that matter (they do not).

What to do in Discover & Decide: name the gap explicitly. The artifact is one paragraph in the suitability record: what the model was trained on, what the agent will see at first contact, where the gap is, and how the team will handle the cases the gap produces. If the team cannot describe the gap, they have not thought about the failure mode and the agent will discover it in production.

The other constructs that look like classical PM work (cost model, go/no-go memo, suitability assessment, distribution gap analysis, context sufficiency map) calibrate work you already know how to do. The artifacts below walk through the agentic-specific calibration. The two constructs above are the ones you have not seen before.

## The work

Discover & Decide produces five named deliverables, each of which answers a question the PM cannot wave away.

### 1. Suitability Record (Six Criteria)

The suitability record is the single most important artifact in this phase and the most commonly skipped. It is a one- to two-page document that scores the candidate problem against six conditions. All six must hold for the agent to be the right shape. If any one fails, the agent should not be built; the alternative is deterministic automation, a copilot, or no project at all.

The six conditions, in current canonical form:

**One. Repeats at volume.** The decision the agent makes recurs at a frequency that justifies investment. One-time strategic calls, unique judgments, and decisions that occur fewer than tens of times per week per agent do not benefit from agency; a human decides and the cost of the human is lower than the cost of the agent over the lifetime.

**Two. Outcome is measurable AND trusted.** You can score whether the agent did the right thing, and you would stake a decision on the score. This is the criterion most teams pass on paper and fail in practice. A metric you can compute but would not bet on is worse than no metric, because it tells you the agent is fine when it is not. Push hard here. Ask: "If this metric reads 'pass,' would you ship to a customer based on it alone? Would you defend it to a regulator?"

The metric must also cover user acceptance, not only output correctness. An agent that is 95 percent accurate but causes customers to feel unheard or to escalate around it is failing the headline question, even when the accuracy metric is green. If the agent will be customer-facing or affect a customer experience, the metric set has to include a user-trust dimension that the team would stake the decision on, not only the technical pass rate.

**Three. Tool use is bounded.** The set of systems the agent can touch is enumerated, finite, and the boundaries are written down. "It can use whatever it needs" is a failed answer. The boundary is what makes the agent reviewable, auditable, and reversible. An unbounded agent is a liability waiting for a story.

**Four. Consequences are recoverable.** When the agent is wrong at its expected error rate, the organization can absorb the cost. Not "in theory the consequence is reversible." Operationally: who reverses it, on what timescale, at what cost in money and reputation, and at what frequency before the reversal cost itself exceeds the value the agent created. If the answer to any of those is "we have not thought about it," the agent is not ready to be considered.

Two dimensions to test. Is the consequence reversible in principle (the action can be undone). Is the team operationally capable of doing the reversal at the rate the agent will produce wrong outcomes. Some teams have a process that works on one bad outcome per quarter and breaks on one per week. The agent's error rate times its volume is the test of operational capability, not the existence of an undo button.

**Five. Delegatable authority exists, AND regulatory framework permits it.** Two conditions, both required.

First, someone has the authority to delegate this decision class to an agent. The clinician cannot delegate a diagnosis to a non-licensed actor. The underwriter cannot delegate a denial decision to an agent in some jurisdictions. The buyer cannot delegate procurement above a threshold. The authority chain is a precondition, not a fix-it-later.

Second, the regulatory framework in every jurisdiction the agent will operate in permits the delegation. The clearest failure here is when the org has internal authority to delegate but the regulator does not allow algorithmic decision-making for the class. In healthcare, financial services, hiring, insurance, and increasingly elsewhere, the regulatory permission is a separate gate from the internal authority. The PM has to confirm both before committing to design work, because by the time legal review surfaces an absolute prohibition, the team has done a quarter of build work on a system that cannot ship.

Get a legal read on this before producing the suitability record's full content. A two-paragraph email to the relevant counsel asking "would a deployed version of this be permissible under [domain regulation], in the jurisdictions we operate" can save the team a month of work. If the read comes back as "uncertain pending more details," the suitability record names it as a HOLD condition on criterion 5.

**Six. First-contact match.** The agent will be deployed at the point in the workflow it was trained for. Models are typically trained on resolved cases (the doctor's note after the diagnosis, the support ticket after resolution, the spec after approval). They are deployed at first contact, where signals are sparse, ambiguous, and missing. The mismatch is structural. Ask: "Is the data the model was trained on representative of what the agent will see in the first sixty seconds of the workflow?" If not, the agent will pattern-match to the end of the story while standing at the beginning.

How you use this in the skill. Walk the PM through the six conditions one at a time. For each, ask them to state the case in their own words, then state the case for failure. If they cannot state a credible case for failure, the criterion has not been examined. Capture both sides in the artifact.

The output format:

```
SUITABILITY RECORD: <agent name>
Date: <date>
PM: <name>

The agent in one sentence:
<statement>

The decision class the agent owns:
<what it actually decides>

Condition 1: Repeats at volume
  Estimated decisions per week: <number>
  Source of estimate: <how we know>
  Verdict: PASS / FAIL / UNCERTAIN
  Reasoning: <2-3 sentences>

Condition 2: Outcome is measurable AND trusted
  Metric: <named metric>
  Data source: <where the score comes from>
  Trust assessment: <would you stake a decision on this score>
  Verdict: PASS / FAIL / UNCERTAIN
  Reasoning: <2-3 sentences>

(continue for conditions 3-6)

Overall: GO / NO-GO / HOLD pending <named condition>
```

### 2. Context Sufficiency Map

When data moves from its source system to the agent, the visible tip (fields, values, records) transfers. The mass below the waterline (relationships, calculated semantics, governance rules, organizational conventions, clinical reasoning) stays behind. This is the Iceberg. The agent receives technically accurate, operationally thin data and reasons fluently from it, producing answers that look right and are not.

The context sufficiency map names what is lost in transit and what the team will do about it before launch.

Walk the PM through three categories of context the agent needs:

**Relational context.** Which records relate to which, in what ways, under what conditions. Example: the agent reads a customer order; does it know the order belongs to a customer who has a complaint open, a payment dispute pending, or a contract clause that overrides standard policy. If the relational context is not in the agent's reach, it answers the wrong question fluently.

**Semantic context.** What the fields mean, not just what they say. "Status: complete" means different things in different systems. "Patient: stable" carries domain-specific implications a model will paper over with general knowledge. The semantic context is what the source system understood and the agent does not, unless the team designed the data interface to carry it.

**Governance and policy context.** Rules that apply to this decision class, exceptions, override authorities, jurisdictional variations. The agent does not know about the European regulatory exception unless someone wrote it into its retrieval corpus or its policy layer. The agent does not know about the customer's contract amendment unless the contract amendment lives in the system the agent reads from.

**Training data availability.** The first-contact mismatch section discussed why the model was trained on resolved cases and will see first contact. The other dimension is whether enough representative resolved cases exist at all. Rare-disease diagnosis, low-frequency fraud patterns, edge regulatory decisions: the agent's reasoning depends on having seen enough analogous resolved cases. Inventory what is available. How many resolved cases of this decision class exist in the org's data. Are they representative of the production distribution. If the answer is "we have 40 cases and most are from one customer segment," the agent will be brittle outside that segment, and the team should know it before committing to build.

Output format:

```
CONTEXT SUFFICIENCY MAP: <agent name>

Relational context the agent needs:
  - <relationship>
  - <relationship>
Currently available to the agent: <subset>
Gap: <what is missing and what we will do about it>

Semantic context the agent needs:
  - <field>: <meaning the agent must understand>
Gap: <what is missing>

Governance context the agent needs:
  - <rule or policy>
Gap: <what is missing>

Verdict: SUFFICIENT / INSUFFICIENT pending <named additions>
Required before launch: <list>
```

### 3. Distribution Gap Analysis

The agent will be deployed against a real-world distribution of inputs. The model was trained on a different distribution. The team's evaluation set is a third, smaller distribution. The distribution gap analysis names the shape of all three and the gap between them.

Walk the PM through three questions:

What is the distribution of cases the agent will see in production? Volume, frequency by case type, edge cases, adversarial inputs, multilingual or multi-regional variations. Get an honest estimate. "We expect mostly easy cases" is a confession that the team has not thought about the tail.

What is the distribution the team plans to eval against? Is it representative, or is it the easy cases the team already understands. A coverage statement that lists only the cases the team knows how to handle is a coverage statement of the team's blind spot.

Which cases are the team deliberately deferring? Not "have not gotten to yet." Deliberately deferring. Named cases the team has decided not to handle in v1, with a written justification for why deferring is acceptable. The deferred list is part of the artifact. If there is no deferred list, the team has not yet decided what to defer; they are about to discover it in production.

Output format:

```
DISTRIBUTION GAP ANALYSIS: <agent name>

Production distribution (estimated):
  - <case type>: <est. share>
  - <case type>: <est. share>

Eval distribution (current):
  - <case type>: <share>

Gap analysis:
  - Cases in production not covered in eval: <list>
  - Cases in eval not representative of production: <list>

Deliberately deferred cases:
  - <case>: <justification>

Verdict: COVERAGE ADEQUATE / GAPS NAMED / GAPS UNNAMED
```

### 4. Cost Model with Break-Even

The cost model exists to answer one question: at what volume does the agent pay back its cost. The PM who does not have this model in hand has not actually decided to build the agent; they have decided to start building, which is different.

The cost model has three layers, all required.

**Per-task cost.** Tokens times the architecture multiplier (typical agentic systems run 5 to 50 times raw model cost; coding agents 100 to 500 times; multi-agent systems add 30 to 40 percent coordination overhead), plus tool invocation costs, plus the human review time per task (the supervisor reading the output is not free), plus the rework cost when the supervisor catches an error.

**Floor price.** The minimum cost per task at the lowest plausible volume. Brownfield deployments have a different floor than greenfield because the existing team and tools already cover the marginal cost; greenfield carries integration, change management, and platform build costs that have to amortize.

**Break-even volume.** At what number of tasks per week does the per-task cost fall below the per-task cost of the human alternative. And then: is that volume achievable. Many agentic products break even at a volume the team cannot deliver. The math passes on paper and the agent loses money for the lifetime of the project.

Test the projection against volume variance. The projected volume is an estimate; the actual volume can be 0.5x or 2x what the plan says. Run the cost model at projected, half-projected, and double-projected volumes. If the agent loses money at half-volume but the team is confident it will hit projected, the team is committing to a volume guarantee that may not hold. The cost model that only clears at the projected line is brittle.

Walk the PM through this. Push hard on the architecture multiplier ("you have token cost in your model; what is the multiplier you are using and where does it come from"), the human review time (most teams omit this and discover they have built a system that requires more human time than the manual process replaced), and the rework cost (the agent's expected error rate times the cost of detecting and reversing each error).

Output format:

```
COST MODEL: <agent name>

Per-task cost components:
  Raw model inference: <$x>
  Architecture multiplier: <2-50x>
  Total compute: <$y>
  Tool invocation: <$z>
  Human review time (supervisor): <$w>
  Rework cost (expected error rate × reversal cost): <$v>
  TOTAL per task: <$T>

Floor price assumption: <greenfield / brownfield>
Justification: <2 sentences>

Per-task cost of the human alternative:
  <$H>

Break-even volume: <tasks per week>
Projected volume: <tasks per week>
Headroom: <projected - break-even>

Sensitivity to volume variance:
  At 0.5x projected volume: <verdict>
  At 1.0x projected volume: <verdict>
  At 2.0x projected volume: <verdict>

Verdict: ECONOMICS CLEAR / ECONOMICS DO NOT CLEAR / VOLUME UNCERTAIN
```

### 5. Go-or-No-Go Memo

The memo is the artifact the PM defends in the room. One page. It synthesizes the prior four artifacts into a single recommendation with a single owner. The memo is signed by the PM and circulated. The signature matters; an unsigned go-or-no-go memo is a wish.

Memo structure:

```
GO-OR-NO-GO MEMO: <agent name>
PM: <name>
Date: <date>

The question this memo answers:
Does an agent do this better than what we do today, at a cost and risk
the business can absorb?

Recommendation: GO / NO-GO / HOLD pending <named conditions>

The agent in one sentence:
<statement>

Why this is suitable for an agent (the six criteria, short form):
  1. Repeats at volume: <PASS/FAIL with one-line justification>
  2. Measurable AND trusted: <...>
  3. Bounded tool use: <...>
  4. Recoverable consequences: <...>
  5. Delegatable authority: <...>
  6. First-contact match: <...>

Why the economics close:
  Per-task cost: <$T>
  Break-even volume: <X>
  Projected volume: <Y>
  Headroom: <Y-X>

What we are not yet sure about:
  <2-3 risks with mitigation plan>

What we will produce in Phase 2 (Design):
  - The two briefs (Human Brief + Executable Brief)
  - Four runtime artifacts (autonomy boundary, approval moment, audit surface, recovery workflow)
  - Channel 2 composition (technical, organizational, regulatory, moral)
  - Adversarial defense plan

Signed: <PM name>
```

## Worked example: a refund agent

The artifact templates above are skeletons. Here is what one full pass looks like, filled in, for an illustrative refund agent. Use it to calibrate what the production version of each artifact should contain. Numbers and copy are illustrative and would be replaced by your team's actual figures and language.

### The agent in one sentence

An agent that reads incoming refund requests on the support team's queue, decides whether to issue the refund automatically, route it for supervisor approval, or escalate to a case manager, and either issues the refund or routes the case.

### Suitability Record (filled)

```
SUITABILITY RECORD: refund-agent-v1
Date: 2026-07-14
PM: J. Park

The agent in one sentence:
A refund agent that reads incoming refund requests, decides whether to
issue, route for supervisor approval, or escalate, and acts.

The decision class the agent owns:
For each incoming refund request, classify outcome (issue / approve /
escalate) and either execute or route accordingly.

Condition 1: Repeats at volume
  Estimated decisions per week: 8,500 (last 12 weeks, support queue)
  Source of estimate: support ticket system, refund-tagged tickets
  Verdict: PASS
  Reasoning: 8,500 weekly decisions, growing 4% quarterly. Decision
    class is bounded (refund or not, and how much), recurs at scale,
    and is not a one-off strategic call.

Condition 2: Outcome is measurable AND trusted
  Metric: weighted composite of (a) refund-approval-rate match against
    senior agent review on a 5% audit, (b) customer satisfaction
    follow-up survey within 48 hours, (c) fraud-flag false-positive rate
  Data source: support system + survey tool + fraud monitoring
  Trust assessment: senior leadership would stake refund-policy decisions
    on this metric set. CFO has signed off on the audit-rate and
    fraud-FPR components as decision-grade. CSAT survey response rate
    is 41%, which is the load-bearing weakness.
  User-trust dimension: customer experience surveys show 12% of refund
    interactions currently feel "unheard" with human agents. The agent's
    metric set has to include the same dimension or it will report a
    pass while customer trust degrades.
  Verdict: PASS (with named monitoring of survey response rate)
  Reasoning: composite metric covers correctness, customer experience,
    and fraud exposure. Each component is independently defensible.

Condition 3: Tool use is bounded
  Allowed actions: read order record, read customer history, read
    fraud-flag service, issue refund (up to $500), submit supervisor-
    approval request (any amount), route to case manager (any amount).
  Forbidden: cross-customer lookups, write to billing system outside
    the active order, any read or write on the chargeback system.
  Verdict: PASS
  Reasoning: action surface is enumerated, finite, and the boundaries
    are written. Engineering has confirmed each can be enforced at the
    tool-gateway layer (not just in prompt).

Condition 4: Consequences are recoverable
  Reversibility per decision class:
    Issue refund (auto, <$500): reversible via clawback within 72 hours;
      after 72 hours, write-down on the books (cost: full refund amount).
    Approve via supervisor: reversible at supervisor discretion.
    Escalate: no agent action taken; no recovery needed.
  Operational reversal capability: support team currently processes
    ~15 reversals per week from human-issued refunds. At 8,500 weekly
    agent decisions and an expected 0.5% wrong-refund rate, the agent
    would produce roughly 42 reversals per week, which is 2.8x current
    operational capacity. Mitigation: dedicated reversal queue with
    automated detection from the 5% audit; CFO has agreed to fund 2
    additional FTE for the reversal queue at launch.
  Verdict: PASS (with operational capacity gap named and funded)
  Reasoning: in principle reversible; in practice the team needs the
    funded reversal queue or the consequence becomes irreversible by
    operational backlog.

Condition 5: Delegatable authority exists, AND regulatory framework permits it
  Internal authority: support VP has authority to delegate refund
    decisions up to $500 to non-human actors per the support policy
    revision dated 2026-05-09.
  Regulatory permission: refund decisions in our operating jurisdictions
    (US, UK, EU, AU) do not require human decision-maker by regulation.
    Outside-counsel email dated 2026-07-08 confirms. No FDA, financial-
    services, or healthcare regulatory hooks apply to standard merchant
    refunds.
  Verdict: PASS
  Reasoning: both internal authority and regulatory permission confirmed
    in writing. Re-verify before any expansion to new jurisdictions.

Condition 6: First-contact match
  Training/eval data: 14 months of historical refund decisions with
    documented outcomes (approved / denied / reversed), 312k total
    decisions, distributed across regions matching production.
  Production first-contact: agent will see refund requests at the
    moment of submission, with the user's natural-language reason
    statement and order context. Training data includes the same fields.
  Verdict: PASS
  Reasoning: training data distribution matches production
    first-contact. One known mismatch: training data underweights
    Spanish-language requests (4% in training, 11% in production for
    the LATAM-adjacent segment). Flagged for distribution gap analysis.

Overall: GO pending the named conditions (reversal queue funded,
survey response rate monitored, Spanish-language coverage gap
addressed in distribution analysis).
```

### Cost Model (filled, condensed)

```
COST MODEL: refund-agent-v1

Per-task cost components:
  Raw model inference: $0.018 per decision (avg tokens × pricing)
  Architecture multiplier: 8x (typical for retrieval+tool agent, derived
    from a comparable agent we shipped six months ago)
  Total compute: $0.144
  Tool invocation (read order, customer history, fraud service): $0.012
  Human review time (supervisor on approval path, ~22% of cases):
    $0.95 fully loaded
  Rework cost (0.5% error × $42 reversal cost): $0.21
  TOTAL per task: $1.32

Floor price assumption: brownfield (existing customer-service platform
  with established tool integrations and observability)
Justification: agent runs on the existing support stack with marginal
  build cost; integration work is incremental, not greenfield.

Per-task cost of the human alternative: $5.40 (avg support agent time
  per refund decision, fully loaded).

Break-even volume: 1,200 tasks per week (covers floor cost amortization)
Projected volume: 8,500 tasks per week
Headroom: 7,300 tasks per week

Sensitivity to volume variance:
  At 0.5x projected (4,250/week): per-task cost $1.46, still clears
  At 1.0x projected: $1.32, clears comfortably
  At 2.0x projected (17,000/week): $1.21, clears with headroom

Verdict: ECONOMICS CLEAR at projected and at half-projected.
```

### Go-or-No-Go Memo (filled)

```
GO-OR-NO-GO MEMO: refund-agent-v1
PM: J. Park
Date: 2026-07-14

The question this memo answers:
Does an agent do this better than what we do today, at a cost and risk
the business can absorb?

Recommendation: GO, conditioned on three named items below.

The agent in one sentence:
A refund agent that reads incoming refund requests, decides whether to
issue, route for supervisor approval, or escalate, and acts.

Why this is suitable for an agent (the six criteria, short form):
  1. Repeats at volume: PASS. 8,500 weekly decisions.
  2. Measurable AND trusted: PASS. Composite metric covers correctness,
     CSAT, and fraud FPR; survey response rate at 41% is the
     load-bearing weakness, to be monitored.
  3. Bounded tool use: PASS. Action surface enumerated; tool-gateway
     enforcement confirmed by engineering.
  4. Recoverable consequences: PASS, conditioned on 2 additional FTE
     for the reversal queue funded by CFO.
  5. Delegatable authority AND regulatory permission: PASS. Internal
     delegation policy + outside counsel email on file.
  6. First-contact match: PASS, with Spanish-language coverage gap
     to be addressed in Phase 2 (Distribution Gap Analysis).

Why the economics close:
  Per-task cost: $1.32 (vs $5.40 human alternative)
  Break-even volume: 1,200 / week
  Projected volume: 8,500 / week
  Headroom: 7,300 / week
  Sensitivity: clears at 0.5x, 1.0x, and 2.0x projected volume.

What we are not yet sure about:
  - Spanish-language production share underweighted in training data.
    Mitigation: explicit eval coverage for the segment in Phase 3, with
    a separate threshold and a human-review fallback for low-confidence
    Spanish cases until coverage is proven.
  - 41% survey response rate may be sample-biased toward unhappy
    customers. Mitigation: incentive shift to lift response rate to
    60%+ within 60 days post-launch; until then, the survey metric is
    advisory not decision-grade.
  - Reversal queue capacity: planned 2 FTE additions assume our 0.5%
    error projection holds. If real wrong-refund rate is 2x, capacity
    breaks. Mitigation: hard ceiling on auto-issue volume per day
    (3,000 decisions max) until 6 weeks of production data confirms the
    error rate.

What we will produce in Phase 2 (Design):
  - The two briefs (Human Brief + Executable Brief)
  - Four runtime artifacts: autonomy boundary at $500 with hard
    enforcement at the refund API; approval moment with full case
    package; audit surface designed for the full retention period
    (3 years per finance) with version pinning; recovery workflow
    with reversal SLA and named owner.
  - Channel 2 composition: technical (eng platform team), organizational
    (support VP, with named supervisor pool), regulatory (legal,
    quarterly review), moral (PM-led customer-experience audit on
    affected-customer segments).
  - Adversarial defense plan: scoped to refund-fraud attack patterns,
    prompt injection on the reason-text field, and known patterns of
    refund-policy gaming.

Conditions on GO:
  1. CFO confirms 2 additional FTE for the reversal queue, before Design
     begins.
  2. Spanish-language coverage plan added to Phase 2 Distribution Gap
     Analysis, with explicit eval coverage target.
  3. Daily auto-issue ceiling (3,000) hard-coded at launch and held for
     6 weeks while error rate is measured.

Signed: J. Park
```

This worked example is the model. A serious Discover & Decide produces a document at roughly this length and specificity. If your version is significantly thinner, the work is not yet done.

## Returning to the headline question

As you walk the PM through the five artifacts, keep returning them to the headline question: does an agent do this better than what we do today, at a cost and risk the business can absorb. Every artifact is testing one half of that question or the other. When an artifact's verdict is uncertain, name which half of the headline question it threatens.

A suitability record with three PASS, two UNCERTAIN, and one FAIL on the six conditions does not fail the headline question because two conditions are unclear. It fails because the agent has not shown it is better than what we do today on a load-bearing dimension. Treat each artifact's verdict as evidence in the larger question, not as a checkbox to pass on its own merits.

If the suitability record passes but the cost model does not close, the headline question still fails. If the cost model is fine but the context sufficiency map shows the agent will not have what it needs, the headline question still fails. The artifacts are partial answers; the headline question is the decision.

## Munger inversion: what failure looks like

Before producing the artifacts, name the failure modes this phase prevents. The PM should be able to recite these. They are the answers to "what happens if we skip Discover & Decide."

**Solutions shopping for a problem.** The team commits to building an agent, then attaches it to the closest problem in reach. The agent gets built, gets deployed, and the team discovers in production that the problem did not need agency. Cost: the full build plus the cost of decommissioning plus the reputational cost of having shipped something nobody asked for.

**The MVP House of Cards.** The team builds an agent on top of an agent on top of an agent, each one passing its own MVP gate, none of them designed against the compound failure surface they form together. Cost: the system that emerges has no owner, no holistic eval, and no recovery path. When it fails it fails everywhere.

**Earned-vs-scheduled autonomy collapse.** The team advances the agent up the autonomy ladder on a calendar instead of evidence. The Utah Doctronic case is the canonical example: an agent moved to autonomous operation because a roadmap said so, not because it had demonstrated competence at the current rung. Cost: the autonomy is granted before the agent can hold it, and the first failure is in production.

**Economics that look fine and are not.** The team has a per-task cost in their model. They do not have the architecture multiplier. They do not have the human review time. They do not have the rework cost. The math passes on paper and the agent loses money for the lifetime of the project. Cost reductions on the order of 70 percent, the difference that has moved real agentic products from unviable to viable, are not engineering achievements; they are the difference between including these terms and not.

Klarna's reset is worth carrying here for the right reason, not the wrong one. The story is usually told as "they over-rotated to AI and walked it back," and that read makes Klarna a suitability failure. Book 2 Ch 3 frames it differently: the walk-back was the maturity. The team discovered, in production, the autonomy level the work actually supported, and corrected. The failure would have been refusing to walk it back. For your Discover & Decide, the lesson is that suitability is not a one-time verdict; the team needs the institutional capability to re-classify if the production read contradicts the original assessment.

**Context insufficiency caught in production.** The data flows. The fields are populated. The model reasons fluently. The answers are wrong because the semantic and relational context never made the trip. This failure is visible only in production. By that time the team has shipped, the supervisors have learned to trust the agent's tone, and the wrong answers are being signed by humans who could not have caught them.

When you produce the five artifacts, refer back to the failure modes. The artifacts exist to prevent specific failures. A suitability record without a real condition-three answer is a future tool-boundary failure. A cost model without the architecture multiplier is a future economics-do-not-clear failure. Name the failure each section prevents as you walk the PM through it.

## Handoffs

When the PM finishes this phase with a GO recommendation:

Hand off to `agentic-pm-design` to produce the four runtime artifacts, the two briefs (Human Brief and Executable Brief), the Channel 2 composition, and the adversarial defense plan.

The eval scope, cost, and timeline are intentionally not produced here. They are Design and Eval phase concerns, sized once the agent's behavior is specified. The PM should expect that a serious agent eval can take 2 to 4 weeks of focused work on the team's side, plus continuous re-eval thereafter; build that into the project plan even before exact numbers are known. If the team's resourcing cannot support that, surface it as a risk in the go-or-no-go memo, not as a reason to defer Discover & Decide.

When the recommendation is NO-GO:

The skill ends. The memo is the artifact. Some teams need a NO-GO memo more than a GO memo, because it documents the decision and the reasoning for the next person who shows up six months later with the same idea.

When the recommendation is HOLD:

The named conditions become the next sprint's work. Reinvoke this skill when the conditions have been addressed.

When the PM is reconstructing Discover & Decide work on a live troubled project:

Run the skill the same way, but mark the artifacts as "reconstructed post-launch" so the team knows the assessment is being done retrospectively. The artifacts may show that the project should not have shipped. That is useful information even now.

## Source

This skill is built from:

Book 1 (*Agentic AI for Busy Product Managers*), Chapter 3 "Not Every Problem Deserves an Agent." The original Discover & Decide foundation.

Book 2 (*Why Agentic AI Products Fail*), Chapter 3 "Not Every Problem Deserves an Agent" (six suitability criteria, brownfield/greenfield, architecture multiplier, Klarna as maturity, MVP House of Cards), Chapter 4 "How the Work Splits" (operating model and the two briefs structure as the downstream artifact).

Framework #27 (Agentic Suitability Assessment), #1 (Iceberg), #4 (MVP House of Cards), #34 (Earned vs Scheduled Autonomy), #9 (First-Contact Mismatch) in the canonical frameworks catalog.

Refer the PM to these sources when they want to go deeper. The skill is a working aid. The books are where the reasoning is.
