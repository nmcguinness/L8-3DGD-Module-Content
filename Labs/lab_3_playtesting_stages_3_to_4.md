---
title: "Playtesting Lab — Stage 3 Audit and Stage 4 Testing"
subtitle: "Y4 Collaborative Project — Validation, Comparative Analysis, and GCA1 Evidence"
author: "Niall McGuinness"
institute: "Dundalk Institute of Technology"
programme: "BSc (Hons) in Computing in Games Development"
module_code: "PROJ I8006"
module_title: "Collaborative Project"
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

# Playtesting Lab — Stage 3 Audit and Stage 4 Testing

> This lab has five parts. Parts A and B are **preparatory** — complete them before your Stage 4 lab session. Parts C and D are **in-session** — you will run them during the designated testing time. Part E is **post-session** — complete it before writing the GCA1 report. Each task produces a specific output. Collect all outputs: they are the raw material for your GCA1 report.

---

## Overview

You have already collected Stage 3 playtest data (Week 9). This lab guides your team through:

- auditing what that data actually contains and what it is worth
- selecting a single, controlled variable for comparative A/B testing
- running a structured Stage 4 validation session
- running a structured Stage 4 comparative session

By the end, you will have the data, decisions, and documentation required to write every section of the GCA1 report.

---

## Learning Outcomes

By the end of this lab your team can:

- classify Stage 3 data as observations or opinions, and identify its evidentiary gaps
- select and justify a single variable for a controlled A/B comparison
- run a validation session with defined observation points and consistent recording
- run a comparative session under controlled conditions with at least one quantifiable metric
- connect each testing activity to the GCA1 report section it generates

---

## Ground Rules

- One team member records all outputs in a shared document during the lab. Rotate this role between Parts C and D.
- Every task that asks for a written output feeds directly into a named GCA1 section — do not skip it.
- If a task reveals a problem with your current plan, stop and resolve it before moving on. A problem identified in Part A that is ignored will reappear as a report weakness.

---

## Part A — Stage 3 Audit

**Complete before your Stage 4 lab session.**

You need your Stage 3 session notes, survey responses, or any other records from your testing. Open them as a team before beginning.

---

### Task A1 — Classify Your Stage 3 Data

Go through every item in your Stage 3 record. For each item, classify it as one of the following:

| Class | Definition | Example |
| :-- | :-- | :-- |
| **O — Observation** | Records what a participant did, with no attributed cause | "Missed the tutorial prompt on first pass" |
| **P — Opinion** | Records what a participant said they felt or thought | "Said the controls felt awkward" |
| **I — Interpretation** | Your team's explanation of a participant's behaviour | "Seemed confused by the UI" |

Write each item into a table with three columns: Item, Class (O/P/I), and Notes.

**Output A1:** Completed classification table. Count how many items fall into each class. Record the totals.

> *GCA1 connection: Methodology — participant details and data quality; Discussion — limitations.*

---

### Task A2 — Assess Consistency

Answer the following questions about how Stage 3 was run:

1. Were all sessions run on the same build version?
2. Were all participants given the same briefing before playing?
3. Did all sessions use the same observation protocol, or did different team members watch for different things?
4. Were any sessions run under significantly different conditions (different room, different time pressure, different number of observers)?
5. What confounding variables may have effected the outcome of your tests?

For each "No" answer, note what it means for the reliability of that session's data. Data from inconsistent sessions should be flagged as lower-confidence in your report.

**Output A2:** Consistency assessment — four answers with brief notes on any reliability implications.

> *GCA1 connection: Methodology — limitations of Stage 3 procedure; Discussion — limitations.*

---

### Task A3 — Identify Unresolved Problems

From your classified data (Output A1), identify every item that:

- is an Observation (Class O), and
- points to a playability problem that has not yet been fixed, or where a fix was made but has not yet been tested with a cold participant

List each unresolved problem in a table with three columns: Problem (described as an observation), Suspected Cause (your team's hypothesis), and Proposed Fix (one specific change).

If a suspected cause has no corresponding observation supporting it, mark it as unconfirmed. Unconfirmed suspected causes must be tested in Stage 4, not assumed.

**Output A3:** Unresolved problems table. This list is the agenda for Part C (Stage 4 validation).

> *GCA1 connection: Introduction — testing objectives; Results — validation findings.*

---

### Task A4 — Identify Coverage Gaps

Review your Stage 3 record and answer:

1. Which sections of your game were observed by at least one participant from start to end?
2. Which sections were partially observed (participant reached them but did not complete)?
3. Which sections were not observed at all in Stage 3?

For each unobserved or partially observed section, note whether it contains content that is relevant to a playability objective in your report. If it does, that section must be covered in Stage 4 validation.

**Output A4:** Coverage map — three lists (fully observed, partially observed, not observed) with notes on Stage 4 priority.

> *GCA1 connection: Methodology — scope of Stage 4 session; Introduction — testing objectives.*

---

## Part B — Variable Selection for Stage 4 A/B Testing

**Complete before your Stage 4 lab session.**

---

### Task B1 — Generate Candidate Variables

As a team, brainstorm design decisions in your current build where you have genuine uncertainty — places where you considered two different approaches and are not confident which is better. List at least three candidates.

For each candidate, write one sentence describing the choice: "We are uncertain whether [Option A] or [Option B] is better for [aspect of player experience]."

Do not evaluate the candidates yet. Just list them.

**Output B1:** List of at least three candidate variables with one-sentence descriptions.

---

### Task B2 — Apply the Single-Variable Test

For each candidate from B1, answer the following questions:

1. **Can it be changed in isolation?** Would implementing Option B require any other change to the build — to level content, other systems, audio, UI — beyond the one variable? If yes, it fails this test.
2. **Can it be measured?** Is there at least one observable, quantifiable player behaviour that would differ between Option A and Option B if the hypothesis is true? Name the metric.
3. **Is it worth testing?** Would the result of this comparison change a decision you have not yet made? If you have already committed to one option, the test has no value.

Eliminate any candidate that fails Question 1. For candidates that pass, record the metric from Question 2 and the answer to Question 3.

**Output B2:** Filtered candidate list — candidates that passed all three questions, with their metrics and justification for testing.

---

### Task B3 — Select and Commit

From the candidates that passed B2, select one for Stage 4 comparative testing. The selection criterion is: which variable has the largest potential impact on the player experience and a metric that can be recorded reliably in a single lab session?

Write your A/B comparison in this formal structure:

> **Variable:** [The single design element being changed]  
> **Build A:** [Current baseline — describe the specific design]  
> **Build B:** [Variant — describe the single change]  
> **H₀:** There is no difference in [metric] between Build A and Build B.  
> **H₁:** Build B will produce a [higher / lower] [metric] than Build A.  
> **Metric:** [Precise, observable, quantifiable measure]  
> **How it will be recorded:** [Who records it, when, how]

**Output B3:** Completed A/B comparison statement. This is the hypothesis block for your GCA1 Introduction section.

> *GCA1 connection: Introduction — hypotheses; Methodology — test design; Results — comparative findings.*

---

### Task B4 — Identify and Plan for Confounds

Before building your two variants, identify the confounds most likely to threaten the validity of your specific A/B comparison. Use the confound taxonomy in Appendix B of the [Validation Testing, Comparative Analysis, and Evidence-Based Evaluation](https://github.com/nmcguinness/L8-3DGD-Module-Content/blob/main/Notes/testing_analysis_evidence_based_evaluation.md) notes as your reference.

For each confound you identify as relevant, complete the following table:

| Confound | Type (Player / Environment / Build / Social) | Likelihood for your session | Control strategy |
| :-- | :-- | :-- | :-- |
| e.g. Tester skill level | Player | High | Randomise build assignment; record self-reported experience |
| | | | |

You do not need to list every possible confound — focus on the ones that could plausibly affect your primary metric. Aim for four to six entries. For any confound you cannot fully control, write one sentence explaining how you will acknowledge it in your report.

**Output B4:** Confound identification and control table.

> *GCA1 connection: Methodology — test design and controls; Discussion — limitations.*

---

### Task B5 — Prepare Both Builds

Before the Stage 4 session, your team must have two separate, stable builds ready:

- **Build A** — your current validated build, unchanged
- **Build B** — Build A with exactly one change applied (the variable from B3)

Before the session begins, do a deliberate diff of the two builds and confirm the only difference is the one you planned. Document any unintended differences and resolve them before testing begins.

**Output B5:** Written confirmation that both builds are stable and differ in exactly one variable, with a note of any unintended differences found and how they were resolved.

---

## Part C — Stage 4 Validation Session

**In-session — Stage 4 lab.**

This part uses your current, stable build (Build A). The goal is to test the unresolved problems identified in Output A3 and the coverage gaps in Output A4.

---

### Task C1 — Set Up the Observation Protocol

Before the first participant enters, agree as a team on your observation points for this session. Take your Output A3 unresolved problems list and convert each problem into a specific, binary observation question:

*"Does the participant [observable behaviour] within [time window or location]?"*

For example: "Does the participant engage with the core mechanic without prompting within the first two minutes?"

Write out each observation question. These are what the observer will watch for and record during the session.

**Output C1:** Observation protocol — a numbered list of binary observation questions, each derived from an unresolved problem in A3.

> *GCA1 connection: Methodology — observation protocol for Stage 4.*

---

### Task C2 — Run the Validation Session

For each participant:

1. Give the standard briefing (same words, every time — read it from a script if needed).
2. Start a timer at the moment the participant begins playing.
3. The observer records answers to each observation question from C1 as the session proceeds. Use a simple table: participant number, observation question number, observed (Y/N), timestamp.
4. Do not intervene, assist, or respond to questions during the session. If the participant asks for help, note it as a hesitation event and say "keep trying as you would if playing at home."
5. At the end of the session, note the total session time and whether the participant completed the experience.

Run at least three participants through Build A.

**Output C2:** Completed observation table for all validation participants.

> *GCA1 connection: Results — validation findings table; Appendices — raw session data.*

---

### Task C3 — Debrief and Record

Immediately after each participant finishes, ask two questions only:

1. "Was there any moment where you weren't sure what to do? If so, where?"
2. "Was there any moment where you tried something and weren't sure if it worked? If so, what?"

Record the responses verbatim. These are opinions, not observations — label them as such in your notes (Class P from Task A1). They may corroborate or contradict your observations; they do not replace them.

**Output C3:** Debrief responses, verbatim, labelled as opinion data.

---

### Task C4 — Identify Confirmed and Unconfirmed Problems

After all validation participants have completed the session, review Output C2 as a team.

For each observation question from C1, count how many participants produced a "No" response (the problem behaviour was observed). A problem observed in two or more out of three participants is a **confirmed problem**. A problem observed in one participant is a **marginal finding**. A problem observed in zero participants is **resolved** — the earlier fix worked.

Write the results in a table: Observation Question | Confirmed / Marginal / Resolved | n / 3 | Notes.

For each confirmed problem, write a one-sentence fix using the structure: "We will change [specific element] to [specific change] because [observation evidence]."

**Output C4:** Confirmed problems table with proposed fixes. This is the iteration evidence for your GCA1 Discussion and Conclusion.

> *GCA1 connection: Results — validation findings; Discussion — insights and recommendations; Conclusion — value to development.*

---

## Part D — Stage 4 Comparative Session

**In-session — Stage 4 lab.**

This part uses both Build A and Build B. The goal is to generate evidence for or against the hypothesis in Output B3.

---

### Task D1 — Assign Participants

Before any participant enters the room, divide your available participants into two groups. Assign each group to a build in advance — do not allow self-selection. Aim for equal group sizes.

Write down each participant's assigned build before the session begins. If you have an odd number of participants, assign the extra participant to whichever build you have less data for.

**Output D1:** Participant assignment list — participant number and assigned build for each person.

---

### Task D2 — Run Both Builds Under Identical Conditions

For each participant, regardless of which build they are assigned:

1. Before play begins, record the participant's **year of study** and **self-reported 3D game experience** (None / Occasional / Regular / Frequent). This takes under thirty seconds and gives you the tester background data needed to assess skill-level confounds in your analysis.
2. Give the identical standard briefing. Use the same script as Part C.
3. Start a timer at the moment they begin playing.
4. Record your primary metric (from Output B3) as precisely as possible. For time-based metrics, record to the nearest second. For count-based metrics (errors, failed attempts), record each event with a timestamp.
5. Record your total session time and completion status.
6. Do not intervene.

Run at least three participants per build (minimum six total). If you have fewer than six available participants, note this explicitly — it is a limitations finding for the report.

**Output D2:** Metric data table — participant number, assigned build, year of study, experience level, primary metric value, session time, completion status.

> *GCA1 connection: Results — raw data for comparative analysis; Appendices — data files.*

---

### Task D3 — Record Secondary Observations

While the primary metric is being recorded, the second team member observer should note any behavioural differences between Build A and Build B participants that were not captured by the primary metric. These are not the focus of the comparison, but they may provide supporting context for the Discussion.

Use the same classification as Task A1: mark each note as O (observation), P (opinion), or I (interpretation).

**Output D3:** Secondary observation notes, classified.

---

### Task D4 — Debrief and Record

After each comparative session participant finishes, ask two questions only:

1. "Was there anything about the [specific changed element] that felt unclear or confusing?"
2. "Did you feel you understood what the game expected of you at all times?"

Record responses verbatim. Label as opinion data. Do not ask questions that reveal which build the participant played.

**Output D4:** Debrief responses, verbatim, labelled as opinion data.

---

## Part E — Post-Session Analysis

**Complete after the in-session work, before writing the GCA1 report.**

---

### Task E1 — Calculate Summary Statistics

Using Output D2, calculate summary statistics for each build group using the following base R code. Replace the vectors with your actual metric values.

```r
# Replace with your recorded metric values from Output D2
build_a <- c()   # e.g. c(46, 51, 39, 44, 50)
build_b <- c()   # e.g. c(28, 31, 34, 29, 33)

summarise_group <- function(x, label) {
  data.frame(
    Build    = label,
    n        = length(x),
    Mean     = round(mean(x), 2),
    Median   = round(median(x), 2),
    SD       = round(sd(x), 2)
  )
}

rbind(
  summarise_group(build_a, "Build A"),
  summarise_group(build_b, "Build B")
)
```

Record the output in a summary table with one row per build.

**Output E1:** Summary statistics table — Build A and Build B, with n, mean, median, and SD. This table goes directly into your GCA1 Results section.

> *GCA1 connection: Results — summary statistics table.*

---

### Task E2 — Calculate a 95% Confidence Interval

For each group's mean, calculate a 95% confidence interval using the following base R code. Replace `build_a` and `build_b` with your actual metric vectors from Output D2.

```r
# Replace these vectors with your recorded metric values
build_a <- c()   # e.g. c(46, 51, 39)
build_b <- c()   # e.g. c(28, 31, 34)

ci <- function(x) {
  n    <- length(x)
  mean <- mean(x)
  se   <- sd(x) / sqrt(n)
  t    <- qt(0.975, df = n - 1)
  c(lower = mean - t * se, mean = mean, upper = mean + t * se)
}

ci(build_a)
ci(build_b)
```

Report each interval in gameplay terms: "We are 95% confident that the true mean [metric] for Build B lies between [lower] and [upper] [units]."

**Output E2:** 95% CI for each build group, stated in gameplay terms.

> *GCA1 connection: Results — confidence intervals.*

---

### Task E3 — Produce a Comparison Plot

Using your data from Output D2, produce a boxplot comparing Build A and Build B on your primary metric using base R. Label both axes, title the figure, and caption it for inclusion in the report.

```r
# Combine into a data frame for plotting
metric  <- c(build_a, build_b)
build   <- c(rep("Build A", length(build_a)), rep("Build B", length(build_b)))

boxplot(metric ~ build,
        xlab    = "Build",
        ylab    = "[Your metric label and units]",
        main    = "[Your metric]: Build A vs Build B",
        col     = c("#d9eaf7", "#fde8c8"),
        border  = c("#2a6496", "#c87941"),
        notch   = FALSE)
```

Replace `[Your metric label and units]` and the title string with your actual metric. Save or export the figure. It must appear in your GCA1 report as a numbered, captioned figure referenced in the text.

**Output E3:** Comparison plot, captioned and labelled.

> *GCA1 connection: Results — group comparison figure.*

---

### Task E5 — Produce a Correlation Matrix

The GCA1 Results section requires a correlation matrix for three to five key numeric metrics from your combined session data. This task uses all participants across both builds — not just the primary metric comparison, but the full set of numeric columns you recorded (primary metric, session time, completion status, experience level encoded as a number, and any secondary metrics from Output D3).

```r
# Build a data frame from all numeric columns you recorded in Outputs C2 and D2
# Adapt column names to match what you actually collected
session_data <- data.frame(
  primary_metric   = c(build_a, build_b),
  session_time_sec = c(),   # total session time per participant
  completion       = c(),   # 1 = completed, 0 = did not complete
  experience       = c()    # encode: 1=None, 2=Occasional, 3=Regular, 4=Frequent
)

# Calculate and display the correlation matrix
cor_matrix <- round(cor(session_data, use = "complete.obs"), 2)
print(cor_matrix)
```

Interpret the matrix: for each pair of variables, note the direction and approximate strength of the relationship (strong positive, weak negative, negligible, etc.) and whether it is relevant to your design conclusions. A correlation between experience level and primary metric, for example, would indicate that tester skill is a confound worth discussing.

**Output E5:** Correlation matrix with a two-to-three sentence interpretation of any relationships relevant to your analysis.

> *GCA1 connection: Results — correlation matrix.*

---

### Task E4 — Write the Comparative Conclusion

Write a short paragraph (4–6 sentences) interpreting your comparative result. The paragraph must:

1. State the direction of the result (Build B produced a higher / lower / approximately equal [metric]).
2. Report the magnitude (by how much, in the units of the metric).
3. Assess consistency (was the direction consistent across all participants in each group, or were there outliers?).
4. Qualify the conclusion appropriately for your sample size.
5. State whether the result supports H₁ or fails to reject H₀.

**Output E4:** Comparative conclusion paragraph. This is the core of your GCA1 Discussion section's comparative analysis.

> *GCA1 connection: Discussion — comparative analysis; Conclusion — design decision justification.*

---

## Lab Output Summary

The table below maps each output to the GCA1 section it contributes to. Before leaving the lab, confirm your team has all outputs either completed or clearly in progress.

| Output | Description | GCA1 Section |
| :-- | :-- | :-- |
| A1 | Stage 3 classification table | Methodology, Discussion |
| A2 | Consistency assessment | Methodology, Discussion |
| A3 | Unresolved problems table | Introduction, Results |
| A4 | Coverage map | Methodology, Introduction |
| B3 | A/B comparison statement with H₀/H₁ | Introduction |
| B4 | Confound identification and control table | Methodology, Discussion |
| B5 | Build confirmation note | Methodology |
| C1 | Observation protocol | Methodology |
| C2 | Validation observation table | Results, Appendices |
| C3 | Validation debrief responses | Discussion |
| C4 | Confirmed problems table | Results, Discussion, Conclusion |
| D2 | Comparative metric data table (with participant profiles) | Results, Appendices |
| D3 | Secondary observations | Discussion |
| D4 | Comparative debrief responses | Discussion |
| E1 | Summary statistics table | Results |
| E2 | 95% confidence intervals | Results |
| E3 | Comparison plot | Results |
| E4 | Comparative conclusion paragraph | Discussion, Conclusion |
| E5 | Correlation matrix with interpretation | Results |

---

## Appendix C — Stage 4 Session Readiness Checklist

Complete this checklist in the class session **before** your Stage 4 testing day. Every unchecked item must be resolved before the session begins. A gap identified today can still be fixed. A gap discovered on the day cannot.

### Part A — Stage 3 Audit Outputs

| Check | Description | ☐ |
| :-- | :-- | :--: |
| A1 | Classification table exists with O/P/I totals recorded | ☐ |
| A2 | Unresolved problems table exists; each entry is an observation (not an interpretation) with a specific proposed fix | ☐ |
| A3 | Unobserved coverage relevant to testing objectives are flagged as Stage 4 priorities | ☐ |

### Part B — A/B Hypothesis and Build Verification

| Check | Description | ☐ |
| :-- | :-- | :--: |
| B1 | A/B hypothesis block complete — all seven components present; metric is quantifiable; written before any Stage 4 data is seen | ☐ |
| B2 | Confound table exists; tester skill level, unintended build differences, developer presence, and performance variation are explicitly addressed | ☐ |
| B3 | Both builds launch and run end-to-end on the session machine; unintended differences resolved or documented | ☐ |
| B4 | Metric recording method written without ambiguity — start point, end point, and unit defined precisely enough that any observer records the same value | ☐ |

### Part C — Logistics and Session Protocol

| Check | Description | ☐ |
| :-- | :-- | :--: |
| C1 | Minimum nine cold[^1] participants confirmed; comparative session assignment list written in advance (no self-selection) | ☐ |
| C2 | Standard briefing script written, covers the three required points, reads in under sixty seconds | ☐ |
| C3 | No-intervention protocol agreed; session controller named | ☐ |
| C4 | Session machine confirmed; both builds profiled on that machine; comparable stable frame rate; identical peripheral (e.g. sound) setup for both build groups | ☐ |

### If a Check Fails on the Day

| Failure | Impact | Action |
| :-- | :-- | :-- |
| Build B differs from Build A in more than one variable | Comparative result cannot be interpreted | Do not run comparative session until the extra difference is resolved |
| Fewer than three participants per build | Below minimum for comparative analysis | Run what is available; report the shortfall explicitly as a limitation |
| Participant has prior knowledge of the game[^1] | Data cannot be used for comparative analysis | Exclude from comparative analysis; may still contribute to validation data with a note |
| No-intervention protocol broken mid-session | Affected participant's data is compromised | Flag the session; exclude from comparative analysis; note in limitations |

[^1]: We will be required to re-use participants given the limited sample size and availability