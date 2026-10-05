# Chapter 5: SiO₂ Etch Chemistry & Fluorine-Oxide Reactions

## Executive Summary

Silicon dioxide (SiO₂) etching with fluorine-based plasma is the foundation of CTO etch selectivity. Understanding SiO₂ etch requires detailed knowledge of how fluorine radicals and ions attack the Si-O bonds, how etch products form and desorb, and how various plasma parameters (temperature, pressure, ion energy) modulate the etch rate. This chapter develops the detailed etch chemistry of SiO₂: the reaction mechanisms at the molecular level, the role of ion-assisted etching versus purely radical-driven etching, the etch-rate dependencies on process parameters, and the strategies for optimizing SiO₂ etch selectivity over Si₃N₄. Special attention is paid to the interplay between fluorine radical density (determined by plasma dissociation in Part I) and surface coverage, which together determine the etch rate. Additionally, the chapter addresses how etch rate changes with oxide thickness, oxide composition, and thermal history—all factors that affect CTO etch uniformity in deep features.

---

## Part 1: Detailed Etch Mechanisms for SiO₂

### 1.1 Elementary Reaction Steps

#### Surface Adsorption of Fluorine Radicals

When a fluorine radical (F•) approaches the SiO₂ surface, it can:

**Step 1: Van der Waals interaction (physisorption)**
$$\text{F•} + \text{(SiO}_2)_\text{surface} \rightarrow \text{[F...O-Si]} \text{ (weakly bound)}$$

Binding energy: ~1-5 kJ/mol (weak)

**Step 2: Chemisorption (strong bonding)**
$$\text{F•} + \text{Si-O (surface)} \rightarrow \text{Si-F} + \text{O•}$$

Binding energy: ~300-400 kJ/mol (strong covalent)

**Energy diagram:**

```
      Activation Energy (~20 kJ/mol)
           ╱╲
          ╱  ╲
         ╱    ╲____  Products
        ╱           ╲
────────────────────────────
       Reactants (Van der Waals)
              ↑
       Chemisorbed state
```

#### Silicon-Fluoride Bond Formation

Once F• bonds to Si, the Si-F bond is very stable:

**Si-F bond strength:** ~576 kJ/mol (comparable to Si-O, actually slightly stronger)

**Why does this drive etch?** The key is **entropy**: 
- Reactant: 1 SiO₂ molecule (ordered solid)
- Products: SiF₄ (volatile gas) + O• (radical, mobile)
- **Entropy increase: ΔS > 0** → drives reaction forward

**Thermodynamic driving force:**

$$\Delta G = \Delta H - T\Delta S$$

At reasonable temperatures (25-100°C):
- ΔH (Si-F formation) ≈ 0 (Si-F and Si-O bond strengths similar)
- T·ΔS (entropy from solid → gas) >> 0
- **Result: ΔG < 0** (spontaneous, exothermic)

#### Product Desorption

**Step 3: Si-F product volatilization**

$$\text{Si-F} + \text{F•} \rightarrow \text{SiF}_2$$

$$\text{SiF}_2 + 2\text{F•} \rightarrow \text{SiF}_4 \text{ (volatile)}$$

**SiF₄ properties:**
- Molecular weight: 104 amu
- Boiling point: -86°C
- At room temperature: **Gas** (easily desorbs from surface)
- Vapor pressure at 25°C: >1 atm (strongly favors gaseous state)

**Consequence:** SiF₄ rapidly leaves the wafer surface → enables continuous etch

---

### 1.2 Rate-Limiting Steps

#### Etch Rate Model: Langmuir-Hinshelwood Kinetics

The overall etch rate depends on which step is rate-limiting. A common model:

$$R_\text{etch} = k_1 \theta_\text{F} \times (1 - \theta_\text{SiF})$$

Where:
- k₁ = reaction rate constant (temperature-dependent)
- θ_F = fractional coverage of adsorbed F• atoms
- θ_SiF = fractional coverage of Si-F intermediates
- (1 - θ_SiF) = available SiO₂ surface sites

#### Coverage Dependence on F• Concentration

**Langmuir adsorption isotherm:**

$$\theta_F = \frac{K[\text{F}^\bullet]}{1 + K[\text{F}^\bullet]}$$

Where K = adsorption equilibrium constant, [F•] = fluorine radical density

**At low [F•] (F• scarce):**
$$\theta_F \approx K[\text{F}^\bullet]$$
$$R_\text{etch} \propto [\text{F}^\bullet]^{1.0} \text{ (first-order in F•)}$$

**At high [F•] (F• abundant):**
$$\theta_F \approx 1 \text{ (saturated)}$$
$$R_\text{etch} = k_1 \times (\text{constant}) \text{ (zero-order in F•)}$$

**In typical CTO etch plasma:**
- [F•] ≈ 10¹¹-10¹² cm⁻³
- Usually in **intermediate regime** → etch rate ≈ [F•]^0.5-0.7

#### Temperature Dependence: Arrhenius Behavior

**Rate constant temperature dependence:**

$$k_1 = A e^{-E_a / RT}$$

**Typical activation energy for SiO₂ etch:** E_a ≈ 10-20 kJ/mol (relatively low)

**Temperature scaling example:**
- At 0°C: R_etch = 100 nm/min (baseline)
- At 25°C: R_etch ≈ 180 nm/min (1.8× higher)
- At 50°C: R_etch ≈ 320 nm/min (3.2× higher)

**Consequence:** For every 10°C temperature rise, etch rate increases by ~30-40%

---

## Part 2: Ion-Assisted SiO₂ Etch

### 2.1 Ion Impact and Sputtering

#### Physical Sputtering vs. Chemical Etch

**Pure radical etch (no ions):**
- Purely chemical process
- F• attacks Si-O bonds
- Etch rate: ~50-150 nm/min (moderate)

**Ion-assisted etch (with ions):**
- Ions (e.g., F⁺, Ar⁺, CF₃⁺) impact surface with kinetic energy
- Create defects, break bonds
- F• then attack damaged bonds more easily
- Etch rate: ~150-400 nm/min (2-4× higher)

#### Ion Impact Damage Model

**When an ion with kinetic energy E hits SiO₂:**

1. **Elastic collisions:** Ion transfers momentum to Si or O atoms
2. **Cascade of secondary collisions:** Knock-on atoms create recoil damage
3. **Defect creation:** Si-O bonds break, leaving dangling bonds
4. **Activation energy reduction:** Etch now proceeds on defective sites

**Damage depth:** Collision cascade extends ~5-20 nm below surface

$$\text{Number of defects} \propto E_\text{ion}^{0.5 \text{ to } 1.0}$$

#### Ion Energy Threshold

**Threshold energy for Si-O bond breakage:** ~30-50 eV

**Above threshold:** Additional ion energy → linear increase in etch rate
$$R_\text{ion-assisted} = R_\text{radical} + \alpha (E_\text{ion} - E_\text{threshold})$$

**Below threshold:** Only radical etch occurs (sputtering negligible)

---

### 2.2 Ion Flux and Current Density Effects

#### Current Density in CTO Etch

**Typical ion flux in ICP CTO etch:**

| Plasma Power | Pressure | Ion Flux | Current Density |
|---|---|---|---|
| **100 W** | 20 mTorr | 10¹⁵ cm⁻² s⁻¹ | ~20 mA/cm² |
| **300 W** | 20 mTorr | 3×10¹⁵ cm⁻² s⁻¹ | ~50 mA/cm² |
| **500 W** | 20 mTorr | 5×10¹⁵ cm⁻² s⁻¹ | ~80 mA/cm² |

**Ion-assisted etch enhancement:**

$$\frac{R_\text{ion-assisted}}{R_\text{radical}} = 1 + k_\text{ion} \times J_\text{ion}$$

Where k_ion ≈ 0.1-0.5 (depends on ion species and energy)

**Typical enhancement:** 20-50% faster than radical-only etch

---

## Part 3: SiO₂ Etch Rate Dependencies

### 3.1 Pressure Effects on Etch Rate

#### Pressure Scaling

**Etch rate vs. pressure (25°C, CF₄, 300 W):**

| Pressure (mTorr) | Etch Rate (nm/min) | Relative Rate |
|---|---|---|
| **5** | ~80 | 0.4× |
| **10** | ~140 | 0.7× |
| **20** | ~200 | 1.0× |
| **50** | ~250 | 1.25× |
| **100** | ~290 | 1.45× |

**Mechanism:**

**At low pressure (<10 mTorr):**
- Low neutral radical density (fewer collisions → lower molecular flux to wafer)
- Ion-assisted component becomes significant
- Etch rate limited by F• supply

**At moderate pressure (10-50 mTorr):** 
- Optimal balance of radical density and ion energy (ions don't lose energy to collisions)
- Maximum etch rate

**At high pressure (>100 mTorr):**
- High radical density but ions lose energy (collision losses)
- Ion-assisted component diminishes
- Etch rate plateaus or slightly decreases

**Mathematical model:**

$$R_\text{etch}(P) = \frac{k [F^•]}{1 + \beta P^n}$$

Where n ≈ 0.5-1.0 (ion energy loss to collisions)

---

### 3.2 Oxide Thickness and "First-Layer Effect"

#### Thickness-Dependent Etch Rate

**Surprising observation:** Etch rate of SiO₂ can depend on **how thick the oxide layer is**.

**Typical behavior (CF₄ plasma, 25°C):**

| Oxide Thickness | Etch Rate |
|---|---|
| **Thin oxide (<10 nm)** | ~240 nm/min |
| **Thick oxide (>100 nm)** | ~200 nm/min |
| **Very thick oxide (>1 µm)** | ~180 nm/min |

**Why?** Several mechanisms:

**1. Charge accumulation and energy redistribution:**
- Thick oxide allows charge accumulation
- Electric field across oxide affects ion trajectories
- Result: ions reach thick oxide at lower effective energy

**2. Secondary electron emission:**
- Ion impact produces secondary electrons
- These electrons escape from thin oxide easily
- Thick oxide traps some electrons (self-bias effect)

**3. Heat dissipation:**
- Thick oxide layer insulates substrate
- Wafer temperature rises more
- Etch rate increases with temperature... but this is overwhelmed by charge effects

**Overall effect:** Thick oxide etches slightly slower than thin oxide (5-20% difference)

#### "Native Oxide Effect" in CTO Stacks

In CTO stacks with 100+ repeated SiO₂/Si₃N₄ layers:

- **Top oxide layers** (0-5 µm depth): etch at ~200 nm/min (no charge buildup, low temperature)
- **Mid oxide layers** (5-15 µm depth): etch at ~180 nm/min (charge begins to accumulate)
- **Deep oxide layers** (15-25 µm depth): etch at ~150 nm/min (significant charge and thermal effects)

**Consequence:** Etch uniformity within CTO stack is not uniform; deep layers etch slower.

**Mitigation:** Use pulsed RF power or feedback control to maintain constant etch rate.

---

### 3.3 Oxide Composition Effects

#### Stoichiometric vs. Sub-Stoichiometric Oxide

**Standard SiO₂ (stoichiometric):**
- Composition: SiO₂.₀
- Etch rate (CF₄): ~200 nm/min

**Sub-oxide (reduced):**
- Composition: SiO₁.₅ (intermediate between SiO₂ and Si)
- Etch rate (CF₄): ~250-300 nm/min (25-50% faster)
- Can form during etch if conditions reduce oxide

**Silicon (fully reduced):**
- Composition: SiO₀ (pure silicon)
- Etch rate (CF₄): ~1000-2000 nm/min (100-1000× faster; sputtering dominates)
- Result: Rapid, uncontrolled etch

**Implication for CTO selectivity:** If etch conditions partially reduce SiO₂ to SiO or Si, the etch rate of the oxide layer increases dramatically, **destroying selectivity** relative to Si₃N₄.

**Prevention:** Maintain oxidizing conditions; avoid conditions that would reduce oxide (high ion energy, low oxygen partial pressure).

---

## Part 4: Selectivity Control Strategies

### 4.1 Selectivity Tuning Parameters

#### Fundamental Selectivity Equation

$$S_{\text{SiO}_2/\text{Si}_3\text{N}_4} = \frac{R_{\text{etch, SiO}_2}}{R_{\text{etch, Si}_3\text{N}_4}}$$

To increase selectivity, either:
1. **Increase SiO₂ etch rate**, or
2. **Decrease Si₃N₄ etch rate**

#### Temperature as Selectivity Knob

**Effect of temperature:**

| Temperature | SiO₂ Rate | Si₃N₄ Rate | Selectivity |
|---|---|---|---|
| **-10°C** | 100 nm/min | 20 nm/min | **5.0:1** |
| **+10°C** | 150 nm/min | 30 nm/min | **5.0:1** |
| **+30°C** | 200 nm/min | 40 nm/min | **5.0:1** |
| **+50°C** | 280 nm/min | 60 nm/min | **4.7:1** |

**Observation:** Selectivity is *relatively stable* to temperature changes because both oxides have similar activation energies.

#### Power as Selectivity Tuning

**Higher RF power:**
- More F• production → faster SiO₂ etch
- More ion current → enhanced Si₃N₄ sputtering
- **Result:** Selectivity *decreases* slightly (Si₃N₄ catches up)

**Example (CF₄, 20 mTorr, 25°C):**

| RF Power | SiO₂ Rate | Si₃N₄ Rate | Selectivity |
|---|---|---|---|
| **100 W** | 150 nm/min | 30 nm/min | **5.0:1** |
| **300 W** | 230 nm/min | 55 nm/min | **4.2:1** |
| **500 W** | 300 nm/min | 75 nm/min | **4.0:1** |

---

### 4.2 Oxide-Nitride Selectivity Enhancement

#### Chemical Selectivity Mechanisms

**Why SiO₂ etches faster than Si₃N₄ (even without considering ion effects):**

1. **Si-O bond vs. Si-N bond strengths are similar** (~466 vs. 473 kJ/mol)
   - This alone explains only ~1% difference in etch rate
   - **NOT the main reason for selectivity**

2. **Nitrogen creates surface passivation** (PRIMARY REASON)
   - F• attacks Si-N bonds
   - Nitrogen-containing species (N•, N-F, NF₂) form on surface
   - These species slow further F• attack (passivation effect)
   - SiO₂ has no equivalent passivation

3. **Product desorption rates**
   - SiF₄ (from SiO₂) highly volatile; rapidly leaves
   - Si-N-F compounds (from Si₃N₄) less volatile; stick longer to surface

#### Selectivity Enhancement Strategies

**Strategy 1: Add polymerizing agent (C₄F₈)**

CF₄ + C₄F₈ blend (70% CF₄ + 30% C₄F₈):
- C₄F₈ produces fluorocarbon polymer
- Polymer deposits preferentially on Si₃N₄ (more reactive surface)
- Polymer acts as etch mask for Si₃N₄
- SiO₂ continues to etch (polymer less stable on SiO₂)

**Result:**

| Chemistry | Selectivity |
|---|---|
| CF₄ only | 4-6:1 |
| CF₄ + C₄F₈ blend | 8-12:1 |

**Strategy 2: Lower temperature**

- Lowers both etch rates but Si₃N₄ etch drops more (N passivation more effective at low T)
- Operating at -10°C vs. +30°C: selectivity increases from 4.0 to 5.2:1

**Strategy 3: Controlled ion energy**

- At very low ion energy (<30 eV threshold): sputtering negligible
- Only radical etch proceeds
- SiO₂/Si₃N₄ selectivity determined purely by chemical reactivity
- Typically achieves 5-8:1 selectivity

---

## Summary: SiO₂ Etch Chemistry for CTO

| Parameter | Effect on SiO₂ Etch Rate | Effect on Selectivity |
|---|---|---|
| **Temperature ↑** | Rate ↑ significantly | Selectivity ↓ slightly |
| **Power ↑** | Rate ↑ moderately | Selectivity ↓ moderately |
| **Pressure ↑** | Rate ↑ then plateaus | Selectivity ↑ (ions lose energy) |
| **[F•] ↑** | Rate ↑ (0.5-1.0 order) | Selectivity ↓ (Si₃N₄ attacks increase) |
| **Add C₄F₈** | Rate ↓ (polymer formation) | Selectivity ↑ significantly (10-20:1 possible) |

**Key insight:** SiO₂ etch selectivity over Si₃N₄ is fundamentally a balance between radical-driven etch (favors selectivity) and ion-assisted etch (reduces selectivity). Modern 3D NAND CTO etch uses multi-step recipes that maintain this balance across the full trench depth.

---

[Continue to Chapter 6: Si₃N₄ Selectivity Control →](./06-sin-selectivity-control.md)
