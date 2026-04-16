# 3D Game Development - Notes & Briefs

This repository contains all notes and assignment briefs materials for **COMP I8015 — 3D Game Development**. 

- The **Notes** folder holds a multi-part series on interior level design for Unreal Engine. 
- The **Briefs** folder contains the formal CA briefs for all assessed components.
- The **Labs** folder contains the lab exercises for the content listed in the TOC.
- The **Reference** folder contains supporting reference documents for use throughout the module.


## Briefs

| CA | Filename | Description | Keywords | Link |
|:---|:---------|:------------|:---------|:-----|
| ICA-1 | `2025-26-gd-3dgd-ica-1` | Individual CA — Single room-based Interactive Micro-Experience. Design and implement a contained escape-room in Unreal Engine demonstrating craft in environment design, materials, lighting, interaction logic, and iteration. | escape room, Examine, Collect, Modify, Substrate material, Niagara VFX, camera sequence, environmental storytelling, Blueprint, puzzle design | [2025-26 - ICA-1](Briefs/2025-26-gd-3dgd-ica-1.md) |
| ICA-2 | `2025-26-gd-3dgd-ica-2.2` | Individual CA — Technical Specialisation within Collaborative Project (Stage 2). Extend the Semester 1 technical specialisation into a developed Unreal-focused contribution, documented through a single Mahara page and a final screencast. | technical specialisation, collaborative project, Unreal Engine, Mahara, screencast, iteration, critical analysis, individual contribution, portfolio | [2025-26 - ICA-2.2](Briefs/2025-26-gd-3dgd-ica-2.2.md) |
| GCA-1 | `2025-26-gd-3dgd-gca-1` | Group CA — User Testing Lab Report. Design and conduct two rounds of user testing for the team game, analyse the results statistically, and produce a written lab report in Quarto. | user testing, playtest, statistical analysis, confidence interval, correlation, Quarto, lab report, summary statistics, hypothesis testing | [2025-26 - GCA-1](Briefs/2025-26-gd-3dgd-gca-1.md) |

## Reference

| Filename | Description | Link |
| :- | :- | :- |
| `game_design_field_guide` | **ICA Concept Sheet — Field Reference Guide** — Definitions and design implications for every dropdown option in the ICA Concept Spreadsheet. Covers genre, visual style, colour palette, setting, narrative tone, mood, lighting, camera, audio, UI approach, puzzle type and complexity, play time, asset source, and the three design keyword columns. Use alongside the concept spreadsheet when completing or revising your ICA concept entry. | [ICA Concept Sheet — Field Reference Guide](Reference/game_design_field_guide.md) |

## Notes - Design to Implementation

| # | Filename | Description | Link |
|:--|:---------|:------------|:-----|
| 1 | `interior_level_design` | **Interior Level Design** — Spatial grammar, lighting hierarchy, object hierarchy, and production discipline for enclosed spaces | [Interior Level Design](Notes/interior_level_design.md) |
| 2 | `interaction_design` | **Interaction Design** — Designing clue-driven interactions through observation, inference, and consequence. Covers clue loops, clue chains, prop readability, and the use of Examine, Collect, and Modify to create a satisfying puzzle solving player experience. | [Interaction Design](Notes/interaction_design.md) |
| 3 | `puzzle_architecture` | **Puzzle Architecture and State Management** — Designing puzzles as state machines, causal chains, gating patterns, dead-end prevention, and Blueprint orchestration using the Game State Actor pattern | [Puzzle Architecture and State Management](Notes/puzzle_architecture.md) |
| 4 | `atmosphere_and_feedback` | **Atmosphere and Feedback** — Niagara VFX as a design tool, Blueprint-driven light state transitions, and non-UI feedback design | *(Work In Progress)* |
| 5 | `camera_design` | **Camera Design and Cinematic Progression** — Sequencer fundamentals, reveal framing, camera timing, and clean return-to-player patterns | *(Work In Progress)* |
| 6 | `testing_analysis_evidence_based_evaluation` | **Testing Analysis And Evidence-based Evaluation** — Validation testing, comparative A/B analysis, independent/dependent/confounding variable identification, readability audits, and structured iteration tied to GCA1 deliverables | [Testing Analysis And Evidence-based Evaluation](Notes/testing_analysis_evidence_based_evaluation.md) |

## Labs

| Nr | CA | Filename | Description | Link |
| :- | :- |:-| :- | :- |
| 1 | ICA | `realistic_interior_lighting` | A practical lab on building believable interior and exterior lighting using Lumen, skylight / directional light / sky atmosphere, post-process exposure control, atmospheric effects, and final tuning. Students should use either their ICA escape-room greybox or a CubeGrid corridor / room study. | [Lighting Lab - Believable interior lighting](/Labs/lab_1_realistic_interior_lighting.md) |
| 2 | GCA | `playability_testing` | A structured group lab covering Stage 3 data audit, A/B variable selection, Stage 4 validation session execution, Stage 4 comparative session execution, and post-session statistical analysis. All outputs map directly to GCA1 report sections. | [Playtesting Lab — Stage 3 Audit and Stage 4 Testing](Labs/lab_3_playtesting_stages_3_to_4.md) |


