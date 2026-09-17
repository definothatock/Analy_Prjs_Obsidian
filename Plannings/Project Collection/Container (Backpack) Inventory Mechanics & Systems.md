## Quick Design Brief

**What is being designed:**  
A replicated, modular storage system where item storage is owned by **containers** (especially wearable/drop-able backpacks), not permanently owned by the player. The player interacts with storage via mechanics such as Pickup and Transfer.

**Experience it should create:**  
The player should understand:

> “My carrying capacity comes from the backpack/container I currently use, not from the character itself.”

**Main player actions:**

- pick up items (into Hand)
- move items into Toolbelt or Backpack
- equip / unequip backpack
- drop backpack
- recover backpack later
- optionally use Toolbelt for fast access

**Main design difference from previous project:**  
The previous tutorial-style inventory (Stephen Ulibarri) was player-bound and over-scoped. This project uses a smaller modular model where **storage is a property of container actors/components**.

**Core principle:**  
The player does not “have an inventory.”  
The player has **access to storage containers**.
(Exception: Toolbelt is a small, intentional player-side quick-access storage.)

---

# 0. Scope and Design Framing

## 0.1 Unit of Design

Primary unit:
- **Container / Backpack Inventory System**

Possible related but separate units:
- Toolbelt System
- Item Pickup System
- Equipment / Wearable Container System
- Container UI System
- Item Definition / Item Instance System

Focus for this plan: **container-based storage structure.****

## 0.2 Design Goal
Create a simple, professional, modular container inventory model with stable replication, without MMO-level complexity.

The container system should:
- support fundamental replication
- avoid permanent player-bound inventory as the primary storage
- support backpacks as physical world actors
- allow backpacks to be equipped/unequipped/dropped and later looted/recovered
- keep item storage modular and reusable
- support simple pickup + transfer flows
- remain expandable later without early overdesign


## 0.3 Design Constraints

### Intended Simplicity
This system initially **NOT** supported:
- complex item grids
- item rotation
- nested containers inside containers
- equipment stat systems
- crafting
- weight simulation
- save/load complexity

### Desired Architecture Constraint
Storage should not be hardcoded into the player.

```text
Player
 └── can access/equip containers

Backpack Actor
 └── owns Storage Component

Chest Actor
 └── owns Storage Component
```


---

# 1. Intended Experience

## 1.1 Target Experience
- physicality
- modularity
- light survival / looting feel
- meaningful container ownership

Containers should feel like real world objects, not abstract UI-only storage.

## 1.2 Player Motivation
The player engages with storage because it lets them:
- carry more items
- organize collected resources
- decide what to keep or abandon
- recover dropped equipment
- change loadout by changing backpack/container
- Share loads among the players

## 1.3 Desired Player Behaviors
The design should encourage the player to:
- value their backpack as an important object
- understand where items are stored
- make decisions about what to carry
- drop or swap bags intentionally
- use Toolbelt as a limited quick-storage
- allow other players to access a backpack worn by another player

## 1.4 Anti-Goals
Avoid:
- making the player inventory a hidden container
- unclear item ownership
- duplicating items between backpack and Toolbelt
- coupling backpack logic directly to player character
- MMO-level architecture before needed

---

# 2. Core Design Frame

## 2.1 System Purpose
The Container Inventory System exists to answer:

> Where are items stored, and how does the player access them?

Its role is to provide modular item storage through container actors/components.

The player character should only handle:
- interaction
- equipping containers
- requesting item actions

>Item definition data (data table/csv/tags & Guid/etc.) is separate; the container system remains semi-operational without final data pipeline.

## 2.2 Success Contribution
The system helps gameplay by:
- limiting what the player can carry
- giving value to containers
- allowing dropped backpacks to preserve their contents
- supporting looting and recovery
- making inventory expandable through types or configs (preferred)

## 2.3 Design Pillars

### Pillar 1: Storage Belongs to Containers
Containers own storage state.

### Pillar 2: Player Access Is a Reference, Not Ownership
```text
Player -> interacted Backpack -> Storage Component -> Item Slots
```


### Pillar 3: Independent item states

These states are distinct:
- item “on hand”
- item in toolbelt
- item in backpack


### Pillar 4: Simple First, Expand Later
Start with fixed slots or simple list storage.  


---

# 3. Core Mechanics

## 3.1 Storage Mechanic

### Goal
Allow actors to store, remove, and transfer items using reusable container logic.

### Functional Verbs
add, remove, move, swap, query, transfer, reject, notify

### Core Behavior
- A storage component owns a list of slots.
- Slot is empty or contains one stored item entry (prototype form).
- Add succeeds if there’s space per capacity rules.
- Storage emits update events when its contents change.
- UI reads storage state but does not own the state.

### Inputs
- item stack
- source slot
- destination slot
- quantity (if stacks)
- capacity rules

### Outputs
- item accepted
- item rejected
- transferred quantity (if stacks)
- slot changed
- UI update event
- pickup destroyed or partially reduced

### 3.1.1 Variant: Toolbelt
- A limited, easy-access storage.
- Mechanically similar to Storage Mechanic, but **player-owned**.
- Intended purpose is quick access, not main capacity.

### 3.1.2 Variant: Hand
- Hand is a **player-owned**, always-available single slot representing the **“on hand” state**.
- Hand is the **default landing state** for pickups: 
	the pickup interaction results in the item becoming “on hand” **before** it is transferred into Toolbelt or Backpack storage.
- Hand is for **holding/using/selecting** an item.
	it does **not** automatically mean the item is stored in Toolbelt/Backpack.
- Hand capacity is **only one slot** (occupied vs available).

**Core behavior (Hand):**
- If Hand is empty, pickup can succeed into Hand.
- If Hand is occupied, pickup is rejected with “Hand Occupied” feedback.
- From Hand, the player may transfer the item into Toolbelt or container storage through the same “request storage action” flow.


## 3.2 Backpack Equip Mechanic

### Goal
Provide mobile storage through a wearable container actor.

### Functional Verbs
equip, unequip, drop, access, preserve

### Core Behavior
- Backpack exists as a world actor owning its storage.
- Player can equip the backpack if allowed.
- Equipped backpack becomes attached (visual/logical).
- Dropping the backpack detaches/spawns it in the world with contents preserved.
- If player has no backpack, pickup still works into Hand.

### Inputs
- backpack actor reference
- player equip request
- attachment socket
- current equipped backpack state

### Outputs
- equipped backpack reference changed
- backpack hidden/attached/removed from world interaction
- active storage changed
- UI refresh
- dropped backpack actor with same storage contents


## 3.3 Item Pickup Mechanic

### Goal
Pick up an item into Hand, then optionally transfer it into accessible storage.

### Functional Verbs
detect, collect, add, reject, destroy

### Core Behavior
- Player interacts with pickup actor.
- Pickup requires Hand available.
- Item becomes “on hand”.
- Player may transfer “on hand” item into Toolbelt/Backpack storage.
- Transfer only destroys/reduces pickup once storage confirms acceptance.
- Rejection produces feedback.

### Failure Cases
- hand occupied
- storage full
- item type not allowed
- pickup already consumed
- storage unavailable

---

# 4. Core Components
These are the suggested elements that might helps building the system and fulfilling the Design Goal.
## 4.1 Example High-Level Structure

```text
APlayerCharacter
 ├── Hand Slot
 │    └── hold/use/transfer items
 │
 ├── Toolbelt Component
 │    └── quick-access storage
 │
 ├── Backpack Access Component
 │    └── equipped backpack reference
 │
 └── Interaction Component(s)
      └── Interacts with pickups, backpacks, containers


AContainerActor
 └── UStorageComponent
 
 ABackpackActor : AContainerActor
 ├── UStorageComponent
 └── Backpack Data


AItemActor
 ├── Item Instance / Stack Data
 └── World pickup representation
```

Note:
- Hand slot
	“on hand” is for using/choosing the currently held item; it is not automatically in Toolbelt/Backpack.

- Toolbelt System
	small player-side quick storage; can share the same storage logic with container storage (or derived variant) if needed.

- Item Actor
	Previously, in Stephen’s example, the world representation and hotbar representation are entirely separated (unrelated object/actor on structual sense). In this project, whether world pickup and "on hand" pickup should strongly decoupled is undecided; prototype can be simpler.


## 4.2 Main Actor / Component Responsibilities

### `APlayerCharacter`
Does not own the primary inventory. Requests storage actions.

Owns/tracks:
- equipped backpack reference (via access component)
- interaction ability
- optional currently opened container reference


### `UBackpackAccessComponent`
Purpose:
- track equipped backpack
- expose active storage to UI
- handle equip/unequip/drop
- hide backpack details from other systems

Suggested functions:
```text
GetEquippedBackpack()
GetActiveStorage()
EquipBackpack(ABackpackActor* Backpack)
UnequipBackpack()
HasBackpack()
```

### `AContainerActor`
This is the physical item in the world that can hold items.

Purpose:
- exists in the world
- preserves contents
- owns a storage component


### `ABackpackActor`
Wearable container variant, where it is more centered towards player.

Additional Purpose:
- can be picked up/equipped, handles equip/drop state changes.


### `UStorageComponent`
This is the core reusable storage logic.

Purpose:
- store item stacks / item instances
- enforce capacity
- support add/remove/move/swap
- emit updates for UI

Possible owned state:
```text
Slots : Array<FStorageSlot>
SlotCount : int32
```


### `UItemDefinition`
Static item data (DataAsset/DataTable/csv).

### `APickupActor`
World pickup; transfers into Hand then storage; never destroys itself before storage acceptance.

---

# 5. State Model

## 5.1 Stateful or Stateless

Stateful
- storage contents
- equipped backpack reference
- optional opened container reference
- item quantities (if stacks)


## 5.2 Owned State by System

Suggestion:
- `UStorageComponent`: Slots, Capacity, Guid/identity
- `ABackpackActor`: StorageComponent, identity/config, world/equipped state
- `UBackpackAccessComponent`: EquippedBackpack ref, OpenedContainer ref (optional)
- `UToolbeltComponent`: Slots, Capacity, 

## 5.3 Reset / Persistence

For prototype:
- storage initializes on actor spawn
- backpack keeps contents while actor exists
- dropped backpack preserves contents
- equipped backpack persists while player remains alive
- on player death: backpack detaches from player as a whole, ToolBelt and Hand storage content are dropped
- Not Storage related content will automatically respawns with the player.


---

# 6. Core Functions
Suggestions.

## 6.0 Network Considerations
Prefix rule applies to **externally-invoked, state-changing** actions:
- `Request_*` external request entry
- `RpcServer_*` client-to-server routing
- `Auth_*` authority execution

Query/internal helpers don’t require prefixes.

## 6.1 `UStorageComponent`
```cpp
CanAddItem();
AddItem();

CanRemoveItem();
RemoveItem();

MoveItem();
SwapItems();
SwapSlots();

GetSlots();
```

```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnStorageSlotChanged, int32, SlotIndex);
```


## 6.2 `UBackpackAccessComponent`
```cpp
HasBackpack();
GetEquippedBackpack();
GetActiveStorage();

CanEquipBackpack();
EquipBackpack();
UnequipBackpack();
DropEquippedBackpack();
```


## 6.3 `ABackpackActor`
```cpp
GetStorageComponent();
OnEquipped();
OnDropped();
IsEquipped();
```

Implementation note:
- `OnEquipped()` can disable collision/interaction and attach to character.
- `OnDropped()` can detach, enable collision/interaction, and restore world presence.


## 6.4 `AItemPickupActor`
```cpp
GetItemStack();
TryPickup();
```

---

# 7. Rules and Constraints

## 7.1 Activation Rules

### Picking up an item
Must be true:
- valid pickup
- player's Hand is available

### Equipping a backpack
Must be true:
- valid backpack actor
- allowed to equip
- player does not already have one
- backpack not already equipped

### Dropping a backpack
Must be true:
- player has equipped backpack
- player's Hand is available (for holding then drop)


## 7.2 Core Constraints

Early constraints:
- backpack has fixed slot count
- only one equipped backpack
- no nested backpacks

## 7.3 Failure / Rejection Cases

### Pickup failure
If Hand is not available:
```text
Do not consume pickup.
Show "Hand Occupied" feedback.
```
### Storage failure
If backpack full:
```text
Do not consume item unless partial transfer is allowed.
Show "Backpack full" feedback.
```
### Equip failure
If already wearing backpack:
```text
deny equip
Show "already wearing" feedback.
```
### Drop "on hand" failure
If drop location invalid:
```text
Try to resolve with collision physic.
Show ultimatly denied feedback.
```


---

# 8. Boundaries

## 8.1 Not Doing
This system does **not** handle:
- crafting
- item stat calculation
- character equipment stats
- animation
- item rotation
## 8.2 External Dependencies
- interaction system
- player character/component lookup
- UI inventory screen
- item definitions/data assets
- world pickup actors
- equipment attachment system
- multiplayer authority
- optional save system later









---

# 11. Recommended Minimum Prototype

## 11.1 Minimum Prototype

First:
- one test item pickup
- store picked up item on hand
- Drop picked up item

Then:
- one backpack actor
- one player backpack access component
- one storage component with fixed slots
- one basic inventory UI
- pickup transfers item into backpack

After that:
- player can wear backpack
- wore backpack keeps contents
- player can drop backpack
- dropped backpack keeps contents
- player can re-equip same backpack
- Toolbelt with 3 slots

Multiplayer support:
- replication required for storage contents and equipped backpack reference


## 11.3 Must-Prove Checks

The prototype must prove:
- item pickup only succeeds when storage accepts item
- backpack owns item state
- dropped backpack preserves contents
- player can lose access to backpack storage
- re-equipping backpack restores access to same contents
- storage component can be reused by chest or loot container
- UI updates when storage changes













---

# 13. Suggested Implementation Order

## Phase 1 — Item Data

Create:

```text
UItemDefinition
FItemStack
FStorageSlot
```

Test with debug items only.

---

## Phase 2 — Storage Component

Create:

```text
UStorageComponent
```

Implement:

```text
AddItem
RemoveItem
MoveItem
SwapSlots
CanAddItem
OnStorageChanged
```

Test storage without UI first.

---

## Phase 3 — Backpack Actor

Create:

```text
ABackpackActor
```

Add:

```text
StorageComponent
Mesh
Interact behavior
Equipped/Dropped state
```

---

## Phase 4 — Player Access Component

Create:

```text
UBackpackAccessComponent
```

Implement:

```text
EquipBackpack
DropEquippedBackpack
GetActiveStorage
```

At this point, prove:

```text
Player can equip backpack.
Player can drop backpack.
Backpack contents persist.
```

---

## Phase 5 — Pickup Actor

Create:

```text
AItemPickupActor
```

Implement:

```text
TryPickup
Transfer into active storage
Destroy only after accepted
```

---

## Phase 6 — Basic UI

Create:

```text
WBP_StoragePanel
WBP_StorageSlot
```

UI should bind to:

```text
UStorageComponent
```

Not directly to player inventory.

The UI may ask player:

```text
GetActiveStorage()
```

But once opened, it displays the storage component.


---

# 14. Suggested Blueprint/C++ Class Layout

Possible class names:

```text
UItemDefinition : UPrimaryDataAsset

FItemStack
FStorageSlot
FStorageAddResult

UStorageComponent : UActorComponent

ABackpackActor : AActor
AItemPickupActor : AActor
AStorageContainerActor : AActor

UBackpackAccessComponent : UActorComponent
UHotbarComponent : UActorComponent

WBP_StoragePanel
WBP_StorageSlot
WBP_Hotbar
WBP_HotbarSlot
```

If using mostly Blueprint, still keep the same conceptual structure.
