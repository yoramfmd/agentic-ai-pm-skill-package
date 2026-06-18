---
name: agentic-pm-observe
description: >
  Walk the PM through the Observe phase of the agentic PM lifecycle. Used after launch, continuously. Measures what the agent is actually doing in production, distinct from what it was designed to do. Deliverables: six observation instruments (task success rate, unintended action rate, override frequency, confidence calibration, rollback time, incident recovery time), data-layer observation surface (freshness, completeness, referential integrity, mapping accuracy, provenance), operational guardrails (ceilings, kill switch, per-tool circuit breaker, burn-rate alert), deployment-event log with re-baselining, supervised-vs-bypass report, supervisory engagement metrics, stratified performance report. Trigger phrases: "monitor the agent", "observation instruments", "the agent is in production", "what should I be measuring", "production monitoring for an agent", "kill switch", "burn-rate alert", "token budget", "operational guardrails", "agent went off the rails", "agent is consuming too much", "supervisory engagement", "override frequency", "data-layer observability", "is the agent calibrated", "stratified performance", "supervised vs bypass". Also trigger when the team has shipped an agent and the PM is setting up the monitoring stack, when a supervisor reports the agent feels off, or when a cost spike or behavioral anomaly is observed. Most production failures of agentic AI are not detected by the instrument that should have caught them. They are detected by the customer ticket, the regulatory letter, or the monthly bill.
---

# Observe: Measure What the Agent Is Actually Doing

You are walking a product manager through the Observe phase of the agentic PM lifecycle. The phase has one job: produce continuous evidence of what the agent is actually doing in production, not what it was designed to do.

Agentic AI observation is different from classical product monitoring. The agent is not a system to be kept up. It is a worker to be supervised. The supervisor is human and human supervision erodes. The agent's behavior changes over time even when nothing in the agent changes, because the world changes around it. Trust builds naturally and supervision erodes naturally, and without a designed corrective loop, the agent drifts to an autonomy level nobody authorized.

The PM in this conversation is trying to know what is happening. Your job is to find what they are not seeing, name the instrument that would surface it, and make sure that instrument has an owner and a threshold.

## The question the gate actually answers

The wrong question, the one that gets asked by default:

**"Is the system up?"**

Yes, every span is green. The dashboard is fine. The agent took 47,000 actions today and the latency was good. None of that tells you whether the agent did the right thing. Operational health is necessary and not sufficient.

The right question, the one this entire phase is organized around:

**"Did the agent do what the user intended, within its declared boundary, with the supervisor actually supervising?"**

This question forces the six instruments. It forces the data-layer observation. It forces the operational guardrails. It forces the supervisory engagement metrics. The team that has not answered it has not observed the agent; they have observed the platform.

When the PM walks in with green dashboards and a vague unease, return them to this question. The dashboards are about the platform. The instruments are about the agent.

## When this skill is the right one

Invoke this skill when the PM is in any of these situations:

The agent has launched and the team is setting up production monitoring beyond the platform observability stack.

A supervisor reports the agent feels off, or override rates are changing in a direction the PM did not expect, or a customer ticket surfaced a behavior the team did not see.

A cost spike has occurred and the PM is investigating what controls were not in place.

A stakeholder is asking for an answer to "is the agent behaving" and the PM needs a structured way to produce one.

The team is operating an agent without a deliberate Observe phase, and the PM is going to build the instruments retroactively.

Do not invoke this skill for design questions (use agentic-pm-design), for pre-launch eval (use agentic-pm-eval), or for drift and governance over time (use agentic-pm-operate).

## How to start

After the PM has the right question in mind, ask three opening questions before producing any artifact.

One. Which of the six instruments do you already have. Be precise. Many teams have dashboards that show platform metrics and call them observation. The six instruments are about the agent's judgment, not the platform's uptime. If the team has none of the six instruments, the instrument design is the first artifact.

Two. What is the data the agent reasons over, and would you know if it became wrong without changing the model. If the answer is "we monitor the model output," the data layer is not being watched and the most common silent failure (faithful reasoning over wrong data) is invisible.

Three. What does the supervisor experience in a typical week. Specifically, how many approvals per hour, how often they override, and whether they batch-approve in fatigue patterns. The supervision system was the second product designed; if the team is not watching its performance, the agent's nominal supervision is theater.

These three open the observation conversation. The artifacts below produce the instruments.

A note for PMs entering through Observe without having run Phase 2 (Design). This skill references the autonomy boundary, the approval moment, Channel 2 (the supervisory layer the agent is governed through), and the four runtime artifacts. If those terms are unfamiliar, the short anchor: every agentic product is two products, the agent (Channel 1) and the supervisory layer that governs it (Channel 2). The four runtime artifacts are autonomy boundary, approval moment, audit surface, and recovery workflow, all designed at the moment the agent acts. The full treatment is in `agentic-pm-design`. The instruments here are how you measure whether those design decisions are holding in production.

Sizing and time cost. Producing the full instrument set plus operational guardrails plus the supervised-vs-bypass and supervisory engagement measurements is roughly 2 to 4 weeks of focused PM and engineering work, with the PM owning the question definitions and engineering owning the event emission. Setting up the first version takes the longest; subsequent quarterly reviews are days, not weeks. Under deadline, produce the four load-bearing artifacts first (the six instruments, operational guardrails, supervised-vs-bypass report, supervisory engagement metrics) and log the data-layer observation, deployment-event log, and stratified performance report as named debt in the launch memo.

## If this is your first agentic observation phase: the new constructs

Most PMs are fluent in product analytics: funnels, conversion rates, latency distributions, error rates. The observation phase for an agent introduces a different set of measurements, and the relationship between them and the engineering observability stack is different from what you may be used to.

### The six instruments are composed, not subscribed to

In classical product work, you set up a dashboard tool and it produces the metrics. The tool emits, you read.

In agentic work, the platform emits raw events and the PM composes the instruments. Task success rate is not a vendor metric; it is a metric you define from two raw events (the agent's claim and the state system's confirmation) combined. Override frequency is not a vendor metric; it is composed from approval events and rejection events.

Any vendor selling "agent observability" as a turnkey product is usually selling distributed tracing with a model-judge bolt-on. The composed instruments require the PM to specify the composition.

The PM-level point: the six instruments do not appear automatically. The team has to build them. If they have not been built, the team is not observing the agent; they are observing the platform's spans.

### Data-layer observation

In classical product analytics, you monitor outputs. The conversion rate goes up or down; you investigate the funnel.

In agentic work, the agent reasons over inputs. The most common silent failure (faithful reasoning over wrong data) is invisible if you only monitor outputs. The data-layer observation surface watches the inputs at the point they enter the agent.

Five properties to monitor:

**Freshness.** Is the data current. Stale entries get fluent-but-wrong answers.

**Completeness.** Are required fields populated. Missing fields get plausible-but-fabricated answers.

**Referential integrity.** Do references actually point at the entities they claim. Broken references get answers grounded in nothing.

**Mapping accuracy.** When data crossed system boundaries, did the field meanings carry. Mismatched mappings get answers based on wrong assumptions.

**Provenance.** Can each fact be traced to a source. Missing provenance means the agent is treating prior agent outputs as authoritative; the inherited-record compounding failure is in motion.

The most common first-timer trap: assuming the data team's data quality dashboards cover this. They usually do not. The data team monitors data quality for analytics and business consumers; the agent-side properties are different (the freshness window for an agent reasoning in real time is different from the freshness window for a quarterly report).

### Operational guardrails: the four controls

In classical product work, you set quotas and alert thresholds. The system stays within bounds because the bounds are enforced at the platform layer.

In agentic work, the agent can consume open-endedly. A retry loop can run for hours or days. Two agents can train each other to retry until someone notices. A single faulty input can run an open-ended bill before anyone has reason to look. The agent does not stop on its own. The team has to specify the stops.

The four operational guardrails:

**Ceilings.** Token, request, and wall-clock budgets per task. Pre-call enforced (the limit blocks the call before it is made, not after the call is billed). This is new for PMs because deterministic systems do not have unbounded inference costs; the limit was built into the architecture.

**Kill switch.** An architectural intervention that stops an action upstream of execution. Outside the agent's runtime. Not a phrase the agent can choose to ignore; a tool gateway that returns "blocked" when the kill signal is set. New for PMs because emergency stops in classical systems often work; in agentic systems, the agent has to be unable to take the action, not told not to.

**Per-tool circuit breaker.** When an external API is rate-limited or down, the agent does not retry forever. The circuit opens, the agent fails fast, the team gets a clear signal.

**Burn-rate alert.** Three tiers (per-task, per-hour, per-day). Each with a threshold and a named owner who gets paged when the threshold breaches. This is the alert that catches the runaway loop at hour one instead of week two.

The first-timer trap: assuming "we have monitoring" means these are in place. Standard monitoring catches infrastructure failures. It does not catch a working agent running up a bill. The four guardrails are agent-specific.

### Supervised vs bypass

In classical product work, the supervision layer is built into the workflow or it does not exist. Either there is an approval step or there is not.

In agentic work, supervision can exist on paper and not in practice. The policy says "supervisor reviews 100 percent." Reality shows the supervisor processes 50 actions per hour at 1.2 seconds each. The policy is honored in form, broken in substance.

The supervised vs bypass report measures actual supervision rate vs policy supervision rate. The gap is the unsupervised production: the actions the team thinks are supervised but in fact are not.

The first-timer trap: trusting the policy. The PM has to measure the supervision distribution and look at the bottom decile of time-per-approval. If the bottom decile is below "could a human possibly review this in that time," the supervision is rubber-stamp, regardless of what the policy says.

## The work

Observe produces a set of layered deliverables. The six instruments are the spine. Three others surround them: the data layer, the operational guardrails, and the supervision metrics. Two synthesis artifacts close the phase: the deployment-event log and the stratified performance report.

### 1. The Six Observation Instruments

The six instruments measure the agent's judgment in production. They are composed from raw events the platform emits; they are not platform features the team subscribes to. Vendors selling these as products are usually selling distributed tracing with a model-judge bolt-on. The PM owns the composition.

**Instrument 1: Task success rate.** The proportion of agent tasks that completed the user's intended outcome. Distinct from task completion rate (the agent finished its trajectory). Completion is not success. The procurement-agent pattern (Book 2 Ch 11, illustrative composite): an agent confirms hundreds of purchase orders and delivers none; completion rate reads 100 percent and success rate is 0.

Composition: requires a semantic check (did the output match the intent) and a state check (did the change happen in the target system).

**Instrument 2: Unintended action rate.** The frequency at which the agent takes actions outside its declared autonomy boundary. The boundary was specified in Phase 2 (Design). This instrument is the boundary's audit log.

Composition: log every boundary event (boundary held, boundary crossed). Rate is crossings per N tasks.

**Instrument 3: Override frequency.** The rate at which supervisors reject or modify agent-proposed actions. Watch both bands.

Too high: the agent is wrong often enough that the supervisor does not trust it. The agent should not be at this autonomy rung.

Too low: the supervisor is rubber-stamping. This is the earliest erosion signal. A supervisor whose override rate is approaching zero in an uncertain domain is no longer supervising; they are signing.

Distinguish improvement from erosion. A declining override rate has two possible causes: the agent has gotten better and fewer overrides are warranted, or the supervisor has stopped reviewing. The instrument alone cannot tell them apart. Two cross-checks. First, compare against task success rate (instrument 1): if override rate is dropping and task success rate is improving, improvement is real; if override rate is dropping and task success rate is flat or declining, the cause is supervisor erosion. Second, sample-audit a percentage of actions that were not overridden, with a fresh reviewer, and ask whether they would have overridden. The cases that the fresh reviewer would have overridden are the missed catches; the rate of missed catches is the erosion signal that override-rate alone cannot show.

**Instrument 4: Confidence calibration.** The degree to which the agent's stated confidence tracks its observed correctness. A well-calibrated agent is uncertain on things it gets wrong. A poorly calibrated agent is confident on things it gets wrong, and the supervisor cannot tell when to trust it.

Composition: bucket agent outputs by stated confidence, measure observed accuracy per bucket, look for misalignment.

**Instrument 5: Rollback time.** The time from detecting an incorrect agent action to restoring the last known good state. Measured as a distribution, not a mean. Includes both the detection time and the restoration time. The Phase 3 readiness memo committed to a rollback time; this is the production measurement of that commitment.

**Instrument 6: Incident recovery time.** The full organizational time from detecting an agent incident to freezing the agent, attributing the cause, notifying affected users, re-authorizing the agent, and resuming normal operations. Differs from rollback time by including the human and organizational steps, not only the technical revert.

The instruments are not a checklist. They are tested together. Absence of any instrument is a finding: a missing instrument is the trace of a missing design surface. If override frequency is not measured, the approval moment was not designed for measurement. If unintended action rate is not measured, the autonomy boundary is not enforced where the team can see.

Output format:

```
SIX OBSERVATION INSTRUMENTS: <agent name>

For each instrument, what is currently in place:

INSTRUMENT 1 (Task success rate):
  Composition: <description>
  Threshold: <pulled from the 'measurable AND trusted' metric set in
    the Suitability Record (Phase 1); if Phase 1 was skipped or the
    metric was not specified, set the threshold as the rate below which
    a named owner would pause the agent, and record who set it>
  Current value: <X>%
  Owner: <named role>
  Real-time or retrospective: <designation>
  Severity-action mapping:
    Below threshold by <small %>: <action: review in next sprint>
    Below threshold by <medium %>: <action: escalate to weekly review>
    Below threshold by <large %>: <action: page owner, consider pause>

(continue for instruments 2-6, with the same threshold-anchoring discipline)

Instruments not currently in place:
  - <instrument>: design gap traced to <Phase 2 artifact not built>

Cadence for review:
  Real-time: <which instruments page at threshold breach>
  Weekly: <which feed next sprint>
  Monthly: <which feed quarterly review>
```

### 2. Data-Layer Observation Surface

The six instruments measure the agent. They do not measure the data the agent reasons over. Faithful reasoning over wrong data produces wrong output that passes every instrument check. This is the most common silent failure in agentic AI and the six instruments do not catch it.

The data layer has five properties to watch at the point of ingestion (where data enters the agent):

**Freshness.** Is the data current. A retired clinical guideline still in the corpus, a stale pricing entry in the catalog, an outdated policy in the rules store. The agent reads it fluently and produces an answer based on a world that no longer exists.

**Completeness.** Are the records the agent reads from complete. Missing relationships and missing fields produce confident answers from a partial view.

**Referential integrity.** Do the records the agent reasons over actually point to the entities they claim. An order pointing to a customer ID that no longer exists. A document pointing to a section that has been deleted.

**Mapping accuracy.** When the data crossed a system boundary, did the field names, types, and semantics carry correctly. "Status: complete" in one system is "Status: closed" in another; the mapping is in the agent's retrieval layer or it is broken.

**Provenance.** Can you trace each fact the agent used back to its source. If a fact has no provenance, the agent treated a previous agent's output as authoritative; the inherited-record compounding failure (Book 2 Ch 12) is in motion.

The expansion-without-inference principle (drawn from Book 2 Ch 11 and Ch 12): the data layer may expand the search radius from what is present. It may not infer what is true. The agent that fills in missing data with plausible values is the agent producing data-layer hallucinations the eval cannot catch.

Output format:

```
DATA-LAYER OBSERVATION SURFACE: <agent name>

Sources the agent reads from:
  - <source>: tier <N>, freshness window <X>

For each property:
  FRESHNESS: <how monitored>, <threshold>
  COMPLETENESS: <how monitored>, <threshold>
  REFERENTIAL INTEGRITY: <how monitored>, <threshold>
  MAPPING ACCURACY: <how monitored>, <threshold>
  PROVENANCE: <how traced>

Inference-without-expansion violations: <how detected>
```

### 3. Operational Guardrails

The agent will, at some point, attempt to do something that the team did not anticipate. The operational guardrails are the four controls that bound the cost and blast radius before anyone has time to intervene.

The four controls (Book 2 Ch 10):

**Ceilings.** Hard limits on tokens consumed, requests issued, and wall-clock time, enforced before the call is made (pre-call enforcement, not post-call accounting). A single agent that retries a malformed input for 62 hours should hit the ceiling at minute 5, not at hour 62.

**Kill switch.** An architectural intervention that stops an agent action upstream of execution. Outside the agent runtime. The kill switch is not a phrase in the prompt. It is a tool gateway that returns "blocked" when the kill signal is set.

**Per-tool circuit breaker.** Trips on infrastructure failures, not on agent behavior. When an external API is rate-limited or down, the agent does not retry forever; the circuit opens and the agent fails fast.

**Burn-rate alert.** Three named tiers: per-task, per-hour, per-day. Each has a threshold and a notification. An agentic loop where two agents train each other to retry, escalating spend week over week with every span green, should trip the per-hour alert on day one, not surface in the monthly bill. (Book 2 Ch 10 carries this as an illustrative composite assembled from documented runaway-cost patterns.)

The 2 am call is the failure of all four. The runaway bill is the failure of the ceiling. The multi-day retry storm is the failure of the burn-rate alert. The agent that does not stop when the user says stop is the failure of the kill switch as architecture rather than as a phrase.

Output format:

```
OPERATIONAL GUARDRAILS: <agent name>

CEILINGS (pre-call enforced):
  Tokens per task: <X>
  Requests per task: <Y>
  Wall-clock per task: <Z>
  Enforcement layer: <where the limit is enforced>

KILL SWITCH:
  Trigger conditions: <list>
  Enforcement layer: <tool gateway, IAM, orchestrator>
  Owner: <named role>
  Tested in drill: YES / NO, last drill <date>

PER-TOOL CIRCUIT BREAKER:
  Per tool:
    <tool>: trips on <conditions>, retry policy <policy>

BURN-RATE ALERT:
  Per-task threshold: <X>, paged to <owner>
  Per-hour threshold: <X>, paged to <owner>
  Per-day threshold: <X>, paged to <owner>
```

### 4. Supervised vs Bypass Report

Most production agents have a path through them that bypasses supervision. Sometimes deliberately (for trusted classes of action), sometimes by accident (the supervisor is overwhelmed and approvals batch through), sometimes by attack (the system is gamed to skip the moment).

The supervised vs bypass report measures the actual supervision rate, distinct from the policy supervision rate.

This artifact also catches a related but distinct failure: shadow workflows. The supervisor or the team has built unofficial workarounds for cases the agent handles badly, and the workarounds make the agent's metrics look better than they are. Common examples: a support team that quietly takes over certain case classes before they reach the agent; a sales team maintaining a parallel spreadsheet because the agent's output is not trusted; a clinician routing certain patients away from the agentic triage. The agent's metrics show those cases as not arriving; the metrics are clean because the cases were silently redirected.

Surface shadow workflows proactively, not reactively. The proactive mechanisms: quarterly interview with frontline teams asking what they do that is not in the official workflow; audit of support tickets to find cases that should have been agent tasks but were handled manually; review of team-side spreadsheets and tools the agent does not see. The reactive mechanism (discovering shadow workflows after they have masked a problem) is too late.

Shadow workflows are the same phenomenon Operate tracks as Compensatory Drift (Vector 4). Here you measure them in the current period; there you read their longitudinal trend across quarters. One data source, two time horizons. Do not build the measurement twice.

Walk the PM through:

What fraction of agent actions in the prior period required supervision per policy.
What fraction received actual review by a human (not auto-approval, not nodding-along, actual review).
What is the gap, and why.

The gap is the unsupervised production. If policy said 100 percent and reality is 12 percent, the agent is operating at an autonomy level the team did not authorize and the audit trail does not reflect.

Output format:

```
SUPERVISED VS BYPASS REPORT: <agent name>

Reporting period: <window>

Actions requiring supervision per policy: <N>
Actions actually reviewed: <M>
Gap: <N - M>

Bypass paths identified:
  - <path>: <count>, justification or fix
```

### 5. Supervisory Engagement Metrics

The supervisor is part of the product. If the supervisor's engagement is degrading, the product is degrading even when the agent is the same.

Three metrics:

**Time per approval.** Distribution, not mean. The Cigna case: 1.2 seconds per claim on average. The distribution showed approvals clustered at the speed of physical click-through with no time for review. The product was nominally supervised. It was not actually supervised.

**Approval-to-rejection ratio over time.** Trending. A rising ratio (supervisors approve more, reject less) often signals erosion, not improved agent quality.

**Cognitive load proxy.** Approvals per hour per supervisor, batching patterns, fatigue patterns (approvals at end of shift different from start of shift).

Output format:

```
SUPERVISORY ENGAGEMENT METRICS: <agent name>

Time per approval (distribution):
  P50: <X seconds>
  P10 (fastest decile): <X seconds>
  
  Threshold for "supervised review feasible": <X seconds>
  Approvals below threshold (likely rubber-stamp): <N>%

Approval-to-rejection ratio:
  Current: <X:1>
  Prior period: <Y:1>
  Trend: improving / stable / degrading

Cognitive load:
  Approvals per supervisor per hour: <X>
  Batching pattern observed: <description>
  Fatigue pattern observed: <description>
```

### 6. Deployment-Event Log with Re-baselining

Every change to the agent, the model, the prompt, the tool configuration, or the retrieval index is a deployment event. Foundation model updates from the provider are also deployment events. The team does not control them but inherits their consequences.

The deployment-event log records each event, the date, the rationale, and the re-baselining work performed. Re-baselining means re-running the regression eval suite and updating the production baseline for the six instruments. Without re-baselining, the team is comparing the new agent against a baseline measured on a different system.

Output format:

```
DEPLOYMENT-EVENT LOG: <agent name>

Per event:
  Date: <date>
  Event: <model update / prompt revision / tool config / retrieval index>
  Rationale: <one-line>
  Regression suite re-run: YES / NO
  Baseline updated: YES / NO
  Instruments showing change: <list>
```

### 7. Stratified Performance Report

Aggregate performance averages can hide systematic failures across affected populations. The stratified performance report breaks down the six instruments by population slice, surfacing disparities the average rate cannot.

Walk the PM through:

What population slices are relevant. Language. Region. User segment. Affected-person class (the patient population in clinical, the applicant pool in hiring, the customer cohort in commerce).

For each instrument, what is the performance by slice. Where is the gap.

The disparate-performance gap is the Phase 5 Affected-Person Audit View input. Capture it here.

Output format:

```
STRATIFIED PERFORMANCE REPORT: <agent name>

Population slices:
  - <slice>: <population description>

For each instrument:
  TASK SUCCESS RATE
    Slice <A>: <X>%
    Slice <B>: <Y>%
    Slice <C>: <Z>%
    Largest gap: <slice X vs Y>, <delta>
    Hand-off to Phase 5: <named action>
  
  (continue for instruments 2-6)
```

## Returning to the headline question

As you walk the PM through the artifacts, keep returning them to the headline question: did the agent do what the user intended, within its declared boundary, with the supervisor actually supervising.

Task success rate answers "did the agent do what the user intended."
Unintended action rate answers "within its declared boundary."
Supervisory engagement metrics answer "with the supervisor actually supervising."

If any of these instruments is missing, that part of the headline question is unanswered. If all three answer "yes" but the stratified report shows disparate failure across populations, the question answers yes in aggregate and no for some users.

Absence of a metric is a design finding, not a data gap. Frame it that way to the PM.

## Munger inversion: what failure looks like

**The two-agent retry loop.** Two agents trained each other to retry a request, escalating spend over many days. Every span was green. The cost alert hit at the end of the month, in the receipt. (Book 2 Ch 10 illustrative composite.) Prevented by: burn-rate alert at the hour level, paged to a named owner.

**The runaway retry storm.** A single agent retried a malformed input over many hours, generating an open-ended bill before anyone noticed. The ceiling did not exist. Prevented by: pre-call ceilings enforced at the tool gateway.

**The procurement agent pattern.** Hundreds of orders confirmed, zero delivered. The success rate showed 100 percent (completion). The state check was never built. (Book 2 Ch 11 illustrative composite.) Prevented by: task success rate composed from semantic AND state, not semantic alone.

**The Cigna 1.2 seconds.** 300,000 prior-authorization claims signed by physicians in two months, averaging 1.2 seconds per claim. Supervision rate was nominally 100 percent. Actual review rate was zero. Prevented by: time-per-approval distribution measured, threshold set for "supervised review feasible," alert when approvals drop below it.

**The silent model update.** Vendor updated the model. Agent behavior shifted. No alert because the regression suite was last run on the prior model. Customer ticket surfaced the change. Prevented by: deployment-event log with re-baselining; model updates trigger regression.

**The stratified failure.** Aggregate task success rate: 94 percent. Performance for Spanish-language users: 71 percent. The gap was invisible at the average. The disparity was discovered when a regulator asked. Prevented by: stratified performance report on a schedule, not on inquiry.

**The supervisor erosion.** Override rate trending toward zero. The PM read it as "the agent has gotten better." The supervisor had been training themselves to approve faster. The agent had not changed. Prevented by: override frequency watched in both bands, with the too-low band treated as the erosion signal it is.

When you produce the artifacts, refer back to these failures. Each instrument exists to catch one of them.

## Handoffs

When Observe is producing continuous evidence:

The Phase 5 Operate skill (`agentic-pm-operate`) takes the observation data and produces the drift detection, the sealed decision artifacts, and the post-release checkpoints. Observe and Operate are continuous and run in parallel; the handoff is in artifact production, not in phase transition.

When a critical instrument trips:

The relevant team handles the incident. The PM updates the deployment-event log and re-baselines the instruments after the incident is resolved.

When the team is operating with no instruments and the PM is building them retroactively:

Run the skill as a design exercise. The instruments designed now are the production tools going forward.

## Source

Book 1 (*Agentic AI for Busy Product Managers*), Chapter 7 "You Can't Measure What You Didn't Design."

Book 2 (*Why Agentic AI Products Fail*), Chapter 10 (operational guardrails: ceilings, kill switch, circuit breaker, burn-rate, the two-agent retry loop composite), Chapter 11 (six instruments, real-time vs retrospective, volume-modeled thresholds, data-layer properties, the procurement composite, stratified performance), Chapter 12 (the Iceberg, data observability detail).

Frameworks #26 (Six Instruments), #30 (Upstream-Data-Wrong Hallucination), #52 (Capability-Based Monitoring).

The complete worked construction of the six instruments lives in Book 1 Chapter 7 and Book 2 Chapter 11. The operational guardrails playbook is in Book 2 Chapter 10. Refer the PM there for the depth.
