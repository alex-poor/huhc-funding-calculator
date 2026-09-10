# HUHC Funding Calculator

A scenario model for New Zealand general practices and PHOs: enter your High Use
Health Card cohort and see what the **1 July 2026 withdrawal of the HUHC
capitation top-up** costs you per year.

**▶ [Open the calculator](https://alex-poor.github.io/huhc-funding-calculator/)**

No install, no sign-in, no data leaves your browser.

---

## The problem it quantifies

Before 1 July 2026, a HUHC patient reduced a practice's Care Plus-eligible count
— but the practice also received the HUHC capitation top-up for that same
patient. The top-up more than covered the Care Plus reduction, so the practice
was modestly *better off*, and carried no Care Plus service obligation for that
person.

From 1 July 2026 the top-up was removed from first-level capitation. **The Care
Plus deduction was not.**

|  | To 30 June 2026 | From 1 July 2026 |
|---|---|---|
| HUHC capitation top-up | ~$156–$370 by age/sex | **$0 — removed** |
| Care Plus eligible count | reduced by HUHC headcount | reduced by HUHC headcount *(unchanged)* |
| Care Plus rate | $289.18 | $296.8718 |
| **Net per HUHC patient** | **small net gain** | **straight loss** |

The point is not that HUHC patients are discounted in the Care Plus calculation
— that was always true and arguably by design. It is that **the mechanism which
made that discount workable has been withdrawn while the discount itself
remains.**

A wrinkle worth noting: because the deduction is a *whole-person* subtraction,
the Care Plus rate rising to $296.8718 makes the deduction **$7.69 worse** per
HUHC patient, not better.

## What you need to use it

| Input | Where it comes from | Required |
|---|---|---|
| HUHC patients enrolled | your monthly register | yes |
| HUHC top-up rate, per patient p.a. | your own funding records — see below | yes |
| Enrolled population | your monthly register | optional |
| Care Plus potential | your PHO, or estimated from the roll | optional |
| Care Plus rates | pre-filled from the published schedule | pre-filled |

You can enter the cohort as a single total, or broken down by the seven
capitation age bands and sex if you have it — the by-band view lets you apply a
proper age/sex rate card instead of one average.

### The one input you have to supply

**The withdrawn top-up rate is not in the current published schedule**, because
it was deleted. The FY2026/27 capitation workbook carries five streams — First
Contact, Contingent, VLCA, CSC and U14 — and no HUHC column. Prior-year
schedules are not publicly retrievable.

So the model takes the rate as a parameter and **always shows the $156–$370
bracket alongside whatever you enter**. If you hold the real rate card you get
an exact figure; if you don't, you still get a defensible range. Nothing is
silently assumed on your behalf.

## What it deliberately does not do

- **It does not model first-level capitation for the patient.** That does not
  change with HUHC status on either side of 1 July, so it nets to zero here.
- **It does not treat Care Plus as practice funding.** Care Plus is paid to the
  *PHO*, which distributes it. Your figure is an **attributable share** of the
  deduction — what actually reaches your settlement depends on your PHO's
  distribution rules. This matters if you are presenting the number.
- **It does not count SIA or Health Promotion.** HUHC holders are excluded from
  those too (the schedule labels them "Non-HUHC"), worth roughly a further $16
  per HUHC patient per year. The calculator flags this but leaves it out of the
  headline so the 1 July change is not overstated.
- **It accepts no patient-level data.** Counts only.

## Privacy

This is a static page on GitHub Pages. There is **no server, no database, no
analytics, no cookies and no tracking**. Your figures are never transmitted
anywhere — every calculation runs in your own browser.

Your inputs, including the optional practice name, are stored in your browser's
`localStorage` so the page remembers them next visit. That never leaves your
device, and **Reset to defaults** clears it. The PDF export uses your browser's
own print-to-PDF; the file is produced on your machine.

## Sources

- [Capitation rates — Health New Zealand](https://www.healthnz.govt.nz/health-professionals/guidance-standards/topic/primary-care/primary-care-funding-subsidies/capitation-rates)
  — the FY2026/27 workbook, effective 1 July 2026, which carries the Care Plus
  rate of $296.8718 and the Care Plus formula quoted in [docs/METHOD.md](docs/METHOD.md).
- [Annual primary care funding — Health New Zealand](https://www.healthnz.govt.nz/health-professionals/guidance-standards/topic/primary-care/primary-care-funding-subsidies/annual-primary-care-funding)
  — records the 2026/27 reweighting as *"removing High User Health Card specific
  rates from first-level capitation"*.

Full derivation, the verbatim formula and the assumptions are in
**[docs/METHOD.md](docs/METHOD.md)**.

## Running it locally

One file, no build step, no dependencies:

```bash
git clone https://github.com/alex-poor/huhc-funding-calculator.git
cd huhc-funding-calculator
python3 -m http.server 8000   # then open http://localhost:8000
```

Opening `index.html` directly in a browser also works.

## Contributing

Corrections to the funding mechanics are especially welcome — particularly from
anyone holding the **pre-1 July 2026 HUHC rate card**, which would let the model
ship a real age/sex rate table instead of asking each user for one. Please open
an issue or a pull request.

## Licence

[MIT](LICENSE). The funding rates and formula quoted are published by Health New
Zealand and are their material, not covered by this licence.

---

*This is an independent tool. It is not published by, endorsed by, or affiliated
with Health New Zealand | Te Whatu Ora. Verify figures against your own funding
statements before relying on them.*
