---
title: "Puzzle Architecture and State Management"
subtitle: "Designing Puzzles as State Machines, Causal Chains, and Gating Patterns"
author: "Niall McGuinness"
institute: "Dundalk Institute of Technology"
programme: "BSc (Hons) in Computing in Games Development"
module_code: "COMP I8015"
module_title: "3D Game Development"
stage: 4
session: 3
academic_year: "2025–26"
version: "1.0"
format:
  html:
    toc: true
    toc-depth: 2
    number-sections: true
  pdf:
    toc: true
    number-sections: true
---

# Puzzle Architecture and State Management

> These notes are production-oriented. The goal is not to theorise about puzzle design in the abstract — it is to give you a structural framework for designing, communicating, and implementing a playable, robust, dead-end-free escape room puzzle in Unreal Engine. Every principle here connects to a decision you must make and commit to before building. Read these notes before you open the engine.

---

## Ten Commandments of Escape Room Puzzle Design

1. **Draw the state graph before you open the engine.** A puzzle you cannot draw, you cannot build reliably.
2. **Every puzzle element is either solved or unsolved.** Never design an element whose current state is ambiguous to the player.
3. **Every gate is explicit.** If a gate can be bypassed by accident, it is not a gate — it is a suggestion.
4. **The clue and the element it unlocks must be spatially separated.** Proximity collapses the puzzle into a single interaction.
5. **No player action should produce no feedback.** Silent gates are broken gates.
6. **A consumable item belongs to exactly one element.** An item that could plausibly satisfy two elements will always be used on the wrong one first.
7. **The win condition is a compound check.** A puzzle that ends when one thing happens is a single-element interaction, not a puzzle.
8. **The win moment must be authored.** Solve the puzzle and nothing changes is the worst player experience in escape room design.
9. **The Game State Actor owns all state.** State distributed across individual prop Blueprints is state you cannot debug.
10. **Cold-playtest before Stage 1.** No designer can accurately predict how a first-time player will read their puzzle.

---

## 1. Why Escape Room Puzzles Fail

Most student escape room puzzles do not fail because they are too complex. They fail because they were never designed as structures — they were assembled as collections of interactions with no explicit logic governing the relationships between them. The result is a puzzle that can be solved in the wrong order, a puzzle with a silent dead end, a puzzle whose solution the designer knows intimately but which a first-time player cannot reconstruct from the available information.

Escape room design is a structural problem before it is a creative one. The creative decisions — what the room is, what narrative it tells, what aesthetic it carries — all depend on a structural foundation being in place first. That structure is a state machine, and this session is about designing it deliberately.

**The three most common structural failures.** The first is **unenforceable order**: the intended puzzle sequence is A → B → C, but nothing in the implementation prevents the player from attempting C before A, which either lets them skip the puzzle or produces a confusing blocked state with no explanation. The second is **clue-element proximity collapse**: the clue prop and the element it unlocks are in the same zone, so the player sees both simultaneously, reads neither carefully, and either solves the puzzle trivially or gets confused by the information surplus. The third is **distributed state**: puzzle state is stored across multiple Blueprint actors — a Boolean on the cabinet, another on the keypad, a third on the exit door — and when the puzzle breaks, there is no single place to look.

All three failures are design failures. They are prevented by committing to a structural design before building anything.

---

## 2. The Puzzle as a State Machine

A **state machine** is a system with a defined set of states, a defined set of transitions between those states, and a defined set of conditions that each transition requires. An escape room puzzle maps directly onto this model. Understanding the model is not academic overhead — it is the tool you will use to design, describe, and debug your puzzle.

### States

A **state** is a specific configuration of the puzzle at a given moment. States are conditions, not actions. "The cabinet is locked" is a state. "The player examines the cabinet" is a transition. The distinction matters because states persist — they remain true until a transition changes them. Transitions are momentary.

Every puzzle element has its own state set. A typical three-element puzzle has the following states:

- **Element A** — `unsolved` / `solved`
- **Element B** — `locked` / `unlocked` / `solved`
- **Element C** — `inaccessible` / `accessible` / `solved`
- **Exit** — `locked` / `unlocked`

The **scene state** is the combined configuration of all elements at any given moment. The scene state at the start of play is the **initial state**. The scene state in which the exit is unlocked is the **terminal state**. Everything in between is the solution space — the sequence of states the player must traverse to reach the terminal condition.

### Transitions

A **transition** is a player action that moves the puzzle from one state to another. In the ICA, transitions correspond directly to the three interaction verbs:

- An **Examine** produces information that changes the player's knowledge state.
- A **Collect** removes an object from the world and adds it to inventory.
- A **Modify** changes a visible world state, typically gated by a prior Examine or Collect.

Every transition requires a **condition** — something that must be true before the transition can fire. That condition is the gate. A transition with no condition is a trivial interaction; it contributes nothing to the puzzle's structural logic.

### The State Graph

The **state graph** is a directed graph in which nodes are states and edges are transitions. For a three-element escape room puzzle, the graph has a clear linear structure with at most one branch point. The graph must be **acyclic** — there should be no path that returns to a previously visited state without explicit design intent, because cycles are the structural source of dead ends.

Draw this graph before opening Unreal. It does not need to be digital. A pencil sketch with labeled nodes and arrows is sufficient. What matters is that every state is named, every transition is labeled with the verb and condition that fires it, and the graph has exactly one terminal node.

### Orchestration

The state graph describes what the puzzle does. **Orchestration** is the design discipline of shaping *how* the player experiences moving through it — controlling the pacing, emotional beat, and intensity of each stage of the solution arc.

A state machine without orchestration produces correct logic and flat experience. The puzzle fires in the right order, every gate works, the win condition is sound — but the player feels nothing, because the system is responding to them, not directing them. Orchestration is the difference between a puzzle that is solvable and one that is satisfying.

Concretely, orchestration decisions operate at every level of the design. At the spatial level: how much physical distance separates clue from element, and whether that distance creates momentum or friction. At the feedback level: how much sensory weight each intermediate solve carries relative to the terminal solve — early solves should feel significant but clearly partial; the final solve should feel conclusive and complete. At the temporal level: the deliberate delay before `OnPuzzleSolved` fires is an orchestration decision, giving the player a beat to register the final element's solve before the room responds at full scale.

The causal chain is the score. Orchestration is the performance of it. Both must be designed.

```{mermaid}
flowchart TD
    S0["<b>Initial State</b><br>Player locked in. All elements unsolved.<br>Exit locked."]
    S1["<b>Clue A Examined</b><br>Player has read clue prop A.<br>Element A information available."]
    S2["<b>Element A Solved</b><br>Modify(A) fired. Element A visually solved.<br>Element B unlocked."]
    S3["<b>Item Collected</b><br>Collect(Item) fired. Item in inventory.<br>Element C accessible."]
    S4["<b>Element B Solved</b><br>Modify(B) fired. Element B visually solved.<br>Contributes to win condition."]
    S5["<b>Element C Solved</b><br>Modify(C,Item) fired. Item consumed.<br>Contributes to win condition."]
    S6["<b>Terminal State</b><br>All elements solved. Exit unlocked.<br>Camera sequence fires."]

    S0 -->|"Examine(Clue A)"| S1
    S1 -->|"Modify(A) [gate: Clue A examined]"| S2
    S2 -->|"Collect(Item) [gate: Element A solved]"| S3
    S3 -->|"Modify(B) [gate: Item collected]"| S4
    S3 -->|"Examine(Clue C)"| S5
    S4 --> S6
    S5 --> S6
```

*The graph above represents a three-element puzzle with a partial parallel path between elements B and C. Both must be solved to reach the terminal state. Element B is gated by item collection; Element C is gated by a separate examination. The exit fires only when both terminal states are true.*

---

## 3. Causal Chain Design

The **causal chain** is the sequence of cause-and-effect relationships that leads the player from the initial state to the terminal state. It is the puzzle's narrative spine. A puzzle with a clear causal chain has a comprehensible solution arc; a puzzle without one has a set of disconnected interactions that the player must solve by trial and error.

### The Chain Template

A three-element escape room puzzle follows a predictable causal chain structure:

> The player **examines Clue A**, which tells them *how to interact with Element A*. The player **modifies Element A**, which *unlocks Element B* (or reveals an item). The player **collects the item** (or examines a second clue), which provides the *information needed to interact with Element C*. The player **modifies Element C**, which *completes the puzzle*. All terminal states true — the **exit unlocks**.

Write this chain in explicit prose before designing the spatial layout. One sentence per step. If any sentence requires more than one clause to express the connection, the link is too complex or the causal logic is unclear.

### Examines Are Not Optional

The Examine verb is the primary information-delivery mechanism in the ICA. Every Modify interaction that carries a gate condition must have a preceding Examine somewhere in the chain that delivers the information required to satisfy that gate. If a player can satisfy a gate condition without examining anything — because the solution is obvious from the element's appearance alone, or because they guessed — the gate is not enforcing your intended sequence. It is producing an accidental shortcut.

Design examines deliberately. Each examined prop should deliver exactly the information required for one downstream action. It should not deliver surplus information that makes the puzzle trivially easy, and it should not deliver incomplete information that makes the gate condition ambiguous.

**Place the examine target in a different zone from the element it informs.** This is not a stylistic guideline — it is a structural requirement. If the clue prop is in the same zone as the element, the player is likely to observe both simultaneously on their first pass through the zone. They will attempt to interact with the element before reading the clue, fail (if gating is correct) or succeed (if it is not), and either become confused or bypass the examination entirely. The spatial separation between clue and element is what creates the investigation arc.

---

## 4. Gate Topology

A **gate** is a condition that must be true before a transition can fire. Gates are the mechanism that enforces the intended solution sequence. Without gates, an escape room is a room with interactable props. With correct gates, it is a puzzle.

### Gate Types

**Knowledge gates** require the player to have examined a specific clue before the gate passes. The gate condition is `bClueExamined == true`. These gates do not prevent the player from physically reaching the gated element — they prevent the element from responding to interaction until the information has been obtained. The player can attempt the interaction before examining the clue, but the element should refuse and provide a hint indicating that information is missing.

**Inventory gates** require the player to be holding a specific item before the gate passes. The gate condition is `bItemInInventory == true`. These gates are the strongest gate type because they are both informational (the player must have collected the item) and physical (the item must be consumed on use, preventing re-use).

**State gates** require a prior puzzle element to be in its solved state before the gated element becomes interactive. The gate condition is `bPriorElementSolved == true`. These gates enforce sequence when one element's solution physically or narratively enables another.

### No Silent Gates

Every gate must provide feedback on its **false branch** — the branch that fires when the player attempts the interaction before the gate condition is satisfied. A silent false branch (the player interacts, nothing happens, no feedback) is a broken gate from the player's perspective. They cannot distinguish between "I cannot do this yet" and "this prop is not interactive" and "this is a bug."

The false branch response should communicate that the interaction is valid in principle but not yet possible, and ideally provide an environmental signal pointing toward what is missing. "This panel needs a code." "I don't have what I need for this." These responses cost nothing to implement and transform a frustrating blocking experience into a productive investigative prompt.

### Gate Strength

A gate is only as strong as its implementation. A gate implemented as a Blueprint `Branch` node on the receiving element's event graph, checking a local Boolean, is inspectable and debuggable. A gate implemented as a comment or a design intention with no Blueprint enforcement does not exist. Every gate in your state graph must correspond to a concrete Boolean check in your Blueprint implementation.

---

## 5. Clue-to-Element Spatial Logic

The physical placement of clue props relative to their target elements is the most direct expression of your puzzle's causal chain in the world. Poor spatial logic produces a puzzle that can be read in the wrong order, a puzzle where multiple clues compete for attention in the same zone, or a puzzle where the solve sequence is legible only to the designer.

### The Separation Principle

Clue A should not be visible from Element A's interaction position. This is not always achievable in a single room — the room may be too small to create genuine occlusion between every clue-element pair — but it is the target. The principle behind it is that the player's investigation arc depends on movement. If the player can see both the clue and its target simultaneously, there is no investigative journey — only a trivial two-step interaction.

Practical separation strategies for a single room:

- **Zone separation** — place the clue in a different functional zone from its element, so the player must change spatial context to connect the two.
- **Height separation** — place the clue at a different height from the element (a high shelf note informs a floor-level mechanism).
- **Occlusion** — use furniture, columns, or partial walls to break the direct sightline between clue and element while keeping both accessible.

### Clue Prop Readability

A clue prop must be **readable** — legible, identifiable as informational, and distinguishable from decorative dressing. Players do not read every prop in a space equally. They read props that stand out as interactive, that carry visual signals of importance, and that are positioned in their primary path.

Clue props should meet the following criteria:

- They carry unique visual differentiation from surrounding props (scale, value contrast, or isolation from prop clusters).
- They are positioned at eye height or slightly above — not floor level and not above natural sightline.
- They are isolated from competing informational props within the immediate zone — no two clue props should be at the same height and value in the same zone.

**Do not dress clue props with excess surrounding information.** A clue prop surrounded by six other decorative notes and papers asks the player to identify which of seven similar objects is the one that matters. This is a readability failure, not a difficulty increase. Make the clue prop the most visually distinct readable object in its zone.

---

## 6. Dead-End Prevention

A **dead end** is a game state from which the player cannot progress without restarting or resetting. Dead ends are the most severe playability failure in escape room design because they are invisible to the designer (who knows the correct path) and immediately obvious to the player (who does not).

### Sources of Dead Ends

**Consumable item misuse.** If an item can be collected and used on multiple elements, and the item is consumed on first use, a player who uses it on the wrong element has reached a dead end. The puzzle cannot be completed. This is the most common source of dead ends in student escape room designs.

Prevention: every collectable item should be constrained to a single target element. The other elements that could plausibly accept the same item should visually or interactively reject it with clear feedback. "This isn't the right place for this." If the item is visually distinctive — its appearance communicates what it is for — unambiguously, misconsumption risk is lower.

**One-way transitions with no undo.** If the player triggers a Modify that changes the world state in a way that makes a preceding element permanently inaccessible, and they have not yet gathered the information that element provided, they have reached a dead end.

Prevention: information from examine interactions should be recorded in the player's inventory or UI (a notes system, or simply a description panel) so that the player does not need to return to the clue prop to re-read it. If re-reading is necessary, the clue prop must remain accessible throughout the session.

**Ambiguous win conditions.** If the win condition check fires on a single element's solved state rather than a compound check of all terminal states, the player may appear to win while other elements are unsolved, producing an incomplete experience or a silent non-response that reads as a bug.

Prevention: the win condition is always a compound Boolean check. All terminal states must be true simultaneously before `OnPuzzleSolved` fires.

### The Stuck State Audit

Before finalising your design document, enumerate every way a player could become stuck. For each one, identify whether the stuck state is:

- **Impossible** — the design prevents this stuck state structurally.
- **Resolvable** — the stuck state can be recovered from through a design mechanism already in place.
- **A reset requirement** — the only resolution is restarting the level.

Any stuck state requiring a reset is a dead end. Redesign the chain to eliminate it. Adding a "reset puzzle" button is not a design solution — it is an admission that the puzzle has a structural fault.

---

## 7. The Win Moment

The **win moment** is the authored response to the player solving all puzzle elements and reaching the terminal state. It is the single most important feedback event in the entire experience. A win moment that fires silently — the exit door quietly unlocks with no environmental response — is a final-beat failure that undermines the entire experience that preceded it.

### The Win Feedback Stack

The win moment should trigger a compound response across all available feedback channels:

- **Camera sequence** — a Sequencer-driven shot that frames the exit, reveals the result of the solve, or provides a final contextual reveal. This is required by the ICA and should be authored as part of the terminal state design, not added as an afterthought.
- **Environmental state change** — the room's lighting state shifts. A Timeline-driven interpolation from the pre-solve light state to a post-solve state (typically warmer, brighter, more resolved) communicates completion more viscerally than any UI element.
- **Audio response** — a solve sound effect or brief musical sting confirming success. This should be layered — a prop-level solve sound fires on each element's completion; a room-level solve sound fires on the terminal state.
- **Visual change on the exit** — the exit door, lock, or gate should visually change state in a way that is readable from across the zone. The player should be able to see from anywhere in the room that the exit has changed.

### Terminal State Timing

The win condition check should fire only after a brief deliberate delay following the final element's solve event — approximately 0.5 to 1.0 seconds. This allows the final element's own feedback (solve SFX, Niagara effect, light change) to complete before the room-level response begins. A win moment that fires simultaneously with the final solve event produces an audio-visual collision that reads as a glitch.

Implement this through a `Delay` node in the Game State Actor between `CheckWinCondition` returning true and `BroadcastEvent(OnPuzzleSolved)`.

---

## 8. Blueprint Implementation: The Game State Actor

The correct implementation pattern for an escape room puzzle in Unreal Engine is the **Game State Actor**: a single, dedicated Blueprint actor placed in the level that owns all puzzle state variables and manages all transitions between states.

### Why Distributed State Fails

The instinct is to place relevant state on individual prop Blueprints — the cabinet owns `bCabinetSolved`, the keypad owns `bKeypadSolved`, the exit door owns `bExitUnlocked`. This produces a puzzle whose state is physically distributed across multiple Blueprint actors. When the puzzle does not work — and it will not work the first time — you must inspect each actor independently to trace the fault. There is no single place to look. There is no single place to set a debug display. There is no single place to write the win condition check.

Distributed state is not a stylistic choice. It is a structural failure mode.

### The Game State Actor Pattern

The Game State Actor contains:

- **One Boolean variable per discrete puzzle state** — `bClueAExamined`, `bElementASolved`, `bElementBUnlocked`, `bElementBSolved`, `bItemCollected`, `bElementCSolved`.
- **One custom event per transition** — `OnClueAExamined`, `OnElementAModified`, `OnItemCollected`. These events are called by individual prop Blueprints when the player interacts with them.
- **The win condition check** — a pure function `CheckWinCondition` that evaluates all terminal state Booleans and broadcasts `OnPuzzleSolved` if all are true.
- **All gate logic** — every gate check lives in the Game State Actor, not in the prop Blueprint that receives the interaction.

Individual prop Blueprints — the cabinet, the keypad, the examining table — are input/output devices. They receive player interaction events via their own `OnInteract` event (or Enhanced Input action), forward those events to the Game State Actor using a **direct reference**, and listen for events from the Game State Actor that instruct them to change their visual state. They do not own state. They do not evaluate gate conditions. Their responsibility ends when they forward the interaction event.

### Implementation Pattern (Pseudocode)

```
// GAME STATE ACTOR VARIABLES
bClueAExamined    = false
bElementASolved   = false
bElementBUnlocked = false
bItemCollected    = false
bElementCSolved   = false

// GAME STATE ACTOR EVENTS

Event OnClueAExamined:
    bClueAExamined = true
    // No unlock here — information only

Event OnElementAInteracted:
    if bClueAExamined == true:
        bElementASolved    = true
        bElementBUnlocked  = true
        Broadcast(OnElementASolved)       // ElementA prop: play solve animation
        Broadcast(OnElementBUnlocked)     // ElementB prop: enable interaction, play unlock feedback
        CheckWinCondition()
    else:
        Broadcast(OnElementAGateFailed)   // ElementA prop: play hint response

Event OnItemCollected:
    bItemCollected = true
    Broadcast(OnInventoryUpdated)         // UI: add item to inventory display

Event OnElementCSolved:
    bElementCSolved = true
    Broadcast(OnElementCSolvedFeedback)   // ElementC prop: play solve animation
    CheckWinCondition()

Function CheckWinCondition:
    if bElementASolved AND bItemCollected AND bElementCSolved:
        Delay(0.75s)
        Broadcast(OnPuzzleSolved)

Event OnPuzzleSolved:
    FireCameraSequence()
    TriggerLightStateTransition()
    PlayRoomSolveAudio()
    UnlockExit()
```

### Getting a Reference to the Game State Actor

Individual prop Blueprints need a reference to the Game State Actor to forward their events. The cleanest pattern at ICA scope is:

1. In the prop Blueprint's `BeginPlay` event, use `GetAllActorsOfClass` with the Game State Actor class to retrieve the actor.
2. Cast the result and store it as a local variable typed to the Game State Actor class.
3. Call Game State Actor events through this stored reference.

Do not use `GetAllActorsOfClass` on every interaction event — call it once on `BeginPlay` and cache the result. Calling it repeatedly at runtime is expensive and unnecessary.

### Debugging the State Machine

During development, add a **debug print display** to the Game State Actor's `Tick` event (or to a custom `DebugDisplay` function called from `Tick`) that renders the value of every Boolean state variable as an on-screen string in Play mode. A display showing `bClueAExamined: false | bElementASolved: false | bItemCollected: false | bElementCSolved: false` tells you the exact state of the puzzle at any moment during a test run. When something does not fire as expected, the state display tells you immediately which Boolean has not been set, which tells you which transition has not fired, which tells you which gate has not been satisfied.

Remove the debug display before Stage 1 submission.

### The Game State Actor as Orchestrator

It is worth being precise about the Game State Actor's role, because "state owner" undersells it. The Game State Actor does not passively record what has happened — it actively sequences what happens next. When `OnElementAInteracted` fires and the gate condition is true, the Game State Actor simultaneously sets a Boolean, broadcasts an event to Element A's prop, broadcasts an event to Element B's prop, and calls `CheckWinCondition`. It is coordinating the responses of multiple independent actors in a deliberate sequence. That is **orchestration**.

This distinction matters practically. When you are deciding what the Game State Actor should do in response to a transition, the question is not only "what state changes?" but "what should the player experience in the next three seconds, and in what order?" The Game State Actor is the director of that sequence. It controls which prop responds first, how long before the next response fires, and when the room-level reaction begins relative to the prop-level reaction.

The `Delay` node before `OnPuzzleSolved` is an orchestration tool. A deliberate 0.1s stagger between broadcasting `OnElementASolved` and `OnElementBUnlocked` — if you want Element A's feedback to complete before Element B reacts — is an orchestration tool. If these feel like minor implementation details, that framing is wrong. They are the decisions that determine whether your puzzle's final beat feels authored or accidental.

---

## 9. The Stage 1 Design Document

The Stage 1 submission requires you to describe your planned puzzle structure in sufficient detail that a peer could implement it without asking you questions. These notes define what a complete puzzle structure document must contain. Submit nothing less.

### Required Content

**State graph diagram.** A directed graph showing every state, every transition, and every gate condition. Nodes are named states. Edges are labeled with the verb and condition that fires the transition. The graph has exactly one initial node and exactly one terminal node. This can be hand-drawn and photographed, diagrammed digitally (Miro, draw.io, Figma), or produced as a Mermaid flowchart in your Quarto document.

**Causal chain prose.** One sentence per step of the causal chain, written as a player-perspective sequence: "The player examines X, which tells them Y, which allows them to do Z to element W." Every step in the state graph must appear in the prose chain.

**Element descriptions.** For each puzzle element: what is it, what is its initial state, what is its solved state, what gate condition must be satisfied before it can be solved, and what transition does solving it enable.

**Clue prop placement rationale.** For each clue prop: where is it placed relative to the element it informs, and what spatial strategy ensures the player discovers it before attempting the element.

**Dead-end audit.** A list of every way the player could get stuck, and for each stuck state, confirmation that it is structurally impossible (and why).

**Win moment description.** What feedback fires when the terminal state is reached — camera sequence, lighting change, audio response, exit change.

A Stage 1 submission that contains a thematic concept without a state graph, or a clue list without explicit gate conditions, is incomplete. The interview at Stage 1 will ask you to trace the causal chain from initial state to terminal state and to identify the gate condition at each step.

---

## 10. Production Checklist

Use this checklist to confirm your puzzle design is structurally complete before building. Every row must be checked before Stage 1 submission. Rows marked with a build-phase note should be confirmed again during implementation.

| Checklist Item | Confirmed |
| :-- | :--: |
| State graph drawn with every state named and every transition labeled | ☐ |
| Causal chain written as explicit one-sentence-per-step prose | ☐ |
| At least one Examine-gates-Modify relationship in the chain | ☐ |
| At least one sequential gate (Modify-gates-Modify) enforcing intended order | ☐ |
| Clue prop for each gated element placed in a different zone from its target element | ☐ |
| No two clue props at the same height and value in the same zone | ☐ |
| Every gate has a false-branch feedback response designed (hint or environmental signal) | ☐ |
| Every consumable item constrained to exactly one target element | ☐ |
| All other plausible target elements confirmed to reject the item with feedback | ☐ |
| Dead-end audit complete — no reset-required stuck states identified | ☐ |
| Win condition implemented as a compound check of all terminal state Booleans | ☐ |
| Win moment feedback stack designed: camera, light, audio, exit change | ☐ |
| Game State Actor pattern planned — state not distributed across prop Blueprints | ☐ |
| *(Build phase)* Debug state display added to Game State Actor | ☐ |
| *(Build phase)* Cold playtest completed by someone unfamiliar with the design | ☐ |

---

## Reflective Questions

These questions are intended for individual reflection after completing your puzzle design document and after each build iteration. Answer them with reference to your current design state, not your intended final state.

1. **State graph completeness.** Draw your state graph from memory without referencing your design document. Are there any states or transitions you could not recall? A state machine you cannot draw from memory is one you do not yet fully understand.

2. **Causal chain legibility.** Without referencing your design notes, write one sentence for each causal link. "The player examines X, which tells them Y, which allows them to do Z." If any sentence requires more than one clause to express the connection, the link may be too complex or the logic unclear.

3. **Gate completeness.** For every interactable element in your puzzle, what prevents the player from solving it before solving the preceding element? If the answer is "nothing," you have a missing gate. If the answer is "the player probably won't try," you have an unenforceable assumption.

4. **Dead-end audit.** For every collectable item in your puzzle, list every Modify interaction in the room that could plausibly accept it. Is the item protected from every Modify except its intended target? What happens when a player uses the item on the wrong element?

5. **Win moment authored.** If someone played your puzzle right now and solved all elements, what would happen? Describe the sequence of visible and audible responses in the room. If the answer is "the exit unlocks," your win moment is incomplete.

6. **First-time readability.** Imagine a player who has never seen your room entering it for the first time. What is the first thing they see? Does it tell them anything about what they should do? Where do they go next? Is that where you intended?

---

## Appendix A: Glossary

**Causal chain.** The sequence of cause-and-effect relationships linking the initial state of the puzzle to the terminal state. Each link in the chain is a player action that produces an outcome enabling the next action.

**Dead end.** A game state from which the player cannot progress without resetting. Dead ends are structurally caused by consumable item misuse, one-way transitions that make information permanently inaccessible, or ambiguous win conditions.

**Game State Actor.** A dedicated Blueprint actor that owns all puzzle state variables and manages all state transitions. The single source of truth for puzzle state during a play session.

**Gate.** A condition that must be true before a transition can fire. Gates enforce the intended solution sequence. Every gate must have a false-branch feedback response.

**Initial state.** The configuration of all puzzle elements at the start of play. All elements unsolved; exit locked; player has no items.

**Knowledge gate.** A gate condition requiring the player to have examined a specific clue prop. Implemented as `bClueExamined == true` in the Game State Actor.

**Orchestration.** The design discipline of shaping the pacing, emotional beat, and intensity of the player's experience of moving through the puzzle's state machine. Where the state graph defines what the puzzle does, orchestration governs how the player feels doing it — controlling spatial distance between beats, the relative feedback weight of intermediate versus terminal solves, and the timing of multi-actor responses coordinated through the Game State Actor.

**Inventory gate.** A gate condition requiring the player to be holding a specific item. Implemented as `bItemInInventory == true` in the Game State Actor.

**Scene state.** The combined configuration of all puzzle elements at a given moment.

**State.** A persistent condition of a puzzle element or the scene as a whole. States are not actions — they are conditions that persist until a transition changes them.

**State gate.** A gate condition requiring a prior puzzle element to be in its solved state. Enforces sequential solution order between elements.

**State graph.** A directed graph in which nodes represent states and edges represent transitions. The state graph is the primary design artefact for puzzle architecture and must be produced before implementation begins.

**Terminal state.** The configuration of all puzzle elements in which the win condition is satisfied. All required elements solved; exit unlocked.

**Transition.** A player action that moves the puzzle from one state to another. Transitions correspond to the three ICA interaction verbs: Examine, Collect, Modify.

**Win condition.** The compound Boolean check that determines whether the terminal state has been reached. Must check all terminal state variables simultaneously.

**Win moment.** The authored feedback response triggered when the win condition is first satisfied. Consists of a camera sequence, an environmental lighting state change, an audio response, and a visible exit change.
