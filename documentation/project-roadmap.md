# Project Roadmap

## Deadline

Symposium presentation: August 19, 2026. Working deadline for the analysis itself: August 18, 2026.

## Working philosophy

This is not a fixed week-by-week schedule. Progress happens in sessions, whenever they happen, not on a forced weekly cadence. The goal is steady, cumulative progress so that at any point between now and August 18, there is enough finished, documented work to build a symposium presentation from. Every session that closes an issue or produces a real finding should leave the repository (documentation, mentor questions, closed issues with summary comments) in a state where someone could pick up the story of the project just from reading it.

## Current phase: Phase 1

Phase 1 covers data setup through a baseline comorbidity-adjusted Cox model, answering both research questions for the first time using Paper 1's 4-category comorbidity framework (cardiovascular disease, COPD, type 2 diabetes, rheumatic/musculoskeletal disorders). Issues 1 through 18 track this phase. Progress as of July 7, 2026:

- Closed: issues 1 through 4 (framework decision, PATNO confirmation, medical history counts, initial data load).
- Open, ready to start: issue 5 (extract and clean unique MHTERM values), issue 6 (local R setup, independent of everything else).
- Open, blocked on issue 5: issues 7 through 16 (wide-format matrix, classification, joins, descriptive stats, Cox models, write-up).
- Open, mentor-hold: issue 17 (ongoing, log questions as they come up).
- Open, new as of July 7: issue 18 (review the 17 MHTERM entries missing the MHONGO ongoing marker, possibly branch the dataset into two versions).

## Candidate next steps after Phase 1 closes

These are not committed tasks and nothing has been filed for them yet. Per the project's own working agreement, new tasks for a phase beyond Phase 1 get scoped and filed as issues only after Phase 1's issues are closed and after checking in on direction. Recorded here only so the ideas are not lost:

- Sensitivity analyses on the comorbidity framework choice (e.g., comparing Paper 1's 4-category approach against Paper 2's full Charlson Comorbidity Index scoring).
- Visualizing and reporting the final Cox regression results.
- Writing up findings for research question 2 in more depth.
- Possibly extending into Paper 2's or Paper 3's methods if time and mentor input support it.
- Possibly introducing Python for parts of the free-text classification or data work, and exploring additional tools (e.g., SQL) if they would help.

Which of these (if any) get picked up, and in what order, will depend on how much of Phase 1 is done, mentor feedback along the way, and how much runway is left before August 18.
