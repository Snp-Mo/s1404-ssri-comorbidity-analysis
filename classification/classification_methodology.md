# MHTERM Classification Methodology

(Originally written as the issue #9 progress handoff; kept and renamed as the permanent methodology reference now that issue #9 is closed - the classification rules and W-cluster resolution documented here are needed for issue #8's spot-check and for the eventual methods write-up.)

## STATUS: COMPLETE, INCLUDING ALL W-TAGGED ENTRIES (Updated July 8, 2026)

All 3,898 cleaned unique MHTERM values have been manually read and classified using real clinical judgment (not just keyword matching). The full list of decisions is in `classification/compact_overrides.txt` in this repo, one term per line, pipe-delimited, in the format:

```
TERM TEXT|CODE
```

Where CODE is one of: C=CVD, P=COPD, D=T2D, R=RMD, N=NOT_A_HEALTH_CONDITION, O=OTHER_CONDITION_NOT_TRACKED (real condition, just not one of the 4 tracked categories), W=NEEDS_REVIEW.

## Final tally

- O (other condition, not tracked): 2,164
- N (not a health condition - procedures, allergies, lab values, injuries, family history): 1,373
- W (needs mentor review): 0
- C (CVD): 182
- R (RMD): 134
- D (T2D): 41
- P (COPD): 6

(As of July 8, 2026 - the 281 W entries have all been resolved, see new section below. Tally updated accordingly.)

Total: 3,899 keys covering all 3,898 source terms (one harmless pre-existing duplicate line in the file, both with matching codes - does not affect the classification).

## Resolution of the 280 W-tagged entries (July 8, 2026)

Megan replied to the July 7 mentor question. She did not give a strict item-by-item ruling. Instead she said she does not recognize the RMD abbreviation and was skeptical that something like chronic ankle pain counts as a real comorbidity, said morbid obesity does seem like an important health condition, asked for existing research on what level of evidence other studies use before including a term, and said the point of this step was to avoid item-by-item judgment calls in the first place, and that spending a lot of time on individual terms might not be the best use of time.

Given that, the 281 W-tagged entries were resolved using evidence from the comorbidity literature instead of going back to her with an item-by-item list. What was found:

1. Hypertension is explicitly NOT one of the scored conditions in the standard Charlson Comorbidity Index (CCI) - it's documented in multiple sources as excluded because its individual impact on mortality is too small relative to the conditions CCI does track. All hypertension variants (HTN, essential hypertension, grade 1/2/3, pre-hypertension, "history of hypertension," etc.) were coded N (not counted as CVD). "White coat hypertension" and "white coat syndrome" were also coded N since by definition they describe blood pressure that's only elevated in a clinical setting, not a hypertension diagnosis.

2. High cholesterol / hyperlipidemia / hypertriglyceridemia (all spelling variants) are risk factors, not part of standard comorbidity indices either. Coded N.

3. Obesity, morbid obesity, overweight, central obesity, and metabolic syndrome are also NOT part of the standard CCI - multiple sources on comorbidity indices explicitly note obesity is excluded from CCI and gets analyzed as its own separate variable in cancer/immunotherapy research rather than folded into a cardiovascular or metabolic comorbidity score. Since Megan flagged this one as seeming important, these 13 entries were coded O (other condition, tracked) instead of N (not a health condition). This keeps them out of the four CVD/COPD/T2D/RMD categories (consistent with the literature) but preserves them as a flagged, real health condition in case a separate obesity variable is useful later, rather than throwing that information away.

4. The remaining W entries (arthralgia, joint pain, back pain, neck pain, shoulder pain, myalgia, decreased range of motion, and similar terms with no diagnosis attached) were coded N. This matches Megan's specific skepticism about chronic ankle pain, and matches how CCI's rheumatic/connective tissue disease category works - it requires a specific diagnosis (like rheumatoid arthritis or lupus), not a pain symptom on its own.

5. Two entries, "ANEURYSM" and "ANEURYSM (ASYMPTOMATIC)," were in the W list but don't belong to the four ambiguous risk-factor/vague-symptom buckets above - an aneurysm is an actual vascular diagnosis. These were corrected to C (CVD) rather than left as a pending risk-factor call.

No further review of these entries is needed. This closes out issue #9.

## The methodology rules that were applied throughout

1. **Conservative default**: only count a term as CVD/COPD/T2D/RMD if it names an actual, specific diagnosis - not a risk factor, not a vague symptom, not a lab value alone.

2. **Risk factors and vague symptoms go to NEEDS_REVIEW (pending mentor), not straight to excluded**: hypertension, high cholesterol/hyperlipidemia/hypertriglyceridemia, obesity, and metabolic syndrome.

3. **MSK pain/symptom-without-diagnosis also goes to NEEDS_REVIEW**: arthralgia, back pain, joint pain, neck pain, shoulder pain, hip pain, knee pain, decreased range of motion, muscle aches/myalgia. Exception: when the pain is explicitly attributed to an acute injury or surgery in the term itself (e.g. "neck pain (neck injury)," "back pain from melanoma surgery," "sports related knee pain from jogging"), coded NOT_A_HEALTH_CONDITION instead, since it's clearly a transient post-injury/post-surgical/acute symptom rather than the kind of chronic MSK complaint the pending mentor question is about.

4. **Diagnoses that ARE counted as RMD**: osteoarthritis, arthritis (plain, unqualified, including site-specific), gout (all variants, including "podagra"), rheumatoid arthritis, herniated/bulged/compressed discs, degenerative disc/joint disease, spinal stenosis, radiculopathy/radiculitis/sciatica, meniscus tears described as chronic/degenerative, tendinosis/tendinopathy (chronic), fibromyalgia, congenital joint dysplasia, arthropathy/arthrosis, ankylosing spondylitis, medial/lateral epicondylitis, synovitis, sacroiliitis, rheumatic fever, systemic lupus erythematosus, polymyalgia rheumatica, Scheuermann's kyphosis, spondylolysis/spondylolisthesis, retrolisthesis, generic "skeletal disorder" and "disorder of skeletal system" phrasing.

5. **Diagnoses NOT counted as RMD (localized/mechanical or acute, kept as OTHER_CONDITION_NOT_TRACKED or NOT_A_HEALTH_CONDITION)**: bursitis, adhesive capsulitis (frozen shoulder), carpal tunnel syndrome, plantar fasciitis, impingement syndrome, flat feet, patellofemoral syndrome, rotator cuff tears/tendonitis (mechanical/acute), acute joint injuries/sprains/dislocations/ligament tears (ACL, meniscus described as an acute tear/repair) - these get NOT_A_HEALTH_CONDITION as injuries. Bone fractures of any kind (including stress fractures and osteoporotic fractures) are NOT_A_HEALTH_CONDITION - acute trauma, not the chronic/degenerative disease Paper 1's RMD category targets. This localized/mechanical vs. systemic/degenerative line is a judgment call, not confirmed by Megan.

6. **CVD**: standard cardiac/vascular diagnoses (MI/heart attack/STEMI/NSTEMI, CAD, CHF, cardiomyopathy, arrhythmias including AFib/bradycardia/tachycardia/PVCs/heart blocks/PSVT/SVT/Wolff-Parkinson-White, valve disease, stroke/CVA/TIA, DVT/PE/blood clots/thromboembolic events, atherosclerosis and coronary/carotid artery calcification/stenosis/blockage, congenital heart defects like Tetralogy of Fallot, structural findings like LV hypertrophy, aneurysms, angina, pulmonary hypertension, pericarditis/pericardial effusion). "History of X" phrasing for a CVD diagnosis still counts as CVD. A diagnosis noted with a secondary "status post" procedure (e.g. "CAD s/p stent") keeps the diagnosis's CVD code. Cardiac procedures themselves (CABG, stent placement, pacemaker, cardiac catheterization, angioplasty, carotid stenting) are NOT_A_HEALTH_CONDITION - interventions, not diagnoses - unless the diagnosis itself is also named in the term.

7. **T2D**: diabetes without a Type 1/gestational/juvenile qualifier defaults to T2D, including plain "diabetes" and all abbreviations (DM, DM2, DM II, Type II, etc.) and insulin-dependent diabetes without a Type 1 qualifier. Diabetes complications (neuropathy, retinopathy, dyslipidemia, hyperlipidemia) count as T2D. Type 1 diabetes and gestational diabetes are excluded. Prediabetes-type language (impaired fasting glucose, glucose intolerance, elevated/high glucose alone, "borderline diabetes," "pre-diabetes") does NOT count unless explicitly qualified as "DM Type II" or similar.

8. **COPD**: explicit COPD/emphysema/chronic bronchitis language only. Asthma, bronchiectasis, and other chronic lung conditions do NOT count.

9. **Lab values, vital signs, and isolated findings** (liver enzymes, bilirubin, creatinine, hemoglobin/hematocrit, electrolytes, blood counts, edema, murmurs, hearing/vision loss, rashes, etc.) are OTHER_CONDITION_NOT_TRACKED, not diagnoses.

10. **Condition + procedure combos**: when the procedure is the dominant descriptor of the term (bare procedure nouns like "X excision/surgery/removal/repair/biopsy/resection," or a minor underlying condition combined with its treatment), coded NOT_A_HEALTH_CONDITION regardless of how significant the implied diagnosis is. Exception: when a real diagnosis is the grammatical subject with a status-post or "with" note attached (e.g. "cervical cancer with hysterectomy," "malignant melanoma of left foot," "history of invasive breast cancer"), the diagnosis's own code is used. Melanoma/skin cancer terms follow this split very consistently throughout the dataset (high-frequency term family, expected for a melanoma trial): diagnosis name alone or with site/stage → OTHER_CONDITION_NOT_TRACKED; excision/resection/removal/Mohs/biopsy phrasing → NOT_A_HEALTH_CONDITION.

11. **Allergies and vaccine/drug reactions** are NOT_A_HEALTH_CONDITION. Allergic rhinitis/hay fever/seasonal allergies as a standing diagnosis are also coded N (matches prior precedent in the file), distinct from OTHER_CONDITION_NOT_TRACKED conditions like atopic dermatitis or asthma.

12. **Family history terms** (e.g. "family history colon cancer," "FH: migraine headache") are NOT_A_HEALTH_CONDITION - they describe a relative's condition, not the patient's own history.

13. **Smoking/tobacco/alcohol/substance use status** (current, former, history of) is NOT_A_HEALTH_CONDITION, consistent with prior precedent for "cigarette smoking" and "alcohol use" already in the file.

## Data quirk note

A small number of source terms contain a mangled Unicode replacement character (U+FFFD) - e.g. "EPSTEIN�BARR VIRUS" and "HYPERTRIGLYCERIDEMIA�" - matched byte-for-byte in the overrides file, not stripped or normalized.

## Next steps (once Megan answers the pending question)

1. Apply Megan's ruling to the 280 W-tagged entries, updating them to their final C/D/N/O/R codes (or leaving as excluded, depending on her answer) - likely a quick find/replace pass on compact_overrides.txt.
2. Close issue #9 with a summary comment.
3. Move to issue #7 (wide-format comorbidity matrix) and issue #8 (manual spot-check of ambiguous classifications), both currently blocked on this.

## Technical notes for future sessions (GitHub/Composio lessons)

- When updating compact_overrides.txt, build the full merged file content as a Python string inside the remote workbench (fetch current file via GITHUB_GET_REPOSITORY_CONTENT, append new lines as a string literal, then commit via GITHUB_COMMIT_MULTIPLE_FILES using run_composio_tool) rather than pasting a large base64 blob into a tool call directly - large base64 payloads (over roughly 40-50KB) risk silent truncation when passed as literal tool-call arguments.
- raw.githubusercontent.com is CDN-cached and can lag behind the actual repo state for a minute or two after a commit - verify commits by re-fetching via GITHUB_GET_REPOSITORY_CONTENT (the live API) first, and only fall back to raw.githubusercontent.com (with a short delay) for local bash-side verification.
- GITHUB_COMMIT_MULTIPLE_FILES takes a `message` field, not `commit_message`.
