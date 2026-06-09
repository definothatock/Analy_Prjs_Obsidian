## Purpose

This document defines a concise structure for **designing** a game/project’s mechanics, systems, and intended player experience from the ground up.

This Standard/Template for:
- creating a new project
- designing a new mode
- designing a system/subsystem
- revising an existing design direction

It is **not** for implementation detail.  
If discussion becomes too technical, move that into a separate implementation document.

This standard is **modular**:
- **Project / Mode** design should emphasize experience, structure, progression, and audience fit.
- **System / Subsystem / Loop** design should emphasize purpose, rules, decision structure, feedback, and interaction with other systems.

> **Design Order Principle:**  
> **intent → player actions → rules/resources → loop → feedback → failure pressure → validation**
> 
> Do not start from labels alone.  
> Start from what the design must make the player **do, notice, decide, and feel**.

---

# 0. Scope and Design Framing
_**Before designing, define what is being designed and why.**_

## 0.1 Unit of Design

Identify what is being designed:
- full Project
- Mode
- System
- Subsystem
- Recurring Loop

If the project is too large, design the most identity-defining unit first.

## 0.2 Design Goal

Clarify the primary design focus:
- create a core experience
- support an existing project identity
- solve a specific design problem
- add depth / variation / progression
- improve clarity / pacing / replayability

## 0.3 Design Constraints

Define major constraints early:
- scope
- complexity budget
- session length
- platform / control limits
- content production limits
- multiplayer / solo structure
- required compatibility with existing systems

> A good design standard should protect against overdesign.  
> State what this design **will not try to do**.

---

# 1. Intended Experience
_**Define the experience before defining the system.**_

## 1.1 Target Experience
What should the player primarily experience?

Possible examples:
- tension
- mastery
- improvisation
- pressure
- planning
- discovery
- expression
- competition
- chaos
- survival

## 1.2 Player Motivation
Why should the player engage with this design?

Possible forms:
- achieve victory
- overcome pressure
- optimize performance
- build mastery
- express playstyle
- gain rewards
- explore possibility space

## 1.3 Desired Player Behaviors
What behaviors should the design encourage?

Examples:
- commit carefully
- adapt quickly
- take calculated risks
- conserve resources
- coordinate with others
- read threats early
- experiment with tools

## 1.4 Anti-Goals
What behaviors or experiences should the design avoid?

Examples:
- passive waiting
- repetitive safe play
- dominant single-strategy use
- unreadable punishment
- fake choice
- excessive mental load
- low-skill busywork

---

# 2. Core Design Frame
_**Define the system in its simplest useful form.**_

## 2.1 System Purpose
What is this system for?

Focus:
- what problem it solves
- what play it creates
- what pressure, opportunity, or structure it adds
- what role it serves in the wider project

Possible roles:
- central
- supporting
- gating
- pacing
- expressive
- progression-driving
- stabilizing

## 2.2 Success Contribution
How does this system help the player succeed or fail?

Focus:
- what outcomes it influences
- what decisions it makes meaningful
- what part of success depends on it

## 2.3 Design Pillars _(short)_
State 2–4 principles this design should obey.

Examples:
- easy to read, hard to master
- reward commitment, not hesitation
- create pressure without constant punishment
- support multiple viable playstyles

> If a later rule conflicts with a pillar, revise the rule or revise the pillar.

---

# 3. Core Components
_**Define the actual design pieces.**_

## 3.1 Core Mechanics
Identify the main rule-bound interaction structures.

At minimum, define:
- **Actor Relation Structure**
- **Core Mechanics**
- any essential pattern labels, if useful

## 3.2 Player Verbs
Identify the main actions the player performs.

Examples:
- move
- aim
- dodge
- collect
- place
- trade
- combine
- retreat

## 3.3 System Verbs
Identify recurring actions applied by the game/system.

Examples:
- spawn
- reveal
- decay
- pursue
- block
- escalate
- alert
- rotate

## 3.4 Core Resources
Identify resources that shape decisions.

Examples:
- health
- time
- stamina
- attention
- ammo
- space
- currency
- cooldown
- position

## 3.5 Core Rules
Identify only the rules necessary to establish behavior.

Typical rule forms:
- A **is** B
- **If** X, then Y
- **When** Q happens, Z changes
- Player **may / may not** do R under condition S

> Keep rules at design level, not code level.

---

# 4. Decision Structure
_**A system is useful when it creates meaningful repeated decisions.**_

## 4.1 Core Decisions
What decisions should the player repeatedly make?

Examples:
- when to commit
- what to spend
- what risk to accept
- what target to prioritize
- whether to push or recover
- whether to act now or hold

## 4.2 Tradeoffs
What makes those decisions non-trivial?

Possible forms:
- safety vs reward
- speed vs certainty
- short-term gain vs long-term stability
- flexibility vs specialization
- resource use vs conservation
- information vs exposure

## 4.3 Failure Pressure
What threatens the player if they misplay, delay, or overcommit?

Possible forms:
- death
- attrition
- time loss
- opportunity loss
- positional collapse
- economic setback
- escalation of future pressure

## 4.4 Dominant Strategy Check
What is the most likely degenerate strategy, and how is it prevented?

Examples:
- turtling
- stalling
- spam usage
- risk-free farming
- one-stat optimization
- single best build
- avoiding the intended interaction entirely

---

# 5. Loop and Progression
_**Define how the design repeats and develops over time.**_

## 5.1 Core Loop
Identify the recurring sequence that structures play.

Describe:
- player commitment
- system response
- feedback / reward
- reset / continuation
- repetition / escalation

## 5.2 Short-Term Rhythm

How does this design alternate between:
- action
- planning
- recovery
- downtime
- payoff

## 5.3 Progression Structure _(if applicable)_
How does this design develop over time?

Possible forms:
- unlocks
- escalating encounters
- economic growth
- skill mastery
- build development
- narrative advancement
- expanding decision space

## 5.4 Variation
How does repeated play remain meaningful?

Possible forms:
- new contexts
- changing constraints
- enemy variation
- tool combinations
- evolving priorities
- random but interpretable variation

---

# 6. Information, Feedback, and Control
_**If players cannot perceive or use the system, the design does not function well.**_

## 6.1 Information Visibility
What must the player know to make informed decisions?

Examples:
- current state
- threats
- timing windows
- resource levels
- likely outcomes
- hidden vs visible information

## 6.2 Feedback
How does the system communicate:

- action success or failure
- state change
- danger
- opportunity
- consequence

## 6.3 Legibility
Can the player form reliable expectations?

Check:
- cause and effect are readable
- system responses are learnable
- randomness stays interpretable
- important states are not overly hidden
- failure feels traceable

## 6.4 Control Demand
What level of execution or attention does the system require?

Focus:
- timing precision
- multitasking
- planning load
- input complexity
- reaction demand

> Match control demand to the intended audience and project identity.

---

# 7. System Integration
_**A strong system works with the rest of the project, not beside it.**_

## 7.1 Dependencies
What other systems does this design depend on?

Examples:
- movement
- combat
- economy
- UI
- progression
- matchmaking
- map structure

## 7.2 Outputs
What does this design feed into?

Examples:
- reward pacing
- encounter difficulty
- progression speed
- player expression
- strategic planning
- social coordination

## 7.3 Alignment Check
Do rewards, pressures, and constraints support the intended behavior?

Ask:
- what behavior is actually incentivized?
- does the system reward the playstyle it claims to support?
- do any surrounding systems distort its intended use?

---

# 8. Risks and Safeguards
_**Identify failure points before production.**_

## 8.1 Main Design Risks
What is most likely to go wrong?

Possible risks:
- unreadability
- low decision depth
- repetitive optimal play
- excessive punishment
- excessive complexity
- low payoff for mastery
- weak system identity
- poor scaling over time

## 8.2 Safeguards
What design choices reduce those risks?

Examples:
- clearer feedback
- stronger tradeoffs
- softer failure early
- harder constraints on dominant strategies
- simpler resource model
- better escalation structure
- narrower mechanic scope

## 8.3 Exclusions
What has been intentionally omitted, simplified, or abstracted?

Focus:
- what the player cannot do
- what complexity is hidden
- what realism is sacrificed
- what interactions are intentionally disallowed

> Strong design often comes from refusal, not accumulation.

---

# 9. Validation
_**Before implementation, define how the design will be judged.**_

## 9.1 Design Success Questions

Ask:
- does this create the intended player behavior?
- are decisions meaningful and repeated?
- is failure pressure understandable?
- does the system remain readable under stress?
- does it support the project identity?
- does repeated use stay interesting?

## 9.2 Test Scenarios
Define a few concrete situations to test.

Examples:
- first-time player interaction
- average repeated play
- high-skill optimization case
- low-resource / high-pressure case
- edge-case abuse attempt

## 9.3 Revision Trigger
What results would mean the design should be revised?

Examples:
- players ignore the intended mechanic
- one strategy dominates
- feedback is misunderstood
- the system creates waiting or busywork
- mastery does not improve outcomes
- it adds complexity without adding decisions

---

# 10. Design Summary
_**A short planning summary for later reuse.**_

May contain:
- **Unit of Design**
- **Target Experience**
- **System Purpose**
- **Core Mechanics**
- **Core Decisions**
- **Main Resources**
- **Main Risk**
- **Validation Focus**

---

# Extra Materials

## Quick Design Brief _(Optional)_
_**A compact planning-first summary.**_

This section should be written last, but placed at the top of an actual design note.

Possible contents:
- **What is being designed**
- **What experience it should create**
- **What the player mainly does**
- **What makes decisions meaningful**
- **What could go wrong**
- **What must be validated first**