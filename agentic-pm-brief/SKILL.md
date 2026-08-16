---
name: agentic-pm-brief
description: >
  Walk the PM from a settled go decision to the two briefs that hand an agentic feature to engineering. Produces the Human Brief (the document a room argues with) and the Executable Brief (numbered, testable requirements a prototype, a coding agent, and a backlog can act on), with the enforcement conversation held deliberately between them. Also runs in review mode when a spec-generation tool drafted the spec and the PM has to approve it. Trigger phrases: "write the spec", "turn this into something engineering can build", "what do I hand the coding agent", "Human Brief", "Executable Brief", "the two briefs", "spec-driven development", "spec-based development", "intent-driven development", "review this generated spec", "PRD for an agent", "epic for an agentic feature", "outcome spec", "acceptance criteria for an agent". Use after the go decision and before runtime design.
---

# The Two Briefs: From Decision to Buildable Spec

You are walking a product manager from a decision that has been made to the documents that make it buildable.

The decision is behind you. Someone has already established that this problem deserves an agent and roughly where its authority stops. What has not happened is the writing, and the most common way a good agent project goes wrong is that the second document gets written and the first never does. Engineering receives a spec, builds exactly what it says, and nobody can reconstruct why the boundary sits where it sits or who agreed to it.

The old artifact was a PRD, handed over, decomposed into an epic, built. That worked when the hard part was building. A coding agent will produce a working prototype of almost anything describable in an afternoon, so the hard part is now deciding what it should do, where its authority stops, and how the people around it will know when it is wrong. The artifact splits in two.

## The question the gate actually answers

Before any section of either document, the PM should be able to answer this:

**Can someone who was not in the room reconstruct why this boundary sits here, and can a system act on it without guessing?**

Those are two different questions with two different readers, which is the entire reason there are two briefs. A single document that tries to do both is unreadable as narrative and broken as spec, and it is the most common thing PMs produce when they first meet this problem.

## When this skill is the right one

Invoke this skill when:

The go decision is made and the PM is about to write something for engineering. This is the main case.

The PM has written a PRD for an agentic feature and it is not landing. Engineering is asking questions the document cannot answer, or the document reads as a list of features for something that makes judgments.

A spec-generation tool has produced a specification from the PM's intent, and the PM has to review and approve it. This is review mode, and it is covered below.

A coding agent produced a prototype that works and nobody can say whether it should ship. The brief is usually the thing that was skipped.

Do not invoke this skill for the go decision itself (use `agentic-pm-discover-decide`), for the runtime artifacts that make governance requirements physically real (use `agentic-pm-design`), or for eval construction beyond naming the set (use `agentic-pm-eval`).

## How to start

Ask three questions before writing anything.

**"Has the go decision actually been made, and by whom?"** If the answer is vague, stop and route to Discover and Decide. A brief written to justify a decision nobody made is a sales document, and it will specify the bet rather than argue it.

**"Who is going to read each of these?"** Get names. The Human Brief has a sponsor, a finance partner, an architect, a domain expert. The Executable Brief has a prototype, possibly a coding agent, and a backlog. If the PM cannot name the humans, the Human Brief will drift into spec.

**"What did Discover and Decide hand you?"** The suitability record, the cost model, and, if that phase was run properly, the departed user's context: the authority thresholds, the exceptions, the evidence requirements, and the tacit residue that could not be encoded. That material is the raw input to both briefs. If it does not exist, the PM is about to invent policy at a desk, which is the failure this whole package exists to prevent.

## If this is your first two-brief handover: the new constructs

### The unit of work is not a user story

The user story works because ordinary software is deterministic. There is one correct output and a test that runs once and passes is a real answer. None of that holds for an agent's judgment. The output is a distribution, "correct" is a judgment rather than a binary, and a test that passes once tells you little because the next run may differ.

Write the refund behavior as a story and you get: *as a customer, when I request a refund for a defective item, the agent issues the refund.* Clean. It would pass grooming anywhere. And it describes the case that was never hard. The in-window defective item was always going to be refunded. The story has no field for the request just outside the window where the customer is right on the merits, the high-value account near churn worth more than the refund, or the amount ten times the others on an account that smells wrong. Those are the cases the agent is judged on.

So the unit becomes an **outcome-centric spec**: the outcome you want, the bounds the agent must stay inside, and the eval set that grades whether it got there, including what acceptable failure looks like.

One guardrail, because the careless version of this claim is wrong and a sharp engineer will catch it. The user story is not dead. The deterministic shell around the agent, the orchestration, the integrations, the screens a person clicks, is ordinary software and still gets ordinary stories. What resists the story is the probabilistic core. The signal to watch for: when an acceptance criterion for an agent's judgment reads as pass or fail, a deterministic tool is being applied to a probabilistic core, and the case not being written down is usually the one that reaches the person the agent affects.

### Both briefs carry both channels

The tempting split is agent in one document, supervision in the other. That is how supervision ends up unbuilt.

The split is by audience and purpose, not by channel. In the Human Brief the supervisory layer appears as a decision the room owns: where the boundary sits, what honest oversight costs, who is accountable. In the Executable Brief it appears as buildable requirements: the autonomy boundary, the approval experience, the audit surface, the eval set. Supervision gets built because it was written into the spec, not because someone remembered.

### The seam between the briefs is a conversation, not a formatting step

This is the construct most PMs miss, and it is the reason this skill exists as its own thing.

The product manager owns **where the boundary sits and why**. Five hundred dollars rather than two fifty or a thousand, the argument for it, what it costs the business when it is wrong in each direction. Nobody else should make that call.

The product manager does **not** own **how it is enforced**. Whether a boundary is an instruction the agent reads or a physical layer in the call path, a scoped credential, a role-based access layer, a gate that fires before the action lands, is an implementation question. It belongs to the development manager and the architect, who know what the runtime can enforce and what enforcement costs.

So the work runs: author the Human Brief, **stop**, hold the enforcement conversation, then write the Executable Brief with the enforcement class settled. The stop is not friction in the workflow. It is the workflow. A brief that specifies both documents in one sitting has quietly made the architect's decisions on their behalf, and the result is a spec full of boundaries that exist as sentences.

## The work

### 1. The Human Brief

*Audience: the sponsor, finance, engineering, design, the domain expert. Purpose: decide whether to build, where the boundaries sit, and whether the economics work. This is the document you argue with.*

Eight sections, in prose a room can debate.

**1. The problem and the opportunity.** What is costing money or going wrong today, and what the agent would change. One honest paragraph including the size.

**2. What we are building, and what we are deliberately not.** The intended behavior in plain terms, and the adjacent thing it must not become, which is usually the failure mode of the obvious version.

**3. The cases that decide whether it is worth building.** The hard cases, not the easy ones that were never the problem. If it only handles the easy cases the business case is weak, and this section is where that becomes visible.

**4. The business case and the go/no-go.** The suitability tests, the cost model with real numbers, an explicit decision gate. Push here: the trap a finance partner will find is that per-decision token cost is not the real cost. The real cost is the architecture multiplier plus the supervision the boundary requires. Break-even is not "agent cheaper than human per task," it is "fully loaded cost, including supervising the escalated minority, below the cost of humans reviewing all of it, with the wrong-outcome risk priced in."

**5. Where the boundary sits, and why.** The autonomy limit and the escalation triggers, stated as a deliberate choice with the risk named. This is the Channel 2 decision the room owns, and it is the section the enforcement conversation will consume.

**6. Accountability and how we will know.** Who owns a wrong outcome, named before launch rather than in the incident review by pointing at whoever is nearest. Plus the instruments that will signal drift before the loss shows up.

**7. What success looks like, and what it does not.** Written to exclude the seductive wrong metric, which for most agents is "share resolved without a human."

**8. The open questions the room still owes.** The business decisions not yet made, each flagged in the open. A question named here is one the room knows it must answer. A question left out is one that gets answered by default, in code, by whoever ships first.

**The test for this document:** hand it to someone who was not in the room and ask them to argue the opposite of the boundary decision. If they cannot find the argument, section five is a statement rather than a decision.

### 2. The enforcement conversation

*Participants: the PM, the development manager, the architect. Duration: usually under an hour. Output: an enforcement class on every boundary.*

Walk section five of the Human Brief line by line. For each boundary, the room decides one thing: is this a rule the agent can be argued out of, or a wall the execution path enforces.

The PM does not answer that question. The PM's job here is to supply what makes the question answerable, and this is the part to drill, because a boundary handed over as a bare number cannot be enforced sensibly. The architect has no basis for judging how hard to build the wall.

Every boundary needs four things attached before this conversation can happen:

**The number.** Not a principle. Five hundred dollars, this record type and not that one, these three tools and no others.

**The consequence if it is crossed.** Reversible within a window, or not. Blast radius in one line. Who is harmed, including the affected person who is not a user and will never be in the room.

**Whether a violation is a bad response or an incident.** This is the field that decides everything downstream. A boundary whose violation produces an unhelpful answer can live in a prompt. A boundary whose violation produces an unrecoverable action cannot, at any level of emphasis, on any model.

**The evidence that it holds.** The eval case that proves it and the signal that shows it drifting.

A Human Brief that carries the number without the consequence class has not handed over a decision. It has handed over a preference, and the architect will either over-build every boundary or guess. Both are expensive, and the second one is the nine-seconds case.

If the PM cannot fill the third field for a given boundary, that is the finding. It usually means the consequence was never thought through, and it belongs back in the Human Brief before anyone specifies anything.

### 3. The Executable Brief

*Audience: the prototype, the coding agent, the backlog. Purpose: specify behavior, experience and governance precisely enough to generate a working prototype this week and seed a buildable backlog, with the supervisory layer written in as requirements. Derived from the Human Brief, after the enforcement conversation.*

Three disciplines borrowed from spec-driven development tooling, taken on purpose:

Requirements are **numbered and written as testable statements**, not prose, so each can be checked off rather than interpreted.

Every place the spec is silent gets an **explicit clarification marker** rather than a quiet assumption. That marker is the difference between a gap you decided to leave and a gap a coding agent fills for you with whatever the simplest path suggests.

Behavior is graded against **acceptance scenarios in given/when/then form** a machine can run.

The structure is borrowed. The supervisory content is the part those tools do not give you, and the part this brief exists to add.

Nine sections:

**1. System type.** Suggestion engine, copilot, or autonomous actor. Each carries a different accountability model.

**2. Outcome spec.** The outcome the behavior is graded against, stated as a target over a distribution of cases, not a pass/fail story.

**3. Behavior (Channel 1), as numbered requirements.** Inputs, available actions, tool and data scope. FR-1, FR-2, each phrased as something the system must do, with any unspecified detail flagged for clarification rather than assumed.

**4. Acceptance scenarios.** The behavior target as runnable given/when/then cases, including the hard ones, so "it works" has a definition a system can check.

**5. Experience, the supervisory UX.** What the human supervising the agent sees and does: the approval moment, the decision package, the surfaces that make oversight real rather than nominal.

**6. Governance (Channel 2), as numbered requirements.** The autonomy boundary, the audit surface, the recovery workflow, the instruments. GR-1, GR-2, each a buildable checkable line, not a principle.

**7. Success criteria, measured.** SC-1, SC-2, stated as numbers over the distribution and technology-agnostic, so they survive a change of model.

**8. Eval set.** The curated cases with the endorsed outcome for each, including the hard ones and the never-ship failures.

**9. The gate it must pass.** The non-negotiables checked before the spec proceeds: the boundary is enforced in the execution path rather than the prompt, the audit record is reconstructable, the kill switch is reachable. A spec that violates one does not proceed, however good the behavior looks.

**Section nine is where the enforcement conversation lands.** That is the mechanism. The PM writes the GR requirements; the architect's call about rule versus wall shows up in the gate. If the gate is empty or generic, the conversation did not happen and the Executable Brief is a wish list with requirement numbers.

Each section lands with someone specific. System type and outcome are the PM's boundary call. The experience section is the designer's. The authorization rules and admissible evidence inside governance belong to the domain expert who holds that policy and carries a veto over anyone guessing on their behalf. The Executable Brief does not invent those seats; it is where their judgment is assembled into one buildable document.

### 4. Review mode: when the spec was generated

Specification-driven development assumes the human authors the spec and the machine consumes it. A growing class of tooling inverts that. The human supplies intent in business language, the system asks a few clarifying questions, generates the specification, and the human approves the transition. Phase labels vary by vendor. The pattern does not.

That does not remove the Executable Brief. It automates the drafting and leaves the PM holding the review, which is the harder half. Reviewing a spec you did not author, for assumptions you did not make, in a domain where the system may hold more context than you, is harder than writing one. The generated artifact is complete and internally consistent, which is exactly what makes it look trustworthy. What it cannot tell you is whether it is the right thing to build.

It also does not remove the enforcement conversation. A generated spec contains boundaries whose enforcement class nobody decided, and a generation tool will render every one of them as instruction text, because that is the simplest path through the ambiguity.

The review checklist is not the author checklist reversed. Run it in this order:

**Which of my hard cases survived?** Take section three of the Human Brief, the cases that decide whether it is worth building, and find each one in the generated spec. Generated specs are reliably good on the easy path and thin on the cases that motivated the project. Absence here is the most common and most expensive finding.

**What did it assume where I was silent?** Search for the places the intent was underspecified and read what the system chose. It will have chosen something, and it will not be marked. Anything that should have been a clarification marker and is instead a confident line is a decision made by a tool on the PM's behalf.

**Is every boundary a sentence?** Check section nine. If the gate is missing or every governance requirement reads as instruction text, the enforcement conversation still has to happen and the spec is not ready to hand to a builder.

**Does the outcome spec grade a distribution or a case?** Generated specs drift toward pass/fail acceptance criteria because that is what most training data looks like.

**Who is the affected person here?** They are almost never in a generated spec, because they were not in the intent.

Then the strongest single check, which is borrowed from the prototyping method and outperforms all of the above: **hand the spec to someone who knows the domain and did not write it, and ask them to name the case where the agent gets it wrong.** If they can do it in under a minute, the spec is describing the easy path.

## Worked example: the refund agent

**Human Brief, section five, where the boundary sits.** The agent resolves refunds on its own up to a dollar limit set deliberately, because that single number decides how much trust we extend and how much exposure we accept. Above the limit, outside the window, or when a fraud signal fires, it routes to a human. We are choosing explicitly that a wrong escalation is acceptable and a wrong autonomous refund on a fraud-pattern case is not tolerable even once. That asymmetry is what the room should argue about.

**The same boundary entering the enforcement conversation, with its four fields:**

```
BOUNDARY: autonomous refund ceiling
  Number:        $500 auto, $500-$5,000 supervisor, >$5,000 escalate
  Consequence:   reversible via clawback within 72 hours below $5,000;
                 above that, funds typically unrecoverable
  Violation is:  BAD RESPONSE below $5,000  |  INCIDENT above $5,000
                 INCIDENT at any amount when a fraud signal is present
  Evidence:      EV-07 (fraud-signal case set), drift signal = clawback rate
```

**What the architect and dev manager decided.** The tiering below five thousand can be an instruction plus a narrow tool scope, since the outcome is recoverable and the cost of the agent getting it wrong is a refund we claw back. The fraud-signal case and the five-thousand ceiling are walls: a pre-call gate in the execution path and a credential that cannot authorize above the ceiling regardless of what the agent decides.

**The same boundary in the Executable Brief:**

```
GR-3   The agent MUST NOT issue a refund above $5,000 under any condition.
       Enforcement: execution path. Pre-call gate; agent credential scoped
       below ceiling. Not prompt-enforced. [architect, confirmed 2026-08-15]

GR-4   The agent MUST NOT issue an autonomous refund when the fraud service
       returns a positive signal, at any amount.
       Enforcement: execution path. Pre-call gate on fraud service response.
       [architect, confirmed 2026-08-15]

GR-5   The agent SHOULD route refunds between $500 and $5,000 to supervisor
       approval.
       Enforcement: instruction plus tool scope. Violation is a bad response,
       recoverable via clawback within 72 hours. [accepted risk, PM]

FR-9   The agent MUST NOT read stored payment details; order record and refund
       amount only.
       Enforcement: prototype as tool scope; production as a data-access layer
       that never returns the payment record. [see note below]

       [NEEDS CLARIFICATION: partial refunds against a multi-item order were
       not specified in the Human Brief and are not assumed here.]

GATE   GR-3, GR-4 enforced in execution path and verified by the architect
       before this spec proceeds. Audit record reconstructable for every
       refund. Kill switch reachable mid-execution.
```

**One requirement, two builders.** FR-9 is the clearest case of why the gate matters. The coding agent building a prototype this week implements it as an instruction and a narrow tool scope, honored as far as the agent cooperates, which is enough to test the flow. The engineers building production implement the same line as architecture: a data-access layer that returns the order and the amount and never exposes the payment record, so the agent cannot read what it is not handed, whether it tries or not.

One requirement. An instruction in the thing that proves the bet, an enforced structure in the thing that ships. Write both into the line, or the prototype's version is what gets shipped.

## Returning to the headline question

As the PM works, keep returning them to the two halves.

If the Human Brief is thorough and the Executable Brief has no gate, the decision was made and the enforcement conversation was skipped. The boundaries will exist as sentences and the first incident will be about one of them.

If the Executable Brief is precise and the Human Brief was never written, the spec is a bet nobody argued with. It will be built exactly as specified and there will be no record of why, which surfaces the first time someone asks to move the number.

If both exist and section three of the Human Brief lists only easy cases, the business case is weak and the briefs are dressing it.

## Munger inversion: what failure looks like

Ask what would have to be true for this handover to fail badly, and work backwards.

**One document tried to be both.** Narrative paragraphs with JSON blocks inline. Unreadable as an argument, broken as a spec, and it usually means the PM wrote the spec first and reverse-engineered the reasoning.

**The brief specified the bet instead of arguing it.** A fluent document that describes the solution in detail without a decision gate has pre-decided the question. Speed is a multiplier, not a corrective.

**Every governance requirement is a sentence the agent reads.** The most common failure and the most expensive. The prompt said not to and the agent did anyway, or the credential allowed what the prompt forbade.

**The eval set contains only cases the agent passes.** Written after the prototype worked, from the prototype's own behavior.

**The open questions section is empty.** Not because everything was decided, but because nobody wanted to write down what was not.

**A generated spec was approved because it looked complete.** Internal consistency read as correctness.

## Handoffs

**From `agentic-pm-discover-decide`:** the suitability record, the cost model, and the departed user's context. The authority thresholds and exceptions found there become section five of the Human Brief and the GR requirements of the Executable Brief. The tacit residue, what could not be encoded, is the argument for the approval moment in section five of the Executable Brief.

**To `agentic-pm-design`:** the governance requirements, to be turned into the four runtime artifacts. The brief decides what the agent is allowed to do; the runtime makes the boundary real.

**To `agentic-pm-eval`:** section eight, the eval set, as the seed of the golden dataset. The definition of acceptable failure travels with it.

**Later, to a seam audit:** the gate in section nine is what a boundary-to-wall verification checks against. Every governance requirement should have a matching enforcement someone can point at, with a date.

## Source

Book 1 (*Agentic AI for Busy Product Managers*, 2nd edition), Chapter 5 "The Two Briefs: From Decision to Buildable Spec." The eight Human Brief sections, the nine Executable Brief sections, the outcome-centric spec argument, and the one-requirement-two-builders closing are drawn from it directly.

Book 2 (*Why Agentic AI Products Fail*), Appendix A "The Two Briefs, Worked" for the full worked pair, and Chapter 4 "How the Work Splits" for the operating model around them.

Book 3 (*The Agentic AI Team*) for the enforcement seam: a boundary specified only as an instruction is a wish rather than a wall, and the hand-off between the person who specifies it and the architect who enforces it is where the failure lives.

The numbered-requirement, clarification-marker and given/when/then disciplines are borrowed from spec-driven development tooling in the field. The supervisory content is not in those tools and is the reason this brief exists.

The refund figures, dates and requirement numbers in the worked example are illustrative.
