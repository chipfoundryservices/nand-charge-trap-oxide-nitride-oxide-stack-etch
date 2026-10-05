# Chapter 7: Layer-by-Layer Selectivity Control & Feedback Mechanisms

## Executive Summary

In CTO etch, maintaining constant selectivity across 60+ repeated SiO₂/Si₃N₄ layers requires real-time feedback and dynamic process control. This chapter develops the mechanisms for detecting etch progress (which layer is currently being removed), predicting selectivity shifts, and adjusting plasma parameters to maintain selectivity within target window. Three primary feedback approaches are discussed: **(1) optical monitoring via reflectance interferometry**, which can detect when each oxide layer has been completely removed; **(2) capacitive sensing**, which detects charge accumulation and electrical state changes at depth; and **(3) time-domain control**, which uses predefined recipes that adjust parameters at specific time points**. The chapter emphasizes the critical challenge in 3D NAND: selectivity requirements become more stringent as depth increases (deep layers have higher risk of over-etch), yet most feedback signals weaken at depth. Understanding these trade-offs and designing robust control systems is central to achieving high-yield 3D NAND manufacturing.

---

## Part 1: Optical Endpoint Detection and Layer Counting

### 1.1 Reflectance Interferometry for CTO Etch

#### Light Interference at Oxide-Nitride Interfaces

**When light reflects from a thin-film stack:**

```
Incident Light (λ = 248 nm, UV)
         ↓
    ╔════════════╗  SiO₂ layer (n ≈ 1.46, t ≈ 10 nm)
    ║ Reflection ║  
    ║   (path 1) ║  
    ╠════════════╣  Si₃N₄ layer (n ≈ 2.0, t ≈ 6 nm)
    ║ Reflection ║
    ║   (path 2) ║
    ╚════════════╝
```

**Optical path difference:** Δ = 2nt cos(θ), where t = layer thickness, n = refractive index

**Constructive/destructive interference depends on Δ:**
- If Δ = mλ (m = integer): **Constructive** (bright)
- If Δ = (m + 0.5)λ: **Destructive** (dark)

#### Reflectance Oscillation as Etch Proceeds

**As SiO₂ layer etches:**

| Time (sec) | Remaining Oxide | Optical Phase | Reflected Intensity |
|---|---|---|---|
| **0** | 10 nm | Constructive | Bright (100%) |
| **10** | 7.5 nm | Transitioning | 75% |
| **20** | 5 nm | Destructive | Dark (0%) |
| **30** | 2.5 nm | Transitioning | 75% |
| **40** | 0 nm (just removed) | Constructive | Bright (100%) |
| **50** | Si₃N₄ now exposed | New phase | **Sudden shift** |

**Key observation:** Reflectance **oscillates** as oxide thickness decreases, then **suddenly shifts** when oxide is completely removed and nitride is exposed.

#### Endpoint Detection: Phase Shift Detection

**When SiO₂ is completely removed and Si₃N₄ is exposed:**

- **Refractive index changes:** From n_SiO₂ ≈ 1.46 to n_Si₃N₄ ≈ 2.0
- **Reflected phase suddenly shifts:** ~180° phase change
- **Intensity sudden drop** (SiO₂ had high reflectance, Si₃N₄ has lower reflectance in UV)

**Algorithm:**
1. Monitor reflected intensity at λ = 248 nm (common choice for UV optics)
2. Detect **first minimum** (destructive interference) = ~50% of SiO₂ removed
3. Detect **phase shift discontinuity** (SiO₂→Si₃N₄ transition) = endpoint
4. **Time to reach endpoint:** Etch duration for single SiO₂ layer

---

### 1.2 Multi-Wavelength Approach for Deep Features

#### Challenge at High Aspect Ratios

**In deep CTO trenches (20+ µm deep):**

- Light penetration limited by absorption in SiO₂ (α ≈ 10⁴ cm⁻¹ in UV)
- **Penetration depth:** L ≈ 1/α ≈ 1 µm
- **Below 1 µm depth:** Light from bottom layers cannot escape; signal lost
- **Result:** Optical endpoint detection fails for deep layers

#### Multi-Wavelength Monitoring Strategy

**Use multiple wavelengths:**

| Wavelength | Penetration Depth | Application |
|---|---|---|
| **UV (248 nm)** | ~1-2 µm | Top 10-20 layers (shallow) |
| **Blue (405 nm)** | ~5-10 µm | Mid-depth layers |
| **Green (532 nm)** | ~10-30 µm | Deeper layers |
| **IR (850 nm)** | ~50+ µm | Very deep features |

**Multi-wavelength algorithm:**
1. **Early etch (top SiO₂):** Use UV (248 nm) for high signal-to-noise
2. **Mid-etch (5-15 µm):** Switch to green (532 nm) as UV signal weakens
3. **Late etch (deep layers):** Use IR (850 nm) for maximum penetration
4. **Combine signals:** Cross-correlate multi-wavelength data to estimate current etch depth

**Accuracy:** ±1-2 nm endpoint detection possible even at 20+ µm depth (verified against SEM cross-sections)

---

### 1.3 Limitation: Optical Signal Loss at Extreme Depths

#### Optical Extinction in CTO Stacks

**Absorption coefficient for SiO₂ varies strongly with wavelength:**

| Wavelength | Absorption α (cm⁻¹) | Penetration L = 1/α |
|---|---|---|
| **UV (248 nm)** | 10⁴-10⁵ | 0.1-1 µm |
| **Visible (400-600 nm)** | 10²-10³ | 1-100 µm |
| **IR (800-1000 nm)** | 10-100 | 100-10000 µm |

**In 64-layer 3D NAND (5-8 µm total depth):**
- Top 10 µm accessible to visible light
- Bottom layers (deep trenches) essentially opaque
- **Optical endpoint unreliable for final 5-10 layers**

**Consequence:** Must combine optical monitoring (for top layers) with **time-based or electrical sensing** (for deep layers).

---

## Part 2: Capacitive and Electrical Sensing

### 2.1 Charge Accumulation at Depth

#### Electric Field Development in Deep Features

**In a deep CTO trench:**

1. **Ions penetrate to surface** creating positive charge (and leaving electrons behind in sheath)
2. **Secondary electrons escape** from surface (leaving positive charge)
3. **Oxide acts as insulator** → charge cannot easily flow away
4. **Net result:** Positive charge accumulates in the oxide

#### Voltage Buildup Model

**Sheath voltage increases with depth:**

$$V_\text{sheath}(z) = V_0 + \frac{Q \cdot z}{\epsilon_0 \epsilon_r A}$$

Where:
- V₀ = initial bias voltage
- Q = accumulated charge (coulombs)
- z = depth into feature
- A = feature cross-sectional area
- ε₀, ε_r = permittivity

**For a 50-nm-wide trench at 25 µm depth:**
- Q ≈ 10⁻¹⁵ C (femtocoulombs)
- V_sheath can rise to **100+ volts** (compared to ~40 V at surface)

#### Effect of Charge Accumulation on Etch Rate

**Higher voltage → higher ion impact energy → higher Si₃N₄ etch rate:**

$$R_\text{etch} \propto (V_\text{ion} - E_\text{threshold})^{0.5}$$

**Consequence:** At extreme depths:
- Si₃N₄ etch rate increases 2-5× above baseline
- Selectivity SiO₂/Si₃N₄ **decreases** with depth
- **Risk:** Deep Si₃N₄ layers can be over-etched if selectivity not carefully managed

---

### 2.2 Capacitance Monitoring

#### Principle: Wafer Impedance Changes with Stack Composition

**The CTO stack acts as a series capacitor:**

$$C_\text{total} = \frac{\epsilon_0 \epsilon_r A}{t_\text{total}}$$

As etch proceeds:
- **Before etch:** Stack is "thick" → Low capacitance
- **After removing SiO₂:** Stack is "thin" → Higher capacitance
- **Capacitance jumps** when Si₃N₄ layer is reached (different dielectric constant)

#### Capacitive Sensor Implementation

**RF electrode–wafer system acts as capacitor:**

At RF frequency (13.56 MHz or 2 MHz):
- Capacitive reactance: X_c = 1/(ωC)
- Impedance changes as etch proceeds

**Measurement:** Monitor phase shift and magnitude of RF current at constant voltage

| Etch Stage | Stack Composition | Capacitance | Impedance |
|---|---|---|---|
| **Start** | Full SiO₂/Si₃N₄ stack | ~10 pF | High (~1 kΩ) |
| **Mid-etch** | Partial stack removed | ~20 pF | Lower (~500 Ω) |
| **SiO₂ complete** | Si₃N₄ layer reached | ~30 pF (different ε_r) | Changes |
| **Si₃N₄ complete** | Silicon substrate exposed | ~50 pF (ε_r of Si much higher) | Low (~200 Ω) |

#### Sensitivity and Limitations

**Advantages:**
- Detects changes at **any depth** (no optical penetration limitation)
- Real-time feedback possible
- No optical components needed

**Limitations:**
- Absolute capacitance depends on electrode geometry, wafer placement, etc.
- Drifts over time (electrode conditioning, chamber wall deposits)
- **Cannot distinguish between SiO₂ and Si₃N₄** (both contribute to stack capacitance)
- Requires baseline calibration per wafer

---

## Part 3: Feedback Control and Selectivity Maintenance

### 3.1 Time-Based Recipe with Adaptive Steps

#### Multi-Step Etch Recipe Design

Modern 3D NAND CTO etch uses **three or more distinct etch phases**, each with different plasma parameters:

**Phase 1: High-Selectivity Etch (0-3 minutes)**
- Goal: Remove top SiO₂ layers without damaging Si₃N₄
- Conditions:
  - Temperature: -5°C (low, favors SiO₂)
  - Power: 200 W (low, reduces ion-assisted component)
  - C₄F₈ fraction: 30% (high, maximum polymerization on Si₃N₄)
  - Selectivity target: SiO₂/Si₃N₄ > 10:1
  - Expected etch depth: ~2-3 µm

**Phase 2: Balanced Etch (3-12 minutes)**
- Goal: Mid-stack etch with balanced selectivity and rate
- Conditions:
  - Temperature: +15°C (moderate)
  - Power: 300 W (moderate)
  - C₄F₈ fraction: 20% (moderate polymerization)
  - Selectivity target: SiO₂/Si₃N₄ = 5-6:1
  - Expected etch depth: ~3-5 µm

**Phase 3: Deep-Feature Etch (12-20 minutes)**
- Goal: Rapid etch of remaining deep SiO₂ with selectivity protection
- Conditions:
  - Temperature: +25°C (higher, faster etch)
  - Power: 400 W (higher)
  - C₄F₈ fraction: 15% (some polymerization for protection)
  - Selectivity target: SiO₂/Si₃N₄ = 4-5:1 (lower, but acceptable due to reduced charge accumulation at partial depth)
  - Expected etch depth: ~1-2 µm (to reach target Si₃N₄)

#### Rationale for Three-Phase Approach

| Metric | Phase 1 | Phase 2 | Phase 3 | Benefit |
|---|---|---|---|---|
| **Selectivity** | 10:1 | 5-6:1 | 4-5:1 | Balanced: High at top (protect charge-trap), acceptable at depth |
| **Etch rate** | 100 nm/min | 180 nm/min | 250 nm/min | Fast completion (< 20 min) |
| **Charge accumulation** | Low (shallow) | Moderate | High (deep) → mitigated by higher ion energy at depth | Manages voltage buildup |
| **Total etch depth** | 2-3 µm | 3-5 µm | 1-2 µm | **Total: ~6-10 µm** (64-layer stack) |

---

### 3.2 Feedback-Controlled Adjustments

#### Real-Time Optical Endpoint Feedback

**Algorithm:**

1. **Monitor reflected intensity** at 248 nm
2. Detect **endpoint signal** (phase shift) when each SiO₂ layer complete
3. **Compare actual time to remove layer** vs. expected time
4. **Adjust future phase parameters** if actual time differs

**Example adjustment:**

```
Expected etch time for layer N: 10 sec (from prior wafers)
Actual etch time for layer N: 12 sec (observed from optical data)

Inference: Etch is slower than expected (selectivity may be higher)
→ Prediction: Next layers will also be slower

Adjustment for next phase:
  Increase RF power by 10% to maintain schedule
  Or decrease C₄F₈ fraction by 2% to reduce selectivity
```

#### Wafer-to-Wafer Adaptation

**Maintain database of etch times for each layer:**

| Wafer | Layer 1 | Layer 2 | Layer 3 | Layer 4 | ... | Layer 64 |
|---|---|---|---|---|---|---|
| **W1** | 9.8 s | 10.1 s | 10.3 s | 10.5 s | ... | 11.2 s |
| **W2** | 10.2 s | 10.4 s | 10.6 s | 10.8 s | ... | 11.5 s |
| **W3** | 9.9 s | 10.2 s | 10.4 s | 10.6 s | ... | 11.3 s |

**Trend analysis:**
- **Layer-to-layer increase:** Each successive layer takes ~0.3 s longer (expected due to charge accumulation)
- **Wafer-to-wafer variation:** ~0.3-0.4 s (chamber conditioning, starting conditions)
- **Extreme outlier:** If a layer takes >50% longer than expected → may indicate equipment issue (RF mismatch, gas imbalance) → flag for maintenance

---

## Summary: Selectivity Control and Feedback

| Method | Advantages | Limitations | Used For |
|---|---|---|---|
| **Optical endpoint** | High-resolution timing, detects layer completion | Only works at shallow depths (<5-10 µm) | Top 20-30 layers |
| **Capacitive sensing** | Works at any depth, detects impedance changes | Cannot distinguish SiO₂ from Si₃N₄, drifts over time | Confirms optical or provides feedback for deep layers |
| **Time-based recipe** | Predictable, reproducible, requires no real-time adjustment | Cannot adapt to changes mid-etch; assumes constant rates | Baseline approach; used in production when well-characterized |
| **Feedback-controlled** | Adapts to wafer-to-wafer and chamber-to-chamber variation | Requires sensors (optical, capacitive) and fast control loop; complex | Advanced production systems for tighter control |

**Key Insight:** No single feedback method is perfect for extreme-aspect-ratio CTO etch. Production systems typically combine **optical monitoring for top layers** + **time-based recipe for deep layers** + **occasional capacitive checks** to maintain selectivity within ±5-10% across all layers.

---

[Continue to Chapter 8: Polymer Formation & Surface Passivation →](./08-polymer-passivation.md)
