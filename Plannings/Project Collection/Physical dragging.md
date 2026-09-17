Intent

Goal:  
Allow players to drag and pull physical objects, with limited strength.

What player should think:  
"I can drag and lift this easily, but maybe not so with this heavy thing"

Success Condition  
The player can drag a physical object depending on the strength of self and the mass of the target.

Functional Definition

Functional Verbs  
drag, pull

Core Behaviour  
player attempts to drag the object. If allowed, a force will try to push the target into the desired point.  
The force is exerted on the initial contact point, not the entirety of the object. (think of lifting a corner of a thing)  
The dragging force is related to the player's strength, the target's mass, and the distance from the desired point; the target may not stay in the desired point if the player drags too hard / target is too heavy / obstruct by environment.  
The "dragging" will be deactivated once it exceeds a distance limitation.

Inputs  
player requestion from gameplay layer  
desired point (centre of the player's screen, with the original player distance from the contact point)  
player strength  
(target mass, can leave it to the physics system)

Outputs  
force that pushes the target

State Model  
likely to be stateful. may need to cache important data.  
Dragging <-> Undrag  
Undrag on: exceeded limit or player demand

Boundaries

Not doing  
This is not the same as "pick up". Pick up is a different request, more specific for items (eg putting it into inventory / using items). There is another system handling that.

Dependencies  
Depends. It could be embedded inside the player or as a component that has no dependency.