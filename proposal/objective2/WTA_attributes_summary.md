# Objective 2 — WTA attributes for adopting agroforestry itself (Spain & Italy)

*Answer to the supervisor's comment on Paper 2. The full technical design, with equations, design rules, survey flow, bias control and references, is in [`DCE_technical_annex.md`](DCE_technical_annex.md).*

> **Assumptions.**
> - "ES and IT" means Spain and Italy.
> - "Stetter (2025)" is most likely **Stetter & Sauer (2024), *Ecological Economics* 224:108266** (online 2024). Please confirm with your supervisor.
> - What is known about that paper comes from search snippets. It is a labelled DCE with 198 Bavarian crop farmers. The alternatives are alley cropping, short-rotation coppice and continued arable farming. The attributes are expected yearly contribution margin, margin variability, minimum useful lifetime, a payment for ecosystem services, and ecological-priority-area eligibility.
> - Its exact levels could not be retrieved; read its Table 1.
> - **All levels below are proposals.** Calibrate them with Paper 1's outputs and a pilot.

---

## 1. The core change in one paragraph

The current DCE asks: *"What payment would make you sign this contract?"* Its WTA therefore contains:
- the practice's opportunity cost (OC);
- the cost of the contract terms: duration, monitoring, paperwork, advice, and trust in the payer.

Paper 1's OC contains none of the contract terms.

The revised DCE asks: *"What would you do with this field of yours: plant agroforestry system A, plant system B, or keep your current crops?"* This is a Stetter-style **labelled land-use choice**. Each alternative is a land use described by its own economics and physical characteristics, and there is **no contract, payment, inspection or adviser**. The only money attribute is each land use's **own average yearly net margin (€/ha/yr)**, calculated with **the same accounting as Paper 1's OC**.

The DCE then measures, in euros, the **premium Π** a farmer needs above financial parity before switching. So:

```
WTA_s,i  =  OC_s,i  +  Π_s,i
            Paper 1    Paper 2 (explained by behaviour in Paper 3)
```

---

## 2. Recommended attributes

| # | Attribute (what the farmer sees) | Proposed levels (to calibrate) | Why Paper 3 needs it |
|---|---|---|---|
| 0 | **Alternative label = agroforestry system** (e.g. "Almond rows in your cereals", "Walnut timber rows in your cereals") + **"Keep current crops, no trees"** (status quo) | Exactly the systems Paper 1 costs. Placeholders: **ES** almond rows, walnut/wild-cherry timber rows in rainfed cereals. **IT** hybrid-walnut/cherry timber rows, poplar (Po Valley) or walnut-for-nut rows | Each WTA pairs one-to-one with Paper 1's system-specific OC. The label constant (ASC) *is* the premium Π_s at Paper 1's configuration |
| 1 | **Average yearly net margin of the field (€/ha/yr)**: the **only money attribute**. Crop + tree sales minus all costs that change (planting, protection, pruning, harvest, removal, extra labour), averaged over the tree lifetime at Paper 1's discount rate; CAP excluded | Pivot on the farmer's own current margin. At Paper 1's configuration, AF margin = own margin + d, with **d ∈ {−450, −200, 0, +150, +350, +600} €/ha/yr** (same grid in ES and IT). Away from that configuration, the margin also moves by Paper 1's modelled change in OC | Same unit, baseline, horizon and discounting as Paper 1's equivalent annual value (EAV). The money coefficient converts every other coefficient into €/ha/yr. The range includes negative OC (Mediterranean agroforestry can outperform arable) |
| 2 | **Bad-year income shortfall** (≈1 year in 10), average unchanged | **0.6 / 1.0 / 1.4 ×** the farmer's own current bad-year shortfall | **Risk premium**, compared with an expected-utility benchmark built from elicited risk aversion |
| 3 | **Planned tree lifetime** (trees removed in year T; the field stays agricultural land) | Nut/fruit **15/20/25** yr; timber **ES 30/40/50**, **IT 20/30/40**; poplar **10/12/15**. Paper 1's T is always the middle level | **Irreversibility / lock-in premium.** Stetter & Sauer reportedly found that a shorter minimum lifetime shifted simulated adoption more effectively than policy support. Money is rescaled to NPV-equivalent units so this premium is non-financial |
| 4 | **Tree layout**: row spacing, shown as "% of field out of crop" and trees/ha | **26 / 38 / 50 m** between rows (2 m strip) ≈ **8 / 5 / 4 %** out of crop. Placeholder; recalibrate to each region's usual sprayer widths, and put Paper 1's layout in as a level | **Density / hassle / machinery-fit premium.** Seegers et al. (2026) find farmers prefer low tree density. The financial effect of layout is already in the margin |

**Five attributes including the label** (4 varied attributes + label) is Stetter's scale and keeps the task manageable. Plan for 10 choice tasks (+1 repeat), 3 blocks, and a Bayesian D-efficient labelled design in Ngene with priors from a pilot.

### Considered and deliberately *not* included as attributes

| Candidate | Why not |
|---|---|
| A payment for ecosystem services / public payment (Stetter had one) | It brings the policy dimension back, and a second money coefficient makes WTA ambiguous. It can instead be tested in the optional "Block 0" (§5) |
| Ecological-priority-area eligibility (Stetter had one) | Obsolete under the 2023–27 CAP. Instead, the scenario states that CAP eligibility and agricultural land status are unchanged |
| Time to first tree income | For timber it equals the lifetime, so the two would be perfectly collinear. It is shown on a fixed fact card, and time preference is measured in the behavioural module |
| Labour hours, crop yield loss near trees | These follow from layout and lifetime and are already inside the margin. Varying them separately would double-count |
| Share of neighbours who have adopted (social norm) | Not credible where almost nobody has trees. It is measured in the module instead |
| Advice / technical assistance, contract length, monitoring | Contract terms. They are fixed or removed in the scenario (§3) |

---

## 3. What is held fixed in every choice card (neutralising the contract)

- **No contract:** "You decide this yourself. Nothing to sign, no inspections, no paperwork."
- **CAP:** direct payments and current eco-schemes stay as today and are **excluded from all margins**. The field keeps agricultural status, is never reclassified as forest, and the tree strips remain eligible. Fear of losing eligibility is a documented deterrent and would otherwise inflate WTA.
- **Establishment:** no grant. A contractor plants exactly the layout shown, and all costs are inside the margin.
- **Markets:** the farmer owns and sells the tree products at today's regional prices.
- **Land:** the farmer's own named, treeless arable field, i.e. owner-operated land. Tenants are an open decision.
- **Discounting:** "averages count future money at r% a year", the same r as Paper 1.
- **Honest framing:** the margins are presented as *what-if situations for a field like yours*, **not** as model forecasts (only one level per card matches Paper 1). Paper 1's actual estimate is revealed in the debrief.

---

## 4. What happens to the old contract attributes

Map your actual list onto these rows.

| Old contract attribute | New design |
|---|---|
| Annual payment | **Replaced** by the land use's own net margin (the money attribute) |
| Contract duration | **Becomes a practice attribute**: planned tree lifetime |
| Flexibility / early exit / penalties | **Fixed**: no contract; early removal allowed, with its margin loss shown on the fact card |
| Technical assistance | **Fixed** (neutral fact card, contractor plants). Knowledge and perceived control are measured in the module |
| Monitoring, sanctions, paperwork | **Fixed**: none |
| Establishment grant / payment schedule | **Fixed**: no grant; all costs are in the margin |
| Collective bonus | **Dropped**. Social norms are measured in the module |
| Result- vs action-based payment | **Dropped**: there is no payment |
| Tree density / species rules | **Become practice attributes**: label + layout |

**What is lost:** direct scheme-design guidance, i.e. the "policy dimension" your supervisor mentions. Part of it comes back, because the supply curves (share of field area adopting vs €/ha/yr) show the support each system would need in each region. Two short policy questions can be asked after the DCE, outside Paper 3.

---

## 5. How behavioural preferences enter (the "clean paper" part)

1. **Inside the choice tasks.** These enter as money-metric premia in €/ha/yr:
   - status-quo bias, identity and distrust through the label constant;
   - risk aversion through the bad-year shortfall;
   - aversion to irreversibility through lifetime;
   - hassle and density through layout.
2. **Respondent-level module**, with incentivised tasks where the budget allows:
   - **beliefs**: expected alley yield loss, tree yield/price, extra hours, asked **before any margin is shown** and run through Paper 1's model to give a subjective OC;
   - **risk**: Dohmen general + farm items, and one paid lottery;
   - **loss aversion**: Gächter-type mixed lotteries;
   - **time preference**: short price lists + a patience item;
   - **attitudes**: productivist/"good farmer" identity, stewardship, descriptive and injunctive norms, perceived control, trust in the numbers and in legal/CAP stability.
3. **Model.**
   - Main model: a WTA-space mixed logit (lognormal money coefficient; premia normal, so they can be negative). The farm's own OC_i and the behavioural measures enter the **mean of Π** in one step. Never regress posterior WTA in a second stage.
   - Extensions: a hybrid choice (ICLV) model for latent attitudes, and a latent-class model with a "never adopt" class.
   - Pool ES and IT with a relative scale parameter.

**What Paper 3 can then report:**
- **The size of Π per system and country**, tested against:
  - zero (the static-NPV, risk-neutral benchmark);
  - a **rational benchmark** (the real-options value of irreversible planting + credit constraints; Frey et al. 2013).

  Only the remainder is called "behavioural".
- **The belief gap:** subjective OC − Paper 1 OC.
- **A leak test:** Π should not depend on OC_i once margins are shown (π₁ = 0, pre-registered as an equivalence test).
- **Supply curves:** adoption under OC alone vs OC + Π, carrying Paper 1's Monte Carlo uncertainty.
- **Optional "Block 0"** (random half of the sample, before any margin is shown): 2 double-bounded "plant X and receive €P/ha/yr on top of market income" questions. They give own-belief WTA and an exploratory test of whether WTA passes OC through one-for-one.

---

## 6. What must be identical in Papers 1 and 2 (agree this before building the design)

| Item | Must match |
|---|---|
| Systems | Species, product, in-row spacing, layout and lifetime per country |
| Baseline | The farmer's current rotation on this type of field (rotation-average margin) |
| Area basis | € per ha of the **whole field**, including tree strips |
| Horizon & discount rate | Same lifetime T for both land uses; same real rate r |
| Cost boundary | Same revenue and cost items (incl. establishment, removal, extra labour at wage w) |
| CAP & grants | Excluded or included identically; no AF grant on either side |
| Regions / farm types | 2–3 region (× farm type) strata per country, identical to Paper 1 |

**What Paper 1 should deliver for the design:**
- OC for 3 spacings × 3 lifetimes per system, or a simple emulator. **Fallback:** if Paper 1 only gives one configuration per stratum (e.g. FADN income forgone), fix layout and lifetime at Paper 1's values and keep label + margin + bad-year shortfall.
- Annual cash-flow profiles.
- The Monte Carlo draws.

**Farm data to collect so each respondent's OC_i can be computed:**
- region;
- farm type and size;
- field size, soil and irrigation;
- 3–5-year rotation with normal- and bad-year yields;
- prices and variable costs;
- implement widths;
- labour;
- rented share of land.

---

## 7. Suggested wording for Objective 2

> **Objective 2.** To estimate the willingness to accept (WTA) of arable farmers in Spain and Italy for adopting, on their own land, the agroforestry systems whose opportunity cost is estimated in Paper 1, using a labelled land-use discrete choice experiment whose money attribute follows Paper 1's accounting; and to quantify and explain the premium farmers require above financial parity through measured beliefs, risk, loss and time preferences, identity, social norms and trust.

- **RQ2.1** What premium above financial parity (€/ha/yr) do farmers require to adopt each system in Paper 1's configuration, and does it differ between Spain and Italy?
- **RQ2.2** How do income risk, planned tree lifetime and tree density change that premium?
- **RQ2.3** How do farmers' beliefs about agroforestry profitability compare with modelled profitability?
- **RQ2.4** Which behavioural and structural factors are associated with the premium, and how much remains after rational components (option value, liquidity) are accounted for?

---

## 8. Decisions to take with the supervisor

- [ ] Confirm "Stetter (2025)" = Stetter & Sauer (2024), and read its Table 1 (levels, design).
- [ ] Which systems (1, 2 or 3 per country) and which regions/farm types does Paper 1 cost? This decides labelled vs unlabelled and the strata.
- [ ] Can Paper 1 deliver OC over a layout × lifetime grid (or an emulator) in time? If not, use the fallback (§6).
- [ ] Discount rate, cost boundary and CAP treatment: sign a one-page concordance with Paper 1.
- [ ] Owners only, or also a tenant group? New silvopasture on grassland as well as silvoarable?
- [ ] Budget: target ≈300 farmers per country (minimum ≈150 by Orme's rule), paid behavioural tasks, participation fee, optional Block 0.
- [ ] Agree the "rational vs behavioural" split of Π (especially the real-options benchmark) before analysis, and pre-register the hypotheses.

---

### Key references *(details from search results; verify before citing)*
- Stetter, C. & Sauer, J. (2024). Tackling climate change: Agroforestry adoption in the face of regional weather extremes. *Ecological Economics* 224, 108266. https://doi.org/10.1016/j.ecolecon.2024.108266
- Seegers, R., Blake-Rath, R., Grote, U. & Nguyen, T.T. (2026). Agroforestry adoption and perceptions in Germany: Evidence from adopter–non-adopter comparisons and a discrete choice experiment. *Trees, Forests and People*.
- Frey, G.E. et al. (2013). A real options model to assess the role of flexibility in forestry and agroforestry adoption and disadoption in the Lower Mississippi Alluvial Valley. *Agricultural Economics* 44, 73–91.
- Dessart, F.J., Barreiro-Hurlé, J. & van Bavel, R. (2019). Behavioural factors affecting the adoption of sustainable farming practices: a policy-oriented review. *European Review of Agricultural Economics* 46(3).
- Leduc, G. & Hansson, H. (2024). Behavioural factors for farmers' adoption of agroforestry practices in Sweden. *Sustainable Production and Consumption* 47.
- Huber, R., Xiong, H., Keller, K. & Finger, R. (2022). Bridging behavioural factors and standard bio-economic modelling in an agent-based modelling framework. *Journal of Agricultural Economics* 73(1), 35–63.
- Train, K. & Weeks, M. (2005); Scarpa, R., Thiene, M. & Train, K. (2008): WTP/WTA-space estimation.
- The full list, all flagged "to verify", is in the technical annex (§13).
