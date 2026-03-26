---
title: "Game Concept Spreadsheet — Field Reference Guide"
subtitle: "COMP I8015: 3D Game Development"
programme: "BSc (Hons) Computing in Games Development"
institution: "Dundalk Institute of Technology"
author: "Niall McGuinness"
date: "2025-26"
format:
  html:
    toc: true
    toc-depth: 3
    number-sections: true
---

# Game Concept Spreadsheet — Field Reference Guide

> Complete the [Game Concept Spreadsheet](https://studentdkit-my.sharepoint.com/:x:/g/personal/mcguinnn_dkit_ie/IQC4q3ydEP71Sb31_i_4vFCJAb2vRiT5EMB3m7M3EwtNMsI?e=w9KHLu) before reading this document. Use this guide to understand what each field and option means, and to revise your entries with greater precision.

## Rationale: designing with intentionality

The ICA Concept Spreadsheet is not an administrative form. It is a design instrument.

Every field in the spreadsheet corresponds to a category of decision that you will have to make during production — about how the space looks, how it sounds, how the player moves through it, and what they are meant to feel. The purpose of completing the spreadsheet before production begins is to make those decisions consciously, in advance, so that they are available to guide every subsequent choice rather than being made ad hoc under time pressure.

The failure mode this document is designed to prevent is **unconsidered design**: a game that has a visual style without knowing why, a mood without knowing what produces it, a puzzle without knowing what cognitive operation the player is performing. Unconsidered design is not the same as bad design — a student can produce an attractive and functional space without ever articulating these choices. But it cannot be developed, iterated, or improved without articulable decisions to return to. When a playtester says the space "feels wrong," unconsidered design leaves you with nothing to adjust; considered design gives you a specific decision to revisit.

The spreadsheet asks you to commit to a position on twenty categories when you begin, in earnest, to work on your game implementation. That commitment serves three purposes. 

- First, it forces you to think through the **implications of your concept** before the cost of changing it is high. 
- Second, it produces a brief that you can use to evaluate whether a **decision is consistent with the original intent**. 
- Third, it trains the habit of **designing from the outside in**: beginning with the player's experience and working backward to the production decisions that produce it, rather than assembling assets and hoping an experience emerges.

Each section of this document explains what a given category means, why it matters in the context of this ICA, and what each dropdown option commits you to producing. Read the explanation for every option you have selected. If the description does not match what you intended, change your selection. If you selected an option without being able to describe what it means in practice, this document will help you decide whether it is the right choice.

The spreadsheet is a contract with your future self. Review it before every significant production session. If your design has evolved, update it. A well-maintained concept sheet is evidence of a designer who understands their own work.

---

## Ten Commandments

1. **Every field is a design decision.** Choosing a dropdown option is not an administrative act. Each choice commits you to a set of production obligations that must be visible in your final submission.
2. **Consistency is craft.** Your genre, visual style, mood, lighting, and soundscape must form a coherent whole. Contradictions between fields signal an unconsidered design.
3. **The tonal reference is not decoration.** If you cannot name a film, book, or soundtrack that captures your intended tone, you do not yet have a tone — you have a theme.
4. **Your protagonist situation drives your spatial design.** Why someone is trapped determines what the room contains, how it is arranged, and what clues are appropriate.
5. **Perspective is not a default.** First person and third person produce fundamentally different experiences of scale, agency, and tension. Choose with intent.
6. **Silence is an audio design choice.** The absence of music or ambient sound must be deliberate, not a deferred task.
7. **UI approach shapes immersion.** A full HUD and a diegetic-only UI produce different levels of player agency and world belief. Your choice must be consistent with your atmospheric and narrative goals.
8. **Colour palette is a storytelling tool.** Desaturated palettes read as loss, decay, or institutional suppression. High-saturation palettes read as energy or instability. Know what yours communicates.
9. **Puzzle complexity must match play time.** A branching or compounding puzzle in a 30-minute experience will frustrate rather than engage. Scope your puzzle to your stated duration.
10. **This sheet is a contract with your future self.** What you enter here describes the game you are committing to build. Review it before every production session.

---

## 1. Genre

The genre signals the player's expectations before they enter the space. It governs what interaction conventions they bring, what risks they expect, and what kind of story they are ready to receive. Genre is not the theme of your game — it is the container in which the theme operates.

| Option | Description |
|:---|:---|
| **Horror** | The primary driver is dread, fear, or threat. The player expects danger, scarcity of safety, and unknown forces. Environmental storytelling is used to build and sustain tension rather than to resolve it. |
| **Psychological Horror** | Fear is generated through cognitive disorientation, unreliable perception, or the collapse of the protagonist's mental state. The environment itself may be a manifestation of the character's psychology. *Examples: Amnesia: The Dark Descent, Silent Hill 2.* |
| **Mystery** | The player is positioned as an investigator. The environment contains evidence; the player's task is to read and interpret it. Information is withheld, then revealed through careful examination. *Examples: Her Story, Return of the Obra Dinn.* |
| **Sci-Fi** | The setting, technology, and rules of the world are extrapolated from or in contrast to the present. Unfamiliar materials, interfaces, and spatial conventions signal that the player is in a different order of reality. |
| **Fantasy** | The world operates according to rules that do not apply in the physical world. Magic, myth, or ancient forces shape the space. Visual language draws on mythology, folklore, or invented cosmologies. |
| **Historical** | The setting is grounded in a specific documented period. Authenticity of materials, objects, and spatial arrangements is expected. Period accuracy creates the primary layer of environmental storytelling. |
| **Adventure** | The emphasis is on exploration, discovery, and forward momentum. The player expects a reward for curiosity — secrets, lore, optional content — beyond the critical path. |
| **Thriller** | Tension is generated by time pressure, stakes, or pursuit rather than supernatural dread. The player is competent but under pressure. Pacing is faster than horror; information is withheld for dramatic effect rather than atmospheric effect. |
| **Comedy** | Tone is light, absurdist, or knowingly playful. The environment may subvert genre conventions deliberately. Player expectations are set up in order to be broken. |
| **Steampunk** | A hybrid of Victorian-era aesthetics and anachronistic industrialised technology. Brass, copper, mechanical systems, and gas lighting define the material palette. |
| **Noir** | A pessimistic worldview filtered through a specific visual vocabulary: high contrast, shadow, rain, moral ambiguity, and urban decay. The protagonist is typically implicated in the situation they are trying to escape. |
| **Survival** | The player is in danger of depletion — of time, health, resources, or options. Scarcity is a designed condition, not an oversight. |
| **RPG** | The player's relationship to the world is shaped by accumulated choices and character state. The escape room context may frame a micro-decision that has consequences in a larger system. |
| **Action-Adventure** | Physical interaction and spatial challenge combine with exploration. The player expects both reactive skill-based moments and investigative ones. |
| **Walking Sim / Narrative** | Interaction is minimal; the primary experience is observation and narrative absorption. The environment is the story; there is no mechanical puzzle in the traditional sense. *Examples: Firewatch, What Remains of Edith Finch.* |
| **Open World** | The player's path through the space is not prescribed. Multiple valid sequences of exploration are intentionally supported. |

---

## 2. Visual Style

Visual style is the aggregate of every surface, silhouette, and colour decision in the scene. It is not an art direction note to yourself — it is a production commitment. Every asset imported or created must be evaluated against this choice before it enters the scene.

| Option | Description |
|:---|:---|
| **Realistic** | Materials, lighting, and proportions are plausibly consistent with the physical world. Assets are not stylised; surface imperfection and physical wear are expected at this fidelity level. |
| **Photorealistic** | The highest fidelity tier. Ray-traced or path-traced lighting, physically accurate materials, and high-resolution geometry. Requires significant asset quality and performance budget management. |
| **Stylised** | A deliberate departure from realism in proportions, colour, or surface treatment. The style is internally consistent and clearly intentional. |
| **Minimalist** | Form is reduced to its essentials. Detail, texture, and decoration are removed; spatial relationships and silhouette carry the full communicative load. |
| **Low Poly** | Geometry is deliberately faceted, with flat or very lightly shaded surfaces. A common indie aesthetic that communicates constraint as a feature rather than a limitation. |
| **Cel-Shaded** | Surfaces are rendered with discrete tonal steps rather than continuous gradients, producing an effect similar to hand-drawn illustration or comics. *Examples: Borderlands, The Legend of Zelda: The Wind Waker.* |
| **Pixel Art** | The image is constructed from visible pixels as the fundamental unit. Retro connotations are strong; the aesthetic signals a knowing relationship with game history. |
| **Hand-drawn** | Assets appear to have been produced by hand — brush strokes, ink lines, or pencil marks are visible in the final surface. |
| **Comic Book** | Strong outlines, flat colour areas, and halftone or cross-hatch texturing. Influenced by American or European sequential art traditions. |
| **Dark & Gritty** | High surface detail, heavy weathering, desaturated base tones, and emphasis on decay and industrial damage. The aesthetic of physical consequence. |
| **Painterly** | Surfaces suggest the texture of paint application — visible brushwork, soft edges, and colour blending that is not photographic. |
| **Retro** | A deliberate evocation of a past technology's aesthetic limitations — scan lines, limited colour palettes, compression artefacts — as a design choice. |
| **Surreal** | The environment violates the spatial and physical logic of the real world. Impossible geometries, non-Euclidean spaces, or dreamlike material behaviour are features, not errors. |
| **Isometric** | A fixed-angle axonometric projection. All three visible faces of a cube receive equal treatment. Depth is suggested rather than perspectivally rendered. |
| **Voxel** | Three-dimensional pixel art: the world is composed of unit cubes. *Examples: Minecraft, 7 Days to Die.* |
| **Anime / Manga** | Visual language derived from Japanese animation and comics conventions: large eyes, expressive exaggeration, speed lines, and characteristic colour treatment. |
| **Flat Design / Vector** | Two-dimensional, shape-based visual language with no simulated depth. Strong in graphic design contexts; produces a deliberately non-immersive, designed-object quality. |
| **Watercolour** | Soft edges, visible paper texture, and the transparency characteristics of water-based paint. Communicates fragility, intimacy, or nostalgia. |

---

## 3. Colour Palette

Colour palette describes the hue and tonal relationships that govern the space. It is one of the most powerful atmospheric tools available and one of the most commonly left unconsidered. A colour palette choice made here must be enforced in every material, light, and post-process decision.

| Option | Description |
|:---|:---|
| **Monochromatic** | All colours derive from a single hue, varying only in lightness and saturation. Produces strong visual coherence; communicates singularity of emotional register — obsession, purity, decay. |
| **Analogous** | Colours from adjacent positions on the colour wheel — warm reds and oranges, or cool blues and greens. Harmonious and naturalistic; reads as organic and internally consistent. |
| **Complementary** | Two colours from opposite positions on the colour wheel — orange and blue, red and green. High visual tension; useful for foreground/background separation and directing attention. |
| **Desaturated / Muted** | Colours are present but drained of intensity. Communicates age, exhaustion, institutional suppression, or emotional flatness. Common in horror and noir. |
| **High Saturation** | Colours are vivid and intense. Communicates energy, instability, artificiality, or the heightened reality of memory and dream. |
| **Warm Dominant** | The space is governed by reds, oranges, and ambers. Communicates danger, intimacy, fire, or organic warmth depending on context. |
| **Cool Dominant** | Blues, teals, and greys dominate. Communicates isolation, technology, death, or institutional cold. |
| **Neutral / Earth Tones** | Browns, tans, ochres, and desaturated greens. Communicates the mundane, the aged, the domestic, or the natural without emotional heightening. |
| **High Contrast Black & White** | All colour information is removed; only luminance remains. Produces the maximum possible tonal range — white as exposure, black as absence. |

---

## 4. Setting / Location Type

The setting is the physical context that justifies the presence of every prop, surface, and spatial relationship in the room. A setting chosen here and then ignored in asset selection will produce an incoherent environment. Every object in the scene must be accountable to this choice.

| Option | Description |
|:---|:---|
| **Domestic (house / flat)** | The space was built and occupied for everyday residential life. Objects are personal, scaled for one or two occupants, and carry the marks of habitual use. |
| **Institutional (office / school / hospital)** | The space was designed to process people in volume — to standardise, categorise, or treat. Materials are durable and impersonal; signage and procedural objects are expected. |
| **Cultural / Civic (gallery / museum / library / theatre)** | The space was built for public display, access to knowledge, or communal cultural experience. Architecture is considered rather than purely functional; lighting is a designed feature rather than a utility; objects are intended to be observed rather than used. Materials tend toward the durable and the prestigious — stone, timber, glass — and the spatial grammar is oriented around display, circulation, and contemplation. |
| **Industrial (factory / warehouse)** | The space was built for production, storage, or mechanical process. Scale is large, materials are heavy, and human comfort was not the primary design consideration. |
| **Underground (bunker / cave / sewer)** | The space is beneath the surface. Natural or engineered containment. Light sources must be artificial or bioluminescent. Psychological weight of enclosure is a design resource. |
| **Abandoned / Derelict** | The space was built for a purpose that has since ended. Decay, deterioration, and evidence of previous occupation are the primary storytelling materials. |
| **Natural (forest / cave)** | The space is defined by terrain and organic materials rather than constructed surfaces. Human objects in this context have been brought in deliberately and their presence requires narrative justification. |
| **Sci-Fi Facility** | A purpose-built environment for activities that do not exist in the present world. Technology, environmental control systems, and non-standard spatial configurations define the material palette. |
| **Fantastical / Otherworldly** | The space exists in a reality with different physical laws, materials, or spatial logic. There is no obligation to justify the environment against the physical world. |
| **Religious / Ritual** | The space was designed to produce altered psychological states through architecture, light, and symbolism. Scale, axis, and material richness are used deliberately to direct attention and induce reverence or fear. |
| **Vehicle (ship / train / plane)** | The space is contained within a moving or formerly moving vessel. The boundary of the room is the hull; escape is physically impossible without the game's own logic. |

---

## 5. Narrative Tone

Narrative tone is the emotional and philosophical register of the story being told. It is distinct from mood: mood is what the player feels; tone is the authorial attitude toward the material. A game can have a tense mood while maintaining a darkly comic tone — or a melancholic mood while maintaining a serious, unsentimental tone.

| Option | Description |
|:---|:---|
| **Serious** | The situation and its stakes are treated without irony. The player's experience is respected as genuinely significant. |
| **Darkly Comic** | The material is grim, but the authorial perspective finds absurdity in it. Horror and comedy coexist without undermining each other. *Examples: Disco Elysium, Neon White.* |
| **Tragic** | Loss is the dominant register. The escape, if achieved, is qualified; something has already been irrevocably taken. |
| **Surreal** | Causality and coherence are suspended. Events and objects resist rational explanation; the logic is emotional or associative rather than consequential. |
| **Deadpan** | Extraordinary circumstances are presented without comment or affect. The player supplies the emotional response; the game does not. |
| **Mythic** | The events are framed as archetypal rather than personal — a recurrence of patterns older than the individual story. |
| **Melancholic** | Sadness that is not acute grief but a sustained, reflective register. The space speaks of things that are absent, ended, or unreachable. |
| **Unsettling** | The environment produces discomfort without identifying its source. The player cannot locate the threat precisely, which is the point. |
| **Hopeful** | Even in difficulty or confinement, the possibility of a positive resolution is sustained and genuine. |
| **Absurdist** | The situation is inherently without rational meaning. The response to that meaninglessness — comic, tragic, or defiant — defines the experience. |
| **Intimate** | The story operates at a personal, small-scale register. The stakes are not world-ending but feel significant precisely because they are private. The player is close to the emotional core of the experience. *Examples: Gone Home, A Short Hike.* |
| **Nihilistic** | The situation is without redemption or resolution. Escape, if achieved, changes nothing of consequence. The design does not offer comfort or meaning; it withholds both deliberately. |
| **Folkloric** | The narrative draws on the logic and cadence of oral tradition — fairy tale, legend, or myth at a local rather than epic scale. Rules are strange but internally consistent; consequences are disproportionate and final. 

## 6. Target Mood

Mood is what the player feels moment-to-moment as they move through the space. Unlike tone, which is consistent across the whole experience, mood can shift in response to discovery, state change, and puzzle progression. The target mood recorded here is the dominant register — the emotional baseline from which shifts depart and to which they return.

| Option | Description |
|:---|:---|
| **Tense** | The player is in a sustained state of anticipatory alertness. Something may happen; the uncertainty itself is the primary driver. |
| **Eerie** | A quality of uncanny wrongness — the familiar made strange. The environment feels observed or occupied by something that cannot be seen. |
| **Whimsical** | Light, playful, and gently surprising. The rules of the world are benign and imaginative rather than threatening. |
| **Dramatic** | Events and stakes feel significant and heightened. The player's actions carry emotional weight. |
| **Mysterious** | Information is withheld in a way that motivates inquiry. The player is not frightened but curious; the unknown is an invitation rather than a threat. |
| **Unsettling** | Discomfort without identifiable cause. The environment is wrong in ways that cannot be immediately articulated. |
| **Hopeful** | The emotional register of a path that is difficult but not hopeless. Small discoveries feel like genuine progress. |
| **Melancholic** | A sustained, quiet sadness. The space communicates loss or absence; the player feels the weight of what is gone. |
| **Frantic** | High stimulation, time pressure, or sensory density. The player is cognitively loaded and must act quickly or decisively. |
| **Playful** | The experience invites joy and experimentation. Interaction has a tactile, game-like quality that rewards exploration without threat. |
| **Claustrophobic** | The space is physically or psychologically confining. The boundary of the room is felt as a pressure rather than a neutral condition. |
| **Oppressive** | An environment designed to diminish the player — institutionally, physically, or narratively. The space communicates that the player is not welcome or not significant. |
| **Serene** | Stillness and spatial openness produce calm. Threats, if present, are distant or unformed. |
| **Haunting** | A lingering quality — the space stays with the player after they leave it. Memory and loss are the primary emotional materials. |
| **Disorienting** | The player's spatial or cognitive orientation is deliberately compromised. Familiar conventions are subverted to produce confusion as a designed experience. |
| **Nostalgic** | The environment evokes a past — personal or cultural — that the player feels as both familiar and irrecoverable. |

---

## 7. Lighting Mood

Lighting mood is the aggregate quality produced by the light rig as a whole, independent of any specific source. It is the first and most powerful atmospheric signal the player receives. In Unreal Engine, lighting mood is produced by the combination of the Sky Light intensity, the Directional Light colour temperature, the Post Process Volume settings, and the balance between exposed and shadowed areas.

| Option | Description |
|:---|:---|
| **High Contrast / Chiaroscuro** | Deep shadows coexist with bright, hard-edged illumination. Large areas of the scene are in darkness; light is a resource rather than a condition. Strong directional sources; minimal fill. |
| **Low Key / Underlit** | The overall luminance of the scene is below the threshold of comfortable visibility. Detail is present but requires effort to extract. Tension is produced by the difficulty of seeing. |
| **Overexposed / Bleached** | The scene is too bright — washed out, detail-burning, uncomfortably luminous. Communicates clinical environments, traumatic memory, or post-apocalyptic exposure. |
| **Warm & Amber** | Dominant light sources are in the 2700–3500K range. Communicates fire, domestic intimacy, age, or organic warmth. All shadows carry blue-green complements. |
| **Cold & Desaturated** | Dominant sources are 6000K and above. Communicates institutional environments, digital spaces, isolation, and mortality. |
| **Neon / Synthetic** | Saturated, coloured artificial light in direct competition with each other. Communicates urban density, artificiality, or the overlap of human and machine space. |
| **Candle-lit / Firelight** | Flickering, warm, spatially localised sources with very limited radius. Produces deep surrounding shadow; the player is always at the edge of visibility. |
| **Natural Daylight** | A single dominant exterior source, likely through windows. Direction, colour temperature, and shadow length communicate time of day and season. |
| **Flat & Diffuse** | No dominant directional source; light appears to come from all directions equally. Communicates overcast exteriors, fluorescent interiors, or the absence of drama. |
| **Fog / Atmospheric Haze** | Volumetric scattering reduces contrast and detail with distance. Communicates depth, mystery, or environmental hazard. |

---

## 8. Time of Day / Lighting Condition

Time of day determines the colour temperature, directionality, and intensity of the dominant natural light source. In interior spaces, it also determines what is visible through windows and what narrative information that visibility communicates.

| Option | Description |
|:---|:---|
| **Dawn** | Warm, low-angle light entering from a consistent direction. Long shadows, cool colour in shadowed areas. The world is just becoming visible; communicates beginning, vulnerability, or the aftermath of the night. |
| **Day** | A neutral, high-angle source with moderate shadow length and minimal colour temperature variation. The baseline against which all other conditions are judged unusual. |
| **Dusk** | The most dramatically saturated natural light condition. Warm reds and oranges at the horizon; the transition from warmth to cold blue in the upper sky. Communicates ending, urgency, or loss. |
| **Night** | The absence of the dominant natural source. Artificial light becomes primary; moonlight is possible as a secondary fill. Communicates secrecy, danger, isolation, or a space outside normal time. |
| **Interior Artificial Light Only** | The space has no relationship to the exterior light condition. The room is sealed; what is outside is irrelevant or unknown. The player's only reference for normality is the room itself. |
| **Timeless / No Natural Light** | The space is underground, sealed, or otherwise entirely removed from any connection to exterior time. There is no diurnal reference; the light conditions are entirely designed. |
| **Abstract / Non-realistic** | The light in the space does not follow any real-world physical logic. Coloured fills, impossibly directed sources, or flat uniform illumination are deliberate design choices rather than production shortcuts. |

---

## 9. Player Perspective

Player perspective determines the spatial relationship between the player's point of view and the body that inhabits the space. It is one of the most fundamental design decisions in the project and cannot be changed late in production without significant rework.

| Option | Description |
|:---|:---|
| **First Person** | The player sees through the protagonist's eyes. The body is absent or only partially visible. Produces maximum spatial immersion and a direct sensory relationship with the environment. Puzzle elements must be readable at head height and within a natural field of view. *Examples: Amnesia, Firewatch, Outer Wilds.* |
| **Third Person (close)** | The camera follows just behind and slightly above the character. The player can see the character's body, producing a stronger sense of character identity. Spatial scale reads differently; the body becomes a spatial reference object. *Examples: Resident Evil Village, Dead Space.* |
| **Third Person (wide)** | The camera is pulled further back, providing a more comprehensive view of the space at the cost of detail visibility. Useful when the spatial layout itself is the primary puzzle. |
| **Fixed Camera** | The camera does not follow the player but occupies a series of predetermined positions as the player moves through the space. Creates a cinematic, authored viewpoint. Each camera position is a design decision about what the player is shown and what is withheld. *Examples: Resident Evil (original), Alone in the Dark.* |
| **Isometric / Top-down** | The player views the space from directly above or at a steep angle. Spatial relationships are immediately legible; individual surface detail is less visible. |

---

## 10. Camera Style

Camera style describes the optical and compositional qualities applied to the player's view, independent of perspective. These are post-process and camera component settings in Unreal Engine and must be budgeted against the performance constraints of the scene.

| Option | Description |
|:---|:---|
| **Shallow Depth of Field** | A narrow focal plane is in sharp focus; areas in front of and behind it are blurred. Directs attention with precision and communicates a cinematic, authored quality. *Use with caution in puzzle contexts — if a puzzle element is outside the focal plane, it may be unreadable.* |
| **Deep Focus** | All distances are simultaneously in sharp focus. Communicates observational objectivity; allows the player to see and process the full scene simultaneously. |
| **Dutch Angle** | The camera is rotated around the lens axis, producing a diagonal horizon. Communicates psychological instability, disorientation, or menace. Use sparingly — its communicative value degrades with frequency. |
| **Cinematic Letterbox** | The aspect ratio is cropped to a widescreen format, adding black bars at the top and bottom of the screen. Communicates a filmic quality and restricts the player's vertical field of view. |
| **Static Fixed** | The camera does not move in response to player movement or action. Produces a composed, pictorial quality. Every frame is an authored composition. |
| **Dynamic / Follow** | The camera responds fluidly to player movement and action. Communicates responsiveness and presence. |
| **Over-the-shoulder** | A third-person perspective where the camera is positioned very close to the character's shoulder, creating an intimate spatial relationship while retaining some body visibility. *Examples: Resident Evil 4, Dead Space.* |
| **Orthographic** | Parallel projection — no perspective foreshortening. Objects at all distances appear at the same scale. Common in isometric and strategy contexts. |

---

## 11. Soundscape / Ambient Audio

The soundscape is the continuous audio layer beneath all event-driven sounds. It establishes the space as a living or formerly living environment and is one of the primary drivers of sustained atmospheric engagement. A room with no soundscape is not neutral — it is conspicuously empty.

| Option | Description |
|:---|:---|
| **Industrial / Mechanical** | Looping mechanical systems — ventilation, hydraulics, electrical hum. Communicates working infrastructure; the space is or was functional. |
| **Natural / Organic** | Wind, water, insects, distant animals. Communicates an exterior or semi-exterior environment; the boundary between inside and outside is permeable. |
| **Silence-dominant** | The near-absence of ambient sound. Every small sound the player produces is amplified by the quiet. Used in horror and psychological contexts to produce acute sensitivity to audio events. |
| **Electronic / Synthetic** | Generated tones, digital artefacts, or processed noise. Communicates technology, data, or the presence of systems that are not biological. |
| **Diegetic Only** | Every sound in the space has a visible or narratively justified source within the world. No sound is added for atmospheric effect without a plausible real-world origin. |
| **Layered Environmental** | Multiple simultaneous ambient layers at different spatial distances — near, mid, and far — producing a sense of environmental depth and complexity. |
| **Weather-driven** | Rain, wind, thunder, or seasonal audio conditions establish exterior environment without visibility. The player hears the outside world but cannot access it. |
| **Abstract / Tonal** | Continuous pitched or textural audio that does not represent any specific real-world source. Produces atmosphere through pure sonic quality rather than environmental verisimilitude. |

---

## 12. Music Style

Music style governs the composed or procedurally generated layer above the soundscape. Unlike the soundscape, which is continuous, music may be triggered by proximity, state change, or puzzle progression. The relationship between music and silence is itself a design decision.

| Option | Description |
|:---|:---|
| **Tense Ambient** | Slow-moving harmonic content with long sustains and unresolved harmonic tension. Produces sustained psychological pressure without rhythmic pulse. *Examples: Ólafur Arnalds, Ben Frost.* |
| **Orchestral** | Scored for traditional instruments; communicates emotional specificity and narrative weight. Requires careful management to avoid overwhelming environmental audio. |
| **Silence / No Music** | No scored layer is present. The soundscape and diegetic audio carry the full atmospheric load. A deliberate absence that communicates severity, realism, or restraint. |
| **Lo-fi / Understated** | Low-fidelity production, minimal arrangement, and muted dynamics. Communicates intimacy, age, or a personal rather than cinematic scale. |
| **Procedural / Reactive** | The music responds in real time to player state, proximity, or puzzle progress. Requires Blueprint or audio middleware integration. *Examples: Dead Space's procedural fear system.* |
| **Dark Electronic** | Synthesiser-based, rhythmically complex or arrhythmic, with a cold or industrial quality. Communicates technology, threat, or systemic menace. |
| **Folk / Acoustic** | Stringed instruments, voice, or traditional forms. Communicates cultural specificity, intimacy, or a world with historical depth. |
| **Choral / Sacred** | Voices, often wordless, associated with ritual or spiritual context. Communicates scale, solemnity, or the presence of forces larger than the individual. |
| **Dissonant / Atonal** | Harmonic language that refuses resolution. Produces sustained cognitive and emotional discomfort. Used in contexts where the player's sense of normality is being deliberately undermined. |

---

## 13. UI Approach

The UI approach governs how game-state information is communicated to the player and whether that communication acknowledges or conceals the artifice of the game interface. This choice has direct implications for the ICA's interaction system requirements.

| Option | Description |
|:---|:---|
| **Diegetic Only (no HUD)** | All information exists within the world — on screens, notes, physical objects. There is no interface layer separate from the game world. Maximum immersion; maximum production complexity. *Examples: Dead Space's health spine, Firewatch's map.* |
| **Minimal HUD** | A small number of interface elements are present on screen — an inventory indicator, a subtle interaction prompt — but they are restrained in visual weight and do not dominate the player's field of view. |
| **Full HUD** | A complete heads-up display communicates all relevant game state: health, inventory, objectives, interaction prompts. Communicates game conventions clearly but at the cost of world immersion. |
| **No UI at All** | There is no interface layer of any kind. The player must infer all state from environmental observation. Used in Walking Sim and narrative contexts where interactivity is minimal. |
| **Hybrid (diegetic + minimal HUD)** | World-embedded information is primary; a minimal interface layer handles edge cases — brief interaction prompts or inventory states that cannot be communicated diegetically without confusion. The most common production choice for atmospheric first-person games. |

---

## 14. Core Mechanic / Puzzle Type

The core mechanic is the primary cognitive operation the player must perform to progress. Most escape rooms combine multiple mechanic types, but one should be primary — the operation that defines the experience and that the player will perform most frequently.

| Option | Description |
|:---|:---|
| **Cipher / Code Breaking** | The player must decode a message, sequence, or symbol system using a key found elsewhere in the environment. Requires the player to hold two pieces of information simultaneously and apply one to the other. |
| **Physical Manipulation** | The player must interact with objects in the world — rotating, placing, combining, or aligning them — to produce a visible change. Requires precise spatial awareness and often communicates progress through immediate visual feedback. |
| **Logic Puzzle** | A formal deductive system: given a set of constraints, what is the only valid solution? The player must eliminate possibilities rather than discover information. |
| **Narrative Discovery** | The puzzle is solved by understanding the story. Documents, objects, and spatial arrangements contain information that, when correctly interpreted, reveals the action the player must take. |
| **Pattern Recognition** | The player must identify a repeating or structured relationship between elements in the environment and apply it to a lock or mechanism. |
| **Observation** | The solution is present in the environment and visible from the moment the player enters the space. The challenge is noticing what is already there. The hardest puzzle type to balance — too obvious and it lacks satisfaction; too subtle and it frustrates. |
| **Sequencing** | The player must determine or discover the correct order in which to perform a set of actions. Incorrect sequences may reset state or produce penalties. |
| **Hidden Object** | An item or piece of information is concealed within the environment and must be located before progress is possible. Requires thorough spatial examination and rewards careful movement through the space. |
| **Inventory Combination** | Two or more collected items must be combined to produce a new object or capability. The logic of which items combine and why must be communicated clearly or the mechanic produces frustration rather than satisfaction. |
| **Environmental Storytelling** | Reading the room is the puzzle. The player must reconstruct an event or understand a relationship from the physical evidence available. There is no lock to open — only an interpretation to reach. |
| **Misdirection** | The player is directed toward a false solution before the real one becomes available. Requires careful design to ensure the false lead feels fair in retrospect. |
| **Teamwork-Dependent** | The puzzle is designed to require multiple players to solve simultaneously or in coordination. Not applicable to solo ICA contexts unless the mechanic is simulated within a single-player framework. |

---

## 15. Puzzle Complexity

Puzzle complexity describes the structural relationship between the puzzle's components — how many steps are required, whether those steps are dependent on each other, and whether the player can be working on multiple components simultaneously.

| Option | Description |
|:---|:---|
| **Single-step** | One action solves the puzzle. The entire experience turns on a single moment of insight and execution. Very difficult to make satisfying at Stage 4 level without exceptional execution. |
| **Multi-step linear** | The player must complete steps A, then B, then C in sequence. Each step unlocks or enables the next. The critical path is clear; the challenge is finding and completing each step. The most common and manageable structure for the ICA scope. |
| **Multi-step branching** | Some steps can be completed in multiple orders, or multiple paths converge on the same solution. Increases apparent complexity without requiring more content; requires careful state management. |
| **Layered / Compounding** | Each discovery adds a new layer of meaning to information the player already holds. Early clues are incomplete; they become interpretable only after later discoveries. The most sophisticated structure and the most demanding to design fairly. |
| **Parallel (multiple active at once)** | The player can be working on multiple puzzle threads simultaneously. Requires the environment to support multiple active investigation states without confusion. Significant Blueprint state management overhead. |

---

## 16. Estimated Play Time

Play time is a design target, not a prediction. The estimate entered here should drive scope decisions throughout production. A room sized for 60 minutes of exploration with puzzles scoped for 30 minutes will frustrate players; a room built for 30 minutes with content sufficient for 60 will lose them.

| Option | Description |
|:---|:---|
| **30 mins** | A very contained experience. One primary puzzle with one or two supporting elements. Extremely limited spatial scope — likely a single functional zone. Appropriate for high-polish, low-scope approaches. |
| **45 mins** | A tight, well-paced experience. Two or three distinct puzzle elements; enough spatial variety to support meaningful navigation. The recommended minimum for a satisfying escape room experience. |
| **60 mins** | The standard commercial escape room duration. Sufficient space for three puzzle elements, a clear spatial grammar, and a structured three-beat narrative arc. The recommended target for this ICA. |
| **75 mins** | An extended experience requiring careful pacing to prevent drag. Every element must earn its place; dead time is more costly at this duration. |
| **90 mins** | The upper limit of the commercial escape room format. Very few single-room experiences sustain engagement at this duration without exceptional content density and pacing. Approach with caution at this production stage. |

---

## 17. Primary Asset Source

Asset source describes the origin of the three-dimensional content populating the scene. This is a production transparency declaration, not a quality judgment. All sources are acceptable; the critical requirement is that the source is declared and that assets are integrated at consistent quality and scale.

| Option | Description |
|:---|:---|
| **Original / Custom** | All assets were created by the student for this project. Guarantees full control over visual style, scale calibration, and material quality. Most time-intensive approach. |
| **Marketplace / Free Assets** | Assets were sourced from Fab, Quixel Megascans, or equivalent sources. Fast production; requires curation for style consistency, scale calibration against the mannequin, and performance optimisation. |
| **Mixed (original + marketplace)** | Hero and signature assets are custom; environment dressing and supporting props are sourced. The most common commercial approach. Custom assets should be identifiable by their importance in the narrative, not compensating for a lack of available alternatives. |

---

## 18. Keyword 1 — Design Quality

Design quality keywords describe the craft-level characteristics of the experience as a designed object. These are the qualities a designer or critic would identify when evaluating the work independently of its emotional effect on the player.

| Option | Description |
|:---|:---|
| **Cohesive** | All elements — visual, audio, narrative, mechanical — operate according to the same internal logic. Nothing contradicts the experience's identity. |
| **Fair** | The player is never required to know something the game has not communicated. Every challenge is solvable from within the game's own evidence. |
| **Elegant** | The design achieves its goals with the minimum number of elements. Nothing is redundant; nothing is missing. |
| **Clear** | The player always knows what they are supposed to do, even if they do not yet know how to do it. Goals are communicated; progress is legible. |
| **Purposeful** | Every element — every prop, every light, every sound — exists for a reason. Set dressing is narrative evidence, not decoration. |
| **Balanced** | Challenge and reward are calibrated against each other. No single element is so easy it provides no satisfaction or so difficult it produces frustration rather than engagement. |
| **Focused** | The experience does not dilute its identity by pursuing too many goals simultaneously. There is a clear primary intention that all other decisions support. |
| **Layered** | Multiple levels of meaning, challenge, or reward exist simultaneously. Attentive players receive more than inattentive ones without the core experience being withheld. |
| **Intuitive** | Interaction conventions are self-evident or consistent with established expectations. The player does not need to be taught; they discover by doing. |
| **Meaningful** | The actions the player performs have narrative or emotional weight beyond their mechanical function. Pressing a button is also doing something in the story of the space. |
| **Consistent** | Rules, visual conventions, and interaction responses behave the same way throughout the experience. Inconsistency produces distrust; consistency produces confidence. |
| **Polished** | The surface quality of every element has been attended to. Rough edges, clipping geometry, and unresolved transitions have been addressed. |
| **Deliberate** | Every decision — including decisions that might appear accidental or informal — was made consciously and with intent. |
| **Restrained** | The design does not overexplain, over-decorate, or over-signal. It trusts the player to complete what the environment begins. |
| **Readable** | The spatial and visual language of the experience can be understood at a glance. Hierarchy is clear; important elements are distinguishable from supporting ones. |

---

## 19. Keyword 2 — Player Experience

Player experience keywords describe the subjective state of a player moving through the experience — what they feel, what they are motivated to do, and how they relate to the designed space. These are the qualities a playtester would articulate in a post-session interview.

| Option | Description |
|:---|:---|
| **Immersive** | The player forgets they are playing a game. The world is convincing enough to produce genuine spatial and emotional investment. |
| **Satisfying** | Actions produce a felt sense of completion — the click of a mechanism engaging, the visual confirmation of a state change, the resolution of a tension that has been building. |
| **Challenging** | The player's skills and knowledge are genuinely tested. Progress requires effort; success is earned. |
| **Rewarding** | Discovery and completion produce a positive response that is proportional to the effort expended. The player feels that their investment was worthwhile. |
| **Engaging** | The player does not want to stop. The experience sustains attention across its full duration without relying on compulsion or artificial urgency. |
| **Surprising** | The experience contains moments the player did not anticipate. The surprises feel earned rather than arbitrary — the player can, in retrospect, see how they should have seen it coming. |
| **Empowering** | The player feels capable and in control of their own progression. Agency is genuine; the player's choices matter. |
| **Thought-provoking** | The experience generates questions or associations that persist after the session ends. The player continues to think about it. |
| **Accessible** | The experience is legible and completable by its intended audience without requiring specialised prior knowledge or exceptional skill. |
| **Cathartic** | The experience provides emotional release — tension that has been built is resolved; grief or frustration finds a form and a conclusion. |
| **Curious** | The player is in a sustained state of inquiry. Every discovery prompts a new question; the experience is structured as a series of answered and replaced unknowns. |
| **Disorienting** | The player's spatial or cognitive orientation is productively compromised. Confusion is a designed experience rather than an oversight. |
| **Absorbing** | The player is consumed by the task. Time passes without notice; external distractions recede. |
| **Propulsive** | Each completed element immediately generates the motivation to continue. The experience has forward momentum; the player never needs to be pushed. |
| **Tense** | The player is in a state of sustained anticipatory alertness. The source of tension may be physical danger, time pressure, or the fear of making a mistake. |

---

## 20. Keyword 3 — Narrative / Atmosphere

Narrative and atmospheric keywords describe the qualities of the world and story as experienced through the environment. These are the qualities that define the space as a place — a location with identity, history, and weight — rather than merely a geometry container.

| Option | Description |
|:---|:---|
| **Atmospheric** | The space produces a sustained, holistic sensory and emotional impression that is greater than the sum of its individual elements. |
| **Thematic** | Every element connects to and reinforces a central idea. The space is not just a location — it is an argument or a statement about something. |
| **Evocative** | The environment produces associations and emotional responses beyond what is explicitly present. The space implies more than it shows. |
| **Grounded** | The world feels physically and historically credible. Objects have weight, age, and plausible origins. Nothing floats free of causality. |
| **Believable** | The player accepts the logic of the space without resistance. Its rules are internally consistent and communicated clearly enough that nothing breaks the contract. |
| **Symbolic** | Objects and spatial relationships carry meaning beyond their literal function. The key is not just a key; the locked door is not just an obstacle. |
| **Paced** | The atmospheric register shifts deliberately across the experience — building, releasing, building again. The player is not held at a single emotional pitch throughout. |
| **Textured** | The world has depth and variety at close inspection. Surfaces, objects, and spatial details reward attention and support the sense that the space was inhabited and used rather than constructed. |
| **Resonant** | The experience produces an emotional response that feels proportional and genuine — not manufactured, not hollow. The player is moved because the design earns the response. |
| **Layered** | Multiple narrative or atmospheric meanings coexist simultaneously. A single object or arrangement can be read several ways; the most attentive reading is the most rewarding. |
| **Understated** | The narrative does not announce itself. Meaning is present but not insisted upon; the player discovers it rather than being told it. |
| **Vivid** | The world has immediate, strong sensory presence. Colours, sounds, and spatial contrasts are intense enough to produce a clear and memorable image. |
| **Anchored** | The experience has a strong sense of place — the player knows exactly what kind of world they are in and what that world's rules are. The space is not generic; it is specific. |