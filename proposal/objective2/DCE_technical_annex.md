# Objective 2 (Paper 2) — Technical annex: practice-level WTA DCE for agroforestry (Spain & Italy)

*Technical annex to [`WTA_attributes_summary.md`](WTA_attributes_summary.md), which gives the short answer. This annex has the full design logic, equations, level-setting rules, the behavioural module, the Paper 3 model and tests, the alignment checklist with Paper 1, the survey flow and bias control.*

**Read this first**
- "ES and IT" is taken to mean Spain and Italy.
- The supervisor's "Stetter (2025)" is most likely **Stetter & Sauer (2024), *Ecological Economics* 224:108266** (to verify). From search snippets only, it is a labelled DCE with:
  - 198 farmers in Bavaria;
  - alternatives: alley cropping, short-rotation coppice, and current arable farming (status quo);
  - 36 choice cards in 3 blocks of 12;
  - attributes: expected yearly contribution margin, its variability, minimum useful lifetime, payment for ecosystem services, ecological-priority-area eligibility.

  Its exact levels are not known; read its Table 1 before claiming any similarity.
- No source could be opened in full text, so **every citation is "(to verify)"**.
- **Every level below is a proposal, to be calibrated with Paper 1's outputs and a pilot.**

---

## 0. Short answer

Replace the contract DCE with a Stetter-style **labelled land-use DCE**. The farmer decides what to do with one named field of their own: plant agroforestry (AF) system A, plant system B, or keep the current crops. The money attribute is each land use's **own average yearly net margin**, calculated with Paper 1's accounting. There is no contract, payment, inspection or adviser.

| # | Attribute | Levels (proposals, to calibrate with Paper 1 outputs and a pilot) | What it gives Paper 3 |
|---|---|---|---|
| 0 | **System label** → premium Π_s | Paper 1's systems. Placeholders: **ES** almond rows in rainfed cereals; walnut or wild-cherry timber rows. **IT** hybrid-walnut or wild-cherry timber rows; poplar (Po Valley) or walnut-for-nut rows | Total premium above financial parity at Paper 1's configuration |
| 1 | **Average yearly net margin of Field X** (€/ha/yr; the only money attribute) | Own current margin + Δ. At Paper 1's configuration, Δ = d ∈ **{−450, −200, 0, +150, +350, +600}**, the same in ES and IT. Away from that configuration, Δ also moves by Paper 1's marginal opportunity cost (OC) (§5.3) | The WTA denominator, in the same units as OC |
| 2 | **Bad-year shortfall** vs a normal year (about 1 year in 10; average unchanged) | ρ·S_i, ρ ∈ **{0.6, 1.0, 1.4}**; S_i = the farmer's own current shortfall, floored at the stratum 25th percentile | Risk premium |
| 3 | **Planned tree lifetime** (trees removed in year T) | Nut/fruit **15/20/25** yr; timber in ES **30/40/50**; timber in IT **20/30/40**; poplar **10/12/15**. Paper 1's lifetime T is always the middle level | Premium for inflexibility beyond the money effect of T (timber: plus delay) |
| 4 | **Tree layout** (row spacing → % of field out of crop; trees/ha per label) | **26/38/50 m** (2 m strip + 24/36/48 m alley) ≈ **8/5/4%** out of crop; trees/ha from Paper 1's in-row spacing per species. Recalibrate to each stratum's dominant boom widths; Paper 1's layout replaces the nearest level | Premium for density, hassle, machinery misfit |
| SQ | **Keep current crops on Field X, no trees** (status quo) | Own margin; own bad-year shortfall | Reference point |

- **The farmer values the practice, not a contract.** One money coefficient, using Paper 1's discount rate r, lifetime T, cost boundary, CAP treatment and area basis.
- **The DCE identifies Π, under the credibility and comprehension assumptions in §6a**: the premium (€/ha/yr) a farmer needs above financial parity. So **WTA = OC + Π**, and Paper 3 explains Π.
- **Misperception is measured before any margin is shown.** Farmers' beliefs about yields, prices and costs, run through Paper 1's model, give a subjective OC^subj, and own-belief WTA_own = OC^subj + Π.
- **Behaviour enters in three ways:** through the attributes; through a short module of paid risk, loss-aversion and time tasks plus attitude scales; and through a one-step WTA-space mixed logit, with each farm's OC_i in the mean of the premium.
- **Paper 1 must deliver before the final design:**
  - a signed concordance sheet;
  - OC over the layout × lifetime grid (a simple emulator);
  - its Monte Carlo draws.

  If it can only deliver stratum-level OC for one configuration, use the §8 fallback.
- **Fieldwork:**
  - about 300 owners of treeless arable fields per country;
  - 10 choice tasks plus 1 repeat;
  - face-to-face tablet interviews (CAPI) via cooperatives and farm unions;
  - about 40–45 minutes as specified, cut towards 35 with a ranked list (§11) or offset by a participation fee.
- **Optional, recommended:** a 2-task, double-bounded "payment on top" block for a random half of the sample, asked before any margin is shown (§7).

> **Core vs optional.**
> - *Core:*
>   - label, margin, bad-year and lifetime attributes (plus layout if Paper 1 can cost it);
>   - the status quo;
>   - belief questions (OC^subj from a simple partial budget);
>   - risk, time and loss measures;
>   - a WTA-space mixed logit with covariates in the mean of Π.
> - *Optional:*
>   - Block 0;
>   - emulator-based OC^subj;
>   - ORIV;
>   - ICLV;
>   - latent classes;
>   - re-running Paper 1 at farmers' own discount rates. Rates from 12-month price lists are often very high, so cap them and treat the re-run as a robustness check.

---

## 1. Why the change

**Contract WTA is not practice WTA.** The current design asks what payment would make a farmer sign a contract:

```
WTA_contract = OC + [duration lock-in, exit penalties, paperwork, inspection risk,
               trust in payer, value of advice] + Π
```

The bracketed terms come from contract design, and Paper 1's OC contains none of them. Free advice lowers stated WTA (Espinosa-Goded et al. 2010) and monitoring shifts it (Vedel et al. 2015b) (to verify).

**Practice WTA** is the minimum yearly compensation (€/ha/yr) at which a farmer would plant a specified system on a specified field, with nothing else attached. In plain words:
- Paper 1 says how much a farmer *loses* by planting trees.
- Paper 2 says how much the farmer *needs* to be paid.
- Paper 3 explains the difference.

```
WTA_own,s,i = OC_s,i + (OC^subj_s,i − OC_s,i) + Π_s,i      (own beliefs)
              Paper 1   belief gap                premium
WTA_s,i     = OC_s,i + Π_s,i                                (disclosed margins; used throughout)

Π_s,i = rational part    (option value of irreversibility, expected-utility risk premium,
                          liquidity, tenure)
      + behavioural part (status-quo bias, loss aversion, present bias, identity, distrust)
      − non-money benefits (stewardship)
```

Agree this split into rational and behavioural parts with your supervisor before you analyse anything.

**State this plainly in the thesis: when margins are disclosed, WTA − OC = Π by construction.** Given the modelled numbers, the main DCE tests whether farmers require a premium (H0: Π = 0) and explains its size. It cannot test whether farmers' own-belief WTA tracks OC; that needs OC^subj and Block 0.

This is not circular. Π = 0 is what an informed, risk-neutral **static-NPV** maximiser would show. Because planting is irreversible, the rational null also includes a real-options value (§6a, §6c).

Paper 3 therefore adds five things:
1. **The belief gap**, OC^subj − OC.
2. **A belief-leak test**: does Π depend on OC_i or the belief gap, although margins were shown?
3. **A rational/behavioural split of Π** against benchmarks (§6).
4. **Supply curves** carrying Paper 1's Monte Carlo draws.
5. **With Block 0**, the mean own-belief WTA for each system × country, and an exploratory estimate of whether it tracks OC one-for-one (§7).

---

## 2. Choice task design

**Alternatives: [System A] | [System B] | [Keep current use of Field X]**, labelled as in Stetter & Sauer (to verify).
- **Labels** are exactly the new systems Paper 1 costs:
  - if Paper 1 costs 1 system, show two unlabelled versions of it plus the status quo;
  - if it costs 3, show two unlabelled alternatives with the system as an attribute;
  - in these unlabelled variants, Ngene constraints exclude same-system pairs where one profile is at least as good on every attribute (given the expected premium signs).
- **Hedgerows** are included only if Paper 1 costs them. They get their own label with a fixed layout.
- **Excluded:** dehesa, wood pastures and olive–cereal intercropping. They already exist, so the decision is maintenance, not adoption (den Herder et al. 2017; Vedel et al. 2015a on additionality; to verify).
- **New silvopasture** (trees on treeless grassland) is also adoption. If Paper 1 costs it, run a parallel version: status quo "keep current grazing, no trees"; the grazing margin per ha of field as money; the same lifetime and bad-year attributes; layout as trees/ha.

**Status quo:** "Keep your current crops on [Field X], no trees": a real land use with the farmer's own margin and bad-year shortfall, not "no contract".

**Reference unit:** the farmer's largest **owned** arable field without trees, of the farm type Paper 1 models.
- **Screen:** the farmer owns at least one such field of at least the minimum size Paper 1 models.
- The farmer names the field. Record its size and share of the farm's utilised agricultural area (UAA), since converting a whole field concentrates scale and risk, plus the farm's rented share of UAA (a reweighting cell) and lease lengths.
- **WTA refers to owner-operated land**; a tenant sub-sample is an open decision (§12).
- All money is in **€ per ha of the whole field** (tree strips plus alleys) per year, in constant euros of the survey year.

**Tasks:**
- The design has 30 rows, split into 3 blocks of 10.
- Task 2 is repeated as task 11 (AF options swapped) as a consistency check only; **task 11 is excluded from estimation.** A "dominance" check suits a labelled design poorly, because preferring one label is legitimate.
- Task order and label positions are randomised. After each task, the farmer rates how sure they are (1–5).

**Example card** (Spain; **all numbers invented**)
- Paper 1's configuration: 38 m spacing; lifetime 20 years (almond) and 40 years (walnut); trees 6 m (almond) and 10 m (walnut) apart in a row.
- Design values d_A = +150 and d_B = −200. Paper 1's lookup table gives ΔOC = −€20 for almond at 26 m / 25 yr and +€30 for walnut at 50 m / 30 yr.
- The farmer's own margin is €290/ha, with a bad-year shortfall of €200/ha.

| | **A: Almond rows in your cereals** | **B: Walnut timber rows in your cereals** | **Keep current crops, no trees** |
|---|---|---|---|
| Average yearly net margin of "Las Eras" | **€460/ha/yr** (+€170 vs now) | **€60/ha/yr** (−€230 vs now) | **€290/ha/yr** |
| In a bad year (about 1 in 10), compared with a normal year, this field earns | €120/ha less | €280/ha less | €200/ha less |
| Trees are removed in year | 25 | 30 | (change crops any year) |
| Tree rows every | 26 m → 64 trees/ha, 8% of field out of crop | 50 m → 20 trees/ha, 4% out of crop | no trees |
| Follows from the layout and lifetime shown (already included in the margin) | first nuts in about year 4; cereal yield between rows −10% once trees are mature; +14 h/ha/yr extra work | first income when felled, year 30; cereal yield −5%; +5 h/ha/yr | none |
| **Your choice** | ☐ | ☐ | ☐ |

**Card footer:** "No contract, payment, inspections or paperwork. Your CAP payments stay as they are today and are not included in any margin. Margins include all planting (contractor fees), care, harvest and removal costs, and your extra hours at €w per hour, averaged over the planned lifetime at r% a year. These are what-if situations for a field like yours. Prices, yields and costs differ between cards, so the margins differ too. Choose as if these averages were true for your field."

"Farm model" appears only on the fact card, which gives the fixed descriptors and, from Paper 1, what removing the trees early would do to the average margin. Each AF option also has a small cash-flow sketch. It shows only the shape of the cash flow over time, with no euro figures, and it changes with the lifetime. The debrief reveals Paper 1's actual estimate.

---

## 3. Recommended attributes

**Coding.** Attributes 2–4 are coded as deviations from **Paper 1's configuration (P1)**, with money in NPV-equivalent units over P1's horizon (§5.4).
- The label constant then equals the whole premium Π_s at P1.
- Each attribute gives a premium per unit of change away from P1.
- Paper 1's value is one of the design levels for every label in both countries. WTA at P1 is therefore always inside the design range and never extrapolated.

*All levels: to be calibrated with Paper 1 outputs and a pilot.*

| Attribute | Wording shown | Levels, Spain | Levels, Italy / pivot rule | Status-quo level | Part of Paper 1's OC it mirrors | Behavioural construct | Expected sign |
|---|---|---|---|---|---|---|---|
| **System label** (→ Π_s) | "Plant [almond / walnut-timber] rows across [Field X]", plus a fact card | Almond; walnut or wild-cherry timber (placeholders) | Hybrid-walnut or cherry timber; poplar or walnut-for-nut (placeholders) | "Keep current crops, no trees" | Which system's equivalent annual value enters OC_s = EAV_SQ − EAV_s | Remaining resistance: status-quo bias, productivist identity, complexity, distrust (net of stewardship) | Π_s > 0: a premium is required (equivalently, a negative utility ASC for the tree options, as Stetter & Sauer reportedly found; to verify) |
| **Average yearly net margin** (money) | "Average yearly net margin of [Field X]: €__/ha/yr (±€__ vs now)" | CM_SQ,i + Δ, where Δ = d − ΔOC_s,i(x) and d ∈ {−450, −200, 0, +150, +350, +600} | Same d grid; ΔOC from Paper 1's Italian strata | Own rotation-average margin CM_SQ,i (Paper 1's boundary), computed on the tablet from the farmer's reported rotation, yields, prices and variable costs, then confirmed and rounded to €10. The FADN stratum mean is only a plausibility check (flag deviations > ±50%) | The **whole OC**: at P1, setting d = −OC_s,i reproduces Paper 1 | Marginal utility of income; loss aversion (robustness check only) | + (utility) |
| **Bad-year shortfall** | "In a bad year (about 1 in 10) this field earns €__/ha less than in a normal year. The average above already includes bad years." | ρ·S_i, ρ ∈ {0.6, 1.0, 1.4}; S_i = max(own shortfall, stratum 25th percentile), stated on the card. Coded as ΔS = (ρ − ρ^P1)·S_i/100 (per €100 of extra loss) | Same | S_i (ρ = 1) | Nothing, if Paper 1 uses expected values (then ρ at P1 = 1). If Paper 1 is stochastic, its simulated ratio is the middle level | Risk and downside aversion; perceived drought buffering | Premium rises with the extra loss |
| **Planned tree lifetime** | "Trees are felled or removed in year __. Earlier removal is possible but lowers the average margin (see fact card). The field stays agricultural land; removal cost is included." | Nut/fruit 15/20/25; timber 30/40/50 | Timber 20/30/40; poplar 10/12/15; nut 15/20/25. Paper 1's T is the middle level | Not applicable ("change crops any year") | The lifetime T used to annualise EAV; **the margin is recomputed at each T** | Inflexibility beyond money (nut); plus delay (timber: first income at felling) | Premium rises with T |
| **Tree layout** | "Tree rows every __ m: __ trees/ha, __% of the field out of crop" (trees/ha label-specific) | 26/38/50 m (placeholder until the pilot shows each stratum's dominant boom widths) | Same rule; Paper 1's layout replaces the nearest level | No trees | Area out of crop; number of trees (establishment, labour, tree revenue, alley yield); extra passes; **margin recomputed at each level** | Non-money cost of trees in the field; "tidy field" identity; machinery misfit | Premium rises with % out of crop |

**Why these attributes**

- **Label.** Each WTA pairs one-to-one with Paper 1's OC for the same system. Because the other attributes are centred at P1, the label constant is the *total* premium at P1. It is not "pure identity".

- **Margin.**
  - This follows Stetter's logic: the money is the land use's own yearly profitability, not a payment for accepting obligations.
  - Stetter's contribution margin is revenue minus variable costs. Here the cost boundary is **widened to match Paper 1's EAV** (§5.2).
  - There is no second money attribute, because two money coefficients would make WTA ambiguous.

- **Bad-year shortfall.**
  - Income variability lowered uptake of woody crops in Germany (Gillich et al. 2019, to verify).
  - Pivoting on the farmer's **own** shortfall captures year-to-year risk on this field; an FADN percentile would capture differences between farms. The floor keeps levels distinct for irrigated farms with near-zero shortfall.
  - Coding per € of loss makes π_V comparable across farms and stops it tracking S_i mechanically. For timber (income only at felling) the shortfall refers to the field's yearly income; π_V is interacted with a timber dummy.
  - Holding the average fixed is only believable because the average is shown, one reason option (a) beats (b) (§5.1).

- **Lifetime.**
  - Stetter & Sauer reportedly found that reducing the minimum useful lifetime shifted choices towards alley cropping more effectively than policy support (to verify).
  - It is a planned management horizon; never word it as a "commitment period". Its money effect is in the margin and early removal is priced on the fact card, so π_T measures perceived inflexibility beyond the money.
  - For timber, the lifetime is also the felling year and first income. The timber-minus-nut difference only *suggests* delay aversion; impatience is measured outside the choice model (§6).

- **Layout.**
  - Farmers prefer low tree density (Seegers et al. 2026, to verify).
  - **Exclusion rule, per stratum and label:** no cropped alley (spacing − 2 m) narrower than the stratum's dominant boom, and no level above 100 trees/ha for any label (the historic eligibility threshold; Santiago-Freijanes et al. 2018, to verify), so the eligibility statement stays credible. The placeholder alleys are whole passes of a 12 m boom at every level and of a 24 m boom at two.
  - **Machinery fit is not promised.** A misfit dummy M records whether each alley is a whole number of passes of the respondent's own boom; Paper 1 costs the extra passes. π_M separates machinery-fit disutility from π_N (§5.4).
  - *Alternative*, if the emulator is validated at farm level: spacing = n·W_i + 2 m, n ∈ {1, 2, 3}, with W_i the farmer's widest implement.
  - Extra hours and the alley yield effect are derived from Paper 1 and already costed, so they are not varied.

**Deliberately left out as attributes**
- **Payment for ecosystem services / public payment:** brings back policy and a second money coefficient.
- **Ecological-priority-area dummy:** obsolete under the 2023–27 CAP.
- **Right to convert back:** a legal term, fixed in the scenario text.
- **Share of neighbours who adopted:** not believable where almost nobody has; measured in the module.
- **Advice:** known to shift WTA.
- **Labour, crop yield, time to first income:** derived descriptions, to avoid double counting.
- **Environmental co-benefits:** move with spacing; stewardship attitudes are measured instead.

**Avoiding collinearity**
- Layout is a single attribute, described in three equivalent ways.
- Lifetime levels are specific to each label.
- Time to first income is not varied separately: it is fixed for nut systems (about year 4 in the example) and equals the lifetime for timber.
- d varies independently of layout and lifetime.

---

## 4. What is held fixed in the scenario (and why)

| Element | Fixed wording (summary) | Why |
|---|---|---|
| Contract | "You decide this yourself. Nothing to sign, no inspections, no paperwork." | Removes monitoring and transaction costs that Paper 1 does not include |
| CAP | "Your direct payments and current eco-schemes stay as today and are not in the margins. The field keeps its agricultural status, is never reclassified as forest, and the tree strips stay eligible. No extra payment for the trees." | CAP eligibility rules (e.g. the historic 100 trees/ha threshold) are documented deterrents (Santiago-Freijanes et al. 2018, to verify), so fear of losing eligibility could inflate stated WTA. Paper 1 must treat CAP the same way |
| Establishment | "No grant; all tree costs are inside the margin. A contractor plants the system exactly as shown (fees inside the margin). Normal farm credit is available." | Keeps one yearly money measure. Machinery fit is not promised: it is recorded (misfit dummy, π_M). Liquidity is recorded |
| After the lifetime | "Trees are removed in the planned year (cost included); earlier removal costs the margin loss on the fact card. No duty to replant." | A management horizon, not a contract term |
| Information | The same neutral fact card for every AF option; no adviser | Advice shifts WTA without changing OC (Espinosa-Goded et al. 2010, to verify) |
| Markets | "You own the tree products and sell them at today's regional prices; no purchase contract." | Matches Paper 1's prices |
| Tenure and water | The field is owned (screened); no new irrigation (unless Paper 1's system is irrigated) | Matches Paper 1's baseline; WTA refers to owner-operated land |
| Discounting | "Averages count future money at r% a year" | Same unit as Paper 1's EAV |

---

## 5. The money attribute and WTA

### 5.1 Resolving the design tension

| Option | What WTA − OC measures | Verdict |
|---|---|---|
| **(a)** Each land use's own margin is shown (Stetter-style) | Π, plus any residual distrust, comprehension or hypothetical-bias component. Cleanest option, conditional on credibility (checked via π₂, π₃ from the pre-choice trust item, and the comprehension check). It overrides farmers' own beliefs about profitability | **Core design** |
| **(b)** A payment on top of market returns, with the practice described physically | The belief gap and Π, which cannot be separated. Also: a guaranteed 25–50-year payment brings back trust in the payer and strategic overbidding; payments ≥ 0 identify negative WTA only through the functional form; and the risk attribute cannot hold an unshown average fixed | Only as the optional **Block 0** (double-bounded, with a negative follow-up) |
| **(c1)** Margin and payment in the same task | Two money coefficients, so WTA is ambiguous and the policy dimension returns | **Rejected** |
| **(c2)** Full split sample, (a) vs (b) | The best decomposition, but only 150 respondents per arm per country at n = 300 | Only if n ≥ 450 per country |
| **Chosen hybrid:** (a), plus beliefs asked before any margin is shown (OC^subj), plus the optional Block 0 | WTA_own − OC = (OC^subj − OC) + Π, assuming the premium is the same with or without disclosure (Block 0 checks this) | **Recommended** |

### 5.2 Definition

The **margin** follows Paper 1's cost boundary: all crop and tree sales minus every cost that changes with the land use. That is variable inputs; variable machinery and contractor costs (operating costs only); planting (including contractor fees) and tree protection; pruning and harvest; tree removal; and own labour only for the extra AF hours, at Paper 1's wage w. Both land uses are annualised over the same lifetime T_s at Paper 1's real rate r. The average year is 0.9 × normal + 0.1 × bad year. CAP payments are excluded everywhere, and there are no grants.

```
EAV_j = NPV_j · r / (1 − (1+r)^−T_s),  j ∈ {SQ, s}        OC_s,i = EAV_SQ,i − EAV_s,i   (€/ha of field/yr)
```

### 5.3 How the margin is set, and why these levels

```
Displayed AF margin:  M_AF,j = CM_SQ,i + Δ_j
Margin gap shown:     Δ_j = d_j − [OC_s,i(x_j) − OC_s,i(x_s^P1)]      x = (spacing, lifetime)
d ∈ {−450, −200, 0, +150, +350, +600} €/ha/yr, identical across strata and countries
```

- **At Paper 1's configuration, Δ = d.** The grid **spans parity (midpoint +€75)** and is the same for everyone; d = −OC_s,i is Paper 1's own market outcome.
- **Away from P1, displayed margins move exactly as Paper 1 predicts** with layout and lifetime, so those coefficients measure non-money costs, not disbelief such as "narrower rows must cost more".

**Why not centre the grid on each stratum's OC (−OC + k)?** Gaps would then run from −OC − 150 to −OC + 750:
- **High OC cuts Π off.** At OC = €600 the largest gap is +€150, so larger premia are extrapolated.
- **Low OC hides negative premia and loss aversion.** If OC < −€150, no negative gap is ever shown.
- **Range effects could bias the key test.** Welfare estimates are sensitive to the range and top level of the money attribute (Glenk et al. 2019, to verify). A stratum-specific grid could therefore make Π co-vary mechanically with OC, which would bias the π₁ test in §6c.

A common grid avoids these problems and avoids scale differences caused by different money ranges (Kragt 2013, to verify). But it is common only in absolute euros: ±€450 is large for a €150/ha rainfed Spanish field and small for a €1,200/ha Po Valley field. So CM_SQ,i enters the mean of Π and the scale function, and Δ/CM_SQ coding is a robustness check.

**Rules for the pilot**
- **Market point in range:** −OC must lie inside the grid for at least 90% of Paper 1's strata. The grid covers OC from −€600 (AF more profitable) to +€450; if this fails, extend the bottom level to −600 in both countries.
- **Top level high enough:** at least 1.3 × the pilot's 90th percentile of Π. If more than 60–65% still keep current crops at +600, raise it to +800 or +900.
- **Negative margins allowed** (e.g. CM_SQ = €250 with d = −450), plausible for long-rotation timber; test credibility in the pilot.
- **No plausibility filter on d:** dropping extreme profiles would cut off the range exactly where large premia are identified. The only exception: if the pilot shows that very low displayed margins are not credible (e.g. where CM_SQ,i is very low or negative), set a floor on them and record where it binds, because it censors Δ.

**In the field:** the tablet computes ΔOC_s,i(x) from the §8 emulator with the farm's own margin and yield, or else from a lookup table by stratum × system × 3 spacings × 3 lifetimes.

### 5.4 Utility, premium and WTA

```
U_i,s,t  = α_i·[a_st·Δ_st − Π_s,i − π_V,i·ΔS_st − π_T,s,i·(T_st − T_s^P1)/10 − π_N,i·(O_st − O_s^P1)
                − π_M·(M_st − M_s^P1)] + ε_i,s,t
U_i,SQ,t = ε_i,SQ,t
a_st = A(T_st)/A(T_s^P1), A(T) = (1 − (1+r)^−T)/r at Paper 1's r;   ΔS_st = (ρ_st − ρ^P1)·S_i/100;
O = % of field out of crop (= 200/spacing in m, the same for every species);  M = misfit dummy (fixed π_M)
```

**Why the money is scaled.** Δ is an annuity over T_st, and the difference from arable lasts only T years, so its NPV weight scales with A(T) (at r = 3%, A(25)/A(20) = 1.17; A(30)/A(40) = 0.85). Unscaled, a profit-maximiser's preference for a longer T when Δ > 0 would load onto π_T, and one-off non-money costs K would enter as K/A(T). a_st puts all money in NPV-equivalent units over P1's horizon. At P1, a = 1, so WTA = OC + Π is unchanged. The unscaled model (a ≡ 1) is a robustness check.

**Distributions (pre-registered main specification)**
- α_i is lognormal.
- Π_A and Π_B are normal, with full covariance among (α, Π_A, Π_B). This "Π block" of the covariance matrix includes a respondent effect shared by Π_A and Π_B.
- π_V, π_T,s and π_N are normal but uncorrelated, or fixed if weakly identified.

**What the parameters mean**
- **Π_s,i** is the margin premium (€/ha/yr) the farmer needs to adopt Paper 1's configuration. The farmer plants if Δ ≥ Π_s,i.
- **The per-unit premia** show how Π would change for other versions of the system: per €100 of extra bad-year loss, per 10 extra years of lifetime, per percentage point of field out of crop, and (π_M) for an alley that does not fit the farmer's boom.
- **Converting Π into WTA:** in the real market Δ = −OC_s,i, so the payment P on top of market returns solves −OC + P = Π:

```
WTA_s,i      = OC_s,i + Π_s,i        (assumes €1 of payment = €1 of margin; state this)
WTA_own,s,i  = OC^subj_s,i + Π_s,i   (assumes the premium is the same with or without disclosure)
```

**Report:**
- Π_s by system and country;
- the share of farmers with Π < 0;
- the share with WTA ≤ 0, compared with the share of farms whose OC ≤ 0. Mediterranean AF may earn more than arable (Kay et al. 2019, to verify).

### 5.5 Estimation

- **Main model:** a WTA-space mixed logit (Train & Weeks 2005; Scarpa et al. 2008) in Apollo (Hess & Palma 2019), all to verify. It uses at least 1,000 quasi-random draws and the §5.4 covariance structure. Covariates enter only the means of Π (covariates on π_V, π_T, π_N are extensions). Choice certainty, task position and CM_SQ,i enter the scale function.
- **Countries:** one pooled model with country-specific means of Π and π, a common α distribution and a relative scale μ_IT (μ_ES = 1), to which the Swait–Louviere test applies (Swait & Louviere 1993, to verify). Separate country models without a scale parameter are a robustness check. Compare WTA only within system and country.
- **Confidence intervals:** Krinsky–Robb simulation (Krinsky & Robb 1986, to verify).
- **Gain/loss split** (Δ⁺ + λΔ⁻): robustness check only. Farmers who treat large gains as not credible would look loss-averse.
- **Sign convention:** a negative preference-space ASC for the tree options corresponds to Π > 0.

---

## 6. Behavioural integration

### 6a. Within the DCE: what identifies what

| Part of Π | Identified by | Assumption needed | Rational benchmark (subtract before calling it "behavioural") |
|---|---|---|---|
| Remaining resistance (status-quo bias, identity, complexity, distrust) | Π_s at P1, explained by covariates | Farmers believe the shown margins and read annualised margins as intended (tested with π₂, π₃ and the comprehension check) | **ROV_s(T_s^P1) + credit/liquidity wedge** (+ expected-utility premium for tree-product price risk if Paper 1 is stochastic), from the volatility in Paper 1's Monte Carlo draws (Frey et al. 2013; Musshoff 2012, to verify) |
| Inflexibility / lock-in | Lifetime coefficient π_T for the nut label | Money scaled to P1-horizon NPV units (§5.4); early removal priced on the fact card | Change in the real-options value with T (same source) |
| Delay / impatience | Timber minus nut π_T (suggestive only); coefficient on OC_s(δ_i) − OC_s(r) in the mean of Π (0 = accept the displayed annuity; 1 = fully re-discount at own rate) | δ_i elicited with risk curvature, winsorised | Cost of credit; liquidity controls |
| Risk | π_V (per €100 of extra bad-year loss; × timber dummy) | Farmers read the shortfall as leaving the average unchanged; Paper 1 is risk-neutral | Pre-registered expected-utility premium on **farm income**, vs the status quo: RP_i ≈ ½·(γ_i/W_i)·h_i·0.09·(ρ² − 1)·S_i² per ha (γ_i elicited CRRA, W_i farm income, h_i field area; two-point distribution, p = 0.1). This ignores correlation with the rest of the farm: if bad years hit the whole farm at once, add the covariance term ½·(γ_i/W_i)·2·0.09·(ρ − 1)·S_i·S_rest,i per ha (S_rest,i = the rest of the farm's bad-year shortfall, in € for the whole rest of the farm). The per-ha (narrow-bracketing) version is an alternative |
| Loss aversion | λ from the gain/loss split; lottery task | Farmers believe large gains | none (behavioural) |
| Density / hassle | π_N; machinery misfit π_M | Hours, alley yield loss, lost area and extra passes are already costed; π_M separates machinery-fit disutility from π_N | 0 |
| Misperception | OC^subj − OC | Beliefs are asked before any margin is shown; the neutral description has no numbers | 0 |
| Identity, norms, trust, perceived control | Covariates of Π | Read as associations, not causes (Chorus & Kroesen 2014, to verify) | none |

By design, Π excludes the know-how cost of designing and planting (the contractor does it; fees are in the margin), so it understates real-world fixed-cost barriers (Espinosa-Goded et al. 2013, to verify). Learning costs of managing the trees remain in Π.

### 6b. Respondent-level module

**Placement:**
- The neutral description of each system is qualitative only: photos, layout and product, with no yields, timing, labour or money figures.
- Beliefs are asked **before** any margin is shown.
- The pre-choice trust item comes right after the fact cards and the comprehension check.
- Everything else comes **after** the DCE. For a random 20% the order is reversed, to test order effects.

**Incentives:** if the budget and ethics approval allow, pay 1 in 10 respondents for the lottery and time tasks. Use one lottery. For ORIV (optional; Gillen et al. 2019, to verify), pair it with the Dohmen farm item.

| Construct | Instrument (to verify) | Paid? | How it enters the model |
|---|---|---|---|
| **Beliefs → OC^subj** (main measure) | For each label at P1: alley crop yield once trees are mature (% vs now, in bins); tree yield and price; year of first income (nut labels only; fixed by T for timber); extra hours. Best guess plus a confidence rating. A remaining "don't know" gets a DK flag and the stratum median of other respondents' beliefs (not Paper 1's value, which would bias the gap towards zero) | No | Emulator or partial budget (§8) → OC^subj. The belief gap and the DK flag enter the mean of Π |
| Beliefs, overall (secondary) | One question with 7 bins: "Compared with now, how would planting X change this field's average yearly net income?" (bins scaled to the stratum) | No | Cross-check; first to cut |
| **Trust in the numbers (pre-choice)** | "How much would you rely on farm-model margin estimates like these for decisions on your own farm?" (1–5) | No | π₃; defines the low-trust robustness subsample |
| Risk | Dohmen et al. (2011) general and farm-specific items; one Eckel–Grossman-type or Holt & Laury (2002) lottery | Lottery only | Π (π_V as an extension); CRRA γ_i for the expected-utility benchmark |
| Loss aversion | Gächter et al. (2022) mixed-lottery acceptance tasks | Yes | Π (π_V as an extension); benchmark for λ |
| Time preference | Two 5-row price lists (today vs 12 months; 12 vs 24 months) plus a patience item (Falk et al. 2023), estimated with risk curvature (Andersen et al. 2008) | Yes | δ_i (winsorised, e.g. at credit rate + 10 pp) for re-running Paper 1; present bias β_i for π_T (extension) |
| Identity | Productivist / "good farmer" identity (Burton 2004; Howley et al. 2015); stewardship; 3 items each | No | Hybrid choice model (ICLV) / mean of Π |
| Social norms | Descriptive (number of farmers the respondent knows with trees in fields) and injunctive (Villamayor-Tomas et al. 2019; Leduc & Hansson 2024) | No | Mean of Π |
| Perceived control, trust, resistance to change | 3 items each, plus a short knowledge quiz and experience with trees; trust covers the numbers shown and legal/CAP stability | No | Mean of Π |
| Rational controls | Age × successor, liquidity, off-farm income, family labour, FADN farm type and size, field's share of UAA, rented share, CM_SQ,i, boom width (→ misfit), drought exposure | n/a | Means of Π (per-unit premia as extensions) |
| Debrief | Credibility of the margins (1–5); ignored attributes; reasons for always keeping current crops; perceived consequentiality; what a typical nearby farmer would choose (Lusk & Norwood 2009). Then reveal Paper 1's estimate | n/a | The post-choice credibility rating is only descriptive, an attribute-non-attendance indicator, or a second indicator of latent trust (ICLV). The rest feeds the scale function, latent classes and sensitivity checks |

Organise these constructs using the Dessart et al. (2019) grouping into dispositional, social and cognitive factors (to verify).

### 6c. Model specification and the one-step Paper 3 test

Pre-register which covariates shift which parameter:

```
Π_s,i = π0_s,c + π1·OC_s,i + π2·gap_s,i + π3·Trust_i + π4·CM_SQ,i + π5·[OC_s(δ_i) − OC_s(r)]
        + m1·OC̄_i + m2·gap̄_i + θ'Z_i + κ'C_i + (Π block of the covariance matrix)
gap_s,i = OC^subj_s,i − OC_s,i;   OC̄_i, gap̄_i = respondent means over the two labels
Extensions:  π_V,i ← risk items/lottery, loss aversion, drought exposure;   π_T,i ← δ_i, β_i, age × successor, liquidity;
             π_N,i ← identity, boom width
```

Z are the behavioural measures (including the DK flag) and C the rational controls. The respondent means and the shared respondent effect absorb farm margin, productivity and general pessimism, so π₁ and π₂ are identified from **within-respondent differences between the two labels** (OC_A,i − OC_B,i; gap_A,i − gap_B,i). **OC_s,i is farm-level, from the emulator.** If Paper 1 delivers only stratum-level OC, use the §8 fallback (no region fixed effects).

**Tests**
1. **Premium–OC independence (π₁ = 0): no belief or range leakage.** Because WTA = OC + Π by construction, this is not a pass-through test. Pre-register it as an equivalence test (TOST, e.g. |π₁| < 0.2) with a power calculation; failing to reject π₁ = 0 is not evidence for it.
2. **No belief or trust leak (π₂ = π₃ = 0).** Under partial leak, with weight w on the displayed margins, π₁ = π₂ = (1 − w)/w, so also test π₁ = π₂ jointly.
3. **Rational nulls.** Π_s = 0 is the static-NPV null. Π_s = ROV_s is the rational real-options null. The behavioural residual is Π_s − ROV_s − credit wedge.
4. **With Block 0:** WTA_own,i = γ₀ + γ₁·OC_i + δ′Z_i, interval-censored. Test only γ₀ = 0, γ₁ = 1 (δ is exploratory), with the same attenuation correction as for π₁, and report power.

**Measurement error in OC_i** attenuates π₁ towards 0 (H7's null) and γ₁ towards 0 (towards rejecting γ₁ = 1). Re-estimating over Paper 1's Monte Carlo draws propagates model uncertainty but does not remove attenuation. Correct it with an instrument (OC from FADN-stratum inputs instrumenting OC from farmer-reported inputs) or with SIMEX, using the emulator's validation error variance. **Never** regress individual posterior WTA on covariates in a second stage.

**Further models**
- **Hybrid choice model (ICLV):** identity, stewardship, norms and trust enter the mean of Π as latent variables (Ben-Akiva et al. 2002, to verify). Report these as associations only.
- **Latent class model**, with covariates predicting class membership. Expected classes: never adopt (in an Irish agri-environment-scheme contingent-valuation study, about 30% would not participate at any payment; McGurk et al. 2020, to verify); ignore the money attribute; close to financial parity.
- **Robustness checks:** preference space; G-MNL; gain/loss split; Δ/CM_SQ coding; unscaled money (a ≡ 1); with and without protest responses; with and without farmers scoring 2 or lower on the pre-choice trust item.

**Supply curves.** w are FADN weights, h_i is the area of Field X, and each curve is a share of field area.

```
S_OC(P)  = Σ w_i h_i·1[OC_s,i ≤ P] / Σ w_i h_i
S_WTA(P) = Σ w_i h_i·Pr(OC_s,i + Π_s,i ≤ P) / Σ w_i h_i
S_own(P) = Σ w_i h_i·Pr(OC^subj_s,i + Π_s,i ≤ P) / Σ w_i h_i
```

Uncertainty combines Krinsky–Robb draws with Paper 1's Monte Carlo draws, recomputing Π_s,i = π0 + π1·OC^(m) + … for each draw m. The horizontal gap at share q is the quantile difference Q_WTA(q) − Q_OC(q); it equals mean Π only if Π is homogeneous. Report it by region and system.

---

## 7. Optional extensions

**Block 0 in detail:**
- Two payment-framed tasks at Paper 1's configuration, one per label.
- Asked of a random 50% of respondents, *before* any margin is shown.
- Wording: "Plant X as described. You keep all crop and tree income, plus €P/ha/yr for T years."
- **Double-bounded:** a random start bid from P ∈ {0, 150, 300, 500, 800, 1200} (the same for everyone), then one step down after "yes" or up after "no".
- **Negative follow-up:** farmers who accept at P = 0 are asked instead "Would you still plant if it cost you €100 / €300 per ha per year?", which bounds a negative WTA_own.
- The top bid (€1,200) is above the main grid's (+€600) because own-belief WTA includes OC^subj, not only Π.
- **Estimation:** WTA_own is interval-censored, pooled over countries and labels, with country × label fixed effects.

| Extension | What it adds | Cost / risk | Recommendation |
|---|---|---|---|
| **Block 0** (as described above) | Mean own-belief WTA per system × country; an exploratory pass-through estimate (γ₁); a joint check that the premium is unchanged by disclosure and that payment euros equal margin euros (not separable). The other half controls for order effects | About 2 minutes. About 150 respondents per country × 2 labels: enough for means, probably underpowered for a slope test (pre-registered power calculation). Some trust in the payer re-enters | **Include if about 300 per country is reachable; always include it in the pilot.** If γ₁ = 1 must be a Paper 3 headline, give it to everyone (losing the order-effect control) |
| Full split sample: payment framing throughout for one arm | A clean split between beliefs and premium | Halves the sample per arm | Only if n ≥ 450 per country |
| Payment-for-ecosystem-services attribute (are payment and market euros alike?) | Mental accounting | Two money coefficients; policy returns | **Do not include** |
| 2 post-survey policy questions (preferred support; acceptable contract length) | Part of the policy dimension, outside Paper 3 | 30 seconds | Include |
| Feeding Π back into Paper 1's model (Huber et al. 2022, to verify) | Adoption simulated with behavioural parameters | Work for Paper 3 | Consider |

---

## 8. Alignment checklist with Paper 1

Agree and sign this one-page concordance **before** building the design.

| Item | Must be identical in both papers |
|---|---|
| Systems | Species, product, in-row spacing per species (sets trees/ha), Paper 1's spacing and lifetime per country. Paper 1 delivers OC for 3 spacings × 3 lifetimes per system, including extra passes |
| Baseline | The current rotation on this type of field, as a rotation-average margin (0.9 × normal + 0.1 × bad year), not a model-optimised farm plan |
| Area basis | € per ha of the **whole field**, including the uncropped strips |
| Horizon | T = tree lifetime for both EAV_SQ and EAV_s; same rule after T (return to arable; removal cost and end value included). Paper 1 also gives the margin effect of early removal (fact card) |
| Discount rate | The same real rate r, stated on the card. Paper 3 adds a check at each farmer's own winsorised rate δ_i |
| Prices | The same price year, in constant euros of the survey year |
| Cost boundary | Revenue minus variable inputs, variable machinery/contractor costs (operating costs only), establishment (including contractor design and planting fees), tree removal, and own labour only for extra AF hours at wage w. Fixed costs excluded in both papers |
| CAP | Basic income support and current eco-schemes unchanged and excluded; tree strips eligible; no AF payment |
| Grants | None on either side |
| Risk | OC based on expected values; Monte Carlo draws kept (volatility for the real-options benchmark) |
| Strata and additionality | At most 2–3 region (or region × main farm type) cells per country with Paper 1 OC; size classes only for reweighting. Treeless fields; non-adopters |

**What Paper 1 must deliver before the final design:**
- its configuration for each system;
- OC by stratum;
- annual cash-flow profiles;
- the emulator inputs;
- the Monte Carlo draws;
- margin volatility, for the option-value benchmark.

**Emulator.** A proposed simple form, to be validated against Paper 1's full model:

```
OC_s,i(x) = σ(x)·CM_SQ,i + (1 − σ(x))·p_i·Y_i·(1 − ȳ_s(x)) + C_s(x) − R_s(x)
```

σ is the share of the field under tree strips; σ·CM_SQ is the margin lost on the strip, so CM_SQ must be on Paper 1's boundary. ȳ is the relative alley crop yield, averaged over the lifetime with discounting (a Yield-SAFE-type output). C and R are tree costs and revenues, annualised at r over T(x).

**Fallback if Paper 1 is stratum-level with one configuration** (e.g. FADN income forgone):
- (i) Fix lifetime and layout at Paper 1's values, unless Paper 1 supplies annual cash-flow profiles so that EAV can be re-annualised at other T.
- (ii) Do not add region fixed effects, which would be collinear with OC. Estimate π₁ only if enough strata have distinct OC (say ≥ 8); otherwise compare stratum WTA with OC descriptively.
- (iii) Compute OC^subj with a simple partial budget: σ·CM_SQ + believed alley yield loss (€) − believed tree revenue + believed tree costs, annualised at r.

**Farm data to collect so OC_i can be computed** (pre-collect by a short pre-visit form or from cooperative records where possible):
- location and structure: NUTS2 region and municipality; FADN farm type and size; rented share of UAA and lease lengths;
- Field X: size, share of UAA, soil and slope, irrigation, any existing trees;
- the rotation over the last 3–5 years, with yields in a normal and a bad year (S_i = normal − bad margin);
- prices received, main variable costs and contractor use;
- sprayer-boom and other implement widths; family labour and the wage for hired labour; CAP payments on the field;
- the current margin, computed on Paper 1's boundary and confirmed by the farmer.

---

## 9. Old contract attributes: what happens to each

The original attribute list is not known here, so map yours onto these rows.

| Old attribute (typical) | What happens | How |
|---|---|---|
| Annual payment | Replaced | By the land use's own margin |
| Contract duration | Becomes a practice attribute | Planned tree lifetime (tied to Paper 1's T) |
| Flexibility, early exit, penalties | Fixed in the scenario | No contract; early removal allowed, with its margin loss on the fact card |
| Technical assistance | Fixed in the scenario, plus module | Neutral fact card, no adviser; contractor plants (fees in the margin); knowledge and control measured |
| Monitoring, sanctions, paperwork | Fixed in the scenario | "No inspections, no paperwork" |
| Establishment grant, payment schedule | Fixed in the scenario | No grant; all costs are inside the margin |
| Collective bonus | Dropped, moved to module | Social norms are measured |
| Result-based vs action-based payment | Dropped | There is no payment |
| Payment for ecosystem services / eco-scheme top-up | Dropped | Payment vs margin euros tested only through Block 0 |
| Eligibility (ecological focus area, CAP status) | Fixed in the scenario | Agricultural status is kept |
| Rules on tree density or species | Becomes a practice attribute | Label plus layout |

**What is lost:** direct guidance on scheme design. Part of it is recovered, because the supply curves show the per-hectare support each system needs in each region.

---

## 10. Suggested wording: Objective 2, research questions, hypotheses

**Objective 2.** *To estimate the willingness to accept (WTA) of arable farmers in Spain and Italy for adopting, on their own land, the agroforestry systems whose opportunity cost is estimated in Paper 1. The instrument is a labelled land-use discrete choice experiment whose money attribute follows Paper 1's accounting. The objective is to quantify the premium that farmers require above financial parity, and to explain it through measured beliefs, risk, loss and time preferences, identity, social norms and trust.*

**Research questions**
- **RQ2.1** What premium above financial parity (€/ha/yr) do farmers require to adopt each system in Paper 1's configuration, and does it differ between Spain and Italy?
- **RQ2.2** How do income risk, planned tree lifetime and tree density change that premium?
- **RQ2.3** How do farmers' beliefs about profitability compare with modelled profitability?
- **RQ2.4** Which behavioural and structural factors are associated with the premium, and how much of it remains after the rational parts are accounted for?

**Hypotheses** (to pre-register)
- **H1:** for each system, the mean premium Π_s is above zero (the static-NPV null) and above the rational benchmark ROV_s + credit wedge (Stetter & Sauer 2024; Howley et al. 2015; to verify).
- **H2:** the lifetime premium π_T (inflexibility beyond the money effect of T) is positive, and larger for timber than for nut systems.
- **H3:** the risk premium π_V is positive, and larger than the pre-registered expected-utility premium on farm income (§6a).
- **H4:** the density premium π_N is positive, and the misfit premium π_M is positive (alleys that do not fit the farmer's boom).
- **H5:** Π rises with productivist identity, loss aversion, resistance to change and distrust of legal stability, and falls with stewardship, known adopters, perceived control and pre-choice trust in the numbers.
- **H6:** farmers' subjective OC differs from Paper 1's OC (no prior on the direction).
- **H7 (Paper 3):**
  - (a) Π is uncorrelated with OC_i given controls (π₁ = 0, equivalence test), with the belief gap (π₂ = 0) and with pre-choice trust (π₃ = 0): Tests 1–2.
  - (b) Own-belief WTA passes OC through one-for-one (γ₁ = 1), tested with OC^subj + Π and Block 0 (Test 4); exploratory if underpowered.

---

## 11. Experimental design, sample size and bias control

**Design**
- A Bayesian D-efficient labelled design built in Ngene, with the same structure in both countries.
- Levels: d has 6; bad-year ratio, lifetime and spacing have 3 each; lifetime levels are specific to each label.
- Priors from a pilot MNL (money sign constrained); efficiency evaluated with typical ΔOC tables per country; a C-efficiency check on the variance of Π at P1; dominance constraints for unlabelled variants (§2).
- Stetter reportedly used a Viney et al. (2005)-type design (to verify); pilot priors improve on this.

**Sample**
- Orme's rule of thumb (Orme 2010, to verify), 500 × 6 / (10 × 2), gives a minimum of 150 per country (about 190 with 8 tasks).
- **Target about 300 per country**, in at most 2–3 sampling strata per country (region, or region × main farm type, with Paper 1 OC), at least 100 each. Size classes are reweighting cells only (or raise n). Placeholder allocation:
  - Spain: rainfed cereal in Castilla y León / Castilla-La Mancha, 200; Andalusia, 100.
  - Italy: Po Valley, 180; central Italy, 120.
- Confirm the sample size with Ngene's S-estimates.
- Reweight the sample to FADN strata, including the rented share of UAA in the cells.
- Recruit through cooperatives and farm unions (trained technicians as interviewers); explore the national FADN networks (RICA in Italy, RECAN in Spain).

**Survey flow (about 40–45 minutes as specified; +2 for the Block 0 half)**

| Step | Minutes |
|---|---|
| Farm and field data (pre-collected where possible) | 7–8 |
| Neutral description of each system (no numbers) | 1 |
| Belief questions | 3 |
| Block 0 (half the sample) | 2 |
| Fact cards, comprehension check, pre-choice trust item | 3 |
| Cheap talk, oath and consequentiality scripts | 1 |
| 11 choice tasks | 12–14 |
| Debrief, including the reveal of Paper 1's estimate | 2 |
| Behavioural module | 10–12 |
| Policy questions | 0.5 |

**Ranked cut list**, applied in order if the pilot's median duration exceeds 35 minutes:
1. Pre-collect farm data (pre-visit form or cooperative records).
2. One lottery only; ORIV only if tasks are paid.
3. One time price list plus the patience item.
4. Scales capped at 4 constructs × 3 items (identity, trust, control, one more).
5. Drop the overall belief question.
6. 8 + 1 tasks (4 blocks of 8 from a 32-row design) if tasks take over 1 minute each.

Alternatively, budget a participation fee for a ~40-minute interview.

**Pilot**
- **Cognitive interviews:** 8–10 per country, checking:
  - understanding of the "average yearly margin";
  - acceptance of the what-if wording and credibility of the margins, including negative ones;
  - the wording of the bad-year shortfall, planned lifetime and early removal;
  - double counting of the derived descriptors;
  - the belief questions and the pre-choice trust item;
  - boom widths and machinery fit of the layout levels.
- **Pilot survey:** 30–50 farmers per country, to set the priors, apply the §5.3 rules (range, top level, share keeping current crops, money ignored, margin floor) and time the interview and each task.

**Bias control** (all citations in this table: to verify)

| Threat | Countermeasure |
|---|---|
| Hypothetical bias | WTA cheap-talk script; honesty oath (Jacquemet et al. 2013); opt-out reminder on each card (Ladenburg & Olsen 2014) |
| Strategic answers | No payment in the main DCE. Neutral consequentiality wording ("results inform research on how farmers view these systems; answer as if the choice were real") that never suggests high answers raise payments (Bush et al. 2013; Vossler et al. 2012); perceived-consequentiality and "typical farmer" questions |
| Farmers not believing the margins | Fact card explains that margins vary by design (what-if wording, no false source claim); cash-flow sketch; pre-choice trust item in Π, with results with and without low-trust respondents; Paper 1's estimate revealed in the debrief |
| Ignored attributes | Stated questions plus non-attendance latent classes, especially for money (Hensher et al. 2005; Scarpa et al. 2009) |
| Protest answers / always keeping current crops | Debrief categories (genuinely high WTA, protest, cannot do it, does not believe the numbers); a never-adopt class (von Haefen et al. 2005). Do not delete by default; report with and without (Villanueva et al. 2017; Meyerhoff & Liebe 2009) |
| Uncertainty, fatigue, order | Certainty and task position in the scale function (Lundhede et al. 2009); randomised order; module order reversed for 20% |
| Inconsistent answers | The repeated task (excluded from estimation) |

---

## 12. Open decisions for the student and supervisor

- [ ] **Reference:** confirm that "Stetter (2025)" means Stetter & Sauer (2024), and read its Table 1.
- [ ] **Scope:** confirm that ES/IT means Spain/Italy, and which 2–3 region (× farm type) cells per country Paper 1 covers.
- [ ] **Number of systems:** how many does Paper 1 cost per country (1, 2 or 3)? This decides labelled vs unlabelled, and whether π₁ is identified within respondents.
- [ ] **Paper 1 method and timing:** bio-economic or FADN income forgone? Can it deliver the layout × lifetime grid, cash-flow profiles, the emulator and the Monte Carlo draws in time? If not, use the §8 fallback.
- [ ] **Concordance values:** discount rate r; what happens after the lifetime and after early removal; price year; cost boundary (contribution margin vs full EAV); CAP treatment and tree-strip eligibility.
- [ ] **Layout:** dominant boom widths per stratum; can Paper 1 cost extra passes (or a per-farm spacing pivot)?
- [ ] **Sample frame:** owners only, or also a separately modelled tenant group told to "assume a lease covering the full tree lifetime"? Whole field, or a fixed area for very large fields? A silvopasture version?
- [ ] **Negative margins:** are negative displayed margins acceptable, or should the bottom level be −350?
- [ ] **Budget:** Block 0 (for half the sample or all)? Money for paid tasks and a participation fee?
- [ ] **Taxonomy:** agree the rational vs behavioural split, especially the real-options benchmark and the lifetime premium.
- [ ] **Logistics and registration:**
  - survey mode and access partners;
  - translation and ethics approval (including the no-deception wording of the margins and the debrief reveal);
  - pre-registration of hypotheses, WTA denominator, covariate pairs, equivalence margin and expected-utility benchmark formula.

---

## 13. References

**None of these could be opened in full text; all details come from search snippets or memory. Verify each before citing.**

- Andersen, Harrison, Lau & Rutström (2008). Eliciting risk and time preferences. *Econometrica* 76(3).
- Ben-Akiva et al. (2002). Hybrid choice models: progress and challenges. *Marketing Letters* 13(3).
- Burton (2004). Seeing through the 'good farmer's' eyes. *Sociologia Ruralis* 44(2).
- Bush, Hanley, Moro & Rondeau (2013). Measuring the local costs of conservation. *Land Economics* 89(3).
- Chorus & Kroesen (2014). On the (im-)possibility of deriving transport policy implications from hybrid choice models. *Transport Policy* 36.
- den Herder et al. (2017). Current extent and stratification of agroforestry in the EU. *Agric. Ecosyst. Environ.* 241.
- Dessart, Barreiro-Hurlé & van Bavel (2019). Behavioural factors affecting the adoption of sustainable farming practices. *ERAE* 46(3).
- Dohmen et al. (2011). Individual risk attitudes. *JEEA* 9(3).
- Espinosa-Goded, Barreiro-Hurlé & Dupraz (2013). Identifying additional barriers in the adoption of agri-environmental schemes: the role of fixed costs. *Land Use Policy* 31.
- Espinosa-Goded, Barreiro-Hurlé & Ruto (2010). What do farmers want from agri-environmental scheme design? *JAE* 61(2).
- Falk et al. (2023). The preference survey module. *Management Science* 69(4).
- Frey et al. (2013). A real options model… agroforestry adoption and disadoption. *Agricultural Economics* 44(1).
- Gächter, Johnson & Herrmann (2022). Individual-level loss aversion in riskless and risky choices. *Theory and Decision* 92.
- Gillen, Snowberg & Yariv (2019). Experimenting with measurement error. *JPE* 127(4).
- Gillich et al. (2019). Combining choice modeling estimates and stochastic simulations… *GCB Bioenergy* 11(1).
- Glenk, Meyerhoff, Akaichi & Martin-Ortega (2019). Revisiting cost vector effects in DCEs. *Resource and Energy Economics* 57.
- Hensher, Rose & Greene (2005). The implications on WTP of respondents ignoring specific attributes. *Transportation* 32(3).
- Hess & Palma (2019). Apollo. *Journal of Choice Modelling* 32.
- Holt & Laury (2002). Risk aversion and incentive effects. *AER* 92(5).
- Howley, Buckley, O'Donoghue & Ryan (2015). Explaining the economic 'irrationality' of farmers' land use behaviour. *Ecological Economics* 109.
- Huber, Xiong, Keller & Finger (2022). Bridging behavioural factors and standard bio-economic modelling. *JAE* 73(1).
- Jacquemet, Joule, Luchini & Shogren (2013). Preference elicitation under oath. *JEEM* 65(1).
- Kay et al. (2019). Agroforestry is paying off. *Ecosystem Services* 36.
- Krinsky & Robb (1986). On approximating the statistical properties of elasticities. *Review of Economics and Statistics* 68(4).
- Kragt (2013). The effects of changing cost vectors on choices and scale heterogeneity. *ERE* 54(2).
- Ladenburg & Olsen (2014). Augmenting short cheap talk scripts with a repeated opt-out reminder. *Resource and Energy Economics* 37.
- Leduc & Hansson (2024). Behavioural factors for farmers' adoption of agroforestry practices in Sweden. *Sustainable Production and Consumption* 47.
- Lundhede et al. (2009). Handling respondent uncertainty in choice experiments. *Journal of Choice Modelling* 2(2).
- Lusk & Norwood (2009). An inferred valuation method. *Land Economics* 85(3).
- McGurk, Hynes & Thorne (2020). Participation in agri-environmental schemes: a CV study of farmers in Ireland. *JEM* 262.
- Meyerhoff & Liebe (2009). Status quo effect in choice experiments. *Land Economics* 85(3).
- Musshoff (2012). Growing short rotation coppice… a real options approach. *Biomass and Bioenergy* 41.
- Orme (2010). *Getting Started with Conjoint Analysis* (2nd ed.).
- Santiago-Freijanes et al. (2018). Agroforestry development in Europe: policy issues. *Land Use Policy* 76.
- Scarpa, Thiene & Train (2008). Utility in willingness to pay space. *AJAE* 90(4).
- Scarpa, Gilbride, Campbell & Hensher (2009). Modelling attribute non-attendance… *ERAE* 36(2).
- Seegers, Blake-Rath, Grote & Nguyen (2026). Agroforestry adoption and perceptions in Germany… *Trees, Forests and People*.
- Stetter & Sauer (2024). Tackling climate change: agroforestry adoption in the face of regional weather extremes. *Ecological Economics* 224, 108266. DOI 10.1016/j.ecolecon.2024.108266.
- Swait & Louviere (1993). The role of the scale parameter… *Journal of Marketing Research* 30(3).
- Train & Weeks (2005). Discrete choice models in preference space and WTP space. In Scarpa & Alberini (eds), Springer.
- Vedel, Jacobsen & Thorsen (2015a). Forest owners' WTA… is sensitive to additionality. *Ecological Economics* 113.
- Vedel, Jacobsen & Thorsen (2015b). Contracts for afforestation and the role of monitoring… *Forest Policy and Economics* 51.
- Villamayor-Tomas, Sagebiel & Olschewski (2019). Bringing the neighbors in. *Land Use Policy* 84.
- Villanueva, Glenk & Rodríguez-Entrena (2017). Protest responses and willingness to accept. *JAE* 68(3).
- Viney, Savage & Louviere (2005). Empirical investigation of experimental design properties of DCEs in health care. *Health Economics* 14(4).
- von Haefen, Massey & Adamowicz (2005). Serial nonparticipation in repeated discrete choice models. *AJAE* 87(4).
- Vossler, Doyon & Rondeau (2012). Truth in consequentiality. *AEJ: Microeconomics* 4(4).

