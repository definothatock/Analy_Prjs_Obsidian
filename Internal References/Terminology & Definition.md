## Purpose

**This document explicit define terms that are vague, misused, or non-deterministic. Well-defined and specific technical terms will not be defined here and will be used as per.**


---
# Structural Terms
Related to understanding the **project as a designed play artifact**.

| *TERM*          | *DEFINITION*                                                                                                                                                          |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Project         | The designed artifact being analyzed as a product or structured whole; includes its systems, rules, content, supporting framework.                                    |
| Game            | The instantiated activity of play as it is being played. The running play-state or ongoing session.                                                                   |
| Play            | The activity of interacting with the game through decision, action, response, interpretation, and adaptation.                                                         |
| Component       | A discrete design element or unit within the project.                                                                                                                 |
| Mechanic        | A rule-bound interaction structure available in play; define how, e.g. actions, inputs, or conditions, produce permitted outcomes.                                    |
| System          | A set of interacting mechanics, rules, resources, states, and components that together produce recurring behaviors, pressures, or possibilities.                      |
| Dynamics        | Emergent or recurring play patterns that arise when mechanics and systems operate during actual play. <br>Examples: action/strategic tendencies, behavioral outcomes. |
| Player Verbs    | Actions initiated by the player.<br>Examples: hide, craft, hit.                                                                                                       |
| Game Verbs      | Actions initiated by the game or game-controlled agents.<br>Examples: hunt, spawn, lift.                                                                              |
| Resources       | Tracked values, assets, or capacities that meaningfully affect decision, planning, or action.<br>Examples: health, space, currency.                                   |
| Rules           | Explicit or implicit logic that governs states, permissions, interactions, constraints, and outcomes.                                                                 |
| State           | A defined condition or data configuration the game can recognize, manage, or transition between.                                                                      |
| Loop            | A recurring sequence of actions, decisions, and outcomes that structures repeated play.                                                                               |
| Characteristics | Holistic experiential qualities or design character produced by the project in play. Examples: tense, oppressive, Chaotic.                                            |

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
# Implementation Terms
Related to building the Project.

| *TERM*    | *DEFINITION*                                                                                                         |
| --------- | -------------------------------------------------------------------------------------------------------------------- |
| Framework | The underlying technical or organizational structure used to build, support, and connect project systems or content. |
| State     | A defined condition and associated data set that the game can store, evaluate, and transition from.                  |
