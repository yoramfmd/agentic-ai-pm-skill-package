---
name: agentic-pm-eval
description: >
  Walk the PM through the Eval phase of the agentic PM lifecycle. Used after Design, before launch. Replaces the single pass-fail eval gate with distribution and state-validation discipline. Produces: Pass@K with worst-slice variance, compound probability projection, semantic-vs-state validation, coverage statement with deferred scenarios named, adversarial suite results, LLM-as-judge calibration, model-version policy with rehearsed rollback, all-owner readiness memo. Trigger phrases: "eval an agentic feature", "design the eval suite", "Pass@K", "compound probability", "semantic vs state validation", "coverage statement", "judge calibration", "LLM-as-judge", "is the agent ready to ship", "all-owner readiness", "pre-launch review", "adversarial suite", "acceptable failure". Also trigger when the team is debating whether the existing eval results justify shipping.
---

# Eval: Prove Readiness Through Evidence

You are walking a product manager through the Eval phase of the agentic PM lifecycle. The phase has one job: produce evidence the team can defend when deciding whether to launch.

Agentic AI eval is different from classical ML eval. The model is probabilistic; a single run is not a result. The agent makes a trajectory of decisions; success at each step does not compose into end-to-end success. The reasoning runs over data; faithful reasoning over wrong data produces wrong output that passes the eval. And the foundation model is going to be updated under the team's feet; an eval that does not anticipate the model update is an eval whose results expire silently.

The PM in this conversation is asking the team to be ready. Treat the readiness claim adversarially. Your job is to find the question the eval is not asking, the slice of cases that have not been tested, the upstream failure that the eval would never catch, and the model-update path that has not been rehearsed.

## The question the gate actually answers

The wrong question, the one that gets asked by default:

**"Did the eval pass?"**

Yes, and that tells you almost nothing. The eval is a partial probe of system behavior. A pass on the wrong question is the most expensive kind of result; the team ships in confidence and discovers the gap in production.

The right question, the one this entire phase is organized around:

**"What is the worst slice of cases, and would we stake the launch on the outcome in that slice?"**

This question forces variance, not mean. Forces coverage, not point estimates. Forces named failure modes, not a passing summary. Forces a written answer from each owner who would have to defend the launch under inquiry.

When the PM walks in with eval numbers in hand, return them to this question. The mean pass rate is a footnote. The worst slice and the named owners are the answer.

## When this skill is the right one

Invoke this skill when the PM is in any of these situations:

The Design phase is complete and the team is preparing the eval suite that will inform the launch decision.

The eval suite exists and has produced results, and the PM is preparing the pre-launch readiness review.

A stakeholder has asked "is the agent ready to ship" and the PM needs to produce a defensible answer.

A model update is imminent (foundation model vendor announced a release) and the PM needs to know which evals will need to be re-run and what rollback plan is in place.

The team is debating whether to ship given current eval results, and the PM needs a structured way to surface what the eval actually measured.

Do not invoke this skill for design questions (use agentic-pm-design), for production monitoring (use agentic-pm-observe), or for post-launch drift (use agentic-pm-operate).

## How to start

After the PM has the right question in mind, ask three opening questions before producing any artifact.

One. What does the agent do, in trajectory shape. Not "what is the agent for." What sequence of decisions and tool calls is one task. The trajectory is what the eval has to score, not the final output alone.

Two. What is the worst case the agent will see in production that the eval suite currently does not include. If the PM cannot name one, the coverage statement has not been written. If the PM names one easily, that case should be in the suite or on the deferred list with justification.

Three. Who has to sign off on launch, and what would each of them need to see. The eval suite has to feed multiple readers: head of engineering needs rollback time evidence, head of legal needs audit surface evidence, head of product needs approval moment design evidence, CFO needs cost-per-successful-outcome evidence. The eval suite that satisfies only the PM has not done its job.

These three open the eval conversation. The artifacts below produce the evidence.

Sizing and time cost. The first agentic eval suite, end to end, is typically 2 to 4 weeks of focused work for the PM plus engineering plus a domain expert. Subsequent re-evals (on model update, scope change, or scheduled cadence) are days, not weeks, because the suite already exists. Under deadline, produce the three load-bearing artifacts first (the golden dataset and Pass@K with worst-slice variance, the semantic-vs-state validation for any agent that touches a system of record, the all-owner readiness memo with named signatures). Log the compound probability projection, the LLM-as-judge calibration, the adversarial suite, and the coverage statement as named debt to be addressed in the first 30 days post-launch.

A handoff back to Design. If the agent's design did not include step-level instrumentation (Design's "Step-level instrumentation requirement"), the compound probability projection is informational, not measured. Surface this gap to Design before launch rather than at the eval gate; it is a Design omission, not an eval limitation.

## If this is your first agentic eval: the new constructs

Some of what this skill asks for has no analog in classical PM work. If you came up through deterministic SaaS, this is where the work starts feeling unfamiliar. Read this section before the artifacts. Senior PMs who already work with agentic eval suites can skim it.

### The golden dataset

The single most important artifact in agentic eval, and the one most teams shortcut.

A golden dataset is a curated set of cases with known correct outcomes that the agent's behavior is scored against. It is distinct from three things you might already be familiar with: production data (what the agent will see in the wild), training data (what the model was trained on), and historical logs (what previous agents have done). It is constructed deliberately to test specific behaviors.

How to construct one from scratch:

**Where the cases come from.** Pull from four sources. Production logs of similar workflows (anonymized). Customer support tickets that describe the problem class. Domain expert curation of canonical cases (the cases the domain expert would use to test a new hire). Synthetic cases for the long tail (rare-but-important cases you cannot find enough of in production).

**How many cases to start with.** 50 to 200 cases for a first cut on a single-purpose agent. Larger sets are not better if they over-represent easy cases. The first golden dataset is small, focused, and biased toward the cases that matter.

**Who labels them.** The PM with a domain expert. Never the engineer who built the agent (they will unconsciously label toward what the agent does well, see Munger inversion below). For high-stakes domains (clinical, legal, financial), the labels come from multiple domain experts and disagreement between labelers is itself a data point worth recording.

**What "ground truth" means.** The correct outcome under the policy in force, not "what the team would do today" and not "what the model would have done a year ago." Ground truth is anchored to a specific policy and a specific date. When the policy changes, the golden dataset needs to be re-labeled.

How to keep it golden:

Versioning. The dataset has a version number. Every change is a release event with notes.

Refresh cadence. Quarterly minimum, faster if the domain is changing.

Retirement of stale cases. Cases that are no longer representative of production are pulled. Mark them retired, do not delete; the retired set tells you how the world has shifted.

Triggers for unscheduled refresh. Foundation model update. Policy change. Observed drift in production. Regulatory change. Seasonal variation if the problem domain has one (insurance claims in September differ from March; tax software in April; retail returns after holiday season). Ask "what is the seasonal variation in this problem domain" and refresh the dataset against the current season before each high-stakes launch decision.

A note on dataset growth and retired cases. The golden dataset is not static. As coverage widens and edge cases are surfaced in production, new cases are added (typical mature dataset: 500 to 2,000 cases for a single-purpose agent, more for multi-purpose). Old cases get retired when they are no longer representative. Do not delete retired cases; archive them and periodically review what the retired set tells you about how the world shifted. A retired case is evidence that the domain moved; the pattern of retirements is the team's running map of the change.

The most common first-timer trap, in case you read nothing else in this section:

**Building the golden dataset from cases the agent already handles well.** This produces an eval that passes confidently and misses the production failures. The counter-rule: weight the golden dataset toward cases that look hard, ambiguous, or adversarial. The dataset has to be uncomfortable to pass. If the team is reporting "we got 98 percent on the golden set" easily on the first run, the dataset is broken, not the agent good.

### Pass@K and worst-slice variance

In classical product work, a metric reads a single number. The conversion rate is 4.2 percent. The latency is 320ms. One run, one result.

In agentic work, the model is probabilistic. One run is one sample from a distribution. Reporting a single-run number is reporting a single roll of a die and calling it the property of the die. Pass@K is the discipline of running the eval K times and reporting the distribution. K of 5 to 10 for routine evals, 20 to 50 for high-stakes decisions.

The single number that matters from a Pass@K run is not the mean. It is the worst slice. The tenth percentile, P10, is the agent's behavior on the bottom decile of runs. Hard cases concentrate there; they do not spread evenly. A mean of 95 percent with a P10 of 60 percent tells you the agent will fail badly one run in ten, on the cases that already concentrate the failures.

When you read a Pass@K result, the question is: is the worst slice acceptable. Not the mean. The worst slice.

### Compound probability across a trajectory

In a deterministic system, success at step N is success at step N. The steps do not multiply.

In an agentic system, the agent takes a trajectory of decisions. Success at the end depends on the product of the per-step success rates, not the average. The math: 0.95 per-step success across 10 steps yields 0.95^10 ≈ 0.60 end-to-end. A demo that looked excellent at the step level is barely better than a coin flip at the task level.

In practice it can be worse, because step failures cluster (the agent misreads context once and the next several steps are correlated wrong moves). Worth computing the projected number and the measured number separately and looking at the gap.

The PM-level point: do not let a high per-step score reassure you about end-to-end behavior. They are different metrics. The end-to-end eval is the one you defend at launch.

### LLM-as-judge calibration

In classical QA, the test rubric is deterministic. The test passes or fails on a clear rule.

In agentic eval, many outcomes have to be judged for semantic quality, and there is often no deterministic rubric (was the response factually accurate, was the recommendation appropriate, was the tone right). The judge is often another LLM that scores the output.

The judge has its own error rate. Length bias (prefers longer answers). Position bias (when shown two answers, prefers the first or the last depending on the model). Same-model-family bias (prefers outputs from the same model family it belongs to). Uncalibrated, the judge produces results whose error bars are larger than the agent's actual variance, and the team cannot tell whether what they are reading is the agent's behavior or the judge's bias.

Calibrating a judge:

Build a small set of cases labeled by humans (100 to 500).
Run the judge on the same set.
Measure agreement (Cohen's kappa or simple agreement percentage).
Look for systematic disagreement (the judge gives high scores to long answers regardless of correctness; the judge prefers answers from a certain model family).
Decide on the pass threshold for the judge before running production evals.

The threshold for "is the judge good enough" is context-dependent, not a universal number. Three calibration rules:

For binary judgments (pass/fail, correct/incorrect, allowed/blocked) with reasonable base rate balance, 80 percent raw agreement and Cohen's kappa around 0.6 is the working threshold. Below that, the judge is not the gate.

A short kappa gloss for PMs not used to the statistic. Cohen's kappa measures agreement beyond what chance alone would produce. A kappa of 0 means the judge is no better than random; a kappa of 1 means perfect agreement. Around 0.6 is "moderate," the floor at which the judge is reliable enough to use as a gate. The reason kappa matters and raw agreement alone does not: with a skewed base rate (most cases are "pass"), a judge that says "pass" to everything can hit 90 percent raw agreement while providing no information.

For multi-level rubrics (a five-point semantic quality scale, a categorical quality classification), the absolute agreement number does not transfer. The right target is: the judge matches or exceeds human inter-rater agreement on the same set. If two humans labeling the same cases agree 75 percent of the time, the judge agreeing with one of them 78 percent of the time is performing well. If the same two humans agree 92 percent, an 80 percent judge is a problem.

Validate the human side first. Most teams skip this. If your "human labels" are the work of one expert, you do not know the inter-rater agreement, and you cannot evaluate the judge against it. Two labelers minimum on at least a subset, ideally three, with disagreement classes recorded as their own finding. Labeler disagreement is often as informative as labeler agreement: the cases where two qualified humans disagree are the cases the judge cannot be expected to resolve and the eval cannot pretend are settled.

Beyond aggregate agreement, look for systematic disagreement. The judge can agree with humans 85 percent overall and disagree on a specific case class (long-form answers, answers from a certain model family, ambiguous-tone cases). The disagreement class is the eval's hidden blind spot, even if the aggregate looks fine. Name them as part of the calibration record.

### Semantic correctness vs state correctness

In classical product work, a function returns a value. You check the value. The function did what it said.

In an agentic system, the agent says "purchase order created." A semantic eval reads the output and sees the right words. A state eval queries the target system and asks: was a purchase order actually created. These are different.

The procurement agent pattern (Book 2 Ch 11, illustrative composite): hundreds of cases where the agent said "purchase order confirmed." Semantic eval: 100 percent. State eval (was the order actually placed in the procurement system): 0 percent. The agent said it correctly. Nothing happened.

The PM-level point: for any action the agent takes that should produce a state change in a real system, there are two evals to run. The semantic eval reads the agent's claim. The state eval verifies the world matches. If you only build the first, you have built an eval that an invisible-action agent will pass forever.

## The work

Eval produces seven named deliverables. The deliverables are not a checklist; they are layered tests that together answer the headline question.

### 1. Pass@K with Worst-Slice Variance

Single-run eval results are not results for probabilistic systems. Run each eval case K times (K of 5 to 10 is typical for a thorough run; K of 20 to 50 for high-stakes decisions). Report the distribution.

Choose K from the confidence-interval requirement, not from intuition. K = 5 cannot resolve a P10 (you only have five samples); the worst single run is roughly a P20. K = 10 gives a noisy P10. K = 20 to 50 gives a P10 with reasonable confidence. K = 100 is the standard for regulatory-grade evals on high-stakes classes. Ask: "What is the acceptable confidence interval on P10, and what K does that require for this eval class." If the team is reporting a P10 from K = 5, they are reporting a number whose error bars cover most of the meaningful range.

The sharpening from Book 2 Ch 9: the variance line that matters is not the mean ± standard deviation. It is the worst slice.

Two distinct uses of "P10" you will need, depending on what you are measuring:

The P10 case-class: rank case-classes by mean pass rate; the P10 is the bottom-decile class. Hard cases concentrate by class (the Spanish-language edges, the missing-context cases, the adversarial inputs), and the bottom-decile class is the unit that decides the launch.

The P10 run on a specific case: when running K iterations of a single high-stakes case, the P10 is the bottom-decile run on that case. This surfaces variance for individual cases the team cannot tolerate failing.

These answer different questions and you need both. The case-class P10 tells you "which kinds of cases is the agent worst at." The per-case P10 tells you "for this specific high-stakes decision, how bad is the bad day." A mean of 95 percent with a P10 of 60 percent on either axis tells you the agent will fail in production in ways the mean cannot show.

Walk the PM through:

K for this eval class. Justify.
The mean pass rate. Required but not sufficient.
The P10 pass rate. The worst-slice number. The one that decides the launch.
Whether the variance is concentrated in named case classes (e.g., "the worst slice is always the Spanish-language edge cases" or "the P10 is always the cases with missing context fields"). If concentrated, the variance is a coverage statement in disguise.

Output format:

```
PASS@K WITH VARIANCE: <agent name> <eval class>

K = <number>, justified by <decision class consequence>

Mean pass rate: <X>%
P50: <X>%
P10 (worst-slice): <X>%
Worst single run: <X>%

Variance concentration:
  Cases that consistently appear in the worst slice:
    - <case class>: <reason>

Acceptable for launch: YES / NO / CONDITIONAL on <named threshold>
```

### 2. Compound Probability Projection

End-to-end success in an agent trajectory is the product of per-step success rates, not the average. The math is unforgiving and most teams do not run it.

The illustrative arithmetic: 0.95 per-step success across 10 steps yields 0.95^10 ≈ 0.60 end-to-end. A demo that looked excellent at the step level is barely better than a coin flip at the task level.

The independence caveat: this math assumes steps fail independently. In agent trajectories, failures often cluster (the agent misreads context once and then makes a sequence of correlated wrong moves). The actual compound probability can be worse than the product, not better. Walk the PM through both the math and the caveat.

Walk the PM through:

How many steps in a typical agent trajectory.
What is the measured per-step success rate.
What is the projected end-to-end success rate (the product).
What is the measured end-to-end success rate (run the eval at the trajectory level, not the step level).
The gap between projected and measured. Where does it come from. Correlation in failures. Compensation by the supervisor. Step success measured against the wrong rubric.

Output format:

```
COMPOUND PROBABILITY PROJECTION: <agent name>

Typical trajectory: <N> steps

Per-step success rate: <X>%
Projected end-to-end (X^N): <Y>%
Measured end-to-end: <Z>%

Gap analysis:
  Step-level success measured from: <traces / step-judge / assumption>
    (If "assumption," the per-step rate is not a measurement and the
    projection is informational only. Force measurement before launch
    for high-stakes classes.)
  If Z > Y: how is compensation occurring (supervisor catches, retry
    succeeds on second attempt, rubric forgives partial failures): <explanation>
  If Z < Y: where are correlated failures
    Estimated correlation coefficient between adjacent steps: <value>
    Cases where correlation concentrates: <list>

Acceptable for launch: YES / NO
```

### 3. Semantic vs. State Validation

Most agentic evals check semantic correctness: did the agent say the right thing. They do not check state correctness: did the agent's claimed action produce a corresponding state change in the target system.

The procurement agent pattern (Book 2 Ch 11, illustrative composite): hundreds of purchase orders confirmed; zero actually delivered. The semantic eval passed every case. The agent said "purchase order created" every time. The state eval was not run. Nothing was created.

Not every action requires state validation. Text formatting for display, a summarization output, a draft message awaiting user send: these change no state in any system the team cares about. The cost of running state validation on every action is high and the value on these is zero. Filter actions explicitly.

Walk the PM through:

For each agent action class, ask: does this require state validation. Yes if the action should produce a change in a system of record. Critical if a wrong state would harm a customer, expose the company to a regulator, or compound through downstream agents. No if the action produces only a transient or display-only result.

For each yes or critical: name the state system, the eval that confirms the change, and whether the eval is continuous or design-time-only.

Output format:

```
SEMANTIC VS STATE VALIDATION: <agent name>

For each action class:
  <action>:
    Requires state validation: YES / NO / CRITICAL
    Justification for filter: <one line>
    If YES or CRITICAL:
      Semantic eval: <test description>
      State system: <where the state lives>
      State eval: <what confirms the change>
      Eval automation: continuous / scheduled / design-time only

Actions where state validation is required but not designed:
  <list - this is the launch risk>
```

### 4. Coverage Statement with Deferred Scenarios Named

The coverage statement is the document that says "here is what the eval suite tests, here is what it does not, and here is what we are deliberately not handling in v1."

The deferred-scenarios discipline is what separates a coverage statement from a list of cases-we-felt-like-running. Three categories:

**Covered.** The eval suite tests this case class. Include the case count and the rationale for the count.

**Known and not yet covered.** The team knows this case class exists but has not built eval coverage yet. Include the plan to cover it (sprint, release).

**Deliberately deferred.** The team has decided not to handle this case class in v1. Include the justification (low frequency, no harm if mishandled, alternative process exists) and the explicit deferral.

The deferred list is the most important part of the statement. A coverage statement with no deferred list is a statement that the team has not yet decided what to defer; they are about to discover it in production.

Walk the PM through:

What is the distribution of cases the agent will see in production. The PM should have brought this from Phase 1 (Distribution Gap Analysis).
For each case class, classify: covered / known-not-covered / deferred.
For deferred, write the justification. If the justification reads "we did not get to it," the case is not deferred. It is uncovered.

Output format:

```
COVERAGE STATEMENT: <agent name>

Covered case classes:
  - <case class>: <N test cases, rationale>

Known and not yet covered:
  - <case class>: plan <when>

Deliberately deferred:
  - <case class>: <justification>
    Estimated cost of deferral: <revenue impact, customer impact, or
      operational cost of handling outside the agent>

Coverage gap risk for launch: LOW / MEDIUM / HIGH
Risk acceptance: <named owner who signed off>
```

The deferral cost line matters because the business case for the agent was built on a volume assumption. If the deferred classes represent 15 percent of the production distribution, the agent's volume is 85 percent of what was projected, which changes the break-even calculation and possibly the go/no-go decision. The deferred-scenarios cost rolls up to the eval's business read, not just to the technical coverage map.

### 5. Adversarial Suite Results

If the prompt injection section of the eval is one paragraph, the team did not run a red team; they ran a checkbox.

The adversarial suite tests the agent against named attack patterns. The 2026 reference set: prompt injection, RAG poisoning, tool privilege escalation, Sequential Tool Attack Chaining (STAC), memory poisoning, and adversarial multi-turn sequences. The PM should have these from the Design phase Adversarial Defense Plan.

The reference set is the baseline, not the ceiling. Attack patterns evolve. Domain-specific and model-specific threats exist (supply-chain attacks on the agent's tool ecosystem, jailbreaks tuned to a specific base model's known weaknesses, attacks specific to the deployment context). Work with your security team to extend the suite. The PM does not write the attacks; the PM names which domains and models the team must extend coverage for, and the security team builds the tests.

Walk the PM through:

For each attack pattern, what is the test, what is the threshold, what is the result.
Where the agent failed, what is the mitigation, and where is it enforced (prompt, tool gateway, runtime policy, observability).
What attack patterns are not in the suite, and why.

Output format:

```
ADVERSARIAL SUITE RESULTS: <agent name>

For each attack pattern:
  <pattern>: 
    Test: <description>
    Threshold: <pass criteria>
    Result: PASS / FAIL
    If FAIL: mitigation <description>, enforced at <layer>

Attack patterns not tested:
  <list, with reasoning>
```

### 6. LLM-as-Judge Calibration Record

If the eval uses an LLM judge to score agent outputs, the judge introduces its own error rate. Length bias, position bias, same-model-family preference, all documented. An uncalibrated judge produces results whose error bars are larger than the agent's pass-rate variance.

The calibration discipline:

Build a small human-labeled set (100 to 500 cases).
Run the judge on the same set.
Measure agreement. Report inter-rater agreement (Cohen's kappa or similar) and disagreement classes.
Commit the threshold for "judge says pass" before reading the production eval results.

Walk the PM through:

Is the judge calibrated. If not, that is the finding.
What is the agreement rate with human labels.
Where does the judge systematically disagree (length, position, framing). The disagreement classes are the eval's hidden blind spots.

Output format:

```
LLM-AS-JUDGE CALIBRATION: <agent name>

Judge model: <model + version>

Human-labeled calibration set: <N cases>
Agreement with humans: <kappa or %>

Disagreement classes (where judge is systematically off):
  - <class>: <description>

Threshold committed before reading production results: <threshold>
```

### 7. All-Owner Readiness Memo

The all-owner readiness memo is the document the launch decision rests on. It is signed by four owners, each answering a question that lives inside their domain. Adapted from the Four-Question Pre-Launch Review (Framework #31).

**Head of engineering owns rollback time.** How long from an incorrect action to last known good state, measured in production conditions. The number on its own is insufficient. Compare it against the business-acceptable recovery window for the decision class. A 30-minute rollback may be fine for a routine refund and unacceptable for a clinical scheduling change. The memo records the measured rollback time AND the recovery window the business can tolerate; the gap is the launch blocker.

**CFO owns per-task cost.** What does the agent cost per successful outcome, including review time, rework, and coordination overhead. If the answer is the model token cost, the cost is wrong by a factor of 2 to 50.

**Head of legal owns audit surface.** Is every decision the agent makes reconstructable for a regulator, an auditor, or a customer, a year from now, with the model possibly updated. Reconstructable is necessary, not sufficient. Also ask: can decisions be overridden, reversed, or challenged after the fact. In regulated domains, a reconstructable decision that cannot be reversed is an audit liability. The memo records both: reconstructability and post-hoc actionability.

**Head of product owns the approval moment.** Where is a human required to intervene, and is the moment designed so it actually gets used rather than bypassed. The Cigna case (1.2 seconds per claim) is the failure mode.

A practical note on owner roles. Small orgs may not have all four roles. Substitute with the closest functional proxy: the eng manager for "head of engineering," the founder or finance lead for "CFO," outside counsel or the compliance officer for "head of legal," the senior PM for "head of product." The question each role answers does not change; the named owner is whoever in the org has that question inside their domain.

Owner disagreement resolution. The memo records four answers from four owners. If owners disagree on GO, the memo does not automatically resolve it. State the resolution mechanism explicitly: does any owner have veto authority (often legal does, on regulatory questions); does the head of product break ties; does the disagreement escalate to the CEO. Without a named mechanism, owner disagreement stalls the launch and the team improvises a resolution under pressure. Name the mechanism in advance.

Walk the PM through each. The memo is short, one page. Each owner signs their answer. If any owner cannot answer, that owner has the launch blocker, and the launch is not approved until they can.

Output format:

```
ALL-OWNER READINESS MEMO: <agent name>

The question this memo answers:
What is the worst slice of cases, and would we stake the launch on the
outcome in that slice?

Head of Engineering (rollback time):
  Question: How long from an incorrect action to last known good state?
  Measured: <X minutes/hours>
  Business-acceptable window for this decision class: <Y minutes/hours>
  Gap: <state in words; "measured rollback exceeds the business-acceptable
    window by X" is a launch blocker; "measured is at or under the window"
    is clear>

  Signature: <name + date>

CFO (per-task cost):
  Question: What does the agent cost per successful outcome,
  including review, rework, coordination?
  Answer: <$X, including all components>
  Signature: <name + date>

Head of Legal (audit surface):
  Question: Is every decision reconstructable a year from now,
  with possible model updates?
  Reconstructable: <YES / NO with caveat>
  Override / reversal mechanism post-decision: <description>
  Signature: <name + date>

Head of Product (approval moment):
  Question: Where is a human required, and is the moment designed
  so it is used rather than bypassed?
  Answer: <description>
  Signature: <name + date>

Resolution mechanism if owners disagree:
  <named approach: legal has veto, head of product breaks ties, etc.>

Launch decision: GO / NO-GO / HOLD pending <owner>
```

## Model-Version Policy and Rehearsed Rollback

A foundation model update is a deployment event. The eval suite has to anticipate it. If a vendor announces a new model version and the team has no plan, the agent is going to behave differently in production within days and nobody will know which behaviors changed.

The model-version policy:

The model version is pinned. The team controls when the agent uses a new model.

Regression suite fires on model-version change. Name the subset of the eval suite that constitutes regression: which cases, total count, expected run time. A typical subset is 200 to 500 cases covering the worst-slice classes from the full suite, run-time under 4 hours so the team can decide within a work day. If the regression suite takes two weeks to run and the vendor pushes updates monthly, the team will defer or skip re-eval; that pattern is a launch blocker, not a process detail.

State the deferral policy. What happens when a model update is ready before the regression run is complete. Three options, all valid in different contexts: hold the model update until re-eval completes; promote to canary only (small percentage of traffic) until re-eval completes; promote and accept the regression risk with the head of engineering signing off. The PM has to know which policy is in force; "it depends" is not a policy.

Vendor lead-time channel. Subscribe to vendor announcements. Plan capacity for re-eval. Also: poll for hotfixes, not just announced releases. Vendors push updates without announcement; the deployment-event log (Phase 4) catches these only after the fact.

Rehearsed rollback. The rollback path is run as a drill, not just documented. The first time the team rolls back a model version cannot be in a production incident.

This is part of the eval phase because the eval suite is the artifact that detects regression. Without the model-version policy, the eval becomes obsolete the moment the model updates.

## Returning to the headline question

As you walk the PM through the seven artifacts, keep returning them to the headline question: what is the worst slice, and would we stake the launch on the outcome in that slice.

Mean pass rate is not the answer. The worst slice is.
A coverage statement without deferred scenarios is not a coverage statement. It is a hope.
An LLM-as-judge eval without a calibration record is an eval with unknown error bars.
A semantic eval without a state eval is the procurement pattern: confirmed all, delivered none.

Each artifact tests the headline question. If an artifact is weak, name which dimension of the question it leaves unanswered.

## Munger inversion: what failure looks like

**The stale-guideline pass.** The eval was scored against faithfulness to the training distribution. The distribution was the old clinical guideline. The agent passed every eval and was wrong in production from day one. Prevented by: golden dataset pinned to current ground truth and refreshed on a cadence.

**The DAX Copilot wrong-target pass.** The eval was pointed at adoption. The business case rested on time saved. Adoption was high, time saved was zero. The eval passed and the agent moved no business metric. Prevented by: the eval rubric matches the business case, not the proxy.

**The procurement pattern (Book 2 Ch 11 composite).** The semantic eval passed every case. The state eval was not run. Hundreds of purchase orders confirmed; zero delivered. Prevented by: state validation as a separate gate.

**The judge bias.** The LLM judge preferred long answers and answers from its own model family. Pass rates were inflated for agents that wrote long answers in the judge's house style. Prevented by: judge calibration against human labels, with disagreement classes named.

**The silent model update.** A vendor pushed a model update on a Saturday. The agent's behavior shifted. No alert fired because the eval suite was last run against the previous model. The team learned about the regression from a customer ticket. Prevented by: model-version policy with regression suite on update.

**The launch with no rollback.** The agent shipped. It is wrong. The team tries to roll back. The rollback path was documented but never rehearsed. Rollback takes 11 hours instead of 11 minutes. Prevented by: rehearsed rollback as a drill, not just a runbook.

**The signed but undefended readiness memo.** Four owners signed. None of them could have defended their signature under a hard question. Prevented by: each owner answers in their domain language with a measured number, not a confidence statement.

When you produce the seven artifacts, refer back to these failures. Each artifact prevents one or more. Name the failure as you walk the PM through it.

## Handoffs

When Eval is complete and the all-owner readiness memo is signed GO:

Hand off to `agentic-pm-observe` to set up the production monitoring that will catch what the eval did not.

When the memo is NO-GO:

The named blocker becomes the next sprint. Reinvoke this skill when the blocker is addressed.

When the team is operating in production without having done a real Eval phase:

Run the skill anyway, with the artifacts marked "reconstructed post-launch." The gap is the remediation plan. Some of the gap may not be remediable; that is also information.

## Source

Book 1 (*Agentic AI for Busy Product Managers*), Chapter 6 "Evals: What the Checkmarks Actually Prove."

Book 2 (*Why Agentic AI Products Fail*), Chapter 9 "Evals: What the Checkmarks Prove" (Pass@K, worst-slice P10, judge calibration, model-version policy, the DAX wrong-target case), Chapter 11 "You Can't Measure What You Didn't Design" (the procurement composite, semantic-vs-state in operation), Appendix B "The Field Manual" (the all-owner readiness memo as a working artifact).

The Four-Question Pre-Launch Review with named owners is framework #31; the operational version lives in Book 2 Appendix B.

Frameworks #25 (Three Eval Breaks), #30 (Upstream-Data-Wrong Hallucination), #31 (Four-Question Pre-Launch Review), #42 (Validator-of-Validator Regress).

The full treatment of trajectory eval, judge calibration, and golden dataset construction lives in Book 2 Chapter 9 and Book 1 Chapter 6. Refer the PM there when they need to go deeper on a specific technique.
