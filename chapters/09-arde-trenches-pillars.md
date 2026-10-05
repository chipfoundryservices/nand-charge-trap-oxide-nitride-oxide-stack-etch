# Chapter 9: Aspect-Ratio-Dependent Etch (ARDE) in Trenches and Pillars

## Executive Summary

In conventional plasma etching of shallow features (aspect ratios <5:1), etch rate is relatively uniform from top to bottom—the top and bottom of a feature etch at approximately the same rate. However, in 3D NAND pillar formation (aspect ratios 100:1 to 2000:1), a dramatic phenomenon occurs: **the etch rate at the bottom of the feature becomes 5-10× slower than at the top**, a phenomenon called **Aspect-Ratio-Dependent Etching (ARDE)**. This chapter develops the physics of ARDE, explaining why it occurs and how to mitigate it. ARDE is fundamentally driven by two competing mechanisms: **(1) neutral radical starvation at depth** due to diffusion limitations in narrow, deep features, and **(2) ion redistribution and charge accumulation** that changes the ion flux and energy distribution with depth. Understanding ARDE is critical because it directly impacts etch uniformity across 3D NAND wafers—if ARDE is not properly compensated, the top layers of a 64-layer stack etch much faster than bottom layers, creating significant non-uniformity and device yield loss.

---

## Part 1: Physical Mechanisms Driving ARDE

### 1.1 Neutral Radical Diffusion Limitation

#### Diffusion in Confined Spaces

In a 50-nm-wide, 25-µm-deep pillar trench:

**Free diffusion distance:** Gas molecules randomly walk through the plasma
$$\lambda_{diff} = \sqrt{D \cdot t}$$

Where D ≈ 0.1-1 cm²/s (diffusion coefficient for neutral radicals), t = diffusion time

**At shallow depth (1 µm):**
- Time to reach bottom: t ≈ 0.1 seconds
- Diffusion distance possible: λ_diff ≈ √(0.1 × 0.1) ≈ 100 µm
- **Radical density at depth ≈ surface density** (no significant depletion)

**At deep depth (25 µm):**
- Effective gap width: 50 nm (extremely narrow; only 500 atoms wide)
- Diffusion is severely restricted by **geometric constraints**
- Radical flux becomes **diffusion-limited**, not supply-limited

#### Radical Density Profile with Depth

**In a deep, narrow trench:**

```
Radical Density vs. Depth

[F•] (cm⁻³)
^
|     Surface: 10¹² cm⁻³ (equilibrium)
|     ███████████ Top (0-1 µm): ~95% of surface
|     ████████░░░ Mid (5-10 µm): ~70% of surface
|     ███░░░░░░░░ Deep (20-25 µm): ~20% of surface
|___________________________________> Depth (µm)
0     5      10     15     20     25
```

**Mathematical model (simplified):**

$$[\text{F}^\bullet](z) = [\text{F}^\bullet]_0 \left(1 - \frac{z}{Z_{eff}}\right)^n$$

Where:
- z = depth into trench
- Z_eff = effective diffusion depth (function of aspect ratio and pressure)
- n ≈ 1-2 (depends on feature geometry)

#### Consequence: Etch Rate Degradation with Depth

**Etch rate is proportional to radical concentration:**

$$R_{etch}(z) \propto [\text{F}^\bullet](z)$$

**If [F•](z) drops to 20% at depth:**
$$R_{etch}(deep) = 0.2 \times R_{etch}(top) = \text{20% of top rate}$$

**ARDE factor:**
$$\lambda = \frac{R_{etch}(bottom)}{R_{etch}(top)} = 0.2 \text{ (ARDE = 5:1)}$$

---

### 1.2 Ion Flux and Energy Redistribution

#### Ion Sheath Formation and Focusing

In a narrow trench, the plasma sheath (ion acceleration region) forms across the wafer-plasma interface. **Ions are preferentially directed toward the trench opening**—this geometric focusing effect means:

**At trench top (wide opening):**
- Ion flux: J_ion(top) = σ_top × n_e × v_e
- Ion energy: E_ion ≈ 40-100 eV (typical)

**At trench bottom (narrow, confined):**
- Ion flux: J_ion(bottom) < J_ion(top) (ions have difficulty reaching narrow bottom)
- Ion energy: E_ion can **increase** locally (charge accumulation) OR **decrease** (collisions)

#### Charge Accumulation and Voltage Buildup

**In deep features, ions create positive charge:**

1. Ion impact → secondary electron emission
2. Electrons escape, leaving positive charge behind
3. In insulating oxide, positive charge cannot easily flow away
4. **Voltage builds up** as etch proceeds

**Voltage buildup equation:**

$$V_{accum}(z) = \frac{Q(z) \cdot d}{\epsilon_0 \epsilon_r A}$$

Where:
- Q(z) = accumulated positive charge at depth z
- d = characteristic distance
- A = trench cross-section area

**At extreme depths:**
- Voltage can rise to 100+ volts (compared to 30-50 V at surface)
- This changes the ion energy distribution

---

### 1.3 Pressure Dependence of ARDE

#### Pressure Effects on ARDE Factor

**ARDE factor (λ) vs. pressure:**

| Pressure (mTorr) | Ion Mean Free Path | ARDE Factor λ |
|---|---|---|
| **5** | ~200 µm | 0.3 (severe ARDE) |
| **10** | ~100 µm | 0.4 |
| **20** | ~50 µm | 0.5 |
| **50** | ~20 µm | 0.65 |
| **100** | ~10 µm | 0.75 (reduced ARDE) |

**Why pressure matters:**

**Low pressure (5-10 mTorr):**
- Long ion mean free path → ions reach deep without collision
- Ions have high energy at depth
- But neutral radical diffusion is MORE limited (fewer gas molecules)
- **Net effect: SEVERE ARDE** (neutral limitation dominates)

**High pressure (50-100 mTorr):**
- Short ion mean free path → ions lose energy via collisions
- Ions deposit energy near surface, less at depth
- But neutral radical diffusion BETTER (more gas molecules available)
- **Net effect: Reduced ARDE** (partial compensation from higher radical density)

**Optimal pressure for CTO etch:** 20-30 mTorr (balance between ARDE and other concerns)

---

## Part 2: ARDE Feedback Correction

### 2.1 Optical Monitoring of ARDE

#### Detecting ARDE from Etch Time Data

**As etch proceeds layer-by-layer:**

| Layer # | Depth (µm) | Expected Time (s) | Actual Time (s) | ARDE Indicator |
|---|---|---|---|---|
| **1-10** | 0-3 | 10 | 10 | Baseline |
| **20-30** | 4-6 | 10 | 11 | +10% slowdown |
| **40-50** | 9-12 | 10 | 13 | +30% slowdown |
| **60-64** | 15-20 | 10 | 18 | +80% slowdown |

**Trend:** Etch time per layer **increases** as depth increases (ARDE slowing down)

#### Real-Time Feedback Algorithm

**Detect ARDE, predict next layers, adjust parameters:**

```
While etch proceeds:
  1. Measure etch time for current layer (T_measured)
  2. Compare to historical average (T_expected)
  3. Calculate ARDE trend: ΔT = T_measured - T_expected
  
  If ΔT > +20% (etch slowing):
     → ARDE detected
     → Predict bottom layers will be even slower
     → Increase RF power by 10-15% to compensate
     → Reduce pressure by 2-3 mTorr to improve radical diffusion
  
  4. Continue monitoring; adjust recursively
```

---

### 2.2 Pulsed-Etch Compensation for ARDE

#### Why Pulsing Helps ARDE

**Continuous etch problem:**
- Deep radicals depleted over 20-minute etch
- Etch rate slows progressively with depth (ARDE worsens)

**Pulsed etch solution:**
- Brief plasma on (10-30 sec) → etch proceeds
- Brief plasma off (3-5 sec) → radicals "refresh," diffuse deep
- Repeat

**Benefit:** Between pulses, radical density profile **recovers**—deep regions regain radical concentration.

**Effective radical density with pulsing:**

$$[\text{F}^\bullet]_{eff, pulsed} = [\text{F}^\bullet]_{steady-state} \times \frac{t_{on}}{t_{on} + t_{off}} + \text{recovery contribution}$$

**Result:** ARDE factor improves from λ = 0.3 (continuous) to λ = 0.6-0.7 (pulsed).

#### Three-Step Etch with ARDE Compensation

Modern 3D NAND uses sophisticated multi-step recipes:

**Phase 1: Top layers (0-5 µm depth)**
- Continuous or long-pulse CF₄ etch
- High selectivity (10:1 SiO₂/Si₃N₄) prioritized
- Etch rate: ~150 nm/min
- Duration: 5 minutes

**Phase 2: Mid layers (5-15 µm depth)**
- Transition to balanced pulsed etch
- Selectivity: 6:1, rate optimization begins
- Etch rate: ~180 nm/min (pulse-averaged)
- Duration: 8 minutes

**Phase 3: Deep layers (15-25 µm depth)**
- Aggressive pulsing (30 sec on / 5 sec off) to fight ARDE
- Higher average RF power to compensate
- Selectivity: 4-5:1 (lower, but acceptable at depth)
- Etch rate: ~250 nm/min (pulse-averaged)
- Duration: 5 minutes

**Result:** Relatively uniform etch across all layers (ARDE compensation)

---

## Part 3: ARDE in Different Feature Geometries

### 3.1 Trenches vs. Pillars

#### Pillar Geometry (3D NAND String Etch)

```
         Pillar (Si core)
            ╱╲
           ╱  ╲  ← Width: 30-50 nm
          ╱    ╲
         ╱______╲
         |      |
         |      | ← Height: 25 µm (deep)
         |      |
         |______|
            25 µm
```

**ARDE mechanism in pillars:**
- Radicals diffuse through gap between pillar and trench wall
- Gap width decreases as pillars etched (gaps narrow)
- ARDE **increases over etch** (worse as etch proceeds)

#### Trench Geometry (Interconnect)

```
         ______
        |      |  ← Width: 200-500 nm
        |      |
        |      | ← Depth: 1-5 µm (shallow)
        |______|
         200 nm
```

**ARDE mechanism in trenches:**
- Radicals diffuse through wider openings
- ARDE **minimal** (radicals reach bottom easily)
- Etch is relatively uniform top-to-bottom

**Key difference:** Pillar ARDE much worse than trench ARDE (narrow width, extreme aspect ratio)

---

### 3.2 Aspect Ratio Scaling Law

#### ARDE Factor vs. Aspect Ratio

**Empirical relationship (verified experimentally):**

$$\lambda = \text{ARDE factor} = 1 - \alpha \times \text{AR}^{-0.5}$$

Where:
- AR = aspect ratio (depth / width)
- α ≈ 0.5-0.8 (chemistry-dependent)

**Examples:**

| Aspect Ratio | Calculation | ARDE Factor λ |
|---|---|---|
| **5:1** | 1 - 0.7 × (5)^-0.5 | 0.69 |
| **10:1** | 1 - 0.7 × (10)^-0.5 | 0.78 |
| **50:1** | 1 - 0.7 × (50)^-0.5 | 0.90 |
| **100:1** | 1 - 0.7 × (100)^-0.5 | 0.93 |
| **500:1** | 1 - 0.7 × (500)^-0.5 | 0.97 |

**Surprising insight:** At very extreme aspect ratios (>200:1), ARDE factor approaches 1.0 (no ARDE)!

**Why?** At AR > 200:1, the diffusion limitation is so severe that the etch is already **diffusion-limited everywhere**—adding more depth doesn't make it worse.

---

## Part 4: ARDE Compensation Strategies in Production

### 4.1 Multi-Parameter ARDE Tuning

#### Four Levers for ARDE Control

| Parameter | Effect on ARDE | Implementation |
|---|---|---|
| **RF Power** | Higher power → more ions → better depth access | Increase power by 5-20% for deep layers |
| **Pressure** | Lower pressure → better radical diffusion | Reduce from 30 to 15 mTorr for Phase 3 |
| **Temperature** | Lower T → slower etch everywhere (less ARDE per se, but slower absolute rate) | Cool to -10°C for high-selectivity phases |
| **Gas Chemistry** | C₄F₈ (polymerizing) → higher ARDE; CF₄ → lower ARDE | More C₄F₈ in Phase 1, less in Phase 3 |
| **Pulsing** | Pulsed etch → ~2× improvement in ARDE | 30 sec on / 5 sec off in Phase 3 |

#### Three-Phase Recipe with ARDE Targets

**Phase 1: High Selectivity (0-3 min, top 2-3 µm)**
- RF Power: 200 W
- Pressure: 30 mTorr
- Pulse: Continuous
- C₄F₈: 30%
- Selectivity: 10:1
- Expected ARDE: 0.5 (mild, but top layers don't need ARDE compensation)

**Phase 2: Transition (3-12 min, mid 7-12 µm)**
- RF Power: 300 W (↑50%)
- Pressure: 25 mTorr (↓20%)
- Pulse: 45 sec on / 5 sec off
- C₄F₈: 20%
- Selectivity: 5-6:1
- Expected ARDE: 0.6 (moderate compensation via power/pressure/pulse)

**Phase 3: Deep Etch (12-20 min, bottom 10-15 µm)**
- RF Power: 400 W (↑100% vs. Phase 1)
- Pressure: 15 mTorr (↓50% vs. Phase 1)
- Pulse: 30 sec on / 5 sec off (aggressive)
- C₄F₈: 15%
- Selectivity: 4-5:1
- Expected ARDE: 0.7-0.8 (ARDE reduced via aggressive compensation)

**Net result:** Overall etch uniformity ±10% across all 64 layers

---

### 4.2 Wafer-to-Wafer Variation

#### Chamber Conditioning Effect on ARDE

**Fresh chamber (after cleans):**
- Electrode surfaces clean
- Plasma properties optimized
- ARDE factor: λ = 0.5

**After 50 wafers (chamber walls conditioning):**
- Fluorocarbon polymer coating on walls
- Reduces ion current slightly
- Affects radical distribution
- ARDE factor: λ = 0.55 (slightly worse)

**After 200 wafers (heavy conditioning):**
- Thick polymer layer
- More pronounced current redistribution
- ARDE factor: λ = 0.60 (noticeably worse)

#### Feedback Control for Chamber Conditioning

**Wafer-to-wafer trend tracking:**

```
Wafer #1-10:   Layer N etch time: 10 sec (baseline)
Wafer #11-50:  Layer N etch time: 10.5 sec (+5%)
Wafer #51-100: Layer N etch time: 11.0 sec (+10%)
Wafer #101+:   Layer N etch time: 11.5 sec (+15%)

Inference: Chamber conditioning worsening ARDE
Action: Increase power in Phase 3 progressively
        Or schedule chamber clean after 150 wafers
```

---

## Summary: ARDE in 3D NAND CTO Etch

| Aspect | Impact on ARDE | Mitigation |
|---|---|---|
| **Neutral radical diffusion** | Dominates at low pressure; ARDE can be 5-10:1 | Reduce pressure, pulse etch, increase power |
| **Aspect ratio scaling** | ARDE factor improves as AR increases >100:1 | Extreme AR features have reduced ARDE problem |
| **Pillar geometry** | Narrow gaps → severe ARDE (5-20× slowdown at depth) | Aggressive pulsing and power control critical |
| **Pressure optimization** | 20-30 mTorr optimal balance | Lower pressure for Phase 3 compensation |
| **Pulsed etch** | ~2× improvement in ARDE factor | Standard in Phase 2-3 production recipes |
| **Multi-phase recipe** | Adaptive power/pressure/chemistry per depth | Essential for ±10% uniformity across 64 layers |
| **Chamber conditioning** | Worsens ARDE over wafer runs | Track trends; adjust parameters or schedule cleans |

**Key Takeaway:** ARDE is the dominant uniformity challenge in 3D NAND CTO etch. Production success requires sophisticated multi-parameter feedback control, pulsed-plasma strategies, and continuous chamber conditioning monitoring to maintain etch uniformity across extreme aspect ratios.

---

[Continue to Chapter 10: Charge Accumulation & Electric Field Effects →](./10-charge-accumulation-efield.md)
