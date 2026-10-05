# Chapter 10: Charge Accumulation & Electric Field Effects in Deep Features

## Executive Summary

As plasma etch proceeds into deep 3D NAND pillars, ions and secondary electrons create a **buildup of electric charge** within the insulating CTO stack. Unlike shallow trenches where charge can escape easily, deep features in narrow pillars create a "charge trap" where positive ions arrive faster than electrons can escape. This charge accumulation creates a **self-biasing electric field** that can exceed 100+ volts at depth—far higher than the externally applied bias voltage of 30-50 V. This chapter develops the detailed physics of charge accumulation: how charge builds up with depth, how voltage rises as etch proceeds, what consequences this has for ion energy distribution, and why charge accumulation can create edge-field enhancement effects that damage selectivity. Special attention is paid to the **nonlinear feedback**: charge accumulation slows etch rate (reducing further charge generation), but charge can remain trapped for extended times, creating history-dependent effects where etch rate depends on prior wafer processing history rather than current conditions alone. Understanding charge accumulation is essential for process stability and yield: excessive charge can cause oxide breakdown, device damage, or catastrophic etch runaway at certain depth ranges.

---

## Part 1: Charge Generation and Trapping Mechanisms

### 1.1 Ion Impact and Secondary Electron Emission

#### Secondary Electron Yield

**When a high-energy ion hits the SiO₂ surface:**

1. **Ion impact creates cascade of secondary collisions**
2. **Secondary electrons are ejected from surface**
3. **Net result:** Each ion impact → 1-3 secondary electrons released

**Secondary electron yield (γ):**

| Ion Type | Ion Energy | Yield γ (electrons/ion) |
|---|---|---|
| **Ar⁺** | 50 eV | 0.5 |
| **F⁺** | 50 eV | 0.3 |
| **CF₃⁺** | 50 eV | 0.2 |
| **Ar⁺** | 200 eV | 1.5 |
| **Ar⁺** | 500 eV | 2-3 |

**Typical CF₄ etch plasma (100 W, 20 mTorr):**
- Ion energy: ~50-150 eV (depends on sheath voltage)
- Average secondary yield: γ ≈ 0.5-1.0 electrons/ion

#### Electron Escape vs. Trapping

**At shallow depth (wafer surface):**
- Secondary electrons generated at SiO₂ surface
- **Electrons escape easily** to plasma (high escape probability)
- Positive charge from ion NOT trapped
- **Net: No charge accumulation**

**At deep depth (inside narrow trench):**
- Ions reach deep feature after traversing trench opening
- Secondary electrons generated at trench bottom/walls
- **Electrons must traverse back up through trench** (difficult)
- Many electrons recombine with ions or stick to walls
- **Net: Positive charge ACCUMULATES**

---

### 1.2 Charge Buildup Dynamics

#### Charge Balance Equation

**Rate of charge accumulation:**

$$\frac{dQ}{dt} = \text{Ion arrival rate} - \text{Electron escape rate}$$

$$\frac{dQ}{dt} = J_{ion} - \gamma J_{ion} \times P_{escape}$$

Where:
- J_ion = ion current (coulombs/sec)
- γ = secondary electron yield
- P_escape = probability electron escapes (depends on depth, trench width)

#### Voltage Buildup with Accumulated Charge

**Accumulated charge creates electric field:**

$$E = \frac{Q}{C} = \frac{Q \cdot d}{\epsilon_0 \epsilon_r A}$$

**Voltage buildup:**

$$V_{accum}(t) = \frac{1}{C} \int_0^t \frac{dQ}{dt'} dt' = \frac{1}{C} \times Q(t)$$

**Where capacitance C depends on oxide thickness:**

$$C = \frac{\epsilon_0 \epsilon_r A}{t_{oxide}}$$

**As etch proceeds and oxide thickness decreases:**
- Oxide becomes thinner → **Capacitance INCREASES**
- Same charge Q → **Voltage DECREASES**
- **Result:** Voltage doesn't increase indefinitely; it plateaus as oxide thins

#### Typical Voltage Buildup vs. Etch Time

**In a 50-nm-wide, 25-µm-deep trench (20 mTorr CF₄, 100 W):**

| Etch Time (min) | Depth Etched (µm) | Oxide Thickness (nm) | Accumulated Charge | Sheath Voltage |
|---|---|---|---|---|
| **0** | 0 | 100 | 0 fC | 50 V (external) |
| **5** | 3 | 85 | 50 fC | 65 V |
| **10** | 6 | 70 | 120 fC | 85 V |
| **15** | 12 | 55 | 200 fC | 110 V |
| **20** | 25 | 40 | 250 fC | 130 V |

**Peak voltage at depth: ~130 V** (compared to external bias of 50 V)

---

## Part 2: Consequences of Charge Accumulation

### 2.1 Ion Energy Redistribution with Depth

#### How Voltage Affects Ion Energy

**Ion energy at wafer surface:**

$$E_{ion, surface} = e \times V_{bias}$$

Where V_bias = externally applied bias voltage (~50 V)

**Ion energy at depth z in feature (with charge accumulation):**

$$E_{ion}(z) = e \times [V_{bias} + V_{accum}(z)]$$

**Example (from table above):**
- At surface: E_ion = 50 eV (from external 50 V)
- At 25 µm depth: E_ion = 130 eV (50 V external + 80 V accumulated)
- **Energy increase: 2.6×**

#### Effect on Etch Rate (Ion-Assisted Component)

**Ion-assisted etch rate depends on ion energy:**

$$R_{etch, ion} \propto (E_{ion} - E_{threshold})^{0.5-1.0}$$

**Example at depth:**
- Energy increase: 50 eV → 130 eV
- Etch rate increase from ion assistance: ~1.5-2×
- **But this is offset by reduced radical density from ARDE**

**Net effect at depth:**
- Radical density: ↓ (ARDE, ~0.3× at 25 µm)
- Ion-assisted component: ↑ (2× from higher ion energy)
- **Total etch rate: ~0.6× of top rate** (slight improvement from ion assist, but still dominated by radical starvation)

---

### 2.2 Edge-Field Enhancement and Sidewall Effects

#### Electric Field Concentration at Pillar Edges

**In the narrow gap between pillar and trench wall:**

```
                  Trench Wall (SiO₂)
                        │
        Gap (20-50 nm)  │  Electric Field Lines
                        │
    ┌─────────────────────┐
    │ Pillar (Si or Si-Ge) │  Pillar Edge
    │      CORE            │
    └─────────────────────┘
        │
        │  High charge density
        │  at corner
        
Electric field stronger at edges than in center
E_corner ≈ 1.5-2.0 × E_center
```

**Consequence:** Ions preferentially focused toward **pillar edges** rather than center

#### Selectivity Breakdown at Edge

**At pillar edges:**
- Higher ion energy (concentrated field)
- Enhanced sputtering of Si₃N₄ passivation layer
- **Local selectivity SiO₂/Si₃N₄ drops** (e.g., from 5:1 to 2-3:1 at edges)
- **Result:** Pillar edges etch preferentially → pillar becomes narrower

**Concern for device:** If pillar tapers too much, it can **break apart** (mechanical failure) or create highly non-uniform charge-trap layer thickness (electrical failure).

---

### 2.3 Charge-Induced Plasma Potential Oscillations

#### Transient Voltage Spikes

**As charge accumulates, the feedback loop can create oscillations:**

1. Charge builds → voltage rises
2. Higher voltage → higher ion energy → faster etch
3. Faster etch → more charge generation
4. But charge can suddenly neutralize (rare electron escape event)
5. Voltage suddenly drops
6. Lower voltage → lower etch rate
7. Cycle repeats

**Timescale:** Oscillations typically 1-100 ms (rapid compared to slow 20-min etch)

**Amplitude:** Voltage can swing ±20-30 V around the mean value (50-130 V)

#### Impact on Process Stability

**Voltage oscillations → etch rate oscillations:**
- Etch rate fluctuates by ±15-20% around mean
- Creates **wavy etch profile** (alternating fast-slow-fast layers)
- Difficult for optical endpoint detection

**Mitigation:**
- Use **pulsed RF power** (turns off electrons' escape chance between pulses)
- Reduces oscillation amplitude
- Stabilizes etch rate

---

## Part 3: Charge Accumulation Limits and Failure Modes

### 3.1 Oxide Breakdown Risk

#### Breakdown Field Strength

**Dielectric breakdown of SiO₂:**

| Oxide Quality | Breakdown Field (MV/cm) | Breakdown Voltage (nm) |
|---|---|---|
| **High-quality thermal oxide** | 6-10 | 600-1000 V (for 100 nm) |
| **Deposited PECVD oxide** | 4-8 | 400-800 V |
| **Defective/thin oxide** | 2-4 | 200-400 V |

**In deep CTO features:**
- Accumulated voltage: up to 130 V (from earlier table)
- Oxide thickness: 40-50 nm (as etch progresses)
- **Electric field:** E = V/d = 130 V / 50 nm = **2.6 MV/cm**

**Breakdown risk:** Close to threshold for defective oxide!

**Consequence if breakdown occurs:**
1. Oxide short circuit → current surge
2. Current spike can **melt** local oxide region
3. Creates permanent short circuit
4. Device failure (catastrophic leakage)

#### Thermal Breakdown Hotspots

**At edge-field enhancement regions (pillar edges):**
- Local field concentrated: E ≈ 2× center
- Heating from current: P = I²R
- Local temperature rises
- **Oxide thermal breakdown possible** even before electrostatic breakdown

---

### 3.2 Charge Accumulation Saturation

#### Why Voltage Doesn't Rise Indefinitely

**As oxide thickness decreases (etch proceeds):**

$$C \propto \frac{1}{t_{oxide}} \rightarrow C \text{ increases}$$

$$V = \frac{Q}{C} \text{ decreases}$$

**Example:**
- Early etch (t_ox = 100 nm): V = Q/C = 80 V
- Late etch (t_ox = 50 nm): V = Q/C = 65 V (voltage actually drops)

**Self-regulation mechanism:**
- As voltage drops, ion-assisted etch rate decreases
- Charge generation decreases
- Charge accumulation rate decreases
- **System reaches quasi-steady state**

#### Practical Saturation Voltage

**For typical CF₄ CTO etch:**

**Maximum voltage reached:** 100-150 V (depends on trench width and geometry)

**After which:** Voltage stabilizes or slightly decreases as oxide thins

**Critical design point:** If breakdown field of oxide < 150 V, **oxide breakdown risk high**

**Mitigation:**
- Use higher-quality oxide (lower defect density)
- Reduce external bias voltage slightly (trades ion energy for safety)
- Pulsed etch (reduces peak voltage spikes)

---

## Part 4: Charge Effects in Production Recipes

### 4.1 Charge Accumulation and Process Margin

#### Process Window Shrinkage Due to Charge

**Without charge accumulation (hypothetical):**
- Safe external bias: 40-60 V
- Safe temperature: 0-30°C
- Safe pressure: 15-40 mTorr
- **Process window: Moderate**

**With charge accumulation (reality):**
- Effective voltage at depth: 50-130 V (2.6× higher)
- Breakdown risk at high voltage
- **Process window: SHRUNK**
- Safe parameter space: narrower

#### Charge-Aware Recipe Design

**Traditional recipe (ignores charge):**
- RF Power: 300 W constant
- Bias: -50 V constant
- Pressure: 25 mTorr constant
- **Result:** Charge accumulates; voltage rises to 100-120 V by end of etch

**Charge-aware recipe (modern):**

**Phase 1 (0-10 min, safe zone):**
- RF Power: 300 W
- Bias: -50 V (voltage rises to ~70-80 V)
- Selectivity good; charge not critical

**Phase 2 (10-18 min, charge-critical zone):**
- RF Power: 250 W (reduce power → fewer ions → less charge)
- Bias: -35 V (reduce bias → lower absolute voltages)
- Pressure: 35 mTorr (higher pressure → less ion penetration to depth)
- **Result:** Voltage peaks at ~90 V (safer margin)

**Phase 3 (18-20 min, final layers):**
- Power: 280 W (slight increase; oxide thinner, safer)
- Bias: -40 V (intermediate)
- Pressure: 20 mTorr (lower pressure for etch rate boost near end)

**Net benefit:** Charge controlled; voltage stays <100 V throughout (safe from breakdown)

---

### 4.2 Wafer-to-Wafer Charge History Effects

#### Charge Persistence and Wafer Conditioning

**Surprising observation:** After completing one wafer:
- Wafer removed from chamber
- But **charge in chamber walls persists** (decays slowly over seconds to minutes)
- Next wafer enters a **partially pre-charged environment**

**Consequence:** First wafer etch ≠ second wafer etch

**Wafer #1 (chamber fresh):**
- Charge starts from 0
- Voltage buildup: 0 → 100 V over etch
- Final etch rate at depth: moderate

**Wafer #2 (chamber charged):**
- Charge starts from ~30% of previous level (partial decay)
- Voltage buildup: 30 → 110 V (starts higher)
- Final etch rate at depth: slightly slower (higher baseline voltage)

#### Charge Relaxation Time

**Charge decay timescale** (affected by chamber wall properties):
- Clean chamber: τ ≈ 5-10 seconds (charge dissipates via electrons)
- After 50+ wafers (walls conditioned with polymer): τ ≈ 30-60 seconds

**Production implication:**
- Shorter time between wafers → higher charge carryover
- Longer chamber idle time → better charge dissipation
- **Optimal:** 60-90 seconds between wafer unload and load

---

## Summary: Charge Accumulation Effects on CTO Etch

| Effect | Magnitude | Consequence |
|---|---|---|
| **Peak voltage at depth** | 100-150 V (vs. 50 V bias) | 2-3× higher ion energy; oxide breakdown risk |
| **Etch rate boost from ions** | 1.5-2× | Partially offsets ARDE (radical starvation) |
| **Edge-field enhancement** | 1.5-2× local field | Pillar edge selectivity loss; tapering risk |
| **Voltage oscillations** | ±20-30 V amplitude | Etch rate stability issues; endpoint detection challenges |
| **Breakdown risk** | High if oxide defective | Potential device failure; yield loss |
| **Wafer-to-wafer carry-over** | 30-60 sec decay | Chamber conditioning effects; recipe adjustment needed |

**Key Insight:** Charge accumulation is a **double-edged sword**:
- *Benefit:* Partial compensation for ARDE (ion energy helps deep etch)
- *Risk:* Voltage buildup can exceed safe operating range; oxide breakdown possible

Modern production recipes carefully **balance** these effects: allow controlled charge accumulation to help uniformity, but not so much that breakdown risk appears.

---

[Continue to Chapter 11: Thermal Management in High-Aspect-Ratio Etch →](./11-thermal-management-har.md)
