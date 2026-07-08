# Issue #9 Progress Handoff - AI-Assisted Classification of MHTERM Entries

Written mid-session on July 7, 2026 to hand off to a fresh chat (previous chat got too long / token-heavy). Updated same day after completing two additional batches of 200 terms each.

## Where things stand

Out of 3,898 cleaned unique MHTERM values (from issue #5's output, file mhterm_unique_clean.csv already in this repo), **2,021 terms have been manually read and classified** using real clinical judgment (not just keyword matching). The full list of decisions is in `classification/compact_overrides.txt` in this repo, one term per line, pipe-delimited, in the format:

```
TERM TEXT|CODE
```

Where CODE is one of: C=CVD, P=COPD, D=T2D, R=RMD, N=NOT_A_HEALTH_CONDITION, O=OTHER_CONDITION_NOT_TRACKED (real condition, just not one of the 4 tracked categories), W=NEEDS_REVIEW.

Of the W (NEEDS_REVIEW) entries in that file, all of them are DECIDED and just waiting on Megan's answer to the July 7 mentor question (questions-for-mentor/2026-07-07.md) - they are hypertension, cholesterol/lipid/triglyceride, obesity/metabolic syndrome, and vague-MSK-pain-or-symptom-without-diagnosis terms (arthralgia, back pain, joint pain, myalgia, decreased range of motion, etc). Nothing more to decide on these until she answers - do not re-review them.

**About 1,877 of the original 3,898 terms remain genuinely unread** (not in compact_overrides.txt, and not resolved by the early pattern-matching pass either). To find exactly which ones, regenerate as described below.

## How to regenerate the current full state and find what's left

1. Load `mhterm_unique_clean.csv` from this repo (3,898 rows, column MHTERM_clean). Note: this CSV is not currently checked into the repo - it lives in the project files; if starting a fresh session without project file access, ask the user for it.
2. Load `classification/compact_overrides.txt` and parse into a dict of term -> category (expand the letter codes above).
3. Any term in mhterm_unique_clean.csv NOT present as a key in that dict is still unclassified and needs the same manual reading process.

## The methodology rules established (apply these to the remaining terms)

1. **Conservative default**: only count a term as CVD/COPD/T2D/RMD if it names an actual, specific diagnosis - not a risk factor, not a vague symptom, not a lab value alone. This was Mohamed's explicit decision, confirmed in questions-for-mentor/2026-07-01.md and 2026-07-07.md.

2. **Risk factors and vague symptoms go to NEEDS_REVIEW (pending mentor), not straight to excluded**: specifically hypertension, high cholesterol/hyperlipidemia/hypertriglyceridemia, obesity, and metabolic syndrome (the composite of those). Every spelling variant and abbreviation of these terms found so far has been tagged NEEDS_REVIEW - keep doing this for any new variants found in the remaining terms.

3. **MSK pain/symptom-without-diagnosis also goes to NEEDS_REVIEW**: arthralgia, back pain, joint pain, neck pain, shoulder pain, hip pain, knee pain, decreased range of motion, muscle aches/myalgia - i.e. any joint or muscle-region symptom that doesn't name an actual diagnosed condition. This was extended from the original "chronic ankle pain" example in the mentor question, on the reasoning that it's the same category of problem (symptom vs. diagnosis) and RMD is exactly the category this affects.

4. **Diagnoses that ARE counted as RMD**: osteoarthritis, arthritis (plain, unqualified), gout, rheumatoid arthritis, herniated/bulged/compressed discs, degenerative disc/joint disease, spinal stenosis, radiculopathy/radiculitis/sciatica (nerve compression from disc disease), meniscus tears, tendinosis/tendinopathy (chronic, e.g. Achilles tendinosis, tennis/golfer's elbow), fibromyalgia, congenital joint dysplasia, arthropathy/arthrosis, ankylosing spondylitis, medial/lateral epicondylitis, disc herniation described anatomically (e.g. "C6 disk hernia").

5. **Diagnoses NOT counted as RMD (localized/mechanical, kept as OTHER_CONDITION_NOT_TRACKED)**: bursitis, adhesive capsulitis (frozen shoulder), carpal tunnel syndrome, plantar fasciitis, impingement syndrome, flat feet, acute joint injuries/sprains/dislocations. Bone fractures are also excluded from RMD - they are acute trauma, not the chronic/degenerative disease Paper 1's RMD category targets, and get NOT_A_HEALTH_CONDITION like other injuries. Reasoning on the localized/mechanical exclusions is a judgment call, not confirmed by Megan - worth flagging if it matters later.

6. **CVD**: includes standard cardiac/vascular diagnoses (MI, CAD/CAD abbreviation, CHF/CHF abbreviation, cardiomyopathy, arrhythmias including AFib/bradycardia/PVCs/heart blocks, valve disease, stroke/CVA/TIA, DVT/PE/blood clots, atherosclerosis and coronary artery calcification/disease, carotid artery stenosis/blockage, congenital heart defects, structural findings like LV hypertrophy or atrial enlargement, aneurysms - aortic and other arterial, angina). A diagnosis noted with a secondary "status post" procedure (e.g. "CAD s/p stent") keeps the diagnosis's CVD code since the diagnosis is still the dominant descriptor - this differs from cases where the procedure is the dominant descriptor (see rule 10). Does NOT include: hypertension (pending), murmurs (usually benign), edema alone (too nonspecific), varicose veins (kept as OTHER), venous/vascular anomalies described as congenital/developmental and benign. Cardiac procedures themselves (CABG, stent placement, pacemaker, cardiac catheterization, angioplasty, carotid stenting) are NOT_A_HEALTH_CONDITION - they are interventions, not diagnoses, even though they imply an underlying CVD diagnosis; only code the diagnosis as CVD when the diagnosis itself is actually named in the term.

7. **T2D**: diabetes mentioned without Type 1/gestational/juvenile qualifier defaults to T2D (reasonable given adult melanoma trial population), including plain "diabetes" and abbreviations like DM, DM2, DM II. Diabetes complications (diabetic neuropathy, diabetic retinopathy, diabetic dyslipidemia, diabetic hyperlipidemia) count as T2D since they imply the underlying diagnosis. Type 1 diabetes explicitly excluded. Gestational/antepartum diabetes excluded (different pathophysiology, resolves postpartum). Prediabetes-type language (impaired fasting glucose, glucose intolerance, elevated/high glucose alone, "borderline diabetes," "pre-diabetes") does NOT count - these are lab findings/risk states, not a diabetes diagnosis, UNLESS explicitly qualified as "DM Type II" or similar.

8. **COPD**: explicit COPD/emphysema (including "centrilobular emphysema")/chronic bronchitis language. Bronchiectasis, asthma, and other chronic lung conditions do NOT count (distinct diagnoses).

9. **Lab values, vital signs, and isolated findings** (ALT/AST, alkaline phosphatase, bilirubin, creatinine, electrolytes, blood counts, edema, murmurs, EF percentages, hearing loss, etc.) are OTHER_CONDITION_NOT_TRACKED, not diagnoses.

10. **Condition + procedure combos** (e.g. "cholecystectomy due to cholelithiasis," "fibroids and subsequent hysterectomy," "cholecystitis (gallbladder) surgery") get NOT_A_HEALTH_CONDITION when the procedure is the dominant descriptor and the underlying condition is minor/benign. This also applies to terms that are just a bare procedure noun like "X excision," "X surgery," "X removal," "X repair," "X biopsy" (e.g. "basal cell carcinoma excision," "ACL repair," "cataract surgery," "CABG," "coronary artery bypass graft") - these get NOT_A_HEALTH_CONDITION regardless of how significant the implied underlying diagnosis is, since the term names the intervention, not the diagnosis. Exception: when a real diagnosis of clinical significance is named alongside a status-post note rather than being wholly subordinated to a procedure name (e.g. "cervical cancer with hysterectomy," "CAD s/p stent"), the diagnosis's own code is used instead of N - judgment call on where "dominant descriptor" tips from diagnosis to procedure; treat cancer diagnoses as keeping their own code even when a procedure is mentioned alongside.

11. **Allergies and vaccine/drug reactions** (e.g. "allergic to penicillin," "allergy to IV contrast," "cat allergy," "dairy allergy," named-drug allergies) are NOT_A_HEALTH_CONDITION, consistent with the existing pattern for allergy entries already in the overrides file. Note: allergic rhinitis / hay fever / seasonal allergies as a standing diagnosis are also coded N in this dataset (matches prior precedent already in the file), distinct from OTHER_CONDITION_NOT_TRACKED conditions like atopic dermatitis or asthma.

## What to tell a fresh Claude chat to resume

Point it at this file (classification/HANDOFF_issue9_progress.md) and classification/compact_overrides.txt in the repo. Ask it to: regenerate the not-yet-classified list using the method above, then continue the same batch-by-batch manual reading process (roughly 200 terms per batch), applying the rules above, and appending new decisions to compact_overrides.txt (same pipe-delimited format, letter codes). Once all terms are read, the pending-mentor items just need Megan's answer before issue #9 can close and hand off to issue #7 (wide-format matrix) and issue #8 (spot-check).

Note on committing to GitHub: when updating compact_overrides.txt, build the full merged file content as a Python string inside the remote workbench (fetch current file via GITHUB_GET_REPOSITORY_CONTENT, append new lines as a string literal, then commit via GITHUB_COMMIT_MULTIPLE_FILES using run_composio_tool) rather than pasting a large base64 blob into a tool call directly - large base64 payloads (over roughly 40-50KB) risk silent truncation when passed as literal tool-call arguments. Also note: raw.githubusercontent.com is CDN-cached and can lag behind the actual repo state for several minutes after a commit - verify commits by re-fetching via GITHUB_GET_REPOSITORY_CONTENT (the live API), not by curling the raw URL.
