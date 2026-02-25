<style>
/* Generic table styling */
table { border-collapse: collapse; width: 100%; }
th, td { padding: .55rem .7rem; border: 1px solid #e5e7eb; }

/* Header color */
thead th { background: #6ec56eff; color: #fff; }

/* Justify normal body text (not headings) */
p { text-align: justify; }

/* Optional: better spacing & hyphenation */
p {
  hyphens: auto;
  overflow-wrap: anywhere;
  line-height: 1.6;
}

/* Don't justify code blocks/lists by mistake */
pre, code, kbd, samp, li { text-align: left; }
</style>

# 3D Game Development - Notes & Briefs

This repository contains all notes and assignment briefs materials for **COMP I8015 — 3D Game Development**. 

- The **Notes** folder holds a seven-part  series on interior level design for Unreal Engine. 
- The **Briefs** folder contains the formal CA briefs for all assessed components.

## Table of Contents

| # | Filename | Description | Link |
|:--|:---------|:------------|:-----|
| 1| `interior_level_design.md` | Interior Level Design — Spatial grammar, lighting hierarchy, object hierarchy, and production discipline for enclosed spaces | [Interior Design](Notes/interior_level_design.md) |
| 2 | `interaction_design.md` | Interaction Design — The three verbs (Examine / Collect / Modify): spatial placement, feedback obligations, UI requirements, and gating as narrative | *(Work In Progress)* |
| 3 | `puzzle_architecture.md` | Puzzle Architecture and State Management — Designing puzzles as state machines, causal chains, gating patterns, and dead-end prevention | *(Work In Progress)* |
| 4 | `storytelling_through_materials.md` | Storytelling Through Materials — Substrate layering, surface narrative, roughness and value as storytelling signals, custom material authorship | *(Work In Progress)* |
| 5 | `atmosphere_and_feedback.md` | Atmosphere and Feedback — Niagara VFX as a design tool, Blueprint-driven light state transitions, and non-UI feedback design | *(Work In Progress)* |
| 6 | `camera_design.md` | Camera Design and Cinematic Progression — Sequencer fundamentals, reveal framing, camera timing, and clean return-to-player patterns | *(Work In Progress)* |
| 7 | `playability_and_polish.md` | Playability, Iteration, and the Final Craft Pass — Readability audits, structured playtesting, iterating from feedback | *(Work In Progress)* |

## CA Briefs

| CA | Filename | Description | Keywords | Link |
|:---|:---------|:------------|:---------|:-----|
| ICA-1 | `2025-26-gd-3dgd-ica-1.md` | Individual CA — Single room-based Interactive Micro-Experience. Design and implement a contained escape-room in Unreal Engine demonstrating craft in environment design, materials, lighting, interaction logic, and iteration. | escape room, Examine, Collect, Modify, Substrate material, Niagara VFX, camera sequence, environmental storytelling, Blueprint, puzzle design | [2025-26 - ICA-1](Briefs/2025-26-gd-3dgd-ica-1.md) |
| GCA-1 | `2025-26-gd-3dgd-gca-1.md` | Group CA — User Testing Lab Report. Design and conduct two rounds of user testing for the team game, analyse the results statistically, and produce a written lab report in Quarto. | user testing, playtest, statistical analysis, confidence interval, correlation, Quarto, lab report, summary statistics, hypothesis testing | [2025-26 - GCA-1](Briefs/2025-26-gd-3dgd-gca-1.md) |
