# Method

How the calculator arrives at its figures, what is published fact, and what is
assumption. Every rate below is annual and GST exclusive.

## 1. The Care Plus formula

Health New Zealand's FY2026/27 capitation rates workbook states the Care Plus
calculation verbatim:

> Health New Zealand will make these calculations by applying the percentages
> shown in the table below for each age, gender, ethnicity and deprivation
> category to the equivalent number of Enrolled Persons in each category,
> summing the resulting numbers in each category, and **subtracting from the
> resulting total the number of Enrolled Persons with High Use Health Cards**.

Two things follow, and both matter.

**The eligible count is a sum of probabilities, not a headcount.** Each enrolled
person contributes a *CarePlusPercentage* between 0.005 and 0.41, set by their
age band, sex, ethnicity and deprivation quintile. The sum is the "expected
number of Care Plus patients" — the calculator calls this **Care Plus
potential**. There are 112 combinations in the published table: 7 age bands
(00-04, 05-14, 15-24, 25-44, 45-64, 65-74, 75+) × 2 sexes × 4 ethnicity groups ×
2 deprivation groups (quintiles 1–4, and quintile 5).

**The HUHC deduction is a whole-person subtraction.** This is the crux. A
patient contributes their CarePlusPercentage to the pool whether or not they
hold a HUHC; holding one then removes a full **1.0** from the total. So the
marginal cost of HUHC status is exactly one Care Plus payment — not a
percentage-weighted fraction of one.

That distinction is worth being precise about, because getting it wrong changes
the answer by roughly sevenfold in either direction. On one observed PHO
population the HUHC cohort's average CarePlusPercentage was 0.146, so a weighted
reading would have understated the deduction by a factor of about 6.9.

## 2. Rates used

| Rate | Value | Status |
|---|---|---|
| Care Plus, from 1 July 2026 | **$296.8718** | Published, FY2026/27 workbook |
| Care Plus, to 30 June 2026 | **$289.18** | Editable input; widely cited |
| HUHC top-up | **not published** | **You supply it** — see §3 |

The Care Plus uplift of **+$7.6918** is applied to the deduction, not against
it. Because the formula subtracts a whole person per HUHC holder, a higher Care
Plus rate makes the deduction more expensive. This is a small effect
(~$7.69 per HUHC patient per year) but it runs the opposite way to intuition,
so the calculator surfaces it as its own line.

## 3. The withdrawn top-up rate — the one assumption

The FY2026/27 workbook contains five capitation streams:

- First Contact
- Contingent Capitation
- VLCA (CSC and non-CSC)
- CSC
- Under 14

**There is no HUHC column.** The companion Health NZ page describes the 2026/27
reweighting as *"removing High User Health Card specific rates from first-level
capitation"*, which corroborates the removal directly.

Prior-year schedules carrying the old rates are not publicly retrievable at the
time of writing. The calculator therefore treats the top-up rate as a required
input and displays results at **$156** and **$370** — the range reported by
practices — alongside whatever figure you enter.

If you hold the pre-1 July rate card, please
[open an issue](https://github.com/alex-poor/huhc-funding-calculator/issues) so
the model can ship a real age/sex table.

### Why the rate cannot be recovered from a PHO's own extract

Worth recording, because it is a natural place to look and it is a dead end. On
one PHO's monthly MOH person extract spanning June–September 2026 — that is,
straddling the change — the top-up proved not to be itemised at all. Four
independent checks:

1. Matched age/sex gaps in first-contact capitation between HUHC and non-HUHC
   patients were **unchanged** across 1 July.
2. Patients who *gained* HUHC status were already sitting at the higher rate
   **before** they gained it.
3. Gaining or losing HUHC status moved first-contact capitation by **under
   $0.15 per month**.
4. Every rate value held by a HUHC patient also occurred among non-HUHC patients
   **in the same age/sex band** — in all four monthly extracts checked.

The elevated average for HUHC holders turned out to be selection: they sit
disproportionately in higher-deprivation, higher-multimorbidity cohorts that
attract more capitation anyway. It is not a HUHC premium. The top-up was paid
through a channel the person extract does not expose.

## 4. Care Plus potential

If you know your expected Care Plus patient count, enter it. Otherwise the
calculator estimates it at **6.9% of the enrolled roll**.

That default comes from an observed PHO of 69 practices and ~480,000 enrolled,
where the ratio ran between **3.5% and 10.3%** by practice, at 6.876% PHO-wide.
It is a reasonable starting point and a poor substitute for your real figure —
the spread is wide because it tracks the age, ethnicity and deprivation profile
of your roll.

Care Plus potential only drives the *"share of your Care Plus pot removed"*
output. The forgone dollar amount is simply HUHC headcount × $296.8718 and does
not depend on it.

## 5. Age profile

The by-band view seeds counts from an observed HUHC cohort — roughly **59% aged
65 or over** and **64% female**:

| Age band | Male | Female |
|---|---:|---:|
| 0–4 | 2.8% | 1.6% |
| 5–14 | 0.9% | 1.1% |
| 15–24 | 0.3% | 3.1% |
| 25–44 | 3.1% | 7.5% |
| 45–64 | 6.1% | 14.6% |
| 65–74 | 7.6% | 10.6% |
| 75+ | 15.6% | 24.9% |

These are a starting shape only — HUHC concentration varies enormously between
practices, and so does its age distribution. Replace them with your register.

The skew matters for the total: capitation rates rise steeply with age, so a
cohort this elderly will sit toward the **upper** half of any flat rate bracket.

## 6. What is excluded, and why

**SIA and Health Promotion.** HUHC holders are excluded from these too — the
FY2026/27 workbook labels the tables "Services to Improve Access (Non-HUHC)" and
"Health Promotion (Non-HUHC)", and on observed data every HUHC patient carries
$0.00 in both, in every month checked. Matched against comparable non-HUHC
patients this is worth roughly **$16 per HUHC patient per year**.

It is excluded from the headline deliberately: HUHC holders were excluded from
these streams *before* 1 July too, so it is not part of the change. It is real
money and belongs in a full picture of what a HUHC patient now costs a practice
— which is why the calculator names it — but folding it into the 1 July figure
would overstate the change.

**First-level capitation for the patient.** Unaffected by HUHC status either
side of 1 July. Nets to zero.

## 7. Care Plus is PHO funding

Health New Zealand pays the Care Plus pool to the **PHO**, not to the practice.
The PHO then distributes it.

So a practice-level figure from this calculator is the **attributable share** of
the deduction — the amount the practice's HUHC cohort removes from the pool it
draws on. What actually lands in a practice's settlement depends on the PHO's
internal distribution rules, which are not modelled here and vary between PHOs.

State this when presenting the number. It is the most likely point of challenge,
and conceding it up front is stronger than being corrected on it.

## 8. Formulae

With `H` = HUHC headcount, `T` = top-up rate (or Σ per-band counts × rates),
`P` = Care Plus potential, `R₀` = old Care Plus rate, `R₁` = new Care Plus rate:

```
Care Plus forgone to the deduction      = H × R₁
Care Plus received                      = (P − H) × R₁
Share of pot removed                    = H ÷ P

Net per patient, before 1 July          = T − R₀
Net per patient, from 1 July            = −R₁
Annual swing                            = −( T + H × (R₁ − R₀) ) ... in total
                                        = −( T + (R₁ − R₀) )      ... per patient
```

The swing decomposes into two parts, which the calculator shows separately: the
top-up no longer paid (`H × T`), and the uplift applied to the deduction
(`H × (R₁ − R₀)`).
