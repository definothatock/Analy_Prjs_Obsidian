## Quick Design Brief

**What is being designed:**  
A modular storage system where item storage is owned by containers, especially wearable/drop-able backpacks, rather than being permanently owned by the player.

**Experience it should create:**  
The player should understand:

> “My carrying capacity comes from the backpack/container I currently use, not from the character itself.”

**Main player actions:**

- pick up items
- place items into a backpack
- equip / unequip backpack
- drop backpack
- recover backpack later
- optionally use hotbar shortcuts for fast access

**Main design difference from previous project:**  
The previous tutorial-style inventory was too large and player-bound. This project should use a smaller, modular storage model where **inventory is a component of containers**, not a permanent player system.

**Core principle:**  
The player does not “have an inventory.”  
The player has **access to storage containers**.

---

# 0. Scope and Design Framing

## 0.1 Unit of Design

Primary unit:
- **Container / Backpack Inventory System**

Possible related but separate units:
- Hotbar System
- Item Pickup System
- Equipment / Wearable Container System
- Container UI System
- Item Definition / Item Instance System

For this plan, the main focus is:
**Container-based storage structure.**

Keep in mind:
In later development, Hotbar can be the same system as the container system, having the player themselves as the "container" (toolsbelt?). Or, a modified/derived version of the container system.


## 0.2 Design Goal

>In previous project, the inventory system was a edited version of Steven Ulibrari's mmorpg spacial inventory system. While Steven's system was highly professional, it accounts for aspects that this project would avoids, or at least not to include from early prototyping.

The goal is to create a simple inventory structure while keeping good professional separation.

The general container system should:
- Supports fundamental, stable Replications 
- avoid permanent player-bound inventory
- support backpacks as physical world objects
- allow backpacks to be equipped, unequipped, dropped, and looted (access content without wearing)
- keep item storage modular and reusable
- support simple pickup and item transfer
- be expandable later without needing MMORPG-level complexity


## 0.3 Design Constraints

### Intended Simplicity
This system should **not** support, at least initially:
- complex item grids
- item rotation
- nested containers inside containers
- equipment stat systems
- crafting
 Planned, but at least not initially:
- weight simulation, unless needed
- save/load complexity, until base structure works

### Desired Architecture Constraint
Storage should not be hardcoded into the player.

Instead:
```text
Player
 └── can access/equip containers

Backpack Actor
 └── owns Storage Component

Chest Actor
 └── owns Storage Component

Loot Bag Actor
 └── owns Storage Component
```

The storage logic should be reusable across any actor that can hold items.

---

# 1. Intended Experience

## 1.1 Target Experience
The system should create:
- physicality
- modularity
- light survival / looting feel
- meaningful container ownership

The player should feel that containers are actual things in the world, not abstract UI-only storage.

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
- use hotbar for quick-access items, not as separate magical storage
- Other player access backpack that is wore on another player

## 1.4 Anti-Goals
Avoid:
- making the player inventory a giant hidden container
- making item ownership unclear
- duplicating items between backpack and hotbar
- coupling backpack logic directly to player character
- building MMO-level item architecture before needed
- having every system directly talk to the player inventory

---

# 2. Core Design Frame

## 2.1 System Purpose
The Container Inventory System exists to answer:

> Where are items stored, and how does the player access them?

Its role is to provide modular item storage through container actors/components.

The player character should only handle:
- interaction
- equipping containers
- accessing the currently equipped storage
- requesting item actions

The actual item list should live elsewhere.

---

## 2.2 Success Contribution

The system helps gameplay by:

- limiting what the player can carry
- giving value to containers
- allowing dropped backpacks to preserve their contents
- supporting looting and recovery
- making inventory expandable through new container types

---

## 2.3 Design Pillars

### Pillar 1 — Storage Belongs to Containers

The player does not directly own most item storage.  
Backpacks, chests, bags, crates, and similar objects own storage.

### Pillar 2 — Player Access Is a Reference, Not Ownership

The player accesses a backpack because they are wearing or interacting with it.

```text
Player -> Equipped Backpack -> Storage Component -> Item Slots
```

### Pillar 3 — Hotbar References Items, It Does Not Duplicate Them

The hotbar should point to usable items in accessible storage.

It should not create a second copy of the item.

### Pillar 4 — Simple First, Expand Later

Start with fixed slots or simple list storage.  
Do not build grid inventory, item rotation, advanced sorting, or nested bags unless the game truly needs them.

---

# 3. Core Components

## 3.1 Recommended High-Level Structure

```text
APlayerCharacter
 ├── UBackpackAccessComponent
 │    ├── EquippedBackpack : ABackpackActor reference
 │    └── GetActiveStorage()
 │
 ├── UHotbarComponent
 │    ├── HotbarSlots
 │    └── References accessible items
 │
 └── Interaction Component
      └── Interacts with pickups, backpacks, containers


ABackpackActor
 ├── UStorageComponent
 │    ├── Slots
 │    ├── Capacity
 │    └── Add / Remove / Move / Query
 │
 ├── Mesh / World Representation
 └── Backpack Data


AChestActor / ALootContainerActor
 └── UStorageComponent


AItemPickupActor
 ├── Item Instance / Stack Data
 └── World pickup representation
```

---

## 3.2 Main Actor / Component Responsibilities

## `APlayerCharacter`

The player should not directly own the full inventory.

The player may own:

- equipped backpack reference
- hotbar component
- interaction ability
- currently opened container reference

The player should request storage actions but not be the storage source.

Example responsibility:

```text
Player presses pickup
→ Player asks equipped backpack storage to add item
→ Backpack storage accepts or rejects item
```

---

## `UBackpackAccessComponent`

This is a useful player-side component.

Purpose:

- tracks currently equipped backpack
- exposes active storage to UI / pickup / hotbar
- handles equip / unequip logic
- prevents the rest of the game from needing to know backpack details

Owned state:

```text
EquippedBackpack : ABackpackActor
OpenedContainer : AActor or UStorageComponent, optional
```

Useful functions:

```text
GetEquippedBackpack()
GetActiveStorage()
EquipBackpack(ABackpackActor* Backpack)
UnequipBackpack()
DropEquippedBackpack()
HasBackpack()
```

This component is not the inventory.  
It is the player’s access point to container storage.

---

## `ABackpackActor`

This is a physical item in the world that can hold items.

Purpose:

- exists in the world
- can be picked up/equipped
- can be dropped
- preserves contents
- owns a storage component

Suggested contents:

```text
ABackpackActor
 ├── Mesh
 ├── UStorageComponent
 ├── BackpackDefinition / DataAsset reference
 └── Equip metadata
```

The backpack itself should not contain complicated storage logic.  
That belongs in `UStorageComponent`.

---

## `UStorageComponent`

This is the core reusable storage logic.

Purpose:

- store item stacks / item instances
- enforce capacity
- support add/remove/move/swap
- emit updates for UI
- be reused by backpacks, chests, loot bags, etc.

Possible owned state:

```text
Slots : Array<FStorageSlot>
SlotCount : int32
AcceptedItemTypes : optional filter
MaxWeight : optional, probably later
```

Suggested simple slot type:

```cpp
USTRUCT(BlueprintType)
struct FStorageSlot
{
    GENERATED_BODY()

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    FItemStack ItemStack;

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    bool bIsLocked = false;
};
```

Or if item identity matters:

```cpp
USTRUCT(BlueprintType)
struct FStorageSlot
{
    GENERATED_BODY()

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    FGuid ItemInstanceId;

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    int32 Quantity = 0;
};
```

For an early prototype, a simpler structure is fine:

```cpp
ItemDefinition + Quantity
```

---

## `FItemStack`

For most simple inventories, use item stacks first.

```cpp
USTRUCT(BlueprintType)
struct FItemStack
{
    GENERATED_BODY()

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    TObjectPtr<UItemDefinition> ItemDefinition = nullptr;

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    int32 Quantity = 0;
};
```

This is enough if items of the same type are identical.

Use item instances only if you need:

- durability
- randomized stats
- unique ammo count per weapon
- custom names
- attachments
- ownership history
- save identity
- condition / spoilage

---

## `UItemDefinition`

Use a Data Asset for static item data.

Example:

```text
UItemDefinition
 ├── DisplayName
 ├── Icon
 ├── MaxStackSize
 ├── ItemType
 ├── bCanUse
 ├── bCanEquip
 └── WorldPickupClass
```

This avoids storing repeated item data in every slot.

Good early item categories:

```text
Consumable
Weapon
Ammo
Resource
Quest
Tool
Backpack
```

Do not overbuild this yet.

---

## `AItemPickupActor`

Represents a loose item in the world.

Purpose:

- holds one item stack or item instance
- can be interacted with
- transfers item into accessible storage
- destroys itself only after successful transfer

Basic behavior:

```text
Player interacts with pickup
→ pickup asks player for active storage
→ active storage tries AddItem()
→ if successful, pickup removes transferred quantity
→ if empty, pickup actor is destroyed
```

Important rule:

> Never destroy the pickup before storage confirms the item was accepted.

---

# 4. Core Mechanics

## 4.1 Storage Mechanic

### Goal

Allow actors to store, remove, and transfer items using reusable container logic.

### Functional Verbs

- add
- remove
- move
- swap
- query
- transfer
- reject
- notify

### Core Behavior

- A storage component owns a list of slots.
- Each slot may be empty or contain an item stack.
- Items can be added if there is an empty slot or compatible stack space.
- Items can be removed if the slot contains enough quantity.
- Storage emits update events when its contents change.
- UI reads storage state but does not own the state.

### Inputs

- item stack
- source slot
- destination slot
- quantity
- item filter rules
- capacity rules

### Outputs

- item accepted
- item rejected
- quantity transferred
- slot changed
- UI update event
- pickup destroyed or partially reduced

---

## 4.2 Backpack Equip Mechanic

### Goal

Allow the player to gain storage access by equipping a backpack object.

### Functional Verbs

- equip
- unequip
- drop
- access
- preserve

### Core Behavior

- Backpack exists as a world actor.
- Player can equip the backpack if allowed.
- Equipped backpack becomes attached to the player visually or logically.
- Player’s active storage points to the backpack’s storage component.
- Dropping the backpack detaches/spawns it in the world with contents preserved.
- If the player has no backpack, pickup/storage actions may be limited or unavailable.

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

---

## 4.3 Item Pickup Mechanic

### Goal

Move loose world items into accessible storage.

### Functional Verbs

- detect
- collect
- add
- reject
- destroy

### Core Behavior

- Player interacts with pickup actor.
- Pickup asks for player’s currently accessible storage.
- Storage attempts to add the item.
- If fully accepted, pickup is destroyed.
- If partially accepted, pickup quantity is reduced.
- If rejected, denied feedback plays.

### Failure Cases

- no equipped backpack
- backpack full
- item type not allowed
- pickup already consumed
- storage unavailable

---

# 5. State Model

## 5.1 Stateful or Stateless

The Storage / Backpack system is **stateful**.

It stores:

- backpack ownership/access state
- storage contents
- item quantities
- equipped backpack reference
- optional currently opened container reference
- optional hotbar slot references

---

## 5.2 Owned State by System

### `UStorageComponent` owns:

```text
Slots
Capacity
Optional filters
```

### `ABackpackActor` owns:

```text
StorageComponent
Backpack identity/config
World/equipped state
```

### `UBackpackAccessComponent` owns:

```text
EquippedBackpack reference
OpenedContainer reference, optional
```

### `UHotbarComponent` owns:

```text
Hotbar slots
References or bindings to accessible items
Selected hotbar index
```

---

## 5.3 Reset / Persistence

For prototype:

- storage initializes on actor spawn
- backpack keeps contents while actor exists
- dropped backpack preserves contents
- equipped backpack persists while player remains alive
- on player death, decide whether backpack drops or disappears

Recommended death behavior:

```text
On death:
    equipped backpack is dropped into world
    backpack keeps contents
    player respawns with no backpack or starter backpack
```

Save/load can be added later.

---

# 6. Core Functions

## 6.1 `UStorageComponent`

Minimum practical functions:

```cpp
bool CanAddItem(const FItemStack& ItemStack) const;
FStorageAddResult AddItem(const FItemStack& ItemStack);
bool CanRemoveItem(int32 SlotIndex, int32 Quantity) const;
FItemStack RemoveItem(int32 SlotIndex, int32 Quantity);
bool MoveItem(int32 FromSlot, int32 ToSlot, int32 Quantity);
bool SwapSlots(int32 SlotA, int32 SlotB);
const TArray<FStorageSlot>& GetSlots() const;
```

Useful result struct:

```cpp
USTRUCT(BlueprintType)
struct FStorageAddResult
{
    GENERATED_BODY()

    UPROPERTY(BlueprintReadOnly)
    bool bSuccess = false;

    UPROPERTY(BlueprintReadOnly)
    int32 QuantityAdded = 0;

    UPROPERTY(BlueprintReadOnly)
    int32 QuantityRemaining = 0;

    UPROPERTY(BlueprintReadOnly)
    FText FailureReason;
};
```

Recommended event:

```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE(FOnStorageChanged);
```

Or with changed slot info:

```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnStorageSlotChanged, int32, SlotIndex);
```

---

## 6.2 `UBackpackAccessComponent`

Suggested functions:

```cpp
bool HasBackpack() const;
ABackpackActor* GetEquippedBackpack() const;
UStorageComponent* GetActiveStorage() const;

bool CanEquipBackpack(ABackpackActor* Backpack) const;
bool EquipBackpack(ABackpackActor* Backpack);
bool UnequipBackpack();
bool DropEquippedBackpack();
```

Optional:

```cpp
UStorageComponent* GetOpenedContainer() const;
void SetOpenedContainer(UStorageComponent* Container);
void ClearOpenedContainer();
```

---

## 6.3 `ABackpackActor`

Suggested functions:

```cpp
UStorageComponent* GetStorageComponent() const;
void OnEquipped(AActor* NewOwner);
void OnDropped(const FTransform& DropTransform);
bool IsEquipped() const;
```

Implementation note:

- `OnEquipped()` can disable collision/interaction and attach to character.
- `OnDropped()` can detach, enable collision/interaction, and restore world presence.

---

## 6.4 `AItemPickupActor`

Suggested functions:

```cpp
FItemStack GetItemStack() const;
bool TryPickup(AActor* InteractingActor);
void ReduceQuantity(int32 Amount);
```

Basic flow:

```text
TryPickup(Player):
    Access = Player.GetBackpackAccessComponent()
    Storage = Access.GetActiveStorage()

    if Storage is invalid:
        play denied feedback
        return false

    Result = Storage.AddItem(ItemStack)

    if Result.QuantityAdded > 0:
        ReduceQuantity(Result.QuantityAdded)

    if ItemStack.Quantity <= 0:
        Destroy()

    return Result.bSuccess
```

---

# 7. Rules and Constraints

## 7.1 Activation Rules

### Picking up an item

Must be true:

- player is interacting with valid pickup
- player has accessible storage
- storage has room for at least part of the item
- item is allowed by storage rules

### Equipping a backpack

Must be true:

- target is a valid backpack actor
- player is allowed to equip backpack
- player does not already have one, or swapping is allowed
- backpack is not already equipped by another actor

### Dropping a backpack

Must be true:

- player has equipped backpack
- drop location is valid enough
- backpack actor can be detached/spawned into world

---

## 7.2 Core Constraints

Recommended early constraints:

```text
Backpack has fixed slot count.
Each item has max stack size.
Only one equipped backpack.
Storage does not allow nested backpacks at first.
Hotbar only references accessible items.
```

Optional later constraints:

```text
Backpack weight limit.
Item category restrictions.
Special slots.
Locked slots.
Multiple worn bags.
Container permissions.
```

---

## 7.3 Failure / Rejection Cases

### Pickup failure

If no backpack:

```text
Do not consume pickup.
Show "Need backpack" feedback.
```

If backpack full:

```text
Do not consume item unless partial transfer is allowed.
Show "Backpack full" feedback.
```

If partial transfer:

```text
Move accepted quantity.
Leave remaining quantity in pickup.
```

### Equip failure

If already wearing backpack:

Options:

1. deny equip
2. auto-swap backpack
3. open compare/swap UI

For minimum prototype, choose:

```text
Deny equip if already wearing backpack.
```

This is simpler and safer.

### Drop failure

If drop location invalid:

```text
Do not unequip.
Show denied feedback.
```

---

# 8. Boundaries

## 8.1 Not Doing

This system does **not** handle:

- damage formulas
- crafting recipes
- item stat calculation
- character equipment stats
- animation blending
- save/load initially
- network replication initially
- vendor economy
- quest logic
- grid layout
- item rotation
- automatic sorting unless added later
- nested containers at prototype stage

---

## 8.2 External Dependencies

The system relies on:

- interaction system
- player character/component lookup
- UI inventory screen
- item definitions/data assets
- world pickup actors
- optional equipment attachment system
- optional save system later
- optional multiplayer authority later

---

# 9. Hotbar System Plan

Hotbar is related but should be treated as a separate subsystem.

## 9.1 Hotbar Purpose

The hotbar exists to provide quick access to selected usable items from storage.

It should not be a separate inventory.

The hotbar should answer:

> “Which accessible item should this input use?”

Not:

> “Where is this item stored?”

---

## 9.2 Hotbar Design Pillars

### Pillar 1 — Reference, Do Not Duplicate

A hotbar slot should reference an item in storage.

Bad:

```text
Backpack has potion x5.
Hotbar also has potion x5.
```

Good:

```text
Backpack Slot 3 has potion x5.
Hotbar Slot 1 points to Backpack Slot 3.
```

### Pillar 2 — Validate Before Use

Because backpacks can be dropped or items can move, hotbar entries may become invalid.

Every hotbar use should check:

- does the storage still exist?
- is the item still present?
- is the item usable?
- does the item quantity remain above zero?

### Pillar 3 — UI Should Show Broken References Clearly

If the player drops a backpack, hotbar entries pointing into that backpack should become:

- empty
- greyed out
- marked unavailable

Do not silently use missing items.

---

## 9.3 Hotbar State Model

Hotbar is **stateful**.

Owned state:

```text
HotbarSlots
SelectedIndex
```

Possible slot structure:

```cpp
USTRUCT(BlueprintType)
struct FHotbarSlot
{
    GENERATED_BODY()

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    TWeakObjectPtr<UStorageComponent> SourceStorage;

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    int32 SourceSlotIndex = INDEX_NONE;
};
```

This is simple but fragile if items move between slots.

A more stable later version could use item instance IDs:

```cpp
USTRUCT(BlueprintType)
struct FHotbarSlot
{
    GENERATED_BODY()

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    FGuid ItemInstanceId;
};
```

### Recommended prototype version

For a simple prototype, use:

```text
Hotbar slot points to storage component + slot index.
```

Then later upgrade if needed.

---

## 9.4 Hotbar Core Behavior

- Player assigns an item from storage to a hotbar slot.
- Hotbar stores a reference to that storage slot.
- When player presses hotbar input, hotbar validates the reference.
- If valid, it requests item use.
- If item is consumed, storage quantity decreases.
- If item reaches zero, storage slot clears.
- Hotbar updates visual state.

---

## 9.5 Hotbar Functions

Suggested functions:

```cpp
bool AssignSlot(int32 HotbarIndex, UStorageComponent* Storage, int32 StorageSlotIndex);
void ClearSlot(int32 HotbarIndex);
bool IsSlotValid(int32 HotbarIndex) const;
bool UseSlot(int32 HotbarIndex);
void SelectSlot(int32 HotbarIndex);
FHotbarDisplayData GetSlotDisplayData(int32 HotbarIndex) const;
```

Optional:

```cpp
void RefreshInvalidSlots();
```

---

## 9.6 Hotbar Use Flow

```text
Player presses hotbar key 1
→ Hotbar checks HotbarSlot[1]
→ Gets source storage
→ Checks source slot still contains usable item
→ Calls item use behavior
→ If use consumes item, remove quantity from source storage
→ Storage broadcasts changed event
→ Hotbar UI refreshes
```

---

## 9.7 Hotbar Failure Cases

Hotbar should reject use if:

- hotbar slot is empty
- source storage no longer exists
- backpack was dropped
- source slot is now empty
- item moved and slot reference is invalid
- item is not usable
- player is stunned/dead/busy
- item use condition fails

Feedback:

```text
Empty click sound
Greyed-out icon
Small denied flash
Optional text: "Item unavailable"
```

---

# 10. Recommended Data Model

## 10.1 Simple Early Model

Use this first unless the project needs unique item instances.

```text
UItemDefinition
    static data

FItemStack
    item definition reference
    quantity

FStorageSlot
    item stack

UStorageComponent
    array of storage slots

ABackpackActor
    storage component

UBackpackAccessComponent
    equipped backpack reference

UHotbarComponent
    references storage slot
```

This is the cleanest starting point.

---

## 10.2 When to Add Item Instances

Add item instances only when you need per-item unique state.

Examples:

```text
Two rifles of the same type have different ammo.
Two swords of the same type have different durability.
Food has different spoil timers.
A weapon has attachments.
An item has generated rarity/stats.
```

Then move toward:

```text
UItemDefinition
    static item data

UItemInstance
    runtime unique item state

FStorageSlot
    item instance reference + quantity if stackable

UStorageComponent
    owns item instances or references them
```

But do not start here unless required.

---

# 11. Recommended Minimum Prototype

## 11.1 Minimum Prototype

Build only:

- one test item pickup
- one backpack actor
- one player backpack access component
- one storage component with fixed slots
- one basic inventory UI
- pickup transfers item into backpack
- player can drop backpack
- dropped backpack keeps contents
- player can re-equip same backpack
- optional hotbar with 3–5 slots

No polish required.

---

## 11.2 Test Depot / Sandbox

Create one test map with:

- player start
- one empty backpack
- one backpack with prefilled items
- several item pickup actors
- one chest with storage component
- debug UI showing backpack contents
- debug button/key to drop backpack
- optional hotbar row

Suggested test objects:

```text
Potion x3
Ammo x20
Wood x10
Stone x10
Backpack A: 8 slots
Backpack B: 12 slots
Chest: 20 slots
```

---

## 11.3 Must-Prove Checks

The prototype must prove:

- item pickup only succeeds when storage accepts item
- backpack owns item state
- dropped backpack preserves contents
- player can lose access to backpack storage
- re-equipping backpack restores access to same contents
- storage component can be reused by chest or loot container
- UI updates when storage changes
- hotbar does not duplicate items

---

# 12. Important Design Decisions to Make Early

## Decision 1 — Can the player hold items without a backpack?

Recommended answer:

```text
No, or only very limited hand storage.
```

Possible options:

### Option A — No backpack, no inventory

Cleanest modular model.

```text
Player with no backpack cannot pick up normal items.
```

### Option B — Small built-in pockets

More forgiving.

```text
Player has 2–4 pocket slots.
Backpack adds main storage.
```

### Option C — Player always has hidden inventory

Not recommended for your stated goal.

This returns to player-bound inventory.

---

## Decision 2 — What happens when the backpack is dropped?

Recommended answer:

```text
Backpack becomes a world actor and keeps its storage contents.
Player loses access to those items.
Hotbar entries pointing to it become unavailable.
```

---

## Decision 3 — Can backpacks be stored inside backpacks?

Recommended answer for prototype:

```text
No.
```

Reason:

- prevents recursion complexity
- prevents exploit storage chains
- avoids UI complexity
- avoids save/load complexity

Later, you can allow empty backpacks only, if needed.

---

## Decision 4 — Can item stacks split?

Recommended answer:

```text
Yes, but only after basic add/remove works.
```

Prototype can initially transfer whole stacks.

Later add:

```text
Split stack
Move quantity
Drop partial stack
```

---

## Decision 5 — What does hotbar reference?

Recommended prototype answer:

```text
Storage component + slot index.
```

Later robust answer:

```text
Item instance ID.
```

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

## Phase 7 — Hotbar

Create:

```text
UHotbarComponent
WBP_Hotbar
```

Implement:

```text
AssignSlot
UseSlot
ValidateSlot
ClearSlot
```

Hotbar should listen to storage changes or refresh when displayed.

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

---

# 15. Final Recommended Structure

The clean version should look like this:

```text
Items
 ├── Item Definition Data Assets
 └── Item Stacks

Storage
 ├── Storage Component
 ├── Storage Slots
 └── Storage Events

Containers
 ├── Backpack Actor
 ├── Chest Actor
 └── Loot Bag Actor

Player
 ├── Backpack Access Component
 ├── Interaction Component
 └── Hotbar Component

UI
 ├── Storage Panel
 ├── Storage Slot Widget
 ├── Hotbar Widget
 └── Feedback Messages
```

The key architectural rule:

> **Storage is modular. Player access is contextual. Hotbar is a shortcut layer.**

This keeps the project much lighter than the previous inventory tutorial while preserving a professional structure that can grow later.