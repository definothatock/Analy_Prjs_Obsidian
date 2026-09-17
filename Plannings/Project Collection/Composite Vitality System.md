Unreal component plugin.

Mechanic Intent

Goal:  
A Stamina/Vitality system that is dynamically capped by status effects.

Player-Facing Effect:  
The player can use their Stamina up to their current Stamina cap;  
The player should be able to roughly estimate their condition from this Stamina meter.

Success Condition:  
Named status (later defined as enum, or assets or external csv, as dynamic as possible) can dynamically affect (cap) the meter.  
A player can use as much Stamina as their dynamic maximum.  
At least one delegate that announces depletion of the meter (specifically: cap reached 0; available stamina used up to 0 is another event)  
Must support multiplayer with server authorisation.

Functional Definition

Core Behaviour:  
It works mainly as the stamina system, and partially as health.  
When the player has taken permanent (eg damage) or temporary (eg poison) negative effects, their meter cap is reduced. Stamina can regenerate up to the meter cap.  
Positive effects may remove negative effects or temporarily increase the meter cap.  
All active effects must be named and stored. This helps later reflect the player's situation visually (which effects and by how much), and allows specific removal/addition of existing effects.

Inputs at least:  
cap reduction amount and responsible effect, optionally active-time/reduction-over-time

Outputs:  
api to fetch meter and status data

State Model

Stateful:  
Some effects reduce over time, or have an active timer, etc.

Reset / Persistence:  
Persistence even when the player has fainted. Reset only for definitive cases, such as concluded-death in the round (possible external requests, eg "last breathe timer").

Rules

at least:  
Curtain player action demands stamina. Use stamina in bulk or gradually at a rate.  
Should let the external system know stamina depletion so the other system can block certain actions.  
Stamina regenerates only in allowed conditions. The external system should be able to inform when it is allowed.  
In a specific situation, Stamina can be locked and will not be consumed (does not directly contradict regeneration)  
Stamina regeneration rate is usually standardised, but external systems might want to change it temporarily.  
The player faints once the meter cap is reduced to 0. Announce it and allow the other system to handle it.  
The player regains consciousness once the cap is above 0. Announce it and allow the other system to handle it.  
Meter cap can go below 0. This does not directly affect concluded-death, but it may make regaining consciousness harder (further from 0).

The same type (name) of effect stacks instead of having a new Id; but if they are "ramp effect", they apply their counts with their respective rate (e.g. 1 per 3s, and 3 per 1s).  
Some effects are removed with a ramp after a duration. Whether the effect was taken with the ramp or not does not matter; this is considered by the effect config.

Activation:  
External requests when the player has not concluded death

Failure:  
do nothing when an activation attempt is invalid.

Boundaries

Not Doing:  
fine-calculation of available meter, i.e., having floats as the final number (data type being float is ok for safety). This should be either handled during input or before output.  
Currently, the meter state is not intended to persist between levels, only the duration of the round.

External Dependencies  
Should not hard depends on anything, So that any actor can use it (even though mostly likely only the player would be using this system)

Notice:  
This system should not care what external systems are going to do with the information. Thus:  
parameter or function names should be generalised or stick to their purpose.