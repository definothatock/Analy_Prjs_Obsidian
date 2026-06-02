## Purpose

This standard defines a compact way to describe an **individual mechanic** so another person can quickly understand:

- what it is for
- what it does
- what it must not do
- what state it needs
- what functions / interfaces it likely needs
- what minimum prototype is enough to validate it

Use this for **mechanic-sized tasks**.


---
# 0. Scope

## 0.1 Unit
Identify the mechanic being described.

Examples:
- dash
- lock-on targeting
- timed parry
- card draw

> One descriptor should cover **one mechanic**.  
> If the thing is too large, split it into separate descriptors.

## 0.2 Descriptor Intent

State what this document is for:
- concept framing
- prototype planning
- implementation handoff
- API/function planning
- test planning


---
# 1. Mechanic Intent

## 1.1 Goal
What problem does this mechanic solve, or what role does it serve?

Examples:
- let player reposition quickly
- create timing-based defense decision
- regulate powerful actions through limited resource
- surface enemy awareness in a predictable way

## 1.2 Player-Facing Effect
If it is facing or adjacent to player, what should the player feel, notice, or be able to do because of it?

Examples:
- “I can escape danger at short notice.”
- “I trade stamina for safety or offense.”

## 1.3 Success Condition
How do we know the mechanic is doing its job?

Examples:
- used regularly in intended situations
- produces meaningful tradeoff
- readable cause/effect
- easy to prototype and tune


---
# 2. Functional Definition

## 2.1 Functional Verbs
List the core verbs this mechanic enables or regulates.

Examples:
- spend
- block
- detect
- pull
- reveal
- recharge

## 2.2 Core Behavior
Describe the mechanic in 2–5 bullets.

Focus on:
- trigger
- main process
- immediate result
- important limitation

## 2.3 Inputs / Outputs
Define what goes in and what comes out.

### Inputs
Examples:
- player input
- collision event
- timer completion
- resource value
- target state

### Outputs
Examples:
- state change
- animation trigger
- damage prevented
- movement impulse
- UI update
- event emission


---
# 3. State Model

## 3.1 Stateful or Stateless
Declare clearly:
- **Stateless**: result depends only on current input/context
- **Stateful**: mechanic stores or updates internal state over time

## 3.2 Owned State
If stateful, list only the state this mechanic owns or directly controls.

Examples:
- current stamina
- cooldown timer
- active target
- charge amount
- suspicion level
- combo step

## 3.3 Reset / Persistence
State when this mechanic’s state:
- initializes
- resets
- persists
- expires

Examples:
- resets on death
- persists during encounter only
- cleared on scene unload
- reinitialized on spawn

---

# 4. Core Functions
Describe the minimum functional pieces needed to build it.

For each function, give:
- **Name**
- **Purpose**
- **Inputs**
- **Outputs**
- **Notes** if needed

Keep this practical, not overdesigned.

Example format:
- `CanActivate()`
    - checks whether use is allowed
- `Activate()`
    - starts mechanic effect
- `ApplyEffect()`
    - performs main state/result change
- `Tick()` / `Update()`
    - advances timed behavior if needed
- `Cancel()` / `End()`
    - stops or clears effect
- `GetFeedbackState()`
    - exposes UI/readability info

> Do not force a fixed API shape.  
> Only describe the functions actually needed.


---
# 5. Rules and Constraints

>Some of these are done on the gameplay programming, rather than mechanic programming. Still, it require enough context to know what APIs will be needed.

## 5.1 Activation Rules
What must be true for this mechanic to occur?

Examples:
- enough stamina
- valid target exists
- player grounded
- cooldown finished
- not stunned

## 5.2 Core Constraints
What limits it?

Examples:
- range
- duration
- cooldown
- resource cost
- line of sight
- stack cap
- target cap

## 5.3 Failure / Rejection Cases
What should happen when activation is attempted but invalid?

Examples:
- do nothing
- fail silently
- play denied feedback
- queue action
- consume no resource


---
# 6. Boundaries

## 6.1 Not Doing
Explicitly state what this mechanic does **not** handle.

Examples:
- does not choose targets automatically
- does not manage animation blending
- does not persist across save/load yet
- does not handle network sync
- does not resolve damage formula
- does not perform pathfinding

## 6.2 External Dependencies
What does this mechanic rely on from elsewhere?

Examples:
- movement controller
- combat state
- resource component
- animation event system
- UI feedback layer
- timer service


---
# 7. Minimum Build Requirement
Define the smallest useful version that proves the concept.

## 7.1 Minimum Prototype
What is the lowest-effort prototype acceptable for testing the mechanic?

Examples:
- greybox only
- debug input + text feedback
- placeholder values
- no polish, just functional behavior
- single test map
- fake target objects

## 7.2 Test Depot / Sandbox
What setup is enough to test it?

Examples:
- one room with 3 enemy dummies
- stamina debug UI
- toggleable cooldown display
- scripted repeated trigger case
- edge-case test buttons

## 7.3 Must-Prove Checks
What must this prototype prove?

Examples:
- mechanic can activate reliably
- core tradeoff is noticeable
- state updates correctly
- feedback is readable enough
- failure cases behave consistently


---
# 8. Optional Decision Notes

## 8.1 Why Not Existing Solution
Examples:
- existing movement ability is too broad
- current status system cannot express timed ownership cleanly
- reused solution creates wrong coupling
- custom version is simpler for tuning

## 8.2 Extra Goods
Nice-to-have additions, not part of minimum scope.

Examples:
- telemetry hooks
- editor visualization
- tuning data table

