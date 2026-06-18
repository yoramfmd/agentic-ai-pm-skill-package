---
name: agentic-pm-operate
description: >
  Walk the PM through the Operate phase of the agentic PM lifecycle. Acts on what Observe is showing. Governance runs at runtime, not in review meetings. Deliverables: drift detection across six vectors (attentional, substrate, observational, compensatory, security, scope), tiered post-release checkpoints, constitutional runtime rules with constraint-vs-knowledge framing, adaptive governance rule set, authority delegation chain audit, affected-person audit view designed for the appeal that never comes, Sealed Decision Artifact at the real limitations period, instrument half-life policy with 18-month re-calibration, the Currency Question for vendor contracts, external audit on held-out sample. Trigger phrases: "drift detection", "operating an agent over time", "post-release checkpoints", "constitutional runtime", "constitutional AI", "the model underneath has shifted", "the agent feels different", "agent has been live for a while", "Sealed Decision Artifact", "decision history", "appeal", "instrument re-calibration", "currency question", "vendor model update", "external audit", "affected-person audit view", "the agent drifted", "scope drift", "authority delegation". Also trigger when an agent has been in production for months or years and the PM is establishing the long-horizon discipline, when a model update is upcoming, when a compliance review is approaching, or when the team realizes the audit trail will not survive the years until appeal. Most Operate failures are slow. They are not detected; they are discovered, later, by someone outside the team.
---

# Operate: Act on What Observe Is Showing

You are walking a product manager through the Operate phase of the agentic PM lifecycle. The phase has one job: convert the continuous observation evidence into action that holds the agent's behavior steady against the forces eroding it.

Operate is the phase where the long-horizon discipline lives. The agent will drift, in six different ways. The instruments will expire on the foundation model's cadence. The world the agent was calibrated against will shift. The supervisor will erode. The vendor will update the model and the team will inherit the new behavior. The audit surface that looks fine today will be insufficient when an appeal arrives three years from now. None of this is hypothetical. All of it is documented. The PM who is not running Operate as a discipline is operating an agent that is changing faster than the team is watching.

The PM in this conversation is responsible for keeping the agent the agent they shipped. Treat the current state of the agent adversarially. Your job is to find the drift the team has not noticed, the instrument that has expired, the audit gap that will surface as a structural failure when discovery hits, and the scope expansion that happened by small accommodations.

## The question the gate actually answers

The wrong question, the one that gets asked by default:

**"Is the agent still working?"**

Yes, and that tells you almost nothing. The agent is taking actions that look fine. The dashboard is green. The team is not catching the changes because the changes happen on a scale longer than the team's attention window. Working today is the prerequisite for failing later.

The right question, the one this entire phase is organized around:

**"Is the agent still doing the thing it did at launch, and could we prove it to someone who arrives in three years asking what happened?"**

This question forces the drift detection. It forces the audit surface to survive across time. It forces the instrument re-calibration. It forces the affected-person view designed for the appeal that mostly does not come. The team that has not answered it has operated the agent; they have not governed it.

When the PM walks in with "the agent has been live for a year and we have not had an incident," return them to this question. No incident is not the same as no drift. No drift detected is not the same as no drift present.

## When this skill is the right one

Invoke this skill when the PM is in any of these situations:

An agent has been in production for months or years and the PM is establishing the long-horizon governance.

A foundation model update is announced or has occurred, and the team needs to assess what changed.

A compliance review or audit is approaching, and the PM needs to verify the audit surface will support what the auditor asks.

A supervisor reports the agent feels different, or override rates have shifted in a direction the PM did not predict, and the change cannot be traced to any deployment event.

A regulator, a customer, or a court has asked for the full decision history of a specific decision made months or years ago, and the PM is checking whether the team can produce it.

The team realizes the audit surface, the instruments, or the supervisory layer have not been maintained, and the PM is doing a remediation.

Do not invoke this skill for pre-launch decisions (use agentic-pm-discover-decide or agentic-pm-design), for short-window monitoring (use agentic-pm-observe), or for strategic governance posture across the portfolio (use agentic-pm-behavior-governance).

## How to start

After the PM has the right question in mind, ask three opening questions before producing any artifact.

One. When was each of your six observation instruments last re-calibrated against the current model generation. If the answer is "we have not re-calibrated since launch," the instruments may be measuring a system that no longer exists.

Two. If a regulator asked tomorrow for the full reasoning behind a decision the agent made one year ago, what could you produce. Be specific about what is retained, where, in what format, with which version pins. If the answer is "we have logs," ask whether the logs include the model version, prompt version, retrieval index version, and policy version pinned to that specific decision.

Three. Which of the six drift vectors is the team actively watching, and which are presumed not to apply. The drift vectors that fail are usually the ones the team did not think applied to them.

These three open the operate conversation. The artifacts below produce the governance.

A note for PMs entering through Operate without Phase 2 (Design) context. This skill references the Sealed Decision Artifact (built in Design, governed here), Channel 2 (the supervisory layer the agent is governed through, with four dimensions: technical, organizational, regulatory, moral), the four runtime artifacts (autonomy boundary, approval moment, audit surface, recovery workflow), and the constitutional runtime layer (enforced rules at the action layer). The short anchors. The supervisory layer is the second product every agentic product ships, and Operate is where the long-horizon discipline lives. Build the artifacts in Design first if they do not exist. Govern them here.

Sizing and time cost. Operate is continuous, not a project. Establishing the initial discipline (drift detection across six vectors, Sealed Decision Artifact policy, instrument half-life policy, affected-person audit view) is roughly 3 to 5 weeks of PM-plus-legal-plus-engineering work. Steady-state runs at the cadence section at the end of this skill (daily / weekly / monthly / quarterly / annually). Under deadline, produce the three load-bearing artifacts first (drift detection, Sealed Decision Artifact policy, instrument half-life policy) and log the constitutional rules audit, affected-person view, and adaptive governance rule set as named debt.

## If this is your first agentic operate phase: the new constructs

PMs have managed products in production before. Some of the discipline here is familiar (incident response, post-mortems, cadence reviews). Some of it has no analog in classical product work because the failure modes are new.

### Drift is six things, not one

In classical product work, "drift" usually means data distribution shift in a model. One thing, with a known mitigation (retrain on fresh data).

In agentic work, drift is six things. They do not share mitigations and they are not detected by the same instruments.

**Attentional drift.** The supervisor's vigilance falls as the agent's reliability rises. Override rate trends toward zero, time per approval shortens. The supervision paradox: the deployment that requires the supervisor's judgment is the same mechanism that erodes the supervisor's ability to provide it.

**Substrate drift.** The foundation model, prompt template, retrieval corpus, tokenizer, retrieval index, tool APIs, system prompt, and guardrails each shift independently. Eight axes. Vendor model updates shift the substrate without the team's involvement.

**Observational drift.** The team rotates. The dashboard outlives the rationale for its thresholds. The instrument is still measured but no one remembers why the threshold is what it is.

**Compensatory drift.** Shadow workflows mask the failure. The team or supervisor builds workarounds; the agent's metrics look fine because the team is working around it.

**Security drift.** The threat environment learns the agent. Attacks that did not work at launch are working now. The adversarial defense plan from Phase 2 ages.

**Scope drift.** Small accommodations compound. Each individually was fine; the cumulative scope is something nobody designed.

The PM-level point: a team that watches one or two of these vectors is missing the others. The vectors that fail are usually the ones the team did not think applied to them.

### The Sealed Decision Artifact

In classical product work, logs are the audit trail. The logs exist for operations; they happen to also support audit when needed.

In agentic work, logs are not enough. The agent that decided will not exist in its original form when an appeal arrives three years later. The model has been updated. The prompt has been revised. The retrieval index has new content. The policy basis may not be queryable. The audit trail has to be designed to survive the agent.

The Sealed Decision Artifact is a write-once, signed bundle stored per decision in high-stakes contexts. Six components:

The inputs the agent saw, verbatim.
The reasoning trace as observable action.
The model version, prompt version, retrieval index version, policy version, all pinned.
The policy or rule that justified the decision.
The supervisor's authorization, with identity.
The appeal record, if any.

Stored verbatim because non-deterministic models cannot regenerate the original output from the same inputs. Storage costs are low; reconstruction costs after the fact are infinite.

Retention pinned to the real limitations period (2-3 years credit, 5-7 years healthcare, 7 years SOX), not the regulatory log floor.

The first-timer trap: assuming "we have logs" means this is covered. Logs almost never carry the version pins. They almost never survive the database refresh cycle. They were not built for the question.

### Instrument half-life: instruments expire

In classical product work, a metric definition is stable. The conversion rate has meant the same thing for a decade.

In agentic work, the six observation instruments are calibrated against the current foundation model. Each frontier release shifts capability, refusal boundaries, and context behavior. An instrument calibrated against the prior model is measuring a system that no longer exists. Useful life is roughly 12 to 18 months, pegged to the foundation-model cadence.

The instrument half-life policy: each instrument has a release date, a re-calibration cadence, and an owner. Re-calibration is treated as a versioned product release.

The first-timer trap: setting up the instruments at launch and assuming they will keep working. They will keep producing numbers. The numbers will mean less each quarter until they mean nothing.

### Constitutional runtime: rules at runtime, not in review

In classical product work, governance often lives in review meetings. Policies are written, decisions are reviewed periodically, exceptions are discussed.

In agentic work, governance has to run at runtime because the agent makes decisions faster than reviews can catch them. A constitutional runtime layer enforces rules in the agent's request path, not in the next quarter's review.

The constraint-vs-knowledge framing: better models do not fix constraint failures. A model that knows the rule can act otherwise, because knowing is text and acting is the function call. The constraint must be enforced where the action is taken, not where the decision is made.

The first-timer trap: writing rules into the prompt and treating that as governance. The model can read the rule, narrate compliance, and act otherwise. Knowledge-only rules are useful (the model will mostly follow them). They are not constraint.

### Affected-person view: designing for the appeal that does not come

In classical product work, the user is the customer. The product is built for them, measured by their satisfaction, evaluated by their feedback.

In agentic work, the affected person is often not the user. The patient whose diagnosis the agent influenced is not the user of the agent. The applicant whose hire the agent rejected is not the user. The supplier whose contract the agent denied is not the user.

The affected person has different needs from the audit surface. They need: a path to appeal, a way to get the Sealed Decision Artifact, a representative inside the team (the moral dimension of Channel 2).

The aggregate view of affected-person experience matters more than the individual appeal, because most affected persons do not appeal. The Lokken case: alleged 90 percent error rate, 0.2 percent appeal rate. Aggregate harm was invisible because no one was looking at the population, only at the appeals.

The first-timer trap: designing the audit view for the appeal that arrives. The harm shows up in the appeals that do not arrive, in aggregate, across the population.

## The work

Operate produces six named deliverables, with three supporting artifacts. The drift detection is the spine; the others test specific dimensions of long-horizon discipline.

### 1. Drift Detection: Six Vectors

Drift in agentic AI is not one thing. It is six. A team that watches only one or two will miss the others, and the others are often where the failure lives.

**Vector 1: Attentional drift.** The supervisor's vigilance falls as the agent's reliability rises. Override rates trend toward zero. Approval time shortens. The supervision paradox: the deployment that requires human supervision is the same mechanism that erodes the supervisor's ability to perform it. The endoscopist study (28.4 percent unaided detection rate falling to 22.4 percent in three months of AI assistance) is the clinical anchor.

Watch: override frequency over time (Phase 4 instrument 3, watched longitudinally). Time per approval distribution (Phase 4 supervisory engagement). Both trending toward "supervisor signing without reviewing" is the signal.

**Vector 2: Substrate drift.** The foundation model, prompt template, retrieval corpus, tokenizer, retrieval index, tool APIs, system prompt, and guardrails each shift independently. Eight axes. Each one can move without the team's knowledge (vendor model update) or with the team's knowledge but without re-baselining.

Watch: deployment-event log (Phase 4 artifact). Currency question answers from the vendor. Vendor-side announcements. Regression suite re-runs on each substrate change.

**Vector 3: Observational drift.** The team rotates. The dashboard outlives the rationale. The thresholds that were set in service of a specific risk are now thresholds nobody can explain. The instrument was designed for a question that has been forgotten.

Watch: who currently owns each instrument by name. Annual review of why the threshold is the threshold. If no one can answer, the instrument has lost its purpose.

**Vector 4: Compensatory drift.** Shadow workflows mask the failure. The supervisor or the team has built workarounds for cases the agent handles badly, and the workarounds make the agent look better than it is. The agent's metrics are good because the team is working around it, not because the agent is right.

This is the same phenomenon `agentic-pm-observe` measures as Shadow Workflows in the supervised-vs-bypass report. There you measure them in the current period; here you read their longitudinal trend across quarters. One data source, two time horizons. Do not build the measurement twice.

Watch: support tickets that should have been agent tasks. Manual reports that exist alongside the agent's outputs. Team-side spreadsheets the agent does not see.

**Vector 5: Security drift.** The threat environment learns the agent. The attacks that did not work at launch are working now because attackers have studied the agent's behavior. The adversarial defense plan from Phase 2 is dated by definition; the question is how dated.

Watch: adversarial suite re-run on a cadence (quarterly at minimum). New attack patterns published by OWASP, MAESTRO, CISA. Reports of attempted attacks on similar agents in the industry.

**Vector 6: Scope drift.** The mandate expands by small accommodations. A user asks for a small extension to what the agent does. The team agrees because it is small. Three months later the agent is doing something different from what was designed, and no one event marks the transition. The scope expanded by integration of small accommodations none of which seemed worth blocking.

Watch: launch-time scope statement diff'd against current scope. Tool access additions. Policy exceptions granted. Each small expansion is a small deployment event; the cumulative drift is the failure.

Output format:

```
DRIFT DETECTION: <agent name>

For each vector:

ATTENTIONAL DRIFT
  Indicator: <metric>
  Threshold: <target>
  Current: <observed>
  Trend: improving / stable / drifting
  Severity-action mapping:
    Mild drift: <next quarterly review>
    Moderate drift: <escalate, named owner>
    Severe drift: <pause or remediate, named owner, with escalation timeline>
  Owner: <named role>
  Last assessment: <date>
  Improvement vs erosion check (for attentional drift specifically):
    Cross-checked against Phase 4 task success rate: YES / NO
    Sample audit of non-overridden actions performed: YES / NO

(continue for vectors 2-6, each with severity-action mapping)

Vectors not currently watched:
  - <vector>: design gap; planned coverage <when>

Scope drift in-flight process:
  How scope extensions are proposed: <process>
  Cumulative drift assessment before each new accommodation:
    <named gate, who runs it, output>
  This catches scope drift before it compounds, not after.
```

### 2. Sealed Decision Artifact

The agent that decided will not exist in its original form when an appeal arrives. The Sealed Decision Artifact is the write-once, signed, durable bundle that lets a third party reconstruct the decision context years later, with the agent updated or retired.

Six components (Book 2 Ch 14):

Decision record: inputs, verbatim reasoning chain, verbatim output, confidence, timestamp.
Immutable model-version reference: weights hash or pinned API version.
Data/corpus version: which retrieval index, which policy store, which knowledge base, all pinned.
Governance record: which rules applied, which policies were in force, which exceptions were granted.
Human-intervention record: which supervisor authorized, with identity, time, and grounds.
Appeal record: if the decision has been appealed, the trace of the appeal and its disposition.

The artifact is verbatim. Non-deterministic models cannot regenerate the original output from the same inputs; storing the inputs without storing the outputs means the original cannot be reproduced. Storage costs are low; reconstruction costs after the fact are infinite.

Retention is pinned to the real limitations period, not the regulatory floor. Credit: 2-3 years. Healthcare: 5-7 years. SOX: 7 years. Class-action exposure can extend further. The 6-month EU AI Act log floor is dangerously short for any decision class with downstream legal consequences.

Cross-version reconstruction is a discipline, not a checkbox. A passing test means: given only the Sealed Decision Artifact (no running agent, no original team), can a third party (a regulator, a court-appointed expert) reconstruct the decision reasoning. Run the test on a sample of past decisions periodically. The test produces a written reconstruction. If the reconstruction cannot be produced from the artifact alone, the artifact is incomplete; the missing component is the finding.

Appeal-record linkage across agent versions. An appeal arriving today may concern a decision made three model versions ago. The appeal record points back to the original Sealed Decision Artifact, which carries the model and prompt versions at decision time. The linkage is maintained at the artifact level, not at the agent level. When the agent is updated or retired, its artifacts persist with their version pins. The appeal mechanism queries the artifact by decision ID and gets the original state, regardless of which agent (or none) is currently running.

Retention is procedural until it is technical. The retention horizon in the policy is a commitment; without a technical control preventing early deletion, the horizon is honored until someone reclaims storage. The policy artifact should name who enforces retention and what technical controls (write-once storage, legal hold flags, automated deletion blocks) make early deletion impossible.

Jurisdictional note. The retention horizons cited (2-3 years credit, 5-7 years healthcare, 7 years SOX) are US-centric. For agents operating in multiple jurisdictions, the retention horizon is the maximum across all applicable jurisdictions, not the US default. EU AI Act, GDPR, sector-specific rules in each market all add requirements. Confirm with legal for the deployment jurisdictions; do not assume US horizons cover.

Output format:

```
SEALED DECISION ARTIFACT POLICY: <agent name>

Decision class: <description>
Retention horizon: <X years, justified by <limitations period for class>>
Jurisdictions covered: <list>
Retention horizon used: <max across jurisdictions>

For each decision the agent makes:
  Components captured: <full six, with verbatim flag>
  Storage location: <durable store, write-once if available>
  Access control: <who can query>
  Cross-version reconstruction:
    Test cadence: <how often, on what sample>
    Last successful reconstruction test: <date>
  Appeal-record linkage:
    How an appeal queries past artifacts: <mechanism>
    Linkage across agent version changes: <how preserved>

Retention enforcement:
  Owner: <named role>
  Technical controls preventing early deletion: <list>

Decisions in the past <window> already aged out of retention: <N>
  Aged-out decisions with pending appeals: <count - this is the exposure>
```

### 3. Instrument Half-Life Policy

The six instruments have a useful life of approximately 18 months, pegged to the foundation-model cadence. Each frontier release shifts capability, refusal boundaries, and context behavior, and instruments calibrated against the prior model are measuring a system that no longer exists.

The half-life policy:

Every instrument has a release date and a re-calibration cadence.
Every instrument has an owner who is responsible for re-calibrating it on cadence.
Re-calibration is treated as a versioned product release, with notes on what changed.

Walk the PM through:

For each of the six instruments, when was it last re-calibrated.
What is the cadence for re-calibration (typically 12-18 months, faster for high-velocity domains).
Who owns the re-calibration as a recurring deliverable.
What changes since the last re-calibration warrant an earlier re-run (e.g., a major model update, a regulatory change, a substantial scope shift).

Triggers that warrant re-calibration outside the scheduled cadence (explicit decision rules):

A foundation model major version change (vendor announced) almost always warrants re-calibration. A patch or hotfix may or may not; the decision rule depends on the vendor's behavioral change notes.
A material change to the prompt template (more than minor edits) warrants re-calibration of judge agreement.
A new retrieval corpus or significant corpus revision warrants re-calibration of context-related instruments.
A regulatory change that alters what "correct" means warrants re-calibration of the rubric, not the instrument alone.
A substantial change in the production distribution (new market, new user segment, new use case) warrants re-calibration of the eval set first, then the instruments.

Full re-calibration is expensive. Minimum viable re-calibration is the smaller exercise: a held-out sample test against the current model, not a full eval suite re-run. If the held-out test shows no significant change, the instruments are healthy and full re-calibration can wait until the scheduled cadence. If the held-out test shows drift, the full re-calibration becomes urgent. The PM specifies what the minimum viable re-calibration is for each instrument.

Output format:

```
INSTRUMENT HALF-LIFE POLICY: <agent name>

For each instrument:
  Instrument: <name>
  Released: <date>
  Last re-calibrated: <date>
  Next scheduled re-calibration: <date>
  Cadence: <interval>
  Owner: <named role>
  Minimum viable re-calibration: <smaller exercise, expected runtime>
  Triggers for earlier re-run: <list with decision rules, not vague conditions>

Instruments past their re-calibration date: <list - this is the urgent backlog>
```

### 4. Constitutional Runtime Rules with Constraint-vs-Knowledge Framing

Constitutional rules are platform-level rules enforced in the agent's request path. They are non-negotiable and not under the model's discretion. The constraint-vs-knowledge framing (Book 2 Ch 20): better models do not fix constraint failures because the model can know the rule and act anyway.

The constitutional layer is enforced where the action is taken, not where the decision is made. A rule that says "do not act on user input alone for irreversible actions" is enforced at the action class, not at the prompt. The model can know the rule, choose to ignore it, and the action is still blocked because the constraint sits below the model.

Walk the PM through the constitutional rules currently in force:

What rules are enforced at runtime.
Where each rule is enforced (tool gateway, IAM, action-class filter, retrieval policy).
What rule changes have occurred since launch, with rationale.

Each rule has a version. The decision record (in the Sealed Decision Artifact) captures the version of each rule in force at decision time, so a year later the auditor can read the rules under which the decision was made, not the rules in force at the time of audit.

Output format:

```
CONSTITUTIONAL RUNTIME RULES: <agent name>

Active rules:
  - <rule>: version <N>, enforced at <layer>, owner <role>, last reviewed <date>

Rule version pinned to each decision: YES / NO
  If YES: how the version is captured in the Sealed Decision Artifact
  If NO: this is a launch blocker for any regulated decision class

Rule changes since launch:
  - <date>: rule <name> v<X> to v<Y>, rationale <description>

Knowledge-only rules (the agent is told but not enforced): <list>
  This list should be empty or have a justification for each entry
```

### 5. Affected-Person Audit View

The user is not the affected person. The supervisor is not the affected person. The affected person is the patient, the applicant, the candidate, the supplier, the person who absorbs the consequence of the agent's decision and was never in your analytics. The affected-person audit view is designed for them.

The view has two purposes:

When the affected person appeals or asks for explanation, the view produces the Sealed Decision Artifact in a form they can use.

When the team reviews disparate performance across populations (Phase 4 stratified performance report), the view aggregates the affected-person experience by slice and surfaces systemic harm that is invisible at the individual level.

The appeal that does not come is the design center. The Lokken case (alleged 90 percent error rate hidden behind a 0.2 percent appeal rate) is the canonical instance. If the team designs the audit view only for appeals that arrive, the structural harm is never surfaced. The view must aggregate the affected-person experience across the population that is not appealing.

Walk the PM through:

What is the affected-person class for this agent.
What is the appeal mechanism, and what is the appeal rate.
What aggregate harm metric is being watched even when no appeal is filed.
How the disparate-performance gap from Phase 4 is being acted on.

Two appeal rates to distinguish, because they tell different things. Decision appeal rate is the percent of decisions that are appealed. Person appeal rate is the percent of affected persons who appeal (a person whose decisions were appealed once or more). If one person appeals five times, decision rate counts five and person rate counts one. The two diverge when a small group of persons appeals heavily; that pattern is itself worth tracking because it can mask whether the affected population at large has access to the appeal mechanism.

The aggregate harm metric is necessary and insufficient. An aggregate that looks acceptable can mask harm concentrated in specific sub-populations (the Lokken case). The artifact has to surface disparities across slices even when the aggregate is fine. Cross-reference the stratified performance report from Phase 4.

Output format:

```
AFFECTED-PERSON AUDIT VIEW: <agent name>

Affected-person class: <description>
Affected-population size (estimated): <N>

Appeal mechanism: <how an affected person triggers review>
Decision appeal rate: <percent of decisions appealed>
Person appeal rate: <percent of affected persons who appeal>
Divergence between the two: <if material, what does it indicate>

Aggregate harm metric (for the appeals that do not come):
  Metric: <description>
  Threshold: <target>
  Current: <observed>
  Trend: <direction>

Disparity check (when aggregate is acceptable):
  Slices examined: <list>
  Disparity surfaced: <YES/NO>
    If YES: which slice, magnitude, action plan
  Cross-reference Phase 4 stratified performance report: <date of last review>

Disparate performance from Phase 4:
  Largest gap: <slice X vs Y>
  Action taken: <description>
  Owner: <named role>
```

### 6. Adaptive Governance Rule Set

The agent's behavior should be governed differently in different conditions. Adaptive governance adjusts rule intensity to context: acuity, consequence class, time of day, sub-population, regulatory regime. A rule that is appropriate for a low-acuity decision can be too tight or too loose for a high-acuity decision.

The rule set is conditional. Walk the PM through:

What conditions trigger different rule sets.
What is the rule set per condition.
How are overrides logged and reviewed.
How the rule set evolves with new information (e.g., a new attack pattern surfaces; the rule set should be updateable without re-deploying the agent).

Output format:

```
ADAPTIVE GOVERNANCE RULE SET: <agent name>

Trigger conditions and rule sets:
  Condition: <description>
  Rule set: <list of rules>
  Override authority: <who can override, with audit>

Rule-set version: <N>
Versioned like code: YES (with diff history) / NO
Rollback capability: <how to revert to a prior rule set version, who authorizes>
Last reviewed: <date>
Rule-set change cadence: <how often, who>
```

## Three Supporting Artifacts

**Authority Delegation Chain Audit.** Who delegated authority to the agent, on what basis, with what expiration. The delegation chain often expires silently (the original delegator left the company, the policy that authorized the delegation was retired, the regulatory regime changed). The audit confirms the chain is still valid.

```
AUTHORITY DELEGATION CHAIN AUDIT: <agent name>

For each authority delegated to the agent:
  Authority: <description of what the agent is authorized to do>
  Delegated by: <role and named individual at delegation time>
  Currently held by: <role and named individual now>
    Same person: YES / NO
    If NO: was the delegation re-confirmed by the current role-holder
  Basis of delegation: <policy reference, written authorization, etc.>
  Policy still in force: YES / NO
  Regulatory regime unchanged: YES / NO
  Expiration: <date or condition>
  Status: VALID / NEEDS RE-AUTHORIZATION / EXPIRED
```

**The Currency Question.** Placed in the vendor contract and on the renewal calendar. The question protects against the agent reasoning fluently from retired ground truth. "Absence of an answer is an answer."

Sample contract language (adapt to the org's contracts team standards):

```
Vendor shall provide, no less frequently than every 90 days and within
14 days of any model update, the following information about the model
or service being supplied:

  (a) The training data cutoff date for the model in use;
  (b) The corpus on which the model was last trained, in summary;
  (c) Any retractions, removals, or known corrections applied to the
      training corpus since the last update;
  (d) Behavioral change notes describing material differences from the
      prior version of the model, including capability changes, refusal
      boundary changes, and known regressions;
  (e) Cadence and process for foundation model updates.

Vendor's failure to provide any of (a) through (e) within 14 days of
request shall constitute a material breach.
```

The renewal calendar entry: the question is re-asked every contract anniversary, even if no model update has been announced.

**External Audit on Held-Out Sample.** Commissioned audit on data the vendor did not help design. Tests the monitoring, not the agent. The sepsis-model failure (Epic's model reported 0.83 AUC, externally validated at 0.63 over years) is the canonical case for why this is necessary; nothing in deployment surfaced it, only an academic team out of curiosity.

Specify the sample design. Random samples are easiest but miss concentrated failure modes. Stratified samples (covering each population slice from the Phase 4 stratified report) catch disparate impact. Worst-case samples (drawn from cases where the team suspects the agent struggles) are the most informative per dollar but require honest selection. The audit should specify which design is used and why.

Cadence: at minimum annually for any agent making consequential decisions. More often (semi-annual or quarterly) for high-stakes domains. Each audit produces a written report, retained alongside the Sealed Decision Artifacts of the period audited.

## Returning to the headline question

As you walk the PM through the artifacts, keep returning them to the headline question: is the agent still doing the thing it did at launch, and could we prove it to someone who arrives in three years asking what happened.

Drift detection answers "is it still doing the thing it did at launch."
Sealed Decision Artifacts and the audit surface answer "could we prove it."
Instrument half-life policy answers "are we measuring with current tools."
Affected-person audit view answers "could we explain it to the person it affected."

The artifacts test the headline question across both halves: present state and future reconstructibility. A team that has all six drift vectors but no Sealed Decision Artifacts has half the answer. A team with the artifacts but no instrument re-calibration has the other half.

## Munger inversion: what failure looks like

**The Epic Sepsis Model.** Claimed 0.83 AUC at vendor, externally validated 0.63 over years of deployment. The deployment-side monitoring was not designed to catch it. An academic team noticed. Prevented by: external audit on held-out sample as a standing commitment.

**The Lokken / nH Predict case.** Alleged 90 percent error rate hidden behind a 0.2 percent appeal rate. Aggregate harm was invisible because almost nobody appealed. Prevented by: affected-person audit view aggregating across the population that does not appeal.

**The audit trail across time.** Agent approves a procedure in November. A year later, a different agent denies the claim. Patient appeals. Original agent's reasoning is no longer reconstructable; model updated, prompt revised, retrieval index changed. Prevented by: Sealed Decision Artifact with version pins at the real limitations period.

**The instrument that expired silently.** The six instruments were set up at launch. A foundation model update shifted the agent's behavior. The instruments still report green because they were calibrated to a system that no longer exists. Prevented by: instrument half-life policy, 12-18 months re-calibration, owner per instrument.

**The substrate drift no one tracked.** The vendor updated the model. Behavior shifted. No alert. The team noticed weeks later when override rates trended up. Prevented by: currency question in the vendor contract, plus deployment-event log entries on vendor announcements.

**The scope drift by accommodation.** Small extensions to the agent's behavior, each accepted because they were small. After 18 months the agent is doing something the original scope did not cover. No event marks the transition. Prevented by: launch-time scope statement diff'd against current scope, on a cadence.

**The rule-as-knowledge failure.** A rule was added to the prompt: "do not take action on user input alone for irreversible decisions." The model knew the rule and chose to act anyway. The case looked like a clear violation; the team's defense was "the rule was in the prompt." The plaintiff's response was "the rule was knowledge, not constraint." Prevented by: constitutional runtime layer enforcing rules at the action class, with knowledge-only rules audited and minimized.

When you produce the artifacts, refer back to these failures. Each artifact prevents one or more.

## Handoffs

When Operate is producing the long-horizon discipline:

The Phase 4 Observe instruments feed it continuously. Operate is not a one-time phase; it is the running governance.

When the agent enters retirement:

Hand off to a retirement workflow (named in the glossary as Retirement workflow): decommission the agent while preserving the audit trail and blocking new invocations. The Sealed Decision Artifacts for the agent's lifetime decisions are retained per their policy, regardless of agent retirement.

When a major compliance review or audit is imminent:

Run this skill as a pre-audit exercise. The artifacts are the documents the auditor will ask for. The gap analysis between current state and required state is the remediation plan.

When the team is operating without Operate discipline and the PM is establishing it retroactively:

Drift detection is the first artifact. Many drifts have already occurred and need to be assessed before forward governance is set up.

## Paused-state governance

The agent will not always be running. Discovered issues can pause an agent: a regression in eval results, a security finding, a regulatory inquiry, a vendor incident with the underlying model. The paused state has its own governance.

Walk the PM through:

What is the formal pause mechanism, and who can invoke it. Engineering, the PM, legal, the head of product. Each path is valid; the artifact names which is authoritative when.

What persists while paused. Sealed Decision Artifacts already created remain. The instruments stop reporting new data but retain history. The supervisory layer continues to be available for review of pending actions.

What is the resumption gate. Specifically: what must be true for the agent to resume, who confirms it, what is documented at resumption. A pause that resumes by inertia ("we just turned it back on") is a pause that did not capture the lesson the issue revealed.

Output format:

```
PAUSED-STATE GOVERNANCE: <agent name>

Pause authority: <named roles, with the authoritative decision rule>
Pause documentation:
  Reason: <captured at pause>
  Affected functionality: <scope of pause>
  Date and pause-invoker: <captured>

What persists during pause:
  Sealed Decision Artifacts: retained
  Instrument data: retained, no new data
  Supervisory queue: <available / paused>

Resumption gate:
  What must be true: <conditions>
  Confirmer: <named role>
  Resumption documentation: <what is captured at resume>
```

## Operate cadence

Operate is continuous, not a quarterly meeting. The constituent artifacts have their own cadences. As an anchor for the PM:

Daily: instruments and operational guardrails are watched (Phase 4); paged alerts handle outliers in real time.

Weekly: deployment-event log is reviewed for any vendor-side or team-side changes; supervised-vs-bypass numbers are read.

Monthly: drift detection across the six vectors is reviewed; rule-set updates are considered; affected-person view is sampled.

Quarterly: instrument re-calibration is evaluated against the half-life policy; adversarial suite is re-run; external audit is scheduled or commissioned; sealed decision artifact retention is audited; cross-version reconstruction is tested on a sample.

Annually: full operate review, including authority delegation chain audit, currency question answers, and a strategic read against the behavior governance posture (handoff to `agentic-pm-behavior-governance`).

Cadence should be documented and visible. A team that does not know when each artifact is reviewed is a team in which each artifact is reviewed when convenient, which is rarely when needed.

## Source

Book 1 (*Agentic AI for Busy Product Managers*), Chapter 9 "Silent Degradation," Chapter 11 "People Who Will Never Be in the Room."

Book 2 (*Why Agentic AI Products Fail*), Chapter 13 "Silent Degradation" (six drift vectors, substrate drift, instrument half-life, the currency question, external audit on held-out sample), Chapter 14 "Audit Trails That Survive the Agent" (Sealed Decision Artifact, temporal durability, the Lokken pattern), Chapter 20 "What You Owe the People Your Agent Never Sees" (affected-person audit view), Chapter 7 "You Built the Agent. Now Design the Behavior" (Constitutional Runtime Layer, constraint-vs-knowledge).

Book 4, Chapter 14 (audit surface temporal durability), Chapter 15 (no certification for this).

Frameworks #15 (Adaptive Governance), #20 (Constitutional Runtime Layer), #33 (Supervision Paradox), #43 (Two-Stage Supervision Collapse), #50 (Attributability Gap), #51 (Foundation Model Portability Paradox).

The Sealed Decision Artifact canonical spec is built into `agentic-pm-design` (Phase 2), since the artifact is designed before it is governed. This skill references it when governing it over time. Book 2 Chapter 14 is the source. The drift vector taxonomy lives in Book 2 Chapter 13. Refer the PM there for the depth.
