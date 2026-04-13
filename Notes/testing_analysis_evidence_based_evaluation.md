---
title: "Validation Testing, Comparative Analysis, and Evidence-Based Evaluation"
author: "Niall McGuinness"
institute: "Dundalk Institute of Technology"
programme: "BSc (Hons) in Computing in Games Development"
module_code: "PROJ I8006"
module_title: "Collaborative Project"
stage: 4
session: "Playability and Polish"
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

# Validation Testing, Comparative Analysis, and Evidence-Based Evaluation

> These notes mark a transition in how you relate to your own game. In the end of Semester 7 the the primary question was *can it be built?* In Semester 8, the question is *does it play well, and can you prove it?* The work now is to evaluate it with the same rigour you applied to building it — and to produce evidence, not opinion.

---

## Ten Principles of Playability and Final Testing

1. **A finished feature is not a finished experience.** A working system and a readable system are different things.
2. **Player behaviour is truth.** What players do overrules what you intended.
3. **Confusion is a signal, not a failure.** Every point of hesitation is a design problem with a design solution.
4. **If it cannot be measured, it cannot be improved.** Observations without metrics produce opinions, not evidence.
5. **One variable at a time.** Changing two things simultaneously tells you nothing about either.
6. **Separate validation from comparison.** They are different questions requiring different test designs.
7. **Consistency creates reliability.** Identical test conditions are the prerequisite for comparable results.
8. **Iteration must be intentional.** A change without a hypothesis is a guess.
9. **Polish is readability.** Making the correct action the most obvious action is the final design task.
10. **Test early enough to act on the results.** Data collected too late to change anything is not testing — it is documentation.

---

## 1. Where You Are in the Production Arc

At this point in the Collaborative Project, you have a complete game. Core systems are implemented, content is in place, and the experience has been through at least one round of playtesting. The instinct at this stage is to keep adding — one more feature, one more level, one more mechanic. That instinct is worth resisting.

The most significant gains available to your project now are not in scope. They are in clarity. A game that communicates well — that a first-time player can orient in, understand, and act on without asking for help — will always be assessed more favourably than a larger game that communicates poorly. Playability is not a quality layer applied on top of a complete product. It is a design discipline, and it has its own structured methodology.

These notes cover that methodology across two phases. The first is an **audit of your Stage 3 playtesting** — reviewing what you already collected to extract the diagnostic signal it contains. The second is the design and execution of **Stage 4 final testing**, which has two distinct tracks: **validation testing** (does the game play well?) and **comparative A/B testing** (between two specific design variants, which performs better on a defined metric?). Understanding the difference between these tracks, and running them correctly, is the central learning goal of this phase.

**On the shift from opinion to evidence.** Earlier in the project, feedback from playtesting sessions likely arrived as subjective responses — "it felt slow," "I wasn't sure what to do," "I liked the look of it." These responses are not worthless, but they are not evidence. Evidence is a structured, repeatable observation: "four out of five participants failed to locate the primary objective within the first sixty seconds," or "average time to first meaningful interaction dropped from 48 seconds in Build A to 31 seconds in Build B." The difference between those two classes of response is the difference between a project that reports on its testing and one that demonstrates it. The latter is the standard you are working toward.

**GCA1 — the formal deliverable for this work.** The testing you conduct across both sessions feeds directly into the **Group Continuous Assessment 1 (GCA1): User Testing Lab Report**. Your Stage 3 session (Week 7) and Stage 4 session (Week 11) are the two rounds of user testing the report is built from. This means the quality of your testing — the rigour of your setup, the accuracy of your observations, the control of your A/B comparison — determines the quality of the evidence available to you when writing. A poorly run session cannot be recovered in the report. See Section 9 for the full GCA1 report structure and requirements.

[GDC plays Hades with Greg Kasavin](https://youtu.be/9LykrwmUu8I)
*Supergiant's early access development of Hades involved continuous playtesting across hundreds of builds. Each major system change — weapon feel, boon balance, room pacing — was evaluated against player behaviour data collected from public players, not internal preference. The game's exceptional clarity of feedback and interaction readability is the accumulated result of that process. The principle scales directly to your project: the final quality of the experience is determined by the rigour of the evaluation process, not the ambition of the feature list.*

---

## 2. What Playability Actually Means

Playability is the degree to which a **first-time player** — someone who has never seen the game, cannot ask the team questions, and has no access to the team's intentions — can understand what to do, interpret the current game state, act effectively on that understanding, and receive clear feedback that confirms or corrects their actions.

A game can be technically complete and still fail playability. The systems compile and run; the win condition fires correctly; the progression logic is sound. But if the first-time player cannot identify which elements are interactive, cannot infer from the environment what is expected of them, and cannot tell whether their last action had any effect — the game has failed its primary obligation. It was built for the player, not the team.

**Why this matters for your assessment.** Playability failures are rarely caused by missing features. They are caused by assumptions the team made that went unverified: that the player would read a prompt in the order it was placed, that a particular visual would draw attention to a key interaction, that a tutorial step would transfer clearly to application. None of these assumptions can be validated without structured observation. The assessment criteria for this module reflect the expectation that you can demonstrate — with data — that your game has been evaluated, not merely completed.


[GDC - Level Design Workshop: Designing Celeste](https://youtu.be/4RlpMhBKNr0)
*Celeste's design process, extensively documented through GDC talks, is characterised by constant first-time player observation. Every assist mode feature, every level checkpoint placement, and every feel parameter was tested against observed player behaviour rather than team intuition. The game's reputation for accessibility and feedback clarity — despite significant mechanical challenge — is directly traceable to the rigour of its evaluation process.*

---

## 3. Two Types of Testing

At this stage of production, testing serves two distinct purposes that must not be conflated. **Validation testing** answers: does this game play well? It is diagnostic — it identifies where the player experience breaks down and informs fixes. **Comparative testing** answers: between two specific design variants, which performs better on a defined metric? It is evaluative — it produces evidence that justifies a specific design decision.

These two test types require different setups, different data collection protocols, and different analysis approaches. Running a general session and attempting to extract both types of result from it produces neither reliably. Before designing any test session, decide which question you are asking.

The correct production sequence is: run validation testing first to identify and address the most significant playability failures; then, once the baseline experience is stable, run comparative testing on the specific design decisions where you have genuine uncertainty. Comparative testing on an unstable baseline measures the baseline's failures, not the variable under comparison.

---

## 4. Auditing Stage 3: What You Already Have

### The Purpose of the Audit

Before designing new tests, extract the maximum value from what you already collected. Stage 3 playtesting produced raw material — observation notes, survey responses, verbal feedback, session recordings — that may contain diagnostic signal you have not yet fully analysed. The audit is a structured re-examination of that material before Stage 4 testing begins.

The audit has two goals: to identify which playability problems are already evidenced by Stage 3 data and do not need further validation testing to confirm, and to identify which questions Stage 3 data cannot answer — either because the right observations were not made, or because the conditions were not controlled enough to produce usable results.

### Auditing for Signal Quality

Not all Stage 3 data is equally usable. Assess what you collected against the following criteria.

**Observation vs opinion.** Stage 3 notes that record what participants did — "missed the objective marker on first pass," "died at the third encounter four times consecutively" — are observations and can be acted on directly. Notes that record what participants said they felt — "found it confusing," "thought it was too hard" — are opinions. Opinions require corroborating behavioural evidence before they can inform a design change. Separate the two categories in your Stage 3 record and weight them accordingly.

**Consistency.** If Stage 3 sessions were run under inconsistent conditions — different briefings, different build versions, different numbers of participants, different observers — results cannot be reliably compared across sessions. Identify which Stage 3 results came from consistent conditions and treat those as the stronger evidence base.

**Coverage.** Identify which parts of your game were observed in Stage 3 and which were not. Late-game content, tutorial-to-application transfer, and end-state feedback are the areas most commonly under-observed in early playtesting because sessions frequently end before participants reach them. Stage 4 must deliberately cover any area that Stage 3 left unobserved.

### What to Carry Forward

From the Stage 3 audit, produce a prioritised list of unresolved playability problems — items where Stage 3 data identified a problem but either the fix has not been implemented or the fix has not yet been tested. This list drives the validation component of Stage 4. Every item on it is a question Stage 4 must answer.

---

## 5. Stage 4 Validation Testing

### What Validation Testing Is

Validation testing is structured observation of first-time players completing your game under conditions as close as possible to how it will be experienced at submission or demonstration. The goal is to identify **where the player experience breaks down** — points of hesitation, misinterpretation, failed action, or missing feedback — so that those breakdowns can be addressed before the final build is locked.

Validation testing is not feedback collection. You are not asking players what they think. You are watching what they do. The distinction matters because what players say and what they do are frequently different. A player who describes an experience as enjoyable while spending four minutes confused in front of an unclear interaction has given you two data points: the first-time player will persist if engagement is sufficient, but the interaction's readability has failed. Their verbal response would have obscured this; their behaviour made it visible.

### Setting Up a Validation Session

A usable validation session requires four elements:

**A stable, locked build.** Test on a build that does not change between sessions. If you patch something mid-testing, you lose the ability to compare results across participants. Lock the build before the first session begins and do not commit changes until the full round of sessions is complete.

**Cold participants.** Each participant must not have previously seen or played the game. A participant who has watched development, received a walkthrough, or played an earlier build is not a valid first-time player. Their familiarity with the team's intentions produces systematically different behaviour from someone encountering the game for the first time.

**Defined observation points.** Before the session, agree as a team on four to six specific behaviours you are watching for. These should map directly to the unresolved items from your Stage 3 audit: "does the player identify the core mechanic without tutorial assistance?", "does the player reach the mid-game section within the first ten minutes?", "does the player understand the feedback on a failed attempt?" Undefined observation produces impressionistic notes that are difficult to compare across participants.

**Accurate, timestamped recording.** Write down what happens, not what you think it means. "Participant attempted the primary interaction six times before succeeding at 4m 22s" is an observation. "Participant found the interaction frustrating" is an interpretation. Record observations; draw interpretations only in the analysis phase, held explicitly as hypotheses.

### Observation Categories

Three categories of observation are relevant for Stage 4 validation:

**Behavioural observations** record what the player does: which elements they interact with, in what order, how long they spend in each section, which mechanics they use and which they ignore. These are the raw material of playability analysis.

**Outcome observations** record what the player achieves: objectives completed, time to key milestones, content reached, whether they finished. These contextualise behavioural observations — a player who spent ten minutes on a single encounter and completed it tells a different story from one who spent ten minutes and abandoned it.

**Hesitation points** are the most diagnostically valuable observation type at this stage. A hesitation — a pause, a repeated failed attempt, an environmental scan without action — signals that the player lacks the information they need to proceed. Map hesitation points spatially and temporally: a cluster at a particular location or moment in the experience identifies exactly where a readability failure is occurring.

[The 4 years of self-imposed crunch that went into Stardew Valley](https://www.gamedeveloper.com/business/the-4-years-of-self-imposed-crunch-that-went-into-i-stardew-valley-i-)
*Stardew Valley's development involved years of iterative testing of UI clarity, interaction legibility, and progression pacing against first-time players outside the games development community. The game's accessibility to non-genre players is the direct result of repeated validation against behaviour, not assumption. The principle applies regardless of team size: clarity is achieved through observation.*

---

## 6. From Observation to Iteration

### Observation Is Not Interpretation

The data from a validation session is a set of behavioural observations. Before those observations can inform design decisions, they must be interpreted — a cause must be hypothesised from the behaviour. These are separate steps, and conflating them is the most common error in post-session analysis.

"Four out of five participants failed to locate the secondary objective within the first two minutes" is an observation. "The secondary objective marker has insufficient visual contrast against the background environment" is an interpretation — a hypothesis about cause. The interpretation may be correct, but it is not the observation, and it should be held as a hypothesis until a design change tests it.

A single validation session rarely produces certainty about causes. It produces a prioritised list of problem locations and candidate explanations. The design response is to make one change per problem, then test again to confirm the fix had the intended effect. A session that produces eight observations and triggers eight simultaneous fixes produces no usable information: if the experience improves, you do not know which fix was responsible; if it does not, you do not know which failed.

### Designing a Fix

A well-designed fix has three components: a clear statement of the observed problem, an explicit hypothesis about its cause, and a single change that tests that hypothesis.

**Observed problem:** "Four out of five participants failed to engage with the core progression mechanic in the first three minutes."  
**Hypothesis:** "The visual affordance for the mechanic's entry point does not read as interactive at the approach distance."  
**Fix:** "Increase the scale of the interaction indicator and add an idle animation to the entry point prop to distinguish it from static dressing."

The fix is specific, tests one variable, and the next session will show whether the observation recurs. If participants now engage with the mechanic reliably, the hypothesis was correct. If they still do not, the cause is something else and a different hypothesis must be formed.

---

## 7. Comparative A/B Testing

### What Comparative Testing Is

Once your baseline experience is stable — validated, iterated, and playing cleanly for first-time players — comparative testing asks: between two specific, controlled design variants, which produces better results on a defined metric?

This is the first time in this module that you are conducting controlled comparative analysis on your own game. Validation asks "what is broken?" Comparison asks "between two valid approaches, which is objectively better, and by how much?" The second question requires a more controlled setup precisely because both options are assumed to work. The test is deciding between them on the basis of evidence, not preference.

**Why this matters for your submission.** A project that has been validated and fixed demonstrates craft and iteration. A project that has additionally been comparatively tested demonstrates the ability to frame a design question as a testable hypothesis, collect controlled evidence, and defend a decision with data. The assessment criteria reflect this distinction.

### Framing a Testable Hypothesis

A valid comparative test begins with a **testable hypothesis** — a specific, falsifiable claim about which variant will produce better results on a defined metric.

A testable hypothesis names the variable under comparison, the expected direction of effect, and the measurement instrument:

> "Version B, which replaces the text-based tutorial prompt with a contextual environmental cue, will reduce average time-to-first-meaningful-action compared to Version A."

This identifies what is being changed (tutorial modality), what effect is expected (faster first action), and how it will be measured (time in seconds). It is falsifiable — the data will either support it or not.

A non-testable hypothesis — "Version B will feel more intuitive" — cannot be evaluated because "intuitive" is not measurable. Before designing the test, rewrite every claim in terms of observable, quantifiable player behaviour. If you cannot express the expected difference as a number, you do not yet have a testable hypothesis.

### Choosing What to Compare

Not every design question is worth a comparative test. Reserve comparative testing for decisions that are genuinely uncertain, have meaningful impact on the player experience, and can be expressed as a single-variable change. Good candidates at this stage include: onboarding approach, difficulty parameters, UI information hierarchy, feedback modality for a key interaction, and navigation signalling. Poor candidates are decisions already clearly resolved by validation data, decisions requiring more than one simultaneous change, and decisions where the expected difference is too small to observe at available sample sizes.

### The Single-Variable Requirement

Comparative testing requires two builds that differ in exactly one variable. This is absolute. If Build A and Build B differ in two or more ways, a difference in measured outcomes cannot be attributed to either variable. The test produces noise rather than evidence.

**Build A** is the baseline — your current, validated build. **Build B** is the variant — a single deliberate change. Every other aspect of both builds must be identical: same content, same levels, same audio, same other interactions, same session conditions, same briefing given verbatim to all participants. Before running the test, confirm the only difference between builds is the one you planned.

### Participant Assignment and Session Control

Assign participants to Build A or Build B in advance. Do not allow self-selection, and do not allow any participant to play both versions — playing Build A before Build B contaminates the second session with familiarity effects. Both groups must complete their sessions under identical conditions: same environment, same briefing script, same observation protocol, same metrics recorded by the same observer.

### Independent, Dependent, Confounding, and Extraneous Variables

Controlled testing depends on being precise about which variables you are managing and in what role. These four categories apply to every comparative test you run.

The **independent variable** is the single design element you are deliberately changing between builds — the one difference between Build A and Build B. Everything else in the test should be held constant. If you are testing whether a visual cue reduces time-to-first-interaction, the presence or absence of the visual cue is the independent variable.

The **dependent variable** is what you are measuring — the outcome you expect the independent variable to affect. It must be quantifiable and observable. In the example above, time-to-first-interaction (in seconds) is the dependent variable. The dependent variable is what your metric captures.

**Extraneous variables** are any other factors that vary between sessions but are not the focus of your test. They are not necessarily harmful — some variation is unavoidable — but they must be identified and managed. A participant who is an experienced 3D games player and a participant who rarely uses a controller are extraneous variables. You cannot eliminate the difference, but you can note it, account for it in your analysis, and avoid deliberately stacking one type of participant in one build group.

**Confounding variables** are the most serious category. A confound is an extraneous variable that is systematically linked to which build a participant plays, meaning it could explain the result instead of — or as well as — the independent variable. If all your experienced players happen to be assigned to Build B, a faster completion time in Build B might reflect player skill rather than the design change. The confound makes the result uninterpretable.

Identifying and controlling for confounds is the practical work of test design. Below are the confounds most likely to affect Stage 4 testing in this module, grouped by source.

**Player-related confounds.** Different skill levels between participants are the most common source of noise in classroom playtesting. A tester experienced with 3D games will navigate, interact, and recover from failures more efficiently than one who rarely uses a controller or mouse-and-keyboard — regardless of which build they play. Prior familiarity is equally disqualifying: a participant who has already seen your game, watched a teammate play it, or knows a puzzle solution is not equivalent to a cold tester, and their results should not be included in comparative analysis. Fatigue and mood also matter — a tester at the end of a long class session may perform differently from one who starts fresh, particularly on timed metrics. Finally, if one tester understands the session objective immediately and another does not, the result may reflect briefing clarity rather than the variable under test.

**Testing-environment confounds.** Classroom-based staged playtesting introduces environmental noise that is easy to underestimate. Multiple groups testing in the same room simultaneously creates audio distraction that can affect concentration, particularly for games where audio feedback is part of the design under test. Hardware differences — screen size, frame rate, mouse sensitivity, controller quality, headphones versus speakers, seating position — can all alter the felt experience of the build in ways that have nothing to do with your independent variable. Time pressure is a confound when some participants feel observed and rushed and others do not. Order effects occur when a participant plays one build before the other: their learning and familiarity from the first session carries into the second, making the second session unrepresentative of a first-time player.

**Build-related confounds.** Bugs, collision issues, missed triggers, and UI failures can distort results completely — a participant who cannot complete an interaction because of a bug is not providing data about the design variable. Performance variation is a particularly significant confound for Unreal-based projects: poor frame rate, stutter, loading hitches, and input lag make mechanics feel worse than their design intent regardless of what has changed between builds. Given this module's emphasis on profiling and optimisation, both builds should be profiled before testing to confirm comparable performance. Inconsistent verbal assistance from team members during the session is also a build-related confound in practice: if one participant receives more guidance than another, the comparison is no longer between the two builds.

**Social confounds.** Testers sitting beside each other may overhear solutions, copy behaviour, or align their responses. Developer presence — the team standing behind or beside the tester — frequently produces more generous feedback than the tester would give privately, not because the experience was better but because social dynamics suppress criticism. Group observation effects are real: some participants perform and verbalise differently when watched than when alone.

**The confounds most likely to affect your Stage 4 session specifically.** Puzzle knowledge carryover is the highest-risk confound for escape room projects: once one participant has seen the solution, any subsequent run they observe or discuss is no longer a valid first-time test. Uneven hinting by team members — where some participants receive more verbal guidance than others — is common and hard to prevent without a strict no-intervention protocol enforced consistently across all sessions. Performance and frame-rate differences between builds are likely in any Unreal project where one build contains additional assets or Blueprint logic; profile both before testing. Tester background differences matter when Year 1 or Year 2 students are used as participants — their baseline familiarity with 3D controls is systematically different from Year 4 students and will produce a different result pattern. Testing-room noise and crowding affect attention and audio perception significantly in classroom conditions. And changing more than one variable between builds — even unintentionally — is the most common reason a comparative result cannot be interpreted.

[One More Run: The Making of 'Spelunky 2'](https://youtu.be/sL7v9ct6Gis)
*Derek Yu's design process for Spelunky 2, documented in postmortems and talks, involved structured iteration on feel, difficulty, and feedback legibility across many internal builds. The comparative question at each stage was not "which version do we prefer?" but "which version produces clearer, more consistent behaviour from a player who has never seen it before?" That framing — player behaviour as the judge, not team preference — is exactly the standard a Stage 4 comparative test should apply.*

---

## 8. Metrics and Measurement

### What Makes a Good Metric

A metric is a quantifiable measure of a specific player behaviour or outcome. Good metrics for Stage 4 testing are **quantifiable** (expressible as a number), **repeatable** (measurable consistently by any observer across all sessions), and **directly relevant** to the design variable under test. A metric that depends on observer judgment is not reliable. A metric that any observer would record the same way is.

Before running any session, define each metric precisely enough that two observers watching the same session would independently record the same value. If there is ambiguity in the definition, resolve it before the session begins, not after.

### Metric Examples

The following metrics span the range of game types in the cohort. Select and adapt based on your game's genre and the specific design question under test.

| Design Variable | Metric | What It Reveals |
| :-- | :-- | :-- |
| Onboarding / tutorial | Time to first meaningful action | Whether the opening teaches the core interaction efficiently |
| Onboarding / tutorial | Errors before first success | Whether instruction transfers to application |
| Core mechanic legibility | First-attempt success rate | Whether the mechanic's affordance communicates correctly |
| Difficulty calibration | Deaths or failures per session | Whether challenge is appropriately scaled |
| UI information hierarchy | Time to locate key UI element from cold start | Whether layout prioritises the right information |
| Feedback effectiveness | Time between action and visible player response | Whether feedback registers without delay |
| Progression clarity | Proportion reaching mid-game content | Whether early pacing retains players through to core content |
| Navigation | Wrong-path excursions per session | Whether spatial or menu navigation communicates direction |
| Overall pacing | Time to session completion | Summary measure of accessibility and pacing |

### Sample Sizes and Honest Conclusions

Five participants per build variant is the realistic minimum for Stage 4 comparative testing at this project scale. Five participants cannot produce statistically robust findings. What it produces is **directional evidence** — a consistent pattern suggesting one variant performs differently, which must be reported as such.

The correct framing for a small-sample comparative result is:

> "Participants in Build B completed the tutorial sequence on average 18 seconds faster than those in Build A. This direction is consistent across all five participants in each group. The sample size is insufficient to draw a definitive conclusion, but the consistency of the pattern supports the decision to proceed with Build B's approach."

Overclaiming certainty beyond what the data supports is a more serious analytical failure than having a small sample. The limitation, reported clearly, demonstrates methodological awareness. Overstating the conclusion undermines the credibility of the entire analysis.

---

## 9. The GCA1 Report: Connecting Testing to Submission

### How Testing Maps to the Report

Everything you do in Stage 3 and Stage 4 is raw material for the GCA1 lab report. The report does not exist separately from the testing — it is the formal account of it. This means the report's quality is determined by the rigour of the testing, not by the quality of the writing alone. Well-run sessions with accurate observations, controlled A/B conditions, and defined metrics produce a report that has real evidence to present. Loosely run sessions produce a report that has opinions dressed as evidence, and the difference is visible to any reader.

The table below maps each report section to the testing activity that generates its content. Use it when planning your sessions to ensure you are collecting what each section will need.

| Report Section | Content Required | Where It Comes From |
| :-- | :-- | :-- |
| **Executive Summary** | 150–200 word standalone summary of purpose, methods, key findings, and recommendations | Written last, from the completed report |
| **Introduction** | Game context; scope of both sessions; 2–4 testing objectives; H₀ and H₁ hypotheses in plain English | Defined before testing begins — objectives and hypotheses must be set in advance |
| **Methodology** | Test design; participant details (n, demographics, consent); materials and tools; step-by-step procedure for both sessions | Documented during session setup and execution |
| **Results** | Summary statistics table (n, mean/median, SD per group); at least one 95% confidence interval; at least one group comparison plot; correlation matrix for 3–5 key metrics; all figures captioned | Calculated from recorded session data |
| **Discussion** | Findings linked to objectives; 3–5 key insights; honest statement of limitations | Analysis and interpretation of Results |
| **Conclusion** | Summary of findings; value to development; future considerations | Synthesis of Discussion |
| **References** | APA-format citations | Throughout |
| **Appendices** | Raw data files; survey instrument; supplementary visualisations | Collected during sessions |

### Hypotheses

The Introduction requires null and alternative hypotheses (H₀ and H₁) stated in plain English. These are not written after testing — they are written before, as part of your test design. A hypothesis written after you have seen the data is not a hypothesis; it is a post-hoc rationalisation.

For each comparative A/B test, write the hypotheses in this form before the session:

> **H₀:** There is no difference in [metric] between Build A and Build B.  
> **H₁:** Build B, which [describes the single change], will produce a [higher/lower] [metric] than Build A.

For a validation test, the hypothesis takes a simpler form:

> **H₀:** There is no systematic point of failure in [section of the game].  
> **H₁:** Players will consistently fail to [specific observable behaviour] in [specific location or moment].

Both must be stated before testing begins and reported in the Introduction as written.

### Required Analysis in the Results Section

The Results section carries 25 marks — the heaviest single component — and has explicit analytical requirements that must be met regardless of what your data shows. These requirements are not optional if the results are inconclusive; they are minimum standards for any submission.

**Summary statistics table.** For each group or build, report n, mean or median (appropriate to distribution), and a measure of spread (standard deviation or interquartile range). This table must be present and must reference the session data in your appendix.

**95% confidence interval.** At least one confidence interval must be calculated and reported in gameplay terms — not as an abstract statistical range, but as a statement about what the interval means for a design decision. For example: "We are 95% confident that the true mean time-to-first-action for Build B lies between 28 and 34 seconds, compared to a point estimate of 46 seconds for Build A."

**Group comparison plot.** At least one boxplot or equivalent visualisation comparing the two groups or builds. The plot must be captioned, labelled on both axes, and referenced in the text.

**Correlation matrix.** A correlation matrix for three to five key numeric metrics from your data. The matrix must be interpreted — identifying any relationships that are relevant to your design conclusions — not simply displayed.

---

## 10. Common Testing Failures

Understanding how testing fails is as important as knowing how to run it well. These failure modes recur consistently at student production scale and each one produces data that cannot support the claims drawn from it.

**Mixing test types in a single session.** Attempting to answer validation and comparative questions simultaneously produces results that reliably address neither. Run them as separate sessions on separate builds.

**Changing multiple variables between builds.** If Build B differs from Build A in three ways, the result cannot be attributed to any of them. One variable. One change. No exceptions.

**Testing on familiar participants.** A participant who has seen development, received a walkthrough, or played an earlier build will behave differently from a genuine first-time player in ways that cannot be corrected in analysis. Prioritise cold participants for comparative testing, where familiarity contamination is most consequential.

**Recording impressions rather than observations.** "Seemed confused during the tutorial" is an impression. "Attempted the primary action four times before succeeding at 1m 44s" is an observation. Observations are comparable across participants; impressions are not.

**Overclaiming from small samples.** Reporting that "Build B is definitively superior" from five participants per group is not supported by the data. Report the pattern, qualify the conclusion, and let the evidence speak at its actual strength. A well-qualified conclusion from a small sample demonstrates analytical rigour. An overconfident conclusion from a small sample undermines the credibility of the entire analysis.

**Testing too late to act.** Plan Stage 4 sessions to allow at least two weeks between the first session and the submission deadline — enough time to implement and verify at least one round of fixes before the build is locked.

---

## 11. Production Checklist

| Item | Confirmed |
| :-- | :--: |
| Stage 3 audit complete — observations separated from opinions | ☐ |
| Stage 3 unresolved problems listed and prioritised | ☐ |
| Stage 4 validation build locked before session begins | ☐ |
| Cold participants secured for all Stage 4 sessions | ☐ |
| Observation points defined in advance of each session | ☐ |
| Session notes record observations, not interpretations | ☐ |
| Hesitation points mapped spatially and temporally | ☐ |
| Fixes designed as single-variable changes with explicit hypotheses | ☐ |
| A/B comparison variable identified and expressed as a testable hypothesis | ☐ |
| Build A and Build B confirmed to differ in exactly one variable | ☐ |
| Participants assigned to builds in advance — no self-selection | ☐ |
| Identical session conditions confirmed for both build groups | ☐ |
| Metrics defined, quantifiable, and consistently recordable | ☐ |
| Conclusions qualified appropriately for sample size | ☐ |
| No debug artefacts, placeholder content, or dev UI in final build | ☐ |

---

## Reflective Questions

These questions are intended for team reflection after each test session and after the final polish pass.

1. **Stage 3 signal quality.** Review your Stage 3 notes as a team. How many recorded responses are observations (what players did) versus opinions (what players said they felt)? For each opinion, is there a corresponding behavioural observation that supports it? If not, is that opinion acting as evidence it cannot actually provide?

2. **Hesitation mapping.** Mark on a level map or session timeline every point where a participant hesitated for more than ten seconds. What is the pattern? Is there a location, moment, or transition where hesitations cluster? What does the clustering tell you about the readability failure at that point?

3. **Variable control.** Write down every difference between your Build A and Build B. If the list contains more than one item, your comparative test cannot produce interpretable results. What would you need to defer to bring it to a single variable?

4. **Hypothesis testability.** Write your A/B hypothesis in this form: "Build B, which [single change], will produce [specific direction] in [specific metric] compared to Build A." If you cannot complete that sentence with concrete, measurable terms, the hypothesis is not yet testable.

5. **Feedback consistency.** Identify every distinct interaction type in your game. Does each carry a consistent feedback signature — the same class of response every time it fires? Are there any two interaction types that share a signature despite having different meanings for the player? Inconsistency here is a readability failure at the level of interaction language.

6. **Data honesty.** Review your A/B conclusions. Write a one-sentence qualification of each that accurately reflects your sample size: "This result is directional evidence from five participants; consistent with the hypothesis but insufficient to establish it definitively." Does adding that qualification change how you would present the decision in your submission? It should not — honest qualification of evidence is analytical rigour, not weakness.

7. **Report readiness.** For each required GCA1 Results component — summary statistics table, 95% confidence interval, group comparison plot, correlation matrix — can you point to the session data that generates it? If any component has no corresponding data, the session design has a gap that must be addressed before Week 11. What would you add to the session protocol to close it?

---

## Appendix A: Glossary

**A/B testing.** A comparative test in which two builds differ in exactly one variable. The relative performance of both builds on a defined metric produces evidence for or against a specific design decision.

**Behavioural observation.** A recorded account of what a participant does during a test session, expressed without interpretation or attributed cause. The foundation of valid playability analysis.

**Cold participant.** A test participant who has not previously seen or played the game being tested. The essential condition for valid validation and comparative testing.

**Comparative testing.** A test designed to evaluate the relative performance of two design variants on a defined metric. Requires a single-variable build setup, identical session conditions, and explicit participant assignment.

**Confound.** An unintended variable difference between Build A and Build B that makes the comparison uninterpretable. Any difference other than the intended test variable is a confound.

**Confounding variable.** An extraneous variable that is systematically linked to which build a participant plays, meaning it could explain the result instead of — or alongside — the independent variable. Confounds make comparative results uninterpretable if not identified and controlled.

**Dependent variable.** The outcome being measured in a comparative test — the metric expected to change in response to the independent variable. Must be quantifiable and observable.

**Directional evidence.** A result from a small-sample comparative test that identifies a consistent pattern without establishing it definitively. The appropriate category of conclusion for tests with five participants per group.

**Final craft pass.** A structured readability audit conducted on a locked build before submission. Addresses clarity and communication only — no new features.

**Hesitation point.** A moment or location where a participant pauses, repeats a failed attempt, or scans without acting. Indicates a readability failure at that point.

**Independent variable.** The single design element deliberately changed between Build A and Build B in a comparative test. Everything else in the test should be held constant.

**Metric.** A quantifiable measure of a specific player behaviour or outcome, reproducible consistently across sessions by any observer.

**Observation.** A recorded account of participant behaviour expressed without interpretation. Distinct from opinion, which attributes a cause, feeling, or intent to the participant.

**Playability.** The degree to which a first-time player can understand what to do, interpret the game state, act effectively, and receive clear feedback — without assistance from the development team.

**Single-variable requirement.** The absolute constraint that a comparative A/B test must differ between builds in exactly one variable. Any additional difference prevents interpretation of results.

**Extraneous variable.** Any factor that varies between sessions but is not the focus of the test. Not necessarily harmful, but must be identified, managed, and noted in the report's limitations.

**Testable hypothesis.** A specific, falsifiable claim naming the variable under comparison, the expected direction of effect, and the measurement instrument.

**Validation testing.** Structured observation of first-time players completing the game, aimed at identifying where the player experience breaks down so that those breakdowns can be addressed before submission.

---

## Appendix B: Confound Reference

A **confound** is any variable, other than the independent variable under test, that could plausibly explain the result. Confounds do not always invalidate a test, but they must be identified before testing, controlled where possible, and honestly reported as limitations where control was not possible. An unacknowledged confound is not just a methodological weakness — it is a claim that your result means more than it does.

### Why Confounds Matter in Game Testing Specifically

Game playtesting is unusually vulnerable to confounds compared to other forms of user testing. The participant is expected to learn a novel system, apply that learning under observation, and produce behaviour that reflects the design rather than their own prior experience or the test conditions. Each of those requirements is a potential confound source. A participant who has played similar games will learn faster. A participant who is being watched by the developer will play more carefully. A participant at the end of a long session will play differently from one at the start. None of these effects are about the design variable under test.

### Confound Taxonomy

The following table provides a structured reference for the confound types most relevant to Stage 4 game testing. The **Likelihood** column reflects how often each type appears in classroom-based staged playtesting at this scale. The **Control Strategy** column gives the most practical intervention available.

#### Player-Related Confounds

| Confound | Description | Likelihood | Control Strategy |
| :-- | :-- | :-- | :-- |
| Skill level | Participants vary in experience with 3D games, mouse-and-keyboard, or controllers. An experienced player will navigate, interact, and recover from failures faster regardless of which build they play. | High | Randomise assignment to builds. Note each participant's self-reported experience level. Flag outliers in the Discussion. |
| Prior familiarity | A participant who has seen the game, watched others play, or knows a puzzle solution is not equivalent to a first-time player. Their results are not valid for comparison. | High | Exclude from comparative analysis. Use cold participants only. Brief all team members not to discuss the game before or during the session. |
| Fatigue and mood | A tester at the end of a long class session, or after completing multiple other tests, may perform differently on timed and effort-based metrics. | Medium | Schedule comparative sessions at the start of available testing time where possible. Note session order in the Methodology. |
| Misunderstood objective | If one participant understands the session goal immediately and another does not, the difference may reflect briefing clarity rather than the variable under test. | Medium | Use a standardised written briefing read verbatim. Do not answer questions about objectives during the session. |

#### Testing-Environment Confounds

| Confound | Description | Likelihood | Control Strategy |
| :-- | :-- | :-- | :-- |
| Noise and distraction | Multiple groups testing simultaneously in one room creates audio and visual distraction that affects concentration and audio feedback perception. | High | Seat participants as far from other active sessions as possible. Use headphones if audio is part of the design under test. Note room conditions in the Methodology. |
| Hardware differences | Screen size, frame rate, mouse sensitivity, controller quality, headphones versus speakers, and seating position can all alter the felt experience independently of the build. | High | Use the same machine and peripheral setup for all participants in both build groups. Document hardware specifications in the Methodology. |
| Time pressure | If some participants feel observed and rushed and others do not, completion times and stress responses become less comparable. | Medium | Give all participants the same time allocation. Do not hover. Inform participants before the session that there is no time pressure. |
| Order effects | A participant who plays Build A before Build B carries learning and familiarity from the first session into the second, making the second session unrepresentative of a first-time player. | High | Never allow the same participant to play both builds. Assign each participant to one build only. |

#### Build-Related Confounds

| Confound | Description | Likelihood | Control Strategy |
| :-- | :-- | :-- | :-- |
| Bugs and instability | A broken interaction, missed trigger, collision fault, or UI error distorts results entirely. A participant who cannot complete an interaction because of a bug is not providing data about the design variable. | High | Test both builds end-to-end on the session machine before participants arrive. Fix all known bugs in both builds before testing begins. |
| Performance variation | Poor frame rate, stutter, input lag, and loading hitches make mechanics feel worse than their design intent regardless of what has changed between builds. Given this module's emphasis on profiling and optimisation, performance should be treated as a first-class confound. | High | Profile both builds on the session machine before testing. Target a consistent, stable frame rate in both. Report average frame rate in the Methodology. |
| Uneven verbal assistance | If team members provide more verbal guidance to some participants than others — intentionally or not — the comparison is no longer between the two builds. | High | Enforce a strict no-intervention protocol before the session begins. The observer records events silently. Designate one team member as the session controller with authority to redirect other team members who break the protocol. |
| Multiple simultaneous changes | If Build B differs from Build A in more than one way — even unintentionally — a result cannot be attributed to the intended variable. | High | Conduct a deliberate diff of both builds before testing. Document every difference. If unintended differences exist, resolve them or reclassify the variable under test. |

#### Social Confounds

| Confound | Description | Likelihood | Control Strategy |
| :-- | :-- | :-- | :-- |
| Peer influence | Participants seated beside each other may overhear solutions, copy behaviour, or align responses based on social context rather than genuine experience. | Medium | Seat participants so they cannot see each other's screens. Conduct sessions one at a time where participant numbers allow. |
| Developer presence effect | Players tend to give more generous feedback and avoid frustration signals when the development team is visibly present, particularly if standing directly behind the participant. | High | Sit the team away from the participant's immediate sightline during the session. Do not react visibly to player behaviour during play. |
| Group observation effects | Some participants perform and verbalise differently when watched than when alone — either more carefully or more self-consciously. | Medium | Minimise the number of observers in the session space. One designated observer is sufficient. |

### Confound Priority for Stage 4 Testing

Not all confounds are equally likely or equally consequential. The following six represent the highest-priority threats to the validity of Stage 4 comparative results at this project scale. Address these before addressing any others.

**1. Puzzle knowledge carryover.** Once any participant has seen a puzzle solution — or heard it discussed — they are no longer a valid cold tester for that puzzle. This is the single most common validity failure in escape room playtesting. Brief all team members to avoid discussing solutions anywhere that waiting participants might overhear.

**2. Uneven hinting by the team.** Groups consistently vary in how much informal verbal guidance they provide during sessions, often without realising it. A single unscripted hint — "you might want to look over there" — can change a completion time by minutes and invalidate the comparison. Enforce the no-intervention protocol with the same rigour you apply to the single-variable requirement.

**3. Performance and frame-rate differences between builds.** In Unreal Engine projects, even minor Blueprint changes can affect rendering cost, particularly in scenes with Lumen, Niagara, or many dynamic lights. If Build B runs at noticeably lower frame rate than Build A, any negative result for Build B may reflect performance rather than the design change. Profile both before testing.

**4. Tester background differences.** Year 1 and Year 2 students used as participants have systematically different baseline familiarity with 3D game controls than Year 4 students. This difference will produce a predictable pattern — earlier-year students will perform worse on timed and navigation metrics regardless of which build they play. If you use mixed-year participants, record year of study for each participant and note it in your analysis.

**5. Testing-room noise and crowding.** In a classroom-based staged playtest with multiple groups running sessions simultaneously, ambient noise affects audio perception, attention, and self-consciousness. If your design under test involves audio feedback, sound cues, or ambient atmosphere, room noise is a high-priority confound and must be documented.

**6. Unintended multiple changes between builds.** The most common reason a comparative result cannot be interpreted is that Build B differs from Build A in more than one way — a variable the team intended to change, plus one or more they did not notice. This can happen when a scene is re-lit for Build B, when an asset update changes collision or interaction behaviour, or when a performance fix inadvertently changes a mechanic. The diff of both builds before testing is not optional.

### Reporting Confounds in the GCA1 Report

Confounds that were identified and controlled should be described in the **Methodology** section: "Participants were assigned to builds in advance to prevent order effects. Sessions were conducted on the same machine with identical hardware to control for performance variation."

Confounds that were identified but not fully controlled should be reported in the **Discussion** as limitations: "Ambient noise in the testing room during Stage 4 may have affected participants' ability to register audio feedback cues, potentially confounding the comparison of feedback modalities between builds."

Confounds that were not identified until after testing — discovered during analysis — should be reported in the **Discussion** as post-hoc limitations with an assessment of their likely impact on the result: "On review, two participants assigned to Build B were Year 1 students with limited prior experience with 3D controls. This represents an unbalanced assignment that may have contributed to the longer completion times observed in that group."

A report that acknowledges confounds honestly and reasons about their likely impact demonstrates a higher level of analytical rigour than one that reports results without qualification. Examiners do not penalise honest limitations — they penalise the absence of them.
