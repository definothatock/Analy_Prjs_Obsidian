
## Purpose

This document defines a standard structure for discussion a game/project’s design, systems, and intended player experience. Intended discussion depth is to understand the design on conceptual level, but not exact implementation level. If the **project as a whole** is too large to analyse or discuss meaningfully, selectively analyse the **most significant system(s)** instead.

This standard is **modular**. Not every section applies equally to every unit of analysis:
- Full-Project / Mode analysis should emphasize framing, play structure, progression, audience fit, and overall alignment.  
- System / Subsystem / Loop analysis should emphasize function, structure, interactions, legibility, and role within the wider project.

>**IMPORTANT:**
>1. It is expected that you have already read about [[Terminology & Definition]] and are aware of specific meanings.
>2. It is expected that you have already read about [[Attribute Reference Table]] and are aware of labels and their limitations.


---
# 0. Scope and Framing
***Before discussion, define the scope of analysis.***

## 0.1 Unit of Analysis

Identify what is being analysed:
- the full Project
- a Mode
- a System
- a Subsystem
- a recurring Loop

Then select the sections necessary for that analysis:
- **Project / Mode** analysis should emphasize framing, play structure, audience fit, and overall alignment.
- **System / Subsystem / Loop** analysis should emphasize function, structure, interactions, legibility, and role within the wider project

>The chosen unit should be large enough to support meaningful discussion of rules, resources, player behavior, and outcomes. 
>
>If a project is too broad, analyse the most identity-defining system, subsystem, mode, or loop instead.
>
>Mechanics-Focused Discussion belongs to [[Analytical Discussion Standard on Implementations]].

## 0.2 Analytical Priority

Clarify the focus of the discussion:
- structural understanding
- experiential understanding
- design intention
- comparative evaluation

## 0.3 Evidence Basis

When possible, distinguish:
- directly observed play behavior
- explicit rules or formal structures
- inferred design intention
- community-facing labels or expectations

>**IMPORTANT:**
>Move from observation to evaluation in order:  
>**observe → identify component → analyse structure / behavior → support inference → Interpret Intent → evaluate**.  
>It is assumed you understood the definition of the above wordings.
>
>Do not treat inferred intention as directly observed fact.


---
# 1. Core Components
***Identify the significant components in the chosen unit of analysis before interpretation.

## 1.1 Core Mechanics
Unit of Rule-bound interaction structure.

>Reference Labels are only shorthand for **already recognized design patterns**. They are NOT a substitute for analysis.
>
>For whatever reason that recognized labels cannot be used, such as no existing similar design patterns, create a separate appropriate framing. 

At minimum, identify:
- **Actor Relation Structure**
- **Core Mechanics ([labels]([[Attribute Reference Table]]) or specify)**

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
Identify **recurring actions**, events, or pressures applied by the game or game-controlled agents that the player must respond or adapt.

Examples:
- Pursue
- Spawn
- Reveal

## 1.5 Core Rules *(optional)*
Identify the underlying **logic** that **governs** state change, interaction, permission, limitation, and consequence.

>Rules in video games are often hidden from outside view. 
>For analysis, rules are only important when certain mechanics or framework is explicitly defined from rules.

Typical rule forms:
- A **is** B
- **If** Q, then R
- **When** X occurs, Y changes
- Z **may / may not** do Y, Depending on X


---
# 2. Gameplay Framework *(project)*
_**Identify the recurring structure of play surrounding the chosen unit of analysis, where applicable.**_

>For full-project or mode analysis, this section is usually central.  
>
>For system-focused analysis, include only the framework elements necessary to explain how the system is encountered, pressured, and repeated in play.

## 2.1 Play Objective / Success State
Identify What the **player** is broadly trying to **achieve**.

This may include:
- formal win conditions
- local objectives
- self-directed goals
- long-term progression aims

## 2.2 Failure Pressure
Identify what **threatens** progress, stability, efficiency, or success.

Possible forms include:
- death
- attrition
- time pressure
- positional collapse
- opportunity loss

## 2.3 Core Loop
Identify what **recurring sequence** most strongly structures play.

Describe, where possible:
- player input / commitment
- system response
- reward / feedback
- reset / continuation
- repetition or escalation

## 2.4 Progression Structure _(if applicable)_
Identify how does play develop over time.

>For some game the Loop is the main, or only Progression.

Possible forms:
- level progression
- unlock progression
- run-based escalation
- economic accumulation
- skill mastery
- narrative advancement


---
# 3 System Analysis
_**Analyse the system’s observable behavior, structure, and functional relations. Do NOT interpret intention or evaluate here.**_

>analyse a system in detail only if it materially shapes player behavior, decision structure, pacing, readability, or project identity.

### 3.1 Identify the Central and Distinctive System(s)
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


### 3.3 Analysing and Inferring
For each selected system, analyse its observable structure, behavior, and functional role before interpretation.
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

##### C. Functional Role *(if applicable)*
What role does this system appear to perform within the project structure, based on observable behavior?

>If there is no apparent inferable design Purpose/Role, skip; Do **not** move into evaluation of deeper intention here, it is reserved for Section 5.

Focus:
- what **recurring function** it serves in play
- what pressures, decisions, or states it helps **organize**
- what other systems it supports, gates, or **regulates**

##### D. Interactions
How does this system relate to players and other systems?
Focus:
- What the **player** can **influence**
- What the system **communicates back**
- What **other systems** does it meaningfully **affect** or **depend on**
- Does it amplify, constrain, destabilize, or support other systems
- Are its **outputs** another system’s **inputs**

##### E. Legibility / Information Structure
How reliably the player can perceive, interpret, and form expectations about the system?
Focus:
- What **information** is visible, hidden, delayed, or ambiguous
- Are cause, effect, and system responses **readable**
- Can the player **learn** the system **organically**
- Are outcomes **bounded** enough to be **usable**
- Does **variability** remain **interpretable**
- Can players form **reliable expectations**
- Is the system **consistent** with its apparent rules

##### F. Friction / Breakdown _(if relevant)_
Where does the system break down or work against itself?

> Friction is not automatically a flaw; it may be deliberately used to create tension, uncertainty, burden, or thematic weight.

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
# 4 Play Structures Analysis _(if applicable; selective)_
***Analyse how play is organized over time based on observable structure and repeated patterns. Do NOT interpret intention or evaluate here.***

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
# 5. Interpretation and Evaluation *(System/Project)*
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

**If analysing a Project or Mode:**  
Interpret what kind of characteristic/experience this project primarily appears to pursue, and evaluate whether it achieves that successfully.

Ask:
- What kind of experience does the project primarily appear to pursue?
- Which systems most strongly define that identity?
- Is that identity coherent or split across competing priorities?

**If analysing a System, Subsystem, or Loop:**  
Interpret what role this unit serves within the larger project, and evaluate how effectively it fulfills that role.

Ask:
- What role does this unit serve in the larger project?
- Is it central, supporting, gating, pacing, expressive, or stabilizing?
- Does it effectively fulfill that role?

## 5.2 Target Evaluation *(if applicable, Project)*
***Reveals intended audience fit.***
Identify the intended target audience, Interpret the elements likely meant to appeal to them, evaluate is it effective.

Base this on Identifiable design evidence such as:
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

## 5.3 Design Alignment
Evaluate whether the project’s systems, rewards, constraints, and pressures support that identity/role **coherently**.
Ask:
- Do the project’s rewards, constraints, pressures, and feedback support the same intended play style?
- Do any systems pull player behavior away from the apparent intended experience?
- Is there tension between formal goals and effective incentives?
- What behaviors does the system actually incentivize, regardless of its stated or apparent purpose?

## 5.4 Communication Effectiveness
Evaluate whether the project's systems **communicate** the necessary information about the state, events, conditions and feedback in a way that **players** will find **sufficient**.
Ask:
- Does the player receive enough information to make informed decisions?
- Are state changes, threats, opportunities, and consequences communicated clearly enough?
- Where does ambiguity support play, and where does it become noise?

## 5.5 Distinctive Strengths
Evaluate what works especially well, and why. Purely case by case.

## 5.6 Design Risks / Weaknesses
Evaluate what limits, distorts, weakens, or confuses the intended experience.
Common pitfalls:
- Does the system encourage player behavior that is effective but narrower, duller, or contrary to the project’s apparent intended experience?

## 5.7 Constraint _(optional)_
***Reveals the value of exclusion.***
Infer what the project intentionally restricts, simplifies, automates, abstracts, or refuses to simulate, then Interpret the reason.

>Unlike designing prototyping, it is virtually impossible to infer original design constraints while analysing the system structures externally; constraints can only be partially inferred after realising the entire structure. 

Focus:
- what the player cannot do
- what is intentionally abstracted away
- what complexity is reduced or hidden
- what is omitted for readability, pacing, or identity

>Design quality is often defined as much by exclusion and restraint as by feature presence.

Ask:
- What has been excluded or compressed?
- Why might these exclusions exist?
- Do these constraints strengthen the intended experience?

## 5.8 Overall Effectiveness
Evaluate whether the System/Project successfully achieve its likely design intentions.
Possible Questions:
- Does the project or system reliably achieve its likely design aims?
- Under what conditions does it work best?
- What most limits that effectiveness?


---
# 6 Evaluative Comparison *(Optional)*
***Comparison clarifies the project’s position.***

## 6.1 Horizontal Comparison
***Reveals comparative distinctiveness.***
Identify similar systems or pursue similar design goals, then evaluate the differences.

Focus:
- distinctive design choices
- meaningful strengths or weaknesses
- comparative legibility
- comparative complexity
- likely reasons for stronger or weaker reception

## 6.2 Backward Comparison
***Show design shifts.***
Compare the project with earlier entries in the same series, lineage, or design tradition, then evalute improvement or principle shifts.

Focus:
- What changed
- What improved or regressed
- What design values appear to have shifted
- How those changes may affect player response


## 6.4 Orthogonal Comparison
**Reveals cross-audience appeal.***
Identify whether the project also strongly appeals to players associated with a meaningfully different design space, then evaluate is there any significant extensibility.

Ask:
- where does another audience segment significantly overlaps
- why might that overlap exist
- does it strengthen or weaken the project’s identity


---
## 7 Outcome Summary

Base one System or Project analysis, may Contain:
- **Project Identity:** What kind of experience is this trying to produce
- **Central Systems:** Which systems most strongly define that identity
- **Design Strengths:** What is working especially well
- **Design Risks / Weaknesses:** What limits, distorts, or weakens the project
- **Overall Judgment:** Does the project successfully achieve its likely design intentions


---
**Reference**: 

Game Mechanics & Systems Thinking
https://www.youtube.com/watch?v=nkLmjJK3vOw&list=PLyTIzr2AVP3_0zeFw9-9tjQNcV2aCnggd&index=3&t=408s