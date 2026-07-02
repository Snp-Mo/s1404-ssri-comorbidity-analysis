# S1404 Trial Paper - Plain-Language Summary

## What this paper is

This is the main publication reporting results of the S1404 trial itself,
the study your whole project's data comes from. It's a large randomized
trial (1,301 patients) comparing pembrolizumab (an immunotherapy drug)
against older standard treatments (high-dose interferon or ipilimumab) in
patients with high-risk melanoma that had been surgically removed.

"High-risk resected" means: the visible tumor was already cut out by
surgery, but the patient's melanoma was aggressive/advanced enough that
doctors worried it could come back. This kind of treatment given after
surgery to try to prevent the cancer returning is called "adjuvant therapy."

## What it found

- Patients on pembrolizumab were less likely to relapse (their cancer
  coming back) than patients on the older treatments. This was a
  statistically meaningful result.
- Patients on pembrolizumab did not show a statistically significant
  difference in overall survival (how long they lived, period) compared to
  the older treatments, even though relapse was reduced. This can happen
  when relapsed patients still get treated effectively afterward, softening
  the survival difference.

## What you need to take away for your project

This paper is where your two key outcome measures come from:

- **RFS (recurrence-free survival)**: time from joining the trial until the
  cancer comes back or the patient dies, whichever happens first. If neither
  happened by their last check-in, they're "censored", you know they were
  okay for at least that long, but not what happened after.
- **OS (overall survival)**: time from joining the trial until death from
  any cause. Same censoring idea applies if they're still alive at last
  contact.

Your SURTIM/SURIND columns are OS; your RFS/R columns are RFS. This
paper is also where PS (performance status), STAGE, PDL1, and BRAF
come from as clinically meaningful variables, they're standard things
doctors record about a melanoma patient's condition at enrollment.

## Keywords

- **Adjuvant therapy** - treatment given after the main tumor is removed, to
  try to prevent the cancer from coming back.
- **Relapse / recurrence** - the cancer returning after treatment.
- **Overall survival (OS)** - how long a patient lived, from any cause of
  death.
- **Recurrence-free survival (RFS)** - how long a patient went without the
  cancer returning (or without dying).
- **Censored** - a patient's outcome is unknown past their last check-in
  because the event (relapse/death) hadn't happened yet.
- **Randomized trial** - patients are randomly assigned to one treatment
  group or another, to make the groups as comparable as possible.
- **Performance status (PS / Zubrod / ECOG)** - a 0-4 scale describing how
  functionally able a patient is (0 = fully active, 4 = completely
  disabled).
