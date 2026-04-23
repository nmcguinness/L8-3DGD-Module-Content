---
title: "Ten-Step Performance Improvement Guide"
subtitle: "A Practical Checklist for the Final Weeks of Development"
author: "Niall McGuinness"
institute: "Dundalk Institute of Technology"
programme: "BSc (Hons) in Computing in Games Development"
module_code: "COMP I8015"
module_title: "3D Game Development"
stage: 4
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

<style>
table { border-collapse: collapse; width: 100%; }
th, td { padding: .55rem .7rem; border: 1px solid #e5e7eb; }
thead th { background: #6ec56e; color: #fff; }
p { text-align: justify; }
p {
  hyphens: auto;
  overflow-wrap: anywhere;
  line-height: 1.6;
}
pre, code, kbd, samp, li { text-align: left; }
</style>

# Performance & Optimisation: Ten-Step Performance Improvement Guide

> You have only a short number of weeks left in your Collaborative Project work. This guide is ordered by impact-per-hour. Work through it in sequence — do not skip to later steps without completing earlier ones, because later steps assume you already know where your bottleneck is. Each step names what to do, how long it should take, and how to confirm it worked. 
> 
---

## Overview

| Step | Area |Primary gain |
| :-- | :-- | :-- |
| 1 | Profiling | Identifies bottleneck — unlocks all other steps |
| 2 | Blueprint | CPU frame time reduction |
| 3 | Light mobility | GPU frame time reduction |
| 4 | Shadow casting | GPU frame time reduction |
| 5 | Textures and materials | VRAM reduction, GPU shader cost |
| 6 | LODs and draw calls | GPU frame time reduction |
| 7 | Niagara VFX | GPU translucency cost reduction |
| 8 | Audio | Memory and load time reduction |
| 9 | Collision | CPU physics query cost reduction |
| 10 | Build and package | Load time and shader compilation reduction |

---

## Step 1 — Profile First, Fix Second

**Before changing anything, find out what is actually slow.**

Run a Play-In-Editor session and enter `stat unit` in the console (backtick `` ` ``). The field with the highest value is your bottleneck. The other fields are not the problem — do not optimise them yet.

| `stat unit` field is high | Go to |
| :-- | :-- |
| **Game** | Step 2 — Blueprint |
| **GPU** | Steps 3–7 — Rendering, Materials, VFX |
| **Draw** | Step 6 — LODs and draw calls |
| **DynRes below 90%** | GPU bottleneck — engine is already compensating |

Once you know which thread is the problem, run the second-level command for that area: `stat game` if Game is high; `stat gpu` if GPU is high (output is now split into **Graphics** and **Compute** totals — check which is higher). Use `dumpticks` if `stat game` is high but the cause is not obvious.

**Verify:** After any change, re-run `stat unit` and confirm the target field dropped. If it did not, the change did not address the actual bottleneck.

---

## Step 2 — Fix Blueprint: Cache, Stop Ticking, Stop Polling

**The fastest CPU wins come from Blueprint. Most projects have several of these problems simultaneously.**

Audit every Blueprint Actor in your project that has a **Tick** event. For each one:

- **Cache component references.** Any call to `GetComponentByClass`, `GetActorOfClass`, or a named component getter inside Tick must be moved to **BeginPlay** and stored in a variable. A search in every Tick graph for "GetComponent" will find them quickly.
- **Disable Tick on Actors that do not need it.** If an Actor only responds to overlaps, timers, or delegates, open its Class Defaults and uncheck **Start with Tick Enabled**. Run `dumpticks` before and after to confirm the Actor is no longer ticking.
- **Cache cast results.** Any `Cast To` node inside Tick must be moved to BeginPlay or to the first valid event (overlap, damage, interaction) and stored in a typed variable.
- **Replace polling with events.** A `Branch` node in Tick checking a condition every frame should become an `OnComponentBeginOverlap`, `OnTakeAnyDamage`, or Event Dispatcher binding instead.

**Verify:** `stat game` value should drop noticeably. Confirm with `dumpticks` that unexpected Actors are no longer in the tick list.

---

## Step 3 — Audit Light Mobility

**Movable lights recalculate shadows every frame. Most lights in a static interior should not be Movable.**

Select every light in your scene and check its **Mobility** setting in the Details panel. For each light:

- If it does not move, change colour, or toggle at runtime: set to **Stationary**.
- If it is not needed for dynamic GI or real-time shadow updates: set to **Static** and rebuild lighting.
- Reserve **Movable** only for lights that genuinely animate or switch during gameplay — a flickering candle, a torch that turns on when a puzzle is solved.

After changing mobilities, go to *Build → Build Lighting Only* to update the lightmap. Any mesh showing a red **Lighting Needs to be Rebuilt** indicator must be rebuilt before the change takes effect.

**Verify:** `stat gpu` Compute total (Lumen) and Shadow Depths in the Graphics total should both drop. `stat unit` GPU time should decrease.

---

## Step 4 — Disable Shadow Casting on Small Props

**Shadow maps are calculated for every shadow-casting mesh within each light's radius. Small props rarely cast legible shadows but still pay the full cost.**

Select every prop under approximately 30cm in its largest dimension — books, bottles, cables, cups, scattered items — and in the Details panel under **Lighting**, uncheck **Cast Shadow**. Do the same for any prop that sits flush against a wall (its shadow would fall behind it, invisible to the player).

A fast way to catch most of these at once: in the **World Outliner**, sort by type, select all Static Mesh Actors, then filter the Details panel for "Cast Shadow" and bulk-edit the selection. Only uncheck for props you have confirmed are small or occluded.

Reduce the **Attenuation Radius** of every Point and Spot light to the minimum that covers its intended area. An oversized radius includes more geometry in the shadow pass unnecessarily.

**Verify:** `stat gpu` Shadow Depths entry in the Graphics total should drop. More lights in a smaller radius means fewer shadow-casting primitives per light.

---

## Step 5 — Fix Textures and Materials

**VRAM waste and excess shader cost come from three common mistakes: wrong compression, wrong sRGB setting, and duplicated material graphs.**

Work through these in order:

**Texture size.** Open each texture in the Texture Editor. Hero props seen up close: 2048×2048 maximum. Mid-distance props: 1024×1024. Small or distant props: 512×512 or smaller. All textures must have power-of-two dimensions (256, 512, 1024, 2048) or mipmapping will not function.

**Compression and sRGB.** Set **Compression** to `Default` for albedo, `Normalmap` for normal maps, `Masks` (no sRGB) for roughness/metallic/AO packed textures. Confirm **sRGB is ON** for albedo and **OFF** for normal maps and mask textures — incorrect sRGB on a normal map produces subtle incorrect shading that is hard to diagnose.

**Material Instances.** Any two materials that share the same graph but differ only in colour, roughness, or emissive value should be replaced with a single **Material** with those values exposed as **Parameters**, and individual **Material Instances** per prop. Right-click a Material → *Create Material Instance*. This reduces the shader permutation count and eliminates redundant draw state changes.

**Verify:** Check VRAM usage with `stat memory`. Check shader instruction count in the Material Editor Stats panel — target under 150 for a standard surface material.

---

## Step 6 — Set Up LODs and Reduce Draw Calls

**Every unique mesh-material pair visible to the camera is a separate draw call. Two techniques address this: LODs reduce polygon cost at distance, and HISM batches repeated instances into one draw call.**

**LODs.** Open any prop with over 500 triangles in the Static Mesh Editor. Go to *LOD Settings*, set **Number of LODs** to 2 or 3, and click **Auto Generate**. Review the generated meshes and confirm transitions are not visible during normal gameplay. For escape room props, LOD 1 at 50% reduction is typically sufficient.

**Hierarchical Instanced Static Mesh (HISM).** Any prop that appears more than four or five times in your level — floor tiles, identical chairs, repeated wall props — should be replaced with a HISM. Select all instances of the prop in the level, right-click → *Replace Selected Actors with* a Blueprint containing a `HierarchicalInstancedStaticMeshComponent`, and use `AddInstance` to place each copy. All instances become one draw call.

Run `stat scenerendering` and check **Mesh draw calls**. Target: under 1500 for a smooth interior scene.

**Verify:** `stat scenerendering` Mesh draw calls count should drop. `stat gpu` BasePass in the Graphics total should decrease.

---

## Step 7 — Audit Niagara VFX Budgets

**Particle systems accumulate. Each emitter is inexpensive; ten emitters in one room are not.**

For every Niagara system in your level:

- Open the system and check **active particle count** during simulation. Keep ambient emitters (dust, mist) under 100 active particles. Keep burst emitters (feedback sparks, steam puffs) under 60.
- Set a **LOD Distance** on each system: *System Properties → Scalability → Add LOD*. Set the spawn rate to zero beyond 800–1200cm. Particles the player cannot see should not be simulating.
- If any emitter is set to **GPU Simulation**, confirm particle counts genuinely warrant it. GPU simulation has overhead; for counts under 200, CPU simulation is usually cheaper overall.

Run `stat gpu` and check the **Translucency** entry in the Graphics total before and after removing or reducing emitters. This is where all particle rendering cost appears.

**Verify:** `stat gpu` Translucency should drop. Frame time should be stable rather than varying with camera angle toward particle-heavy areas.

---

## Step 8 — Fix Audio Compression and Streaming

**Uncompressed audio assets are the most commonly overlooked source of memory waste in student projects. They also increase load times.**

Open each Sound Wave asset in your project and check its **Compression** settings:

| Audio type | Correct compression | Streaming |
| :-- | :-- | :-- |
| Short SFX (< 5 seconds) | `ADPCM` or `PCM` | Off |
| Long ambient loops (> 5 seconds) | `Opus` (best ratio) or `Vorbis` | **On** |
| Music tracks | `Opus` | **On** |

Enable **Streaming** on all assets over five seconds. Streaming loads audio from disk on demand rather than holding it all in memory. For a project with several ambient loops and a music track, this alone can reduce audio memory by 60–80%.

Check the **Quality** slider — the default (100) is uncompressed. For `Opus` compression, a quality setting of 40–60 is transparent to the listener and dramatically smaller.

**Verify:** `stat memory` — check the **Audio** category before and after. Total audio memory should drop significantly after enabling streaming and setting compression.

---

## Step 9 — Simplify Collision Geometry

**Complex collision — mesh-accurate physics shapes on every prop — is one of the quietest performance costs in student projects. The physics engine processes every query against every complex collision mesh every frame.**

For every Static Mesh that a player walks near but does not interact with physically (decorative props, wall-mounted items, ceiling fixtures), open the Static Mesh Editor and set **Collision Complexity** to `Use Simple Collision As Complex`. Then assign a simple collision shape — a box, sphere, or convex hull — from the **Collision** menu.

For props that should have no physical interaction at all (small decorative items above player height, paintings, distant background props), set **Collision Presets** to `NoCollision` in the Details panel.

Reserve **Use Complex Collision As Simple** (mesh-accurate collision) only for geometry the player must walk on or interact with precisely — floor surfaces with unusual shapes, puzzle prop surfaces that require exact hit detection.

**Verify:** With `stat game` active, compare Game thread time before and after. Physics query cost reduction appears here. `stat physics` can also be used for a more specific breakdown if needed.

---

## Step 10 — Clean Up the Build

**The final pass removes dead weight that accumulates during development: unused plugins, unreferenced assets, redundant shader permutations, and debug content that should not ship.**

Work through each item:

**Disable unused plugins.** Go to *Edit → Plugins*. Disable any plugin your project does not actively use — each enabled plugin compiles shaders and increases editor startup time. Common ones to check: VR frameworks, platform SDKs, experimental features enabled during earlier experimentation.

**Run the Reference Viewer on large assets.** Right-click any large texture or mesh in the Content Browser → *Reference Viewer*. Assets with no references to your map or any active Blueprint are safe to delete or exclude from the cook.

**Remove dev-only content from the build.** Floating text labels, debug collision spheres, visible nav meshes, test Blueprints, and placeholder meshes should be deleted from the level or placed in a separate development-only level that is excluded from the final build.

**Check packaging settings.** In *Project Settings → Packaging*, confirm **Use Pak File** is enabled, **Share Material Shader Code** is enabled, and any maps not used in the final build are removed from the **Maps to include** list. Fewer maps = fewer shaders cooked = faster packaging and smaller build.

**Verify:** Package the project (*Platforms → Windows → Package Project*) and check the output size and cook time. Compare against a previous package if available. Launch the packaged build and re-run `stat unit` — packaged builds typically show better performance than PIE due to shader compilation being complete.

---

## Where to Go Deeper

Each step in this guide is a summary. Full technical detail, command references, and worked examples for every topic are in the accompanying notes:

| Topic | Notes document |
| :-- | :-- |
| Profiling (stat unit, stat gpu, Unreal Insights) | [Practical Optimisation in Unreal Engine 5](unreal_optimisation_practical.md) — Section 1 |
| Blueprint caching, tick, cast | [Practical Optimisation](unreal_optimisation_practical.md) — Section 2 |
| Materials, textures, compression | [Practical Optimisation](unreal_optimisation_practical.md) — Section 3 |
| LODs, HISM, draw calls, occlusion | [Practical Optimisation](unreal_optimisation_practical.md) — Section 4 |
| Light mobility and shadow casting | [Practical Optimisation](unreal_optimisation_practical.md) — Section 5 |
| Niagara VFX budgets | [Atmosphere and Feedback](atmosphere_and_feedback.md) — Section 2.4 |

---

## Appendix A — Stat Command Glossary

All stat commands are entered in the editor or in-game console (backtick `` ` ``). Most commands toggle their display on and off — enter the command a second time to dismiss the overlay. Commands marked **[file]** write output to the Output Log or a `.uestats` file rather than displaying on screen.

---

### Frame Timing

| Command | What it shows |
| :-- | :-- |
| `stat fps` | Current frames per second and the raw frame time in milliseconds for the last frame. Colour-coded: green at 60fps+, yellow at 30–59fps, red below 30fps. The simplest first check. |
| `stat unit` | Six values: **Frame** (total wall-clock frame time), **Game** (game thread cost), **Draw** (render thread cost), **GPU** (graphics card cost), **RHIT** (RHI translation thread cost), **DynRes** (current dynamic resolution percentage). The bottleneck is the highest value. From UE 5.6, also displays the current render resolution alongside these values. |
| `stat unitgraph` | The same six values as `stat unit` displayed as a scrolling line graph. Useful for identifying intermittent spikes and frame time variance while moving through the scene, rather than a static number. |
| `stat startfile` | **[file]** Begins recording all active stat groups to a `.uestats` file saved to `[Project]/Saved/Profiling/UnrealStats/`. Use this to capture a session for later analysis in the Unreal Frontend Session Browser. |
| `stat stopfile` | **[file]** Stops a recording started by `stat startfile` and closes the output file. |
| `stat namedevents` | Enables named-event markers in the profiling trace, making custom code-level events visible in Unreal Insights. Can also be passed as `-statnamedevents` on the command line at launch. |

---

### GPU and Rendering

| Command | What it shows |
| :-- | :-- |
| `stat gpu` | Per-pass GPU cost in milliseconds. From UE 5.6, output is divided into **[Graphics]** and **[Compute]** sections. Graphics covers rasterisation passes (shadow depths, base pass, translucency, post-processing). Compute covers compute shader workloads (Lumen GI, GTAO, TSR/TAA). The highest total identifies which pipeline is the bottleneck. |
| `profilegpu` | **[file]** Captures a single GPU frame and writes a detailed table-format breakdown to the Output Log, divided into Graphics and Compute columns. More sub-pass detail than `stat gpu`. The in-editor popup present in earlier versions was removed in UE 5.6; use the Output Log (*Window → Output Log*) and search for `[GPU]` to find the output. |
| `stat scenerendering` | Per-frame rendering counts: **Mesh draw calls** (total draw calls submitted), **Visible static mesh elements** (meshes passing culling), **Frustum culled primitives** (rejected by view frustum), **Occluded primitives** (rejected by occlusion culling). Use when GPU time is high and draw call volume is suspected. Target: under 1500 mesh draw calls for an interior scene. |
| `stat initviews` | Detailed visibility culling metrics: time spent in visibility processing, number of processed primitives, frustum-culled count, and occluded count — split by static and dynamic primitives. More granular than `stat scenerendering` for diagnosing culling problems. |
| `stat rhi` | RHI (Render Hardware Interface) level statistics: render target memory, index/vertex buffer memory, total triangles drawn, and draw primitive call count. Useful for confirming VRAM budget and raw triangle throughput. |
| `stat shadowrendering` | Per-frame shadow map cost: number of shadow-casting lights, shadow depth pass count, and shadow map memory usage. Use when `stat gpu` shows high Shadow Depths cost but you need more detail about which lights are responsible. |
| `stat lightrendering` | Per-frame lighting pass cost: direct and indirect lighting evaluation time. Complements `stat shadowrendering` — shadow depths and lighting evaluation are separate passes. |
| `stat foliage` | Instance count and total triangle count for all Instanced Static Mesh and Hierarchical ISM components in the scene. Use when instanced meshes (foliage, repeated props using HISM) are suspected to be contributing high triangle counts. |
| `stat landscape` | Triangle count and draw calls for all Landscape actors. Use when large outdoor or terrain surfaces are present and contributing to GPU load. |

---

### Memory

| Command | What it shows |
| :-- | :-- |
| `stat memory` | Memory usage broken down by subsystem: physical RAM used, virtual memory, texture memory, mesh memory, audio memory, animation memory, and engine overhead. The most useful starting point for memory budget investigations. |
| `stat streaming` | Texture streaming pool status: current pool size, memory used, pending requests, and whether the pool is over budget. A pool over budget causes visible texture pop-in as the engine swaps textures under pressure. |
| `stat llm` | Low Level Memory Tracker summary — top-level memory categories with total allocation per category. Requires LLM to be enabled at launch (`-LLM` command-line argument). Less granular than `stat llmfull` but fast to read. |
| `stat llmfull` | Full Low Level Memory Tracker output — every tracked allocation category with its current size. Useful for identifying which engine subsystem is consuming unexpected memory. Requires `-LLM` at launch. |
| `stat texturegroup` | Memory consumption broken down by texture group (World, Character, Weapon, UI, etc.). Use when `stat memory` shows high texture memory and you need to identify which texture group is responsible. |

---

### Game Thread and Gameplay Systems

| Command | What it shows |
| :-- | :-- |
| `stat game` | Game thread cost broken down by system: total tick time, Actor tick count, Component tick count, Blueprint execution time, AI evaluation, animation, and physics queries initiated from gameplay code. Use when `stat unit` shows high Game time. |
| `dumpticks` | **[log]** Writes the name and tick function of every Actor and Component currently registered for Tick to the Output Log. Use alongside `stat game` to identify which Actors are unexpectedly ticking. Not a display overlay — check the Output Log after running it. |
| `stat physics` | Physics simulation cost: broadphase collision detection time, narrowphase contact resolution time, and solver iteration time. Use when `stat game` is high and the project uses physics simulations, destructibles, or cloth. |
| `stat anim` | Animation evaluation cost per Skeletal Mesh Component: time spent evaluating animation graphs, blending, and IK. Use when `stat game` is high in projects with animated characters or props using Skeletal Mesh. |
| `stat ai` | AI system tick cost: total time spent in Behaviour Tree evaluation, Environment Query System queries, and perception updates. Use when `stat game` is high in projects with AI-controlled characters. |
| `stat navigation` | NavMesh query cost: time spent on pathfinding requests and navigation updates. Use when `stat game` is high and the project uses AI navigation. |
| `stat asyncloadgame` | Async content loading cost: time spent processing async load requests on the game thread. High values indicate the game is stalling to load content that should have been loaded earlier or streamed differently. |
| `stat levels` | Displays all level streaming states in the current session: each level's name and its current status (Visible, Loading, Unloading, Loaded but hidden). Use when testing level streaming to confirm levels are loading and unloading as expected. |

---

### Particles and VFX

| Command | What it shows |
| :-- | :-- |
| `stat particles` | Total active particle count, sprite count, and mesh particle count across all Niagara and legacy Cascade emitters. Use when `stat gpu` shows high Translucency cost and VFX is suspected. |
| `stat niagara` | Niagara-specific simulation cost: CPU simulation time per system, GPU simulation dispatch count, and total active Niagara component count. More granular than `stat particles` for Niagara-only projects. |

---

### Audio

| Command | What it shows |
| :-- | :-- |
| `au.Debug.Sounds` | Displays active Sound Wave playback information in the viewport: sound name, volume, pitch, and distance from the listener. Equivalent to the older `stat sounds` command. Use to confirm which sounds are currently playing and at what cost. |
| `au.Debug.SoundCues` | Displays active Sound Cue evaluation information: which cues are active, their current node state, and output volume. Use when debugging complex Sound Cue graphs. |
| `au.Debug.SoundMixes` | Displays the state of all active Sound Mix modifiers: which mixes are applied, their current blend state, and the effect on each sound class. |
| `au.DumpActiveSounds` | **[log]** Writes a full list of all currently playing sounds to the Output Log, including their asset name, volume, and attenuation distance. Use when audio memory or voice count is unexpectedly high. |

---

### Profiling Utilities

| Command | What it shows |
| :-- | :-- |
| `stat none` | Clears all active stat overlays from the screen. Equivalent to running each active stat command again individually to dismiss it. |
| `stat slow [threshold] [duration]` | Highlights any stat that exceeds a defined millisecond threshold for a given duration. Useful for surfacing intermittent spikes that are easy to miss in a static numeric display. Example: `stat slow 8 5` flags anything above 8ms for 5 seconds. |
| `stat dumpframe` | **[log]** Writes a complete dump of all stat values for the current frame to the Output Log. Captures a snapshot of every active stat group at once. |
| `stat dumpnonframe` | **[log]** Writes all non-frame-based counters (totals, averages, counts that do not reset each frame) to the Output Log. |
| `stat hitches` | Displays a running count of frames that exceeded a hitch threshold (default: 33ms). Use to detect infrequent hitches that are difficult to observe in normal `stat unit` monitoring. |
| `stat colorlist` | Displays a reference list of all colour-coding conventions used by the stat system overlays. Useful when interpreting colour-coded stat displays for the first time. |

---

### Network (Reference)

These commands are included for completeness. At single-player project scale they will show minimal or zero activity.

| Command | What it shows |
| :-- | :-- |
| `stat net` | Network bandwidth usage: bytes sent and received per second, packet count, packet loss rate, and ping. Use in multiplayer projects to diagnose replication overhead. |
| `stat netpackets` | Per-packet breakdown of network traffic: number of reliable and unreliable packets, bunches, and acknowledgements per frame. More granular than `stat net`. |

---

## Appendix B — `stat unit` Field Reference

`stat unit` is the first command to run when investigating performance. From UE 5.5 onwards it displays up to eleven values simultaneously. The table below explains what each field measures, what constitutes a healthy value, and what action to take when it is not.

**Colour coding** on the timing fields (Frame, Game, Draw, GPU): green indicates the value is within a healthy range for the current frame rate target; yellow is a warning; red indicates a bottleneck. The default thresholds are calibrated for a 30fps target — for a 60fps project, treat yellow as red.

| Field | What it measures | Healthy range (60fps target) | High value means | Action |
| :-- | :-- | :-- | :-- | :-- |
| **Frame** | Total wall-clock time for one complete frame — the time between the start of this frame and the start of the next. This is the value `stat fps` reports as milliseconds, and it is the ceiling all other threads must fit inside. | ≤ 16.67ms | No single thread is close to Frame time → thread synchronisation overhead; one thread is waiting for another | Identify which thread is highest and optimise that one first |
| **Game** | Time the **game thread** spent on all gameplay logic: Blueprint Tick events, Actor and Component updates, AI, animation state machines, physics queries, and all C++ gameplay code. | ≤ 10ms | CPU bottleneck in gameplay code | Step 2 — cache references, disable tick, stop polling |
| **Draw** | Time the **render thread** spent preparing GPU work: building draw call lists, translating scene visibility results into GPU commands, and issuing them to the command queue. Also labelled **RenderThread** in some displays. | ≤ 8ms | Too many draw calls for the render thread to process efficiently | Step 6 — LODs, HISM, reduce draw call count |
| **GPU** | Time the **GPU** spent executing all render passes for this frame. This is almost always the bottleneck in complex interior scenes. Pipelining means GPU time can legitimately be slightly higher than Frame time without being the limiting factor. | ≤ 14ms | GPU-bound — a rendering pass is too expensive | Run `stat gpu`; check Graphics vs Compute totals; Steps 3–7 |
| **RHIT** | Time the **Render Hardware Interface Thread** spent translating engine render commands into platform API calls (DirectX 12, Vulkan). Normally runs in parallel with the render thread and is rarely the bottleneck. | ≤ 4ms | Driver or platform issue; not a scene complexity problem at this value | Check driver version; at extreme values (>12ms independent of Draw) investigate RHI settings |
| **DynRes** | Current **Dynamic Resolution** scaling percentage. When GPU load is high, the engine reduces the internal render resolution to maintain frame rate. 100% means rendering at native resolution; lower values mean the engine is compensating for GPU pressure. | 100% | GPU is under pressure; engine is already reducing quality to cope | Treat as GPU bottleneck — the scene needs GPU optimisation even if frame rate appears acceptable |
| **Input** | Time spent processing **input events** on the game thread before the frame begins. Added in UE 5.5. **Note:** this field has a known inflation issue present in UE 5.5 and 5.6 where it reports 60–85ms even on blank projects; as of UE 5.7 this may or may not be fully resolved. Cross-reference with behaviour — if the game feels responsive, an elevated Input value is likely the known issue rather than a genuine problem. | ≤ 2ms under normal conditions | Input processing overhead, or the known engine-side inflation issue | If gameplay feels unresponsive, investigate input binding complexity; otherwise treat with caution pending Epic documentation |
| **Mem** | Current process **resident memory** usage in megabytes — the physical RAM the engine process is actively consuming, including all loaded assets, engine systems, and OS-level overhead. | < 3,000MB on a 8GB machine; watch for gradual increase over a session | Excessive asset memory, memory leaks, or unstreamed content | Run `stat memory` and `stat llm` to break down by subsystem; enable streaming on large audio and texture assets |
| **RenderRes** | The **internal render resolution** currently being used by the renderer, shown as pixel dimensions (e.g. `1920×1080`). When Dynamic Resolution is active and DynRes drops below 100%, this value decreases accordingly. Added in UE 5.6. | Native display resolution (e.g. `1920×1080` or `2560×1440`) | Dynamic Resolution is active and reducing quality due to GPU pressure | Address GPU bottleneck; DynRes field will confirm |
| **Draws** | Total number of **DrawPrimitive calls** submitted to the GPU this frame. Each unique visible mesh-material pair is one draw call. Includes geometry, decals, shadow passes, translucent volumes, and post-processing — not just visible world meshes. | < 1,500 for a contained interior scene | Too many unique mesh-material combinations visible simultaneously | Step 6 — LODs, HISM, material instancing, occlusion review |
| **Prims** | Total **triangles** sent to the GPU this frame, after frustum and occlusion culling. Reflects the polygon complexity of everything the renderer actually processed. | < 1,000,000 (1M) triangles per frame | High-polygon meshes without LODs, or poor occlusion culling allowing distant geometry through | Step 6 — add LODs to complex meshes; review occlusion culling |

### Reading the Fields Together

The fields are most useful in combination. Some common patterns and what they mean:

| Pattern | Interpretation |
| :-- | :-- |
| Frame high, Game high, GPU low | CPU-bound on gameplay code — Blueprint optimisation will recover the most frame time |
| Frame high, Game low, GPU high | GPU-bound — the graphics card is the bottleneck; rendering optimisation needed |
| Frame high, Draw high, GPU low | Render thread is overloaded preparing draw calls — high Draws count is usually the cause |
| Frame high, all threads moderate | Thread synchronisation stall — one thread finishing late forces all others to wait; Unreal Insights will identify which |
| DynRes below 90% consistently | GPU is already under enough pressure that the engine is compensating by reducing resolution — the GPU situation is worse than frame rate alone suggests |
| Draws high, Prims low | Many small simple meshes — instancing (HISM) will help more than LODs |
| Draws low, Prims high | Few large complex meshes — LODs will help more than instancing |
| Input above 10ms | Either the known inflation issue (UE 5.5–5.6) or genuine input processing overhead; check responsiveness and cross-reference with a blank project to distinguish |

