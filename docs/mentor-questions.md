# Mentor Meeting Notes & Questions

Running log. Add a new dated section each time something comes up worth
asking or reporting. Keep entries short, bullet points, not essays.

---

## Template for each entry

```
## YYYY-MM-DD

### Findings since last check-in
-

### Open questions for mentor
-

### Decisions made (and by whom / why)
-
```

---

## 2026-07-01 (starting point)

### Findings since last check-in
- Confirmed medical history file structure: MHTERM (free text) + MHONGO
  (ongoing flag). No PATNO in the AI-facing copy, as expected per privacy
  protocol.
- Read all three comorbidity/context papers and the main S1404 trial paper.

### Open questions for mentor
- Comorbidity category framework: lean toward Paper 1's 4-category approach
  (CVD/COPD/T2D/RMD) over Paper 2's full CCI, given free-text data without
  ICD codes. Does this tradeoff seem right, or is there a reason to push
  for the fuller CCI despite the extra classification burden?
- Any guidance on how to handle clearly non-clinical entries (e.g., prior
  surgeries, allergies) in the classification step, exclude entirely, or
  keep a separate "other/non-comorbidity" bucket for transparency?
- Any preference on how ongoing vs. resolved conditions (MHONGO) should
  factor into comorbidity classification, count both, or only ongoing?

### Decisions made (and by whom / why)
- (fill in after meeting)
