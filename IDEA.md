# JaundiceCheck: Smartphone AI Screening for Newborn Jaundice During ASHA Home Visits

**NeuraViz AI Challenge 2026-27 — Stage 2 Idea Submission**

**One-line summary:** An offline smartphone app that lets India's ASHA community health workers photograph a newborn's eye and skin next to a printed color card during routine home visits, estimates bilirubin risk with an on-device AI model, and flags babies who need a blood test before jaundice becomes dangerous.

---

## 1. The Problem

Neonatal jaundice is one of the most common conditions in newborns. Most cases are harmless, but if bilirubin rises too high and is not treated, it can cause kernicterus, a form of brain damage that is permanent and fully preventable. Treatment (phototherapy) is cheap and widely available. The hard part is finding the babies who need it in time.

In India, the timing makes this difficult:

- **Bilirubin peaks after discharge.** Levels usually peak around days 3–5 of life. Many mothers who deliver in public facilities go home within 48 hours, before that peak.
- **Detection happens at home, by eye.** Under the national Home-Based Newborn Care (HBNC) program, ASHA (Accredited Social Health Activist) workers visit newborns on a fixed schedule (days 3, 7, 14, 21, 28, and 42 for facility births). Today they check for jaundice by looking at the baby's skin and pressing on it. This visual check is known to be unreliable, especially on darker skin and in poor indoor light.
- **The tools that work are out of reach.** Transcutaneous bilirubin meters cost too much to give to every ASHA. A blood test (total serum bilirubin) means a trip to a facility, so families only go once the baby looks very yellow, which is often too late.

**Real users and real pain:** ASHA workers make the call alone in a village home, with no device to back them up. Parents often cannot tell normal yellowing from dangerous yellowing. Block-level medical officers end up seeing severe cases late.

## 2. The AI Solution

**JaundiceCheck** is an Android app built for the low-cost phones ASHAs already use. It runs fully offline.

**How it works during a home visit:**

1. The ASHA places a printed **color calibration card** (a cheap laminated card with reference color patches) next to the baby.
2. The app guides her to take two photos with the phone camera: one of the **sclera** (white of the eye) and one of the **skin on the forehead or chest**. On-screen prompts help with framing, focus, and avoiding glare.
3. The app **corrects the color** of each photo using the card's reference patches, so results do not depend on lighting, phone model, or skin tone.
4. An **on-device AI model** estimates a bilirubin range and places the baby in one of three groups, taking the baby's age in hours into account:
   - **Green:** low risk. Continue routine visits.
   - **Amber:** recheck within 24 hours.
   - **Red:** refer now for a blood test and possible phototherapy.
5. The app shows clear instructions in the local language, records the result, and syncs the referral to the existing health record system when the phone has a connection.

**Data inputs:**
- Calibrated sclera and skin images.
- Baby's age in hours, gestational age, and birth weight (already collected during HBNC visits).
- Known risk factors: preterm birth, jaundice in the first 24 hours, or a sibling who needed phototherapy.

**Model approach:**
- A lightweight convolutional network (MobileNet-class, quantized for phones) extracts color and texture features from the calibrated sclera and skin regions.
- A small tabular model (gradient-boosted trees) combines those features with age in hours and the risk factors to predict a bilirubin range.
- The risk groups are mapped to hour-specific bilirubin thresholds from existing clinical guidelines (nomogram-based). The AI estimates the value; the clinical thresholds decide the action.
- **Training data:** paired photos and same-day blood bilirubin results, collected with consent at partner district hospitals and newborn care units. Data collection would deliberately cover a wide range of skin tones, phones, and lighting conditions.

**Safety by design:**
- The app is a **screening and referral tool, not a diagnosis**. When unsure, it defaults to referral.
- Thresholds are tuned for **high sensitivity**: missing a sick baby is much worse than an extra blood test.
- If photo quality is poor, the app asks for a retake. If the retake also fails, it falls back to referral.

## 3. Expected Impact

- **Earlier detection:** babies at risk are flagged during routine home visits around the bilirubin peak, before severe jaundice develops.
- **Fewer preventable brain injuries:** catching high bilirubin in time means treatment with low-cost phototherapy instead of lifelong disability from kernicterus.
- **Fewer unnecessary trips:** low-risk babies stay home, which saves families travel time and lost wages and keeps facility workloads down.
- **More confident frontline workers:** ASHAs get an objective second opinion and a clear next step, replacing a subjective visual check.
- **Better data for planning:** anonymized referral data helps district health teams see where severe jaundice clusters and where phototherapy capacity is needed.

**How success would be measured (pilot):**
- Sensitivity and specificity for detecting babies who need a blood test, compared against blood bilirubin results.
- Average age at referral, and the share of severe cases referred before day 5.
- Number of referrals per confirmed case that needed treatment.
- ASHA usability and time per screening (target: under 2 minutes).

## 4. Feasibility

- **The science has precedent.** Published studies have already estimated neonatal bilirubin from smartphone photos of skin and sclera with a color reference. JaundiceCheck adapts this approach to the ASHA home-visit workflow and to Indian conditions.
- **Low-cost hardware.** It needs a mid-range Android phone and a printed card that costs a few rupees. No extra device is needed.
- **Fits an existing program.** HBNC visits, schedules, and referral paths already exist. The app adds a step to a visit that is already happening, rather than creating a new service.
- **Works offline.** The quantized model runs on the phone, so it works in villages with poor connectivity.
- **Phased rollout:**
  1. Collect paired image and blood test data at 2–3 partner hospitals.
  2. Train and validate the model, including separate checks across skin tones and phone models.
  3. Run a supervised pilot with ASHAs in one block, with outcomes reviewed by pediatricians.
  4. Scale through district health systems after the pilot is validated and regulatory requirements are met.

**Key risks and mitigations:**

| Risk | Mitigation |
| --- | --- |
| Lighting and phone variation | Color calibration card, plus quality checks before each prediction |
| Skin-tone bias | Diverse training data, sclera images (less affected by skin tone), and accuracy reported separately per skin-tone group |
| Over-reliance on the app | Clear screening-only messaging, referral when unsure, and danger signs (poor feeding, lethargy) always override a green result |
| Privacy | Images processed on the device; only the risk result and minimal referral data are synced, with consent |

## 5. Who Benefits

- **Newborns and their families**, especially in rural and low-income areas far from facilities.
- **ASHA workers**, who get a simple, objective tool for a decision they currently make by eye.
- **Doctors and newborn care units**, who see high-risk babies earlier and fewer low-risk ones.
- **District and state health programs**, which get earlier referrals and better data for planning.

---

*This is an idea-stage concept for Stage 2 of the NeuraViz AI Challenge 2026-27. No code is required at this stage.*
