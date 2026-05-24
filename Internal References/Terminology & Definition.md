## Purpose

**This document explicitly defines terms that are often casual, vague, misused, or non-deterministic. Well-established technical terms are used in their conventional sense unless otherwise specified.**


---
# Structural Terms
Related to understanding the **project as a designed play artifact**.

| *TERM*             | *DEFINITION*                                                                                                                                                                                             |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Project            | The designed artifact being analyzed as a product or structured whole; includes its systems, rules, content, supporting framework.                                                                       |
| Game               | The instantiated activity of play as it is being played. The running play-state or ongoing session.                                                                                                      |
| Play               | The activity of interacting with the game through decision, action, response, interpretation, and adaptation.                                                                                            |
| Component          | A discrete design element within the project, typically treated as a manipulable part of a larger system or structure.                                                                                   |
| Mechanic           | A rule-bound interaction structure available in play; it defines how actions, inputs, or conditions produce permitted outcomes.                                                                          |
| System             | A set of interacting mechanics, rules, resources, states, and components that together produce recurring behaviors, pressures, or possibilities.                                                         |
| Dynamics           | Recurring or emergent patterns of play behavior, pressure, and response that arise when mechanics and systems operate during actual play.<br>Examples: action/strategic tendencies, behavioral outcomes. |
| Player Verbs       | Actions initiated by the player.<br>Examples: hide, craft, hit.                                                                                                                                          |
| Game Verbs         | Actions initiated by the game or game-controlled agents.<br>Examples: hunt, spawn, lift.                                                                                                                 |
| Resources          | Tracked values, assets, or capacities that meaningfully affect decision, planning, or action.<br>Examples: health, space, currency.                                                                      |
| Rules              | Explicit or implicit logic that governs states, permissions, interactions, constraints, and outcomes.                                                                                                    |
| State (Structural) | A meaningful gameplay condition recognized by the rules or systems, such that different conditions permit, restrict, or alter actions, outcomes, or pressures.                                           |
| Loop               | A recurring sequence of actions, decisions, and outcomes that structures repeated play.                                                                                                                  |
| Characteristics    | The resulting holistic experiential qualities or overall design feel. <br>Examples: tense, oppressive, Chaotic.                                                                                          |

## Relationship Mapping:

	Project
		├─ Components
		├─ Rules
		├─ Resources
		└─ Mechanics
			│
			├─ Rules (internal)
			├─ Player Verbs
			└─ Game Verbs


	Rules + Mechanics + Resources + Components
						↓
					 Systems
						↓
			  Game (instantiated play)
						↓
					 Dynamics
						↓
				 Characteristics


---

# Design Terms
**Concepts** for designing, planning, prototyping the Project.

| *TERM*         | *DEFINITION*                                                                                                                                    |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Decision Space | The range of meaningfully distinct choices available to the player at a given point, shaped by rules, resources, information, and consequences. |
| Agency         | the degree to which player decisions can meaningfully influence outcomes within the game’s rule structure.                                      |


---
# Implementation Terms
Related to **building** the Project.

| *TERM*                 | *DEFINITION*                                                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Framework              | The underlying technical or organizational structure used to build, support, and connect project systems or content.           |
| State (Implementation) | The stored or computed data condition used by the built system to represent, track, or evaluate gameplay-relevant information. |
