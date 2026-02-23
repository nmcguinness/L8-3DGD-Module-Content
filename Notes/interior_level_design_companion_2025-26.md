---
title: "Interior Level Design — Project Companion"
subtitle: "Application to ReBeat, Cob Cop, and Ale & Ambition"
author: "Niall McGuinness"
institute: "Dundalk Institute of Technology"
programme: "BSc (Hons) in Computing in Games Development"
module_code: "COMP I8015"
module_title: "3D Game Development"
stage: 4
academic_year: "2025–26"
version: "1.0"
date: "2026-02-23"
format:
  html:
    toc: true
    toc-depth: 2
    number-sections: true
  pdf:
    toc: true
    number-sections: true
---

# Interior Level Design — Project Companion 2025–26

> This document applies the principles in the **Interior Level Design base notes** directly to this year's three games: ReBeat, Cob Cop, and Ale & Ambition. It is a production support document, not a principles document — read the base notes first. This companion expires at the end of the 2025–26 academic year.

---

## How to Use This Document

Each section below maps to a numbered section in the base notes. Within each section, the three projects are addressed in turn where the principle applies differently to each. Where a principle applies identically to all three, only shared notes are given.

Section numbers match the base document throughout so you can cross-reference directly.

---

## §1 — Why Interior Spaces Demand Discipline

All three projects this year depend heavily on interior quality, but the nature of that dependency differs across the games.

**Cob Cop** is the most interior-dependent project in the cohort. The investigation loop is entirely interior-driven — the quality of the investigation spaces is the quality of the game. There is no exterior environment to provide visual breathing room or perceptual contrast. Every scene must be credible, readable, and evidence-legible without UI assistance. Interior design here is not craft — it is mechanics.

**Ale & Ambition** requires its tavern to function simultaneously as a visual environment and as a management interface. Stations must be spatially legible as interactive elements from the hub position. The interior layout is also a UX layout. A player who cannot read the station arrangement in two seconds will struggle with the management loop regardless of how well the underlying system is built.

**ReBeat** is the least interior-dependent game in the cohort, but interior spaces still appear in camera sequences, score reveal moments, and potentially in the hub from which runs originate. The concern for ReBeat is not investigation or management legibility — it is **camera behaviour** in enclosed spaces. Any contained composition must be validated for third-person camera collision and framing before assets are placed.

---

## §2 — Greybox First. No Exceptions.

### Project-Specific Greybox Validation Criteria

Before leaving the greybox phase, each project must satisfy the following minimum tests. These are not suggestions — they are gates. Do not place final assets until every item on this list is confirmed.

**Cob Cop — each investigation interior:**

- Can the player identify the investigation zone on entry without any UI prompt?
- Are all evidence interaction points reachable from the entry position without unnecessary backtracking in the intended discovery sequence?
- If a combat encounter occurs in this space, does the geometry support it without producing degenerate cover situations — positions where the player or enemy AI is cornered with no viable movement option?
- Is every evidence prop silhouetted clearly enough to be identifiable under a single overhead directional? (Run the silhouette test in the greybox, not after assets are placed.)

**Ale & Ambition — the tavern interior:**

- Are all station interaction points reachable from the hub position within a consistent movement budget? Measure the path length from the hub centre to each station and confirm they are roughly equivalent, or that the variation is intentional and gameplay-justified.
- Does the layout create any traffic conflict between the player's movement paths and NPC pathfinding zones? Walk the expected NPC routes in the greybox and confirm they do not cross the player's primary station-to-station paths at high-frequency points.
- Does the camera clip or produce ambiguous angles at any station during the expected interaction animation? Test with the actual character mesh at the correct animation pose, not the mannequin alone.
- Is the hub centre position clearly identifiable by spatial and lighting cues from every point in the tavern? The player must always be able to find their way back to neutral.

**ReBeat — any contained interior composition:**

- At every gameplay position the player is expected to occupy in this space, does the third-person camera maintain a clean frame without geometry collision?
- If the player executes fast directional movement near any wall or corner, does the camera produce a disorienting cut or clip event? Test at the expected maximum movement speed.
- Are ceiling heights sufficient to avoid camera pitch-up collision during any jump or aerial state the player character can enter?

---

## §3 — Spatial Grammar: Primary Paths, Zones, and Sightlines

### Cob Cop — Sightlines as Investigation Design

For Cob Cop, sightline management in the greybox is the primary tool for controlling the investigation arc without scripted sequences or UI waypoints. The sequence in which evidence is discovered is largely determined by the sequence in which evidence becomes visible to the player as they move through the space.

Map your intended discovery sequence before building the greybox. Then build the geometry so that each piece of evidence enters the player's sightline approximately when they should discover it in the sequence. Evidence that is visible from the entry point will be investigated first — which may or may not be where you want the arc to begin. Evidence that requires the player to cross the room and turn a corner will be discovered later.

This is spatial puzzle design without scripting overhead. The layout teaches the investigation sequence.

### Ale & Ambition — Three-Depth in a Hub

The three-depth rule applies to Ale & Ambition's tavern differently than to a linear space. Rather than foreground-mid-background along a single axis, the tavern should read as **hub-spoke-periphery** from the entry sightline:

- **Hub (foreground equivalent):** The central bar counter or primary management position — the first thing the player sees on entry, and the spatial anchor to which they return between tasks.
- **Primary stations (mid-ground equivalent):** The stations accessed most frequently — visible from the hub, reachable in one to two seconds, differentiated by lighting temperature.
- **Secondary stations or storage (background equivalent):** Less frequently accessed areas — further from the hub, slightly darker, requiring deliberate movement to reach.

If the player cannot read this hierarchy from the entry sightline, the management loop will feel spatially disorganised even if the underlying system logic is correct.

### ReBeat — Spatial Clarity for Camera Framing

ReBeat's platforming spaces should treat sightlines primarily as camera composition problems. The player's forward movement direction should always be the primary sightline, and the camera framing at the player's most common positions should be validated before geometry is finalised. Geometry that creates unintended camera cuts or ambiguous depth relationships between the player character and the background will degrade readability of ghost actors — which are the game's primary escalating challenge.

---

## §4 — Functional Zoning

### Cob Cop — Zone Type per Scene Function

Each Cob Cop investigation interior should map to the following zone structure:

| Zone type | What it contains in Cob Cop |
|:---|:---|
| Orientation | Entry point, immediate visual survey of the space, no evidence in this area |
| Activity | Main investigation area, ambient props establishing the scene context |
| Interaction | Evidence prop locations, each visually differentiated from the surrounding activity zone |
| Transition | Doorways and corridors between rooms, used to pace the investigation sequence |

A common error will be placing evidence (interaction zone content) in the orientation zone — near the entry — because it feels natural to begin the investigation immediately. Resist this. The orientation zone is where the player reads the space, not where they begin interacting with it. Starting the investigation too early removes the player's ability to build a spatial model before they are given information to process.

### Ale & Ambition — Stations as Interaction Zones

Every management station in the tavern is an interaction zone by definition. The zoning error most likely to occur in Ale & Ambition is **interaction zone bleed** — two adjacent stations without a clear spatial or visual delimiter between them, causing the player to misread which station they are activating.

Zone separation between stations does not require physical walls. It can be established through:

- A change in floor material or tile pattern at the station boundary.
- A distinct localised light temperature per station (each station has a visually identifiable colour cast).
- A slight spatial offset — one station recessed into the wall, the adjacent station flush.

Any of these alone is sufficient. Combining two of the three is robust. Do not rely on UI labels alone to differentiate stations — the spatial design must be legible before UI is added.

---

## §5 — Lighting Hierarchy

### Cob Cop — Cinematic Lighting as Investigation Tool

Cob Cop's lighting must perform two jobs simultaneously: it must be atmospherically credible (the space must feel like a real location with plausible light sources) and it must be functionally hierarchical (evidence props must be the brightest, most visually prominent objects in their zones).

The point interest light in each interaction zone should be positioned to fall directly on the evidence prop, not on the surrounding decorative context. A common error is lighting a zone evenly and then adding a point interest light to the general area — this creates ambient brightness without directing the player's attention. The point interest light must be **narrower and brighter than its surrounding zone fill**, creating a visible pool of elevated luminance that marks the interaction position.

For Cob Cop's scene transition lighting — entering a new location, discovering a key piece of evidence, completing an investigation — use a Blueprint timeline-driven light state change as described in the base notes. The transition from the neutral investigation state to the "evidence found" state should be a coordinated change: light colour shift, a brief Niagara particle, and an optional camera cut to a close-up framing. These three elements together constitute a readable state signal. Any one of them alone is insufficient.

### Ale & Ambition — Day/Night Lighting States

Ale & Ambition's day/night cycle is a primary gameplay mechanic and must be implemented as a lighting state change, not a time-of-day simulation. The distinction matters: a time-of-day simulation uses a dynamic sky and a moving directional light, which is expensive and unnecessary in an interior hub. A lighting state change uses Blueprint-driven interpolation between two pre-defined interior lighting setups.

Define two lighting states: **day state** (warmer, busier, brighter overall, individual station lights at operational brightness) and **night state** (cooler, quieter, ambient reduced, individual stations dimmed except those relevant to the dungeon idle loop). The transition between them is a Timeline-driven Lerp across all relevant light components simultaneously — typically four to eight lights depending on station count. This is a straightforward Blueprint system that should take one day to implement and will carry significant visual and gameplay communication value.

### ReBeat — Lighting for Ghost Readability

ReBeat's ghost actors — the spawned replays of previous runs — are the game's primary escalating challenge. They must be visually distinct from the player character and from the environment at all times, including during fast movement and in poorly lit areas.

The lighting recommendation for ReBeat's play spaces is a **high ambient base with low zone fill variation**. This counteracts the instinct toward dramatic, high-contrast lighting, which produces situations where ghost actors become invisible in shadow areas. Ghost readability requires relatively even luminance across the play space so that actor outlines are always visible regardless of position. Reserve dramatic lighting contrast for hub and menu spaces, not play spaces.

If ghosts are rendered with an emissive material or a custom post-process effect (outline, tint), validate that the effect remains readable across the full luminance range of the play space at the brightest and darkest points in the scene.

---

## §6 — Prop Readability

### Cob Cop — Evidence as Hero Props

Every piece of evidence in Cob Cop is a hero prop by definition. The set dressing hierarchy must be built around evidence placement first: the evidence position is established, its silhouette and value contrast are confirmed, and then secondary and tertiary props are placed around it in ways that do not compete with it visually.

The most likely failure mode is **tertiary prop contamination** — placing small detail objects (cups, papers, personal items) near evidence props at similar scale and value, reducing the evidence's visual priority. Every tertiary prop within one metre of an evidence item should be checked against the silhouette test: if it reads as clearly as the evidence item under a single directional light, it is competing with the evidence and should be moved, scaled down, or darkened.

### Ale & Ambition — Station Visual Identity

Each management station needs a **consistent visual identity** that persists across its idle, active, and needs-attention states. This identity is established through a combination of the station's primary prop silhouette (the dominant hero prop that identifies the station type — the cooking pot, the serving counter, the brewing barrel) and its associated point interest light.

The station's hero prop should be the largest, most silhouette-distinct object in its interaction zone. Secondary props provide contextual dressing — ingredients, tools, containers — but should be lower value and smaller scale than the hero prop. Players should be able to identify which station they are looking at from across the tavern by hero prop silhouette alone, before they are close enough to read any label or interact.

---

## §7 — Mechanics-Driven Layout

### Cob Cop — Layout as Investigation Sequence

The layout of each Cob Cop investigation interior is the investigation sequence. The order in which rooms connect, the order in which sightlines reveal evidence, and the distance between related evidence pieces all determine the shape of the player's investigative experience.

For each scene, define the intended discovery sequence before building the greybox. Then build the spatial layout so that movement through the space produces discoveries in the intended order. The geometry teaches the sequence — the player should be able to solve the investigation by following the spatial logic of the room, even without explicit prompting.

A related piece of evidence should be visible from the position of the evidence that implies it. If clue A implies looking for clue B, then from the position where A is examined, B should be in the player's visual field or accessible along the immediately obvious next movement direction.

### Ale & Ambition — Station Layout as Management UX

The tavern layout is a UX problem as much as a level design problem. The management loop requires the player to cycle between stations repeatedly under time pressure. The layout must minimise the cognitive load of that cycle.

Apply the following layout principles in the greybox:

- **Reachability parity.** All stations that are used at equal frequency should be approximately equidistant from the hub position. A station that takes twice as long to reach as its peers will be systematically under-used, breaking the intended management balance.
- **Movement economy.** The most common station sequence — the order in which the player typically visits stations in a single management cycle — should form a natural loop in the space, not a backtracking path.
- **Visual separation.** No two stations should share a sightline from the hub that would cause them to visually merge. Each station must be identifiable as a distinct target from the hub centre.

### ReBeat — Layout for Ghost Navigation

ReBeat's ghost actors follow the recorded paths of previous player runs. If the layout contains tight geometry, narrow corridors, or sharp corners, ghost actors will navigate these elements unpredictably — potentially clipping through walls or producing inconsistent threat behaviour. Keep play space geometry clean and open: rounded corners, generous corridor widths (minimum 200 cm), and no geometry features that are narrower than the character capsule.

---

## §8 — Contained Hub Design

### Ale & Ambition — The Tavern as a Persistent Hub

The tavern in Ale & Ambition is the most hub-intensive space in the cohort. It is visited on every game loop, across the entire play session. Its legibility must not degrade with familiarity — the player should be able to orient instantly on every return, regardless of how many loops they have completed.

Define the tavern's landmark anchor early and protect it: the central bar counter, or whichever structural element anchors the hub's geometry. This element must remain visually dominant across all lighting states (day and night), at all progression stages, and despite any decorative additions made as the tavern upgrades. It is the one element that must not change in visual character as the game progresses.

For tavern upgrades — new stations added, existing stations visually upgraded — design the upgrade additions to respect the existing zone structure rather than disrupt it. A new station added during progression should slot into an existing interaction zone slot, not require the player to re-learn the tavern's spatial logic from scratch.

### Cob Cop — The Hub/Precinct as an Orientation Anchor

If Cob Cop features a precinct or home-base hub that the player returns to between missions, apply the same landmark anchor principle: one visually dominant element that is always in the player's first sightline on return, and that communicates the player's current mission state through environmental signals rather than UI alone. A notice board, a case map, or a key prop that updates with mission progress — something that makes the hub feel like it is accumulating history rather than remaining static across the session.

---

## §9 — Modularity and the Content Pipeline

### Shared Note — Asset Pack Selection

All three projects are working with free asset packs from Fab or equivalent sources. The most common error at this stage is selecting asset packs that look good in their promotional screenshots but have inconsistent grid units, making assembly difficult and seam-prone.

Before committing to a primary architecture kit, build a small test assembly in a blank level: place four wall segments, a floor tile, a ceiling panel, and a door frame and confirm that all pieces meet cleanly at the correct snap value with no gaps. If this test takes more than twenty minutes to resolve, the kit has inconsistent grid units and should be replaced before significant build time is invested.

---

## §10 — Scale and Ergonomics

### Cob Cop — Keep Rooms Tight

The instinct when building investigation spaces is to make them large enough to feel "realistic". Real investigation locations — offices, residential rooms, back-of-house service areas — are almost always smaller than students expect, and significantly smaller than the spaces students naturally build.

A tight room with correct proportions reads as credible and produces a dense, discovery-rich investigation experience. A large room with correct proportions reads as sparse, requires more navigation per unit of evidence, and reduces the feeling of accumulating discovery that drives the investigation loop. Unless the scene specifically requires a large architectural space (a warehouse, a civic building), keep investigation rooms within the following bounds: 6–10 m wide, 8–15 m long, 2.4–3.0 m ceiling height.

### Ale & Ambition — Counter Height is a Usability Variable

Management station counter height directly affects whether the player character visually disappears behind the station during interaction animations. Test every station with the actual character mesh in the expected interaction pose before finalising counter height. As a starting point, use 90 cm (standard bar/counter height), but adjust per station based on the character's interaction animation height.

### ReBeat — Ceiling Height and Camera

For play spaces, ReBeat's third-person camera requires sufficient ceiling clearance to avoid pitch-up collisions during aerial states. The minimum safe ceiling height for a play space is 400 cm — enough to accommodate a standard jump arc with camera offset. For areas where the player executes the highest jumps (peak verticality in the platforming layout), test ceiling height explicitly against the camera's maximum upward pitch at the apex of the jump animation.

---

## §11 — Environmental Storytelling

### Cob Cop — Storytelling Is the Mechanic

For Cob Cop, environmental storytelling is not supplementary atmosphere — it is the core investigation mechanic. The crime scene tells the story; the player reads it. This means that every prop placement decision is simultaneously a narrative decision and a game design decision.

Apply the cause-and-effect chain technique explicitly to each crime scene: define the narrative sequence of the event that occurred in the space, then place props that represent each step in that sequence in spatial positions that lead the player through it. The final evidence item in the chain should occupy the interaction zone that is last in the discovery sequence, positioned so that finding it feels like a conclusion rather than an interruption.

Particular attention should be paid to **temporal layering** — Cob Cop's investigation spaces need to communicate not just what happened, but when. A crime scene that occurred recently has different physical characteristics than one that occurred days ago. Material state, dust accumulation, food decomposition, and blood oxidation are all temporal signals. Use Substrate materials to express this layering: a fresh scene looks different from an old one, and that difference carries investigative information.

### Ale & Ambition — Tavern History Through Materials

Ale & Ambition's tavern should accumulate visual history as the game progresses. Early in the session, the tavern is clean and new. As the session progresses and the tavern upgrades, its surfaces should show the evidence of use — spills, wear, accumulated grime in high-traffic areas. This can be achieved through material parameter variation tied to progression state rather than requiring entirely new materials per stage.

Define a **wear parameter** in the tavern's primary surface materials (floor, bar counter, tables) that is driven by a progression value in the game's data system. At low progression, the parameter produces a clean material appearance. At high progression, the same material shows accumulated use. This is a single material with a progression-driven parameter, not multiple material swaps — it is lightweight, data-driven, and narratively coherent.

### ReBeat — Environmental Storytelling as Score Feedback

ReBeat's environmental storytelling serves a different purpose than Cob Cop or Ale & Ambition — it communicates **escalating stakes** rather than investigative narrative. As ghost count increases and the play space becomes more threatening, the environment should reflect that escalation through material emissive intensity, Niagara density, and lighting temperature drift toward cooler, more urgent values.

This is state-driven environmental storytelling: the space itself tells the player how close they are to failure through visual intensity, not through explicit UI. Define two or three environment states tied to ghost count thresholds and implement the transitions as Blueprint-driven light and material parameter changes on the same pattern as the lighting state system described in §5.

---

## Project-Specific Reflective Questions

These questions supplement the generic reflective questions in the base document. Answer them with reference to your specific project and current build state.

### Cob Cop

1. For your primary investigation scene: draw the intended discovery sequence as a numbered list. Then walk the greyboxed space and record the actual sequence in which each evidence item enters your sightline. Where do the two sequences diverge, and what spatial change would align them?

2. A first-time player enters your crime scene with no briefing. Write three sentences describing what they would conclude about what happened, based solely on prop arrangement. Does this match the intended narrative? If not, which specific props are producing the wrong inference?

3. Your investigation loop requires the player to build a mental model of the event that occurred. At what point in the player's spatial journey through the scene does the most critical piece of evidence become visible? Is that the right moment, or does it reveal the solution too early or too late?

### Ale & Ambition

1. Stand at the hub centre position. List every station you can identify from this position by hero prop silhouette alone, without moving. Are there any stations that are not identifiable from this position? What is preventing their readability — occlusion, scale, or value — and how would you resolve it?

2. Walk the most common station management sequence in your greybox — the order in which you would visit stations in a single busy cycle. Does the movement form a natural loop or does it require backtracking? What is the total distance walked? What layout change would reduce it?

3. Describe what the tavern looks like at maximum progression state. Does the visual evolution of the space — through material wear, new station presence, and lighting character — tell the story of a successful, growing establishment without UI confirmation?

### ReBeat

1. In your primary play space, place five ghost actors on paths that cross at a single chokepoint. Run the scene and observe: are the ghost actors legible against the environment and against each other at the moment of crossing? What is the minimum lighting or material change that would maintain legibility under maximum ghost density?

2. Execute a full-speed run through your play space and observe the camera behaviour at every direction change and near every piece of geometry. Note every moment where the camera produces an unintended cut, a collision event, or a loss of player character visibility. How many of these are geometry problems versus camera settings problems?

3. Define the three environment states you intend to use to communicate escalating threat through the space (see §11). For each state, describe the specific light, material, and VFX changes that define it. Could a player who ignores the UI completely understand their threat level from the environment alone?
