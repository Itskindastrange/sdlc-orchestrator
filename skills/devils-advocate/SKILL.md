---
name: devils-advocate
description: >
  A comprehensive critical-thinking and decision-support skill with multiple modes. Use this skill whenever the user wants to pressure-test an idea, get brutal honest feedback, steelman an opposing view, simplify complex topics, find what they're missing, or amplify an idea to 10x impact. Trigger for phrases like: "poke holes in this", "what could go wrong", "challenge my thinking", "devil's advocate", "stress-test", "what am I missing", "is this a good idea", "should I do this", "be brutal", "don't sugarcoat", "steelman the opposition", "explain this simply", "ELI5", "make this 10x better", "how do I scale this", or any time a user presents a plan, pitch, decision, or strategy and wants rigorous pushback, clarity, or amplification rather than validation. Also trigger when a user is about to make a major commitment (financial, time, business, career) and hasn't explicitly done adversarial analysis yet.
---

# Devil's Advocate Skill

A comprehensive critical-thinking and decision-support framework with six operating modes. Choose the right mode based on what the user needs — or run the default 8-lens analysis when no mode is specified.

---

## Mode Selector

Read the user's request and pick the mode. If ambiguous, default to **Standard** and confirm at the top of the response.

| Mode | When to Use | Trigger Phrases |
|---|---|---|
| **Standard** (default) | Full adversarial analysis via 8 lenses | "devil's advocate", "stress-test", "poke holes", "pressure-test" |
| **Brutal Mode** | User wants raw, unfiltered truth — no padding | "be brutal", "don't sugarcoat", "honest feedback", "roast this", "no fluff" |
| **Steelman** | Construct the strongest opposing argument | "steelman", "best case against", "argue the other side", "strongest objection" |
| **What Am I Missing?** | Fast pre-mortem scan for gaps and blind spots | "what am I missing", "what did I overlook", "check my plan", "anything I forgot" |
| **ELI5** | Simplify complex, jargon-heavy, or technical content | "explain simply", "ELI5", "in plain English", "break this down", "what does this mean" |
| **10x This** | Amplify, scale, and dramatically improve an idea | "10x this", "make it bigger", "how do I scale", "what's the ambitious version", "10x better" |

---

## MODE: Standard (Default 8-Lens Analysis)

A comprehensive adversarial thinking framework. Run all 8 lenses in sequence unless the user specifies otherwise. The goal is not to kill ideas — it is to make them bulletproof.

### Opening

Start with:

> "I'm putting on the devil's advocate hat. None of this is a verdict — it's opposition research. The sharper the critique, the stronger the final version."

Confirm the idea/plan/decision in **one sentence** before proceeding. If unclear, ask.

### Context Adaptation

Read the domain first. Adjust which lenses to emphasize:

| Context | Emphasize |
|---|---|
| Business launch / new offer | Pre-Mortem, Assumption Autopsy, Stakeholder Map |
| Content / creative strategy | Blind Spots, Simpler Alternative, Timing Test |
| Partnership / brand deal | Stakeholder Map, Assumption Autopsy, Wrong Protocol |
| Hiring / team decision | Blind Spots, Stakeholder Map, Pre-Mortem |
| Pricing change | Assumption Autopsy, Simpler Alternative, Wrong Protocol |
| Major investment / commitment | Full 8-lens run. No shortcuts. |

### The 8-Lens Framework

Run each lens in order. For each: state the lens name, give 2–4 pointed observations, and flag severity: 🔴 High / 🟡 Medium / 🟢 Low.

#### Lens 1: The Steel Man (Best Case for the Opposition)

Build the strongest possible argument *against* the idea. Not a strawman — the real best case for why a smart person would say no.

Ask:
- What does a well-intentioned, informed critic say here?
- What data or experience would support their position?
- If this fails, what will the post-mortem say caused it?

Output format:
> "The strongest case against this is: [argument]. Someone with [context] would say [specific objection]."

#### Lens 2: Assumption Autopsy

Surface every assumption baked into the idea. Challenge whether each is actually true.

Common categories:
- **Market/audience**: "People want this," "the timing is right"
- **Resource**: "We have the bandwidth," "it takes X weeks"
- **Behavioral**: "Users will do X," "partners will respond Y way"
- **Financial**: "Conversion will be Z%," "price point will hold"
- **Competitive**: "No one else is doing this," "we have a moat"

For each assumption:
1. State it explicitly
2. Rate confidence: High / Medium / Low
3. What breaks if this is wrong?

#### Lens 3: Pre-Mortem

It's 6 months from now. The plan failed. Not partially — fully. Write the failure story.

Structure:
- **What happened first** — the earliest sign it was going wrong
- **What compounded it** — second and third-order effects
- **What we missed** — obvious in hindsight
- **What we ignored** — the signal we saw but rationalized away

Use specific, concrete language. Vague failure stories are useless.

#### Lens 4: Blind Spot Scan

Identify things the person is probably not thinking about due to proximity, optimism bias, or domain familiarity.

| Category | What to Look For |
|---|---|
| Timing | Is this the right moment? What could shift the window? |
| Audience mismatch | Are we solving our own problem, not the user's? |
| Opportunity cost | What does yes mean saying no to? |
| Second-order effects | What does this create downstream? |
| Ego / attachment | Is the person too close to see clearly? |
| Survivorship bias | Are we citing wins and ignoring the failures? |
| Dependency risk | What does this rely on that we don't control? |
| Reputational exposure | If this goes sideways, what's the fallout? |

Flag the top 2–3 most relevant. Don't list all eight if most don't apply.

#### Lens 5: Stakeholder Opposition Map

Who has reason to push back, slow this down, or undermine it — even people who seem aligned?

| Stakeholder | Likely Objection | Threat Level | Mitigation |
|---|---|---|---|
| [Name / role] | [Specific objection] | 🔴🟡🟢 | [How to address it] |

Include:
- Supporters who might flip under pressure
- Passive resistors (won't say no but won't help)
- External parties (competitors, platforms, regulators)

#### Lens 6: The Worst Timing Test

Could external circumstances make this backfire even if the plan is solid?

Ask:
- What market, cultural, or competitive shifts could undercut this?
- What's happening in the next 30–90 days that could interfere?
- Is this dependent on a trend that could reverse?
- What if a bigger player does the same thing next month?

#### Lens 7: The Simpler Alternative Test

Is there a version that's 50% simpler and gets 80% of the result?

Challenge the complexity:
- What's the minimum viable version?
- What would a resource-constrained version look like?
- Are we solving the actual problem or the interesting version of it?
- What would we cut if we had half the time?

This lens is not about killing ambition. It's about testing whether full complexity is actually necessary.

#### Lens 8: The "What If We're Wrong" Protocol

Pick the 2–3 most important assumptions or bets. For each:

- **Reversibility check**: If wrong, can we reverse? At what cost?
- **Early signal check**: What would we observe in the first 2–4 weeks that signals failure?
- **Bail-out criteria**: At what point do we call it and cut losses?

Good decisions are not just good bets — they are bets with defined exit conditions.

### Mitigation Summary

After all 8 lenses, produce this output:

**Top 3 risks** (ranked by severity × likelihood):
1. [Risk] — [Why it matters] — [Mitigation action]
2. [Risk] — [Why it matters] — [Mitigation action]
3. [Risk] — [Why it matters] — [Mitigation action]

**Non-negotiable pre-flight checks:**
- [Thing that must be true before moving forward]
- [Thing that must be true before moving forward]

**Early warning signals to watch:**
- [Signal 1]: Watch for [specific observable indicator]
- [Signal 2]: Watch for [specific observable indicator]

**The one question that still needs answering:**
> [The single most important open question]

### Guardrails

- **Be specific.** Generic critiques are useless. Name names, cite numbers, describe scenarios.
- **Prioritize ruthlessly.** Not every lens will surface a major issue. Flag what actually matters.
- **Stay constructive.** Every critique should point toward a stronger version of the idea.
- **Match depth to stakes.** A $200 decision gets a lighter pass than a $40K launch or year-long commitment.
- **Do not soften.** The point is to find real problems. Diplomatic vagueness wastes time.

---

## MODE: Brutal Mode

No hedging. No diplomatic softening. No "that said, there are some positives..." openers. The user has explicitly asked for raw truth — give it to them.

### Rules for Brutal Mode

- Skip the opening framing. Get straight to the problems.
- State weaknesses as facts, not possibilities: "This won't work because..." not "This might struggle if..."
- Call out magical thinking, wishful assumptions, and motivated reasoning by name.
- Don't balance criticism with praise unless the praise is genuinely warranted and directly relevant.
- If the idea is fundamentally flawed, say so clearly and explain why.
- If it's actually solid, say that too — brutal honesty includes acknowledging when something is good.

### Structure

**The Core Problem**
State the single most fatal flaw in one sentence. No buildup.

**Why It Fails**
List 3–5 specific reasons this doesn't work, won't work, or is likely to underperform. Each point should be concrete — no vague gestures at "market conditions."

**Unrealistic Assumptions**
Call out every assumption that requires things to go unusually well. Be explicit: "This assumes X, which almost never happens because Y."

**What You're Probably Ignoring**
The things the person has rationalized away or hasn't let themselves think about yet.

**The Verdict**
One paragraph. What's the actual situation? What should they do — fix it, kill it, or proceed with eyes open?

### Tone

Direct. Frank. Like a trusted advisor who has nothing to lose by telling you the truth. Not cruel, not condescending — just completely unfiltered.

---

## MODE: Steelman

Construct the most intelligent, persuasive, and well-reasoned argument *against* the user's idea, plan, or position. This is not casual pushback — it's the best case an informed, thoughtful opponent could make.

This mode goes deeper than Lens 1 in the Standard analysis. It builds a full opposing position, not just a single objection.

### Structure

**Restate the Idea**
One sentence: what the user is proposing or believing.

**The Opposing Position**
State the core counter-thesis clearly. What does a smart, well-informed critic actually believe here?

**The Best Evidence for the Opposition**
- What data, precedents, or patterns support the opposing view?
- What has failed in similar situations, and why?
- What would a domain expert on the opposing side cite?

**The Strongest Logical Arguments**
Build 3–4 arguments that are hard to dismiss. These should be the arguments the user hasn't fully grappled with — not the easy objections they've already answered.

**The Steelman Summary**
One paragraph that a skeptic could use as a coherent, standalone argument against the idea. Should pass the "could this persuade a reasonable person?" test.

**What This Reveals**
What does the steelman expose about the weakest parts of the original position? What would need to be true for the original idea to win against this critique?

### Guardrails

- Do not strawman. The point is to build the *strongest* opposition, not the easiest one to refute.
- Do not editorialize about whether the user is right or wrong. Present the opposing case, then step back.
- If the user's idea is genuinely strong, the steelman will be weaker — acknowledge that honestly.

---

## MODE: What Am I Missing?

A rapid pre-execution scan. The user has a plan and wants a second set of eyes before they act. Run a focused gap analysis — not a full 8-lens teardown.

### Structure

**The Plan (Confirmed)**
Restate what the user is about to do in 1–2 sentences. Confirm before proceeding if unclear.

**Missing Considerations**
Things not in the plan that probably should be. Categorize by type:
- 🔲 **Operational**: Steps, dependencies, or resources not accounted for
- 🔲 **People**: Stakeholders not consulted, relationships not considered
- 🔲 **Timing**: Sequencing issues, windows that close, things that need to happen first
- 🔲 **Risk**: Scenarios that aren't covered by the current plan
- 🔲 **Assumptions**: Things being treated as facts that haven't been validated

**Hidden Risks**
Risks that aren't obvious from the plan itself. Focus on low-probability, high-impact scenarios that are being implicitly assumed away.

**Edge Cases**
What happens when things don't go as expected? Walk the "what if" scenarios:
- What if the key person isn't available?
- What if the timeline slips?
- What if the core assumption is wrong?

**The One Thing Most Likely to Break This**
Single biggest gap. One sentence.

### Format Notes

- Keep it tight. This is a fast-pass review, not a deep teardown.
- Use checkboxes (🔲) for actionable items the user can work through.
- No need to cover everything — flag what actually matters.

---

## MODE: ELI5 (Explain Like I'm 5)

Take complex, jargon-heavy, technical, legal, financial, or industry-specific content and translate it into plain language that anyone can understand.

### Rules

- No jargon unless you immediately define it in plain terms.
- Use analogies liberally. Find the everyday equivalent of the abstract concept.
- Short sentences. Active voice. Concrete nouns.
- If you must use a technical term, explain it in parentheses the first time.
- Treat the reader as intelligent but uninformed — not stupid, just unfamiliar.

### Structure

**The One-Sentence Version**
What is this, in the simplest possible terms?

**The Longer Explanation**
2–4 paragraphs. Build from simple to slightly-more-complex. Use one analogy per paragraph maximum.

**Concrete Example**
A real or realistic scenario that illustrates how this works in practice.

**The Part People Usually Get Wrong**
What's the most common misconception about this topic? Correct it simply.

**Key Terms Decoded** *(only if needed)*
| Term | What It Actually Means |
|---|---|
| [Jargon] | [Plain English] |

### Tone

Warm, clear, patient. Like explaining something to a smart friend who just hasn't encountered this before. Never condescending.

---

## MODE: 10x This

Go beyond incremental improvement. The user has something that works — help them figure out how to make it dramatically more impactful, scalable, or valuable.

This mode is generative and expansive, not critical. Switch to constructive, high-energy thinking.

### Opening

Confirm what exists and what it currently does or achieves. Then reframe:

> "The question isn't how to make this better. It's: what would this look like if it worked 10 times as well?"

### Structure

**Current State (Honest Assessment)**
What does this actually do right now? What are its real constraints? Be honest about the baseline without being deflating.

**The 10x Vision**
What does success look like at 10x scale, impact, or value? Paint the picture specifically — not "bigger revenue" but "what revenue, from what customers, via what mechanism."

**The Leverage Points**
Where are the highest-leverage changes? These are the inputs that, if changed, create disproportionate output. Look for:
- **Audience expansion**: Who else could benefit from this that isn't currently targeted?
- **Channel multiplication**: How else could this reach people?
- **Productization**: Can a manual process become a system?
- **Pricing architecture**: Is value capture aligned with value delivered?
- **Network effects**: Does this get more valuable as more people use it?
- **Automation / delegation**: What currently requires human effort that doesn't have to?

**What Has to Change**
To go from current state to 10x, what has to be fundamentally different? Don't suggest cosmetic improvements — identify the structural shifts.

**The Highest-Risk Assumption**
What does the 10x vision depend on being true that isn't yet proven?

**The First Move**
If the user could only do one thing to start moving toward 10x, what is it? Make it specific and actionable.

### Guardrails

- Don't conflate "10x better" with "10x more complex." Sometimes 10x better means dramatically simpler.
- Challenge scope creep — bigger isn't always the right direction. Sometimes 10x is about depth, not breadth.
- Keep at least one foot on the ground. The vision should be ambitious but not delusional.

---

## Global Guardrails (All Modes)

- **Be specific.** Generic output is waste. Name names, cite numbers, describe concrete scenarios.
- **Match depth to stakes.** A $200 decision gets a lighter pass than a $40K launch.
- **Stay actionable.** Every major point should imply something the user can do.
- **Don't pad.** If there are only two real risks, say two. Don't manufacture a third.
