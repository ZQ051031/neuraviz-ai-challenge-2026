# JaundiceCheck

**Smartphone AI screening for newborn jaundice during ASHA home visits**

*Idea submission for the [NeuraViz AI Challenge 2026-27](https://neuraviz.com/aichallenge2026/), Stage 2 (idea only).*

> An offline smartphone app that lets India's ASHA community health workers photograph a newborn's eye and skin next to a printed color card during routine home visits, estimates bilirubin risk with an on-device AI model, and flags babies who need a blood test before jaundice becomes dangerous.

## Problem

Newborn jaundice is common and usually harmless. When bilirubin gets too high and goes untreated, it can cause kernicterus, which is permanent brain damage that cheap phototherapy prevents. In India, many mothers go home within 48 hours of birth, but bilirubin peaks around days 3–5. At that point the only check is an ASHA worker looking at the baby's skin during a home visit, which is unreliable on darker skin and in dim light. Bilirubin meters are too expensive to hand out widely, so dangerous cases are often found late.

## AI Solution

- **Capture:** during a routine Home-Based Newborn Care visit, the ASHA takes guided photos of the baby's sclera and skin next to a low-cost printed color calibration card.
- **Calibrate:** the app corrects color using the card, so results hold up across lighting, phone models, and skin tones.
- **Predict:** a quantized on-device CNN extracts color features. A small tabular model combines them with age in hours, gestational age, birth weight, and risk factors to estimate a bilirubin range.
- **Act:** clinical, hour-specific thresholds turn the estimate into **Green** (routine), **Amber** (recheck in 24 hours), or **Red** (refer now for a blood test). The app works offline and syncs referrals when connected.
- **Safe by design:** it screens, it does not diagnose. It is tuned for high sensitivity, refers when unsure, and danger signs always override a green result.

## Expected Impact

- Babies at risk are found around the bilirubin peak, before severe jaundice develops.
- Fewer preventable kernicterus cases and fewer lifelong disabilities.
- Low-risk babies stay home, saving families travel costs and keeping facility workloads down.
- ASHAs get an objective second opinion. District teams get data on where referrals cluster.

## Feasibility

It builds on published research on estimating bilirubin from smartphone photos. It runs on mid-range Android phones with a printed card, so no new hardware is needed, and it fits into the existing HBNC home-visit schedule. Rollout: collect paired image and blood test data at partner hospitals, validate the model across skin tones and phones, run a supervised pilot in one block, then scale through district health systems.

## Who Benefits

Newborns and families in rural and low-income areas, ASHA workers, newborn care units and pediatricians, and district and state health programs.

---

The full Stage 2 submission text is in **[IDEA.md](IDEA.md)**.
