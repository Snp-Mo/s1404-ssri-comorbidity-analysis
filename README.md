# S1404 - SSRI Use, Comorbidity Burden, and Survival

Private working repo for an undergraduate research project at Fred Hutch Cancer
Center (SeattleStatGROWS internship). This repo holds **planning docs, paper
summaries, and a task board only** - no patient data, no CSVs, no PATNO, ever.
All analysis and real datasets live locally on the researcher's own machine.

## Project purpose

The S1404 trial tested pembrolizumab vs. investigator's choice therapy in
high-risk resected melanoma. A prior analysis found no survival difference
between patients on SSRIs and those not on SSRIs. This project asks whether
that result holds once comorbidity burden is accounted for i.e., whether
SSRI users were systematically healthier or sicker, which could confound the
original estimate. Mouse research motivating this question showed SSRIs may
enhance antitumor immunity by blocking SERT on CD8 T cells.

**Research questions**
1. What was the comorbidity burden in the S1404 trial?
2. Does adjusting for comorbidity burden change the estimated association
   between SSRI use and OS (overall survival) or RFS (recurrence-free
   survival)?

## Repo structure

```
docs/
  paper-summaries/     Plain-language summaries of all reference papers
  mentor-questions.md  Running log of open questions/findings for mentor check-ins
  data-dictionary.md   Column naming conventions only, no data, no values
```

## Data & privacy notes (read before doing anything)

- Real datasets (main trial file, medical history file) are never pushed
  to this repo.
- PATNO (patient ID) is never sent to any AI tool. Classification work is
  done on de-identified free-text terms only; the join back to patient-level
  data happens locally in R.
- This repo is private and should stay that way.

## Status

Tracked via the GitHub Project board attached to this repo (columns: Not
Started, In Progress, Review, Complete, Blocked) and the Issues tab for the
individual task checklist.
