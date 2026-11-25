# JaundiceCheck: Smartphone Screening for Newborn Jaundice During Home Visits

**NeuraViz AI Challenge 2026–27 — Stage 2 Idea Submission**

The [public challenge page](https://neuraviz.com/aichallenge2026/) asks entrants to describe the problem and their AI solution. Its FAQ says the NeuraViz team reviews each idea; the page does not publish a detailed scoring rubric or weights.

**One-line summary:** JaundiceCheck proposes an offline smartphone tool to help India's community health workers identify newborns who may need a bilirubin blood test during routine home visits.

## 1. The Problem

Jaundice is common and usually benign in term and late-preterm newborns. [1] Very high bilirubin can cause kernicterus, a permanent neurological condition. [2] Total serum bilirubin (TSB) usually peaks on days 3–5, and judging bilirubin by appearance alone is unreliable, particularly in newborns with darker skin. [1, 2]

Under India's Home-Based Newborn Care (HBNC) program, the national job aid schedules Accredited Social Health Activist (ASHA) visits on days 3, 7, 14, 21, 28, and 42 after facility births, with an additional visit on the day of birth for home births. [3, 4] The job aid lists yellow palms and soles as a sign for referral. [4] The scheduled day-3 visit therefore overlaps the usual bilirubin peak window. [1, 4]

A Hyderabad hospital study cited cost as a barrier to making transcutaneous bilirubin meters available at all centers; it did not measure ASHA access or procurement costs. [5] **Assumption to check locally:** equipping every ASHA with a meter would be unaffordable in the pilot district. The design question is whether a phone could add a useful screening signal without delaying an existing referral.

## 2. The AI Solution

JaundiceCheck would guide an ASHA to capture a skin photo with a printed color reference and a paired image of the white of the eye. A lightweight, quantized convolutional network would extract image features on the phone; a small gradient-boosted model would combine them with age in hours and gestational age to estimate whether an infant should be referred for a blood test. Color calibration would aim to reduce capture variation, not eliminate it. **Feasibility hypothesis:** ASHAs can capture usable images on the phones they carry under typical home lighting.

Published work provides a starting point, not validation of JaundiceCheck: the Hyderabad study compared color-card smartphone chest photos with TSB in 143 newborns and reported a correlation of 0.60. A separate 37-newborn hospital pilot evaluated smartphone sclera images against TSB using a different method to adjust for ambient light. Neither study tested this combined workflow during ASHA home visits. [5, 6]

The app would be a screening aid, not a diagnosis or a replacement for HBNC checks. It would prompt a retake for poor images and recommend referral if the second capture is unusable or the model is uncertain. A low-risk result would never cancel a referral indicated by standard care. The clinical team would set the pilot's referral criteria in advance; blood TSB, not the app estimate, guides treatment decisions. Published treatment guidance uses age in hours, gestational age, and neurotoxicity risk factors. [2, 4]

**Validation and feasibility plan.** With ethics approval and consent, aim to enroll 2,400 newborns born at 35 weeks' gestation or later: 1,600 for development and 800 for a locked test at separate sites, targeting at least 150 reference-positive infants in that test. Pair images and blood TSB at the same encounter; clinical reviewers blinded to app output would classify whether each infant meets the protocol's predefined TSB referral criterion. Test the referral decision at **target sensitivity ≥95% and specificity ≥75%**, counting unresolved captures and uncertain outputs as referrals. Report 95% confidence intervals, sample counts, and ungradable rates overall and by documented light, medium, and dark skin-tone groups using a standard shade chart; at least six Android models spanning budget and mid-range devices; and daylight, typical indoor, and dim indoor lighting. Report gaps where subgroup counts are too small to draw conclusions.

**Field check.** If the benchmark is met, run a supervised, silent ASHA pilot in one block: collect usability and image-quality data without letting the app change care. Test offline operation, time per screen (target: under two minutes), and whether mothers and other caregivers understand the proposed referral message.

**Consent and oversight.** Before taking photos, the ASHA would explain the tool and ask permission in the caregiver's preferred language. Declining would not affect care. Home-visit photos would be processed on the phone and not saved by default. Keeping any photos for research would require separate consent and an approved plan for who can access them and when they are deleted. A designated pediatric lead would review false negatives and image failures by subgroup and keep the tool out of care decisions if there are unresolved safety issues or too little subgroup evidence to judge performance.

## 3. Expected Impact

**Hypothesis:** adding a screening signal at an already scheduled visit could help ASHAs identify newborns who need assessment sooner, without sending too many families for unnecessary testing. Newborns and their families would be the primary beneficiaries; ASHAs would get a second input for their referral decision, and clinics could see more timely referrals. A later comparative pilot would measure time from visit to confirmed TSB test and referrals per reference-positive infant versus usual care. These are proposed benefits, not demonstrated outcomes.

### References

1. Canadian Paediatric Society, Fetus and Newborn Committee (principal authors: Keith Barrington and Koravangattu Sankaran). [Guidelines for detection, management and prevention of hyperbilirubinemia in term and late preterm newborn infants (35 or more weeks’ gestation) – Summary](https://pmc.ncbi.nlm.nih.gov/articles/PMC2528724/). *Paediatrics & Child Health*. 2007;12(5):401–407. DOI: [10.1093/pch/12.5.401](https://doi.org/10.1093/pch/12.5.401). Used for background, not pilot treatment thresholds.
2. Kemper AR, Newman TB, Slaughter JL, et al. [Clinical Practice Guideline Revision: Management of Hyperbilirubinemia in the Newborn Infant 35 or More Weeks of Gestation](https://pubmed.ncbi.nlm.nih.gov/35927462/). *Pediatrics*. 2022;150(3):e2022058859. DOI: [10.1542/peds.2022-058859](https://doi.org/10.1542/peds.2022-058859).
3. National Health Mission, Himachal Pradesh. [Home-Based Newborn Care](https://nhm.hp.gov.in/child-health/community-based-care/hbnc). Program page, undated; lists schedules for facility and home births.
4. National Health Mission, India. [Job Aid for Home Visits by ASHA (Newborn and Young Child)](https://nhm.gov.in/New-Update-2022-24/CH-Programmes/HBNC-&-HBYC-Resource-%20Material/HBNC_&_HBYC_Jobaid_for_ASHA.pdf). Undated; see “About Home Based Care” and “Key Tasks & Messages During Home Visits.”
5. Lingaldinna S, Konda KC, et al. [Validity of Bilirubin Measured by Biliscan (Smartphone Application) in Neonatal Jaundice – An Observational study](https://doi.org/10.3126/jnps.v40i3.29412). *Journal of Nepal Paediatric Society*. Published online 2021;40(3). DOI: 10.3126/jnps.v40i3.29412.
6. Outlaw F, Nixon M, Odeyemi O, MacDonald LW, Meek J, Leung TS. [Smartphone screening for neonatal jaundice via ambient-subtracted sclera chromaticity](https://doi.org/10.1371/journal.pone.0216970). *PLOS ONE*. 2020;15(3):e0216970. DOI: 10.1371/journal.pone.0216970.

### Claim audit

| Claim or premise | Source or status |
| --- | --- |
| Jaundice is common and usually benign in term and late-preterm newborns. | [1], abstract and background. |
| Very high bilirubin can cause kernicterus, a permanent neurological condition. | [2], introduction. |
| TSB usually peaks on days 3–5. | [1], “Who should have their bilirubin concentration measured, when and how?” |
| Visual assessment alone is unreliable, particularly in newborns with darker skin. | [1], same section; [2], visual estimation section. |
| HBNC schedules ASHA visits on days 3, 7, 14, 21, 28, and 42 after facility birth, plus a birth-day visit for home births. | [3], schedule; [4], “About Home Based Care.” |
| The ASHA job aid lists yellow palms and soles as a sign for referral. | [4], “Key Tasks & Messages During Home Visits.” |
| The scheduled day-3 visit overlaps the usual TSB peak window. | Inference from [1], [3], and [4]; not a claim about actual visit timing or attendance. |
| A Hyderabad study cited cost as a barrier to availability of transcutaneous bilirubin meters at all centers. | [5], abstract and introduction; not a price estimate. |
| Providing a meter to every ASHA would be unaffordable in the pilot district. | **Assumption**; verify local prices, access, and budgets. |
| ASHAs can capture usable images on their phones in typical home lighting. | **Feasibility hypothesis**; test in the field. |
| The Hyderabad Biliscan study compared color-card chest photos with TSB in 143 newborns and reported a correlation of 0.60. | [5], methods and results. |
| A 37-newborn hospital pilot studied ambient-adjusted smartphone sclera images against TSB. | [6], abstract and methods. |
| Neither study tested the combined ASHA home-visit workflow. | [5, 6], study settings and methods. |
| TSB guides treatment; published thresholds account for age in hours, gestational age, and neurotoxicity risk factors. | [2], Key Action Statement 3 and treatment figures. |
| The tool could lead to earlier assessment without excessive additional referrals. | **Impact hypothesis**; test against usual care. |

The model, workflow, dataset sizes, and performance figures above are proposals and targets, not clinical findings. This is an idea-only submission.
