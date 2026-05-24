
## Purpose

**This document defines a standard structure for analyzing a game/project’s design, systems, and intended player experience.**

If the **project as a whole** is too large to analyze meaningfully, selectively analyze the **most significant system(s)** instead.

>This page is a guide for structured discussion and evaluation.  
>It is **not** a taxonomy page and **not** a terminology page.
>Reusable labels belong in the [[Attribute Reference Table]].
>Definitions belong in [[Terminology & Definition]].


---
# 0. Scope and Framing
***Before analysis, define the scope of discussion.***

## 0.1 Unit of Analysis
Identify what is being analyzed:

>Isolated mechanics or rules are usually ***too narrow*** to serve as a primary unit of design analysis, unless they are examined in relation to the larger system, loop, or project context.
>Mechanics-Focused Discussion belongs to [[Analytical Discussion Standard on Implementations]].

- the full Project
- a Mode
- a System
- a Subsystem
- a recurring Loop

Then select necessary sections to analyze accordingly .

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

## 1.1 Reference Labels ("Genre")
Reference labels are only shorthand for **already recognized design patterns**. They are NOT a substitute for system analysis.

At minimum, identify:
- **Player Unit Dynamics**
- **Core Mechanics labels**

>For whatever reason that recognized labels cannot be used, such as no existing similar design patterns, create a separate appropriate framing. 

## 1.2 Player Verbs
Identify the **primary actions** the player repeatedly or meaningfully performs throughout play. Should complement the mechanics.

Examples:
- Jump
- Escape
- Collect

## 1.3 Core Resources
Identify the **resources** that directly **shape** decisions, planning, tradeoffs, or action.

Examples:
- Health
- Time
- Currency
 
## 1.4 Game Verbs _(if applicable)_
Identify **recurring actions**, events, or pressures the game applies to the player, especially those requiring response or adaptation.

Examples:
- Pursue
- Spawn
- Reveal

## 1.5 Core Rules *(if visible or inferable)*
Identify the underlying **logic** that **governs** state change, interaction, permission, limitation, and consequence.

Typical rule forms:
- A **is** B
- **If** Q, then R
- **When** X occurs, Y changes
- Z **may / may not** do Y, Depending on X


---
# 2. Gameplay Frame
***Identify the project’s immediate structure of play; more combine and abstracted.***

## 2.1 Play Objective / Success State
What is the **player** broadly trying to **achieve**.

This may include:
- formal win conditions
- local objectives
- self-directed goals
- long-term progression aims

## 2.2 Failure / Loss Pressure
What **threatens** progress, stability, efficiency, or success.

Possible forms include:
- death
- attrition
- time pressure
- positional collapse
- opportunity loss

## 2.3 Core Loop
What **recurring sequence** most strongly structures play.

Describe, where possible:
- player input / commitment
- system response
- reward / feedback
- reset / continuation
- repetition or escalation

## 2.4 Progression Structure _(if applicable)_
How does play develop over time.

Possible forms:
- level progression
- unlock progression
- run-based escalation
- economic accumulation
- skill mastery
- narrative advancement

## 2.5 Game Characteristics
The overall experiential qualities or design character of the project.

Examples:
- Tense
- Punishing
- Relaxed
- Chaotic


---
# 3 System Analysis
***Analysis the system's behaviours and appearances. Do not infer.***   

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
##### A. Function
What does this system do?
Focus:
- What does this system **produce**, **regulate**, or **maintain**
- What **conditions**, **pressures**, **opportunities**, or **state changes** does it **create**
- *If applicable*, what **inputs** does it respond to, and what **outputs** does it produce

##### B. Structure
What is this system made of?
Focus:
- What **mechanics** and **resources** are **central** to this system
- What are the central **rules**, **states**, or **constraints** that **govern** it
- What **triggers**, **probabilities**, or **feedback loops** shapes the **behavior**

##### C. Intention
Why does this system appear to exist?
Focus:
- What **design purpose**, **goal**, or **experience** does it serve
- What is its **role** in the in the wider project
- What **player** **behaviors**, **decision** patterns, or forms of **attention** does it encourage, shape, or regulate
- What **pacing**, **tension**, **mastery**, or **fantasy** does it support

##### D. Interactions
How does this system relate to players and other systems?
Focus:
- What the **player** can **influence**
- What the system **communicates back**
- What **other systems** does it meaningfully **affect** or **depend on**
- Does it amplify, constrain, destabilize, or support other systems
- Are its **outputs** another system’s **inputs**

##### E. Legibility / Communication
How reliably the player can perceive, interpret, and form expectations about the system?
Focus:
- What **information** is visible, hidden, delayed, or ambiguous
- Are cause, effect, and responses are **readable**
- Are **outcomes** are **bounded** and usable
- Is **variability** remains **interpretable**
- Can players form **reliable expectations**
- Is the system **consistent** with its apparent rules

##### F. Friction / Breakdown _(if relevant)_
Where does the system break down or work against itself?

>Friction may be intentional and supportive of the intended experience.

Focus:
- confusion
- Degenerate incentives
- Excessive burden
- Weak feedback
- Unreadable randomness
- Avoidable repetition
- Edge-case failure
- Contradiction between stated purpose and actual effect


---
# 4 Play Structures _(if applicable; selective)_
***Analyze how play is organized over time. Do not infer.***

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

>Not all games support repeated play; in rare case some games are very linear, not even small puzzle loops. 

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


---

# 5. Independent Interpretation and Evaluation *(System/Project)*
***Transform analysis & descriptions into judgments.***

>A system need **NOT** to produce uniform outcomes (consistency). It may be variable, probabilistic, or partially autonomous. What matters is that the system operates ***reliably according to its design logic*** and meaningfully contributes to the project’s play, structure, or experience.

>Design intention should be treated as a structured inference from the artifact, its systems, and available external evidence; **NOT** as something that can always be known with certainty.
> 
> When discussing intention, distinguish clearly between:
> 	- Developer-Intention: 
> 		explicit developer-stated intention
> 	- Discussion Interpretated: 
> 		strongly supported inference from design evidence
> 	- Community Interpretated: 
> 		people thought what it was for


## 5.1 Project Identity / System Role
What kind of experience is this project primarily trying to produce?
OR
What role is this system fulfilling?

## 5.2 Target Evaluation (if applicable, Project)
***Reveals intended audience fit; potentially effectiveness.***
Identify the intended target audience and the elements likely meant to appeal to them.

Base this on observable design evidence such as:
- pacing
- complexity
- failure severity
- theme / fantasy framing
- control demand
- social structure
- progression design

Ask:
- who is this project primarily for
- what design elements appear aimed at that audience
- how well does the project serve them
- if relevant, how successful was it relative to earlier entries or competitors
- 
## 5.3 Design Alignment
Do the project’s systems, rewards, constraints, and pressures support that identity/role coherently?

## 5.4 Communication
Does the project’s systems signal state, event, condition, feedbackand relevant information that players would feel sufficient?

## 5.5 Distinctive Strengths
What works especially well, and why?

## 5.6 Design Risks / Weaknesses
What limits, distorts, weakens, or confuses the intended experience?

## 5.7 Constraint Evaluation _(optional)_
***Reveals the value of exclusion.***
Identify what the project intentionally restricts, simplifies, automates, abstracts, or refuses to simulate.

>Design quality is often defined as much by exclusion and restraint as by feature presence.

>Unlike designing prototyping, it is virtually impossible to infer original design constraints while analysing the system structures externally; constraints can only be partially inferred after realising the entire structure. 

Focus:
- what the player cannot do
- what is intentionally abstracted away
- what complexity is reduced or hidden
- what is omitted for readability, pacing, or identity

Ask:
- What has been excluded or compressed?
- Why might these exclusions exist?
- Do these constraints strengthen the intended experience?

## 5.8 Overall Effectiveness
Does the System/Project successfully achieve its likely design intentions?


---
# 6 Evaluative Comparison
***Comparison clarifies the project’s position.***

## 6.1 Horizontal Comparison _(if applicable, System / Project)_
***Reveals comparative distinctiveness.***
Compare the project with other projects that use similar components or pursue similar goals.

Focus:
- distinctive design choices
- meaningful strengths or weaknesses
- comparative legibility
- comparative complexity
- likely reasons for stronger or weaker reception

## 6.2 Backward Comparison _(if applicable, System / Project)_
***Show design shifts.***
Compare the project with earlier entries in the same series, lineage, or design tradition.

Focus:
- What changed
- What improved or regressed
- What design values appear to have shifted
- How those changes may affect player response


## 6.4 Orthogonal Comparison _(optional)_
**Reveals cross-audience appeal; possible extensibility.***
Identify whether the project also strongly appeals to players associated with a meaningfully different design space.

Ask:
- where does another audience segment significantly overlaps
- why might that overlap exist
- does it strengthen or weaken the project’s identity


---
## 7 Outcome Summary

Base one System or Project analysis, May Contain:
- **Project Identity:** What kind of experience is this trying to produce
- **Central Systems:** Which systems most strongly define that identity
- **Design Strengths:** What is working especially well
- **Design Risks / Weaknesses:** What limits, distorts, or weakens the project
- **Overall Judgment:** Does the project successfully achieve its likely design intentions


---
**Reference**: 

Game Mechanics & Systems Thinking
https://www.youtube.com/watch?v=nkLmjJK3vOw&list=PLyTIzr2AVP3_0zeFw9-9tjQNcV2aCnggd&index=3&t=408s