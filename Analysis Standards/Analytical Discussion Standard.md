
## Purpose

**This document defines a standard structure for analyzing a game/project’s design, systems, and intended player experience.**

If the **project as a whole** is too large to analyze meaningfully, selectively analyze the **most significant systems** instead.

>This page is a guide for structured discussion and evaluation.  
>It is **not** a taxonomy page and **not** a terminology page.
>Reusable labels belong in the [[Attribute Reference Table]].
>Definitions belong in [[Terminology & Definition]].


---
# 0. Scope and Framing
***Before analysis, define the scope of discussion.***

## 0.1 Unit of Analysis

Identify what is being analyzed:

- the full project
- a mode
- a subsystem
- a recurring loop
- a specific version / patch / release state

## 0.2 Analytical Priority

Clarify the focus of the discussion:

- structural understanding
- experiential understanding
- design intention
- system reliability
- comparative evaluation

## 0.3 Evidence Basis

When possible, distinguish:

- directly observed play behavior
- explicit rules or formal structures
- inferred design intention
- community-facing labels or expectations


---
# 1. Systematic Core Components
***These are the minimum components to identify before higher-level analysis.***

## 1.1 Genre Labels
Genre labels are only shorthand for already recognized design patterns. They are NOT a substitute for system analysis.

At minimum, identify:
- **Player Unit Dynamics**
- **Core Mechanics** *(Labels if applicable)*

## 1.2 Player Verbs
Identify the primary actions the player repeatedly or meaningfully performs throughout play. Should complement the mechanics.

Examples:
- Jump
- Escape
- Collect

## 1.3 Core Resources
Identify the resources that directly shape decisions, planning, tradeoffs, or action.

Examples:
- Health
- Time
- Currency
 
## 1.4 Game Verbs _(if applicable)_
Identify recurring actions, events, or pressures the game applies to the player, especially those requiring response or adaptation.

Examples:
- Pursue
- Spawn
- Reveal

## 1.5 Core Rules *(if visible or inferable)*
Identify the underlying logic that governs state change, interaction, permission, limitation, and consequence.

Typical rule forms:
- A **is** B
- **If** Q, then R
- **When** X occurs, Y changes
- Z **may / may not** do Y, Depending on X

## 1.6 Game Characteristics
The overall experiential qualities or design character of the project.

Examples:
- Tense
- Punishing
- Relaxed
- Chaotic


---
# 2. Gameplay Frame
***Identify the project’s immediate structure of play.***

## 2.1 Play Objective / Success State
What is the player broadly trying to achieve?

This may include:
- formal win conditions
- local objectives
- self-directed goals
- long-term progression aims

## 2.2 Failure / Loss Pressure
What threatens progress, stability, efficiency, or success?

Possible forms include:
- death
- attrition
- time pressure
- positional collapse
- opportunity loss

## 2.3 Core Loop
What recurring sequence most strongly structures play?

Describe, where possible:
- player input / commitment
- system response
- reward / feedback
- reset / continuation
- repetition or escalation

## 2.4 Progression Structure _(if applicable)_
How does play develop over time?

Possible forms:
- level progression
- unlock progression
- run-based escalation
- economic accumulation
- skill mastery
- narrative advancement


---
## 3 System Analysis
***A System is a structured set of mechanics, rules, states, resources, and related components that together produce recurring behaviors, pressures, or possibilities.***

>A system need **NOT** to produce uniform outcomes (consistency). It may be variable, probabilistic, or partially autonomous. What matters is that the system operates ***reliably according to its design logic*** and meaningfully contributes to the project’s play, structure, or experience.

### 3.1 Identify the Central and Distinctive Systems

Focus first on the systems that most strongly define:
- player behavior
- project identity
- decision structure
- experiential tone

Examples:
- movement system
- combat system
- economy system
- progression system
- inventory system
- encounter system

### 3.2 Supporting Systems *(if relevant/exceptional)*
Identify smaller systems only when they materially shape play, readability, pacing, or system interaction.

Examples:
- map System
- save System
- inventory UI System
- weather System
- tutorial System


### 3.3 For each selected system, *interpret* and *ask*:
#### A. Function
What does this system do?
Focus:
- What does this system produce, regulate, or maintain?
- What conditions, pressures, opportunities, or state changes does it create?
- If applicable, what inputs does it respond to, and what outputs does it produce?

#### B. Structure
What is this system made of?
Focus:
- What **mechanics** and **resources** are central to this system?
- What are the central **rules**, **states**, or **constraints** that **govern** it?
- What **triggers**, **probabilities**, or **feedback loops** shapes the behavior?

#### C. Intention
Why does this system appear to exist?
Focus:
- What **design purpose**, **goal**, or **experience** does it serve?
- What is its **role** in the in the wider project?
- What **player** **behaviors**, **decision** patterns, or forms of **attention** does it encourage, shape, or regulate?
- What **pacing**, **tension**, **mastery**, or **fantasy** does it support?

#### D. Interactions
How does this system relate to players and other systems?
Focus:
- What the **player** can **influence**?
- What the system **communicates back**?
- What **other systems** does it meaningfully **affect** or **depend on**?
- Does it amplify, constrain, destabilize, or support other systems?
- Are its **outputs** another system’s **inputs**?

#### E. Legibility
How understandable the system is to the player?
Focus:
- Are **cause** and **effect** are **readable**?
- Are **outcomes** are **bounded** and usable?
- Is **variability** remains **interpretable**?
- Can players form **reliable expectations**?
- Is the system **consistent** with its apparent rules?

#### F. Friction / Failure _(if relevant)_
Where does the system break down or work against itself?
Focus:
-  confusion
- degenerate incentives
- excessive burden
- weak feedback
- unreadable randomness
- avoidable repetition
- edge-case failure
- contradiction between stated purpose and actual effect


---
# 4 Play Structures _(if possible; selective)_
***Analyze how play is organized over time.***

## 4.1 Entry and Onboarding
How does the player enter the play structure?
Focus:
- initial readability
- tutorial
- early rule exposure
- early demand level
- how the project teaches action and consequence

## 4.2 Repetition and Variation
How does the project sustain repeated play?

>Not all games support repeated play.

Focus:
- repetition of core actions
- variation in challenge, context, or decision-making
- whether repetition deepens mastery or merely extends duration

## 4.3 Pacing
How does the project alternate between:
- action
- planning
- recovery
- downtime
- escalation
- resolution

## 4.4 Escalation and Mastery
How does complexity or pressure increase?
Focus:
- whether demands scale clearly
- whether new problems build on prior understanding
- whether mastery is mechanical, strategic, informational, or expressive

## 4.5 Short-Term and Long-Term Structure
How do immediate play and broader progression interact?
Focus:
- local success vs long-term gain
- tactical vs strategic priorities
- temporary vs persistent rewards
- whether long-term systems enrich or distort moment-to-moment play







### 4.1 Play Objective / Success State
Identify what the player is broadly trying to achieve, whether locally or across the project.

> This is NOT limited to formal win conditions. Many projects are driven by soft goals, self-set goals, or long-term progression goals.

Possible forms:
- Survive
- Defeat opponents
- Optimize output
- Reach the end state
- Solve uncertainty

### 4.2 Failure / Loss Pressure
Identify what threatens player progress, stability, or success.

> Failure pressure often reveals the project’s real priorities more clearly than genre labels do.

Possible forms:
- Death
- Resource exhaustion
- Time pressure
- Positional collapse
- Opportunity loss

### 4.3 Significate Systems
PLACEHOLDER
Mostly the system discussed about







---
# 5 Gameplay Analysis _(if possible)_
PLACEHOLDER
Analyze how play is structured

Focus:
- how the player enters, learns, and repeats the main loop
- pacing between action, planning, recovery, and resolution
- escalation of complexity, pressure, and mastery demands
- transitions between short-term play and long-term progression
- whether downtime, friction, and repetition are purposeful

PLACEHOLDER

---
# 6 Comparative Analysis
Comparison clarifies the project’s position.

## 6.1 Horizontal Analysis _(if applicable, System / Project)_
***Reveals comparative distinctiveness.***
Compare the project with other projects that use similar components or pursue similar goals.

Focus:
- Distinctive design choices
- Meaningful strengths or weaknesses
- Likely reasons players do or do not respond positively
- Whether the project is more legible than comparable projects


## 6.2 Backward Analysis _(if applicable, System / Project)_
***Show design shifts.***
Compare the project with earlier entries in the same series, lineage, or design tradition.

Focus:
- What changed
- What improved or regressed
- What design values appear to have shifted
- How those changes may affect player response

## 6.3 Target Analysis
***Reveals intended audience fit; potentially effectiveness.***
Identify the intended target audience and the elements likely meant to appeal to them; 

>Should refer to observable design evidence.

Ask:
- Who is this project primarily for?
- What design elements appear aimed at that audience?
- Was that intention successful?
- If relevant, how successful was it relative to earlier entries or competitors?

## 6.4 Orthogonal Analysis _(optional)_
******Reveals cross-audience appeal; possible extensibility.***
Identify whether the project also appeals strongly to an audience associated with a noticeably different genre or design space;

Ask:
- Is there a significant overlap with another audience segment?
- Why might that overlap exist?
- Does it strengthen or weaken the project’s identity?

## 6.5 Constraint Analysis _(optional)_
***Reveals the value of exclusion.***

> Design quality is often defined as much by exclusion and restraint as by feature presence.

Focus:
- What the player cannot do
- What is intentionally abstracted away
- Where complexity is reduced or hidden
- What constraints make the design readable, playable, or identity-consistent

Ask:
- What has been excluded or compressed?
- Why might these exclusions exist?
- Do these constraints strengthen the intended experience?

---
## 7 Outcome Summary
**Reveals the value of exclusion.**

May Contain:
- **Project Identity:** What kind of experience is this trying to produce?
- **Central Systems:** Which systems most strongly define that identity?
- **Design Strengths:** What is working especially well?
- **Design Risks / Weaknesses:** What limits, distorts, or weakens the project?
- **Overall Judgment:** Does the project successfully achieve its likely design intentions?


---
**Reference**: 

Game Mechanics & Systems Thinking
https://www.youtube.com/watch?v=nkLmjJK3vOw&list=PLyTIzr2AVP3_0zeFw9-9tjQNcV2aCnggd&index=3&t=408s