# Chapter 3: Silicon Nitride Properties & Deposition/Oxidation Mechanisms

## Executive Summary

Silicon nitride (Si₃N₄) is the cornerstone of charge-trap flash memory. Unlike SiO₂ (which confines tunneling oxides), Si₃N₄ is the **active charge-storage medium**—electrons are trapped within its band gap states, where they persist for years. Understanding Si₃N₄ requires understanding its crystal structure, its electrical properties (band gap, trap states), its thermal stability, its deposition methods (PECVD, LPCVD, ALD), and its oxidation behavior. This chapter establishes the material science of Si₃N₄ from first principles, then develops the implications for CTO etch selectivity, trap density optimization, and residue prevention. Special attention is paid to **trap states** (where charge is stored), **oxidation of Si₃N₄** (which can occur during post-etch cleaning), and the balance between trap density (device needs high density for tight Vth distribution) and defect density (which causes charge loss).

---

## Part 1: Silicon Nitride Fundamentals

### 1.1 Crystal Structure and Stoichiometry

#### Si₃N₄: Crystal Phases

Silicon nitride exists in two primary crystal phases:

**α-Si₃N₄ (Alpha phase, hexagonal)**
- Most common at moderate temperatures (<1200°C)
- Trigonal crystal structure
- Stability: Room temperature to ~1200°C
- Density: 3.22 g/cm³

**β-Si₃N₄ (Beta phase, cubic)**
- Stable at high temperatures (>1200°C)
- More thermodynamically stable at elevated T
- Slightly higher density: 3.27 g/cm³

**In semiconductor processing:** Both phases are used:
- **PECVD/LPCVD (low-T deposition):** Amorphous or α-phase
- **Thermal oxidation of Si₃N₄ layers:** Can partially convert α → β if heated

#### Si₃N₄ in Amorphous Form (CTO Etch Context)

For CTO stacks, Si₃N₄ is deposited as **amorphous films** via:
- PECVD (Plasma-Enhanced Chemical Vapor Deposition): 300-500°C
- LPCVD (Low-Pressure Chemical Vapor Deposition): 700-900°C
- ALD (Atomic Layer Deposition): 200-400°C

Amorphous Si₃N₄ has:
- **Random bonding network** (not crystalline lattice)
- **Composition range:** Si₃N₄ to Si₂N₂O (substoichiometric to oxynitride)
- **Band gap:** 5.0-5.5 eV (similar to crystalline, but defects can reduce effective gap)

#### Si-N Bonding

**Molecular structure:**

```
        N
       / \
      Si  Si
     / \
    N   N
     \
      Si
```

**Bond characteristics:**

| Property | Si-N Bond | Si-O Bond |
|----------|-----------|----------|
| **Bond length** | 1.74 Å | 1.62 Å |
| **Bond energy** | 473 kJ/mol | 466 kJ/mol |
| **Coordination** | Si bonded to 3-4 N; N bonded to 3 Si | Si bonded to 4 O; O bonded to 2 Si |
| **Polarity** | Moderate (2.5 Pauling) | Lower (2.7 Pauling) |

**Key insight:** Si-N bond is slightly *longer* but *stronger* than Si-O. This makes Si₃N₄:
- Harder to etch (requires more energetic plasma)
- Thermally more stable
- More resistant to oxidation

---

### 1.2 Trap States and Charge Storage

#### Defect States in Si₃N₄ Band Gap

The charge-trap mechanism works because Si₃N₄ has **trap states** within its band gap:

**Band gap of Si₃N₄:** E_g ≈ 5.0-5.5 eV

**Trap states within band gap:**

```
Conduction Band ────────────────────────────── +5.5 eV
                  
Trap States:
    • Si dangling bonds (E_c - 2.0 eV) ← high-lying traps
    • Nitrogen vacancies (E_c - 3.0 eV)
    • Bonding defects (E_c - 4.0 eV) ← deep traps
    
Valence Band ────────────────────────────────── 0 eV
```

#### Trap State Density and Type

**Trap density in high-quality Si₃N₄:** 10¹²-10¹³ cm⁻³
- Typical for production nitride
- Varies with deposition method (PECVD higher than LPCVD or ALD)

**Trap state types:**

| Trap Type | Energy | Capture Cross Section | Trap Density | Function |
|---|---|---|---|---|
| **Interface traps** | E_c - 1.0 to 2.0 eV | 10⁻¹⁴ cm² | 10¹⁰-10¹¹ cm⁻² | At Si-SiO₂ or SiO₂-Si₃N₄ interfaces |
| **Nitrogen vacancy (V_N)** | E_c - 2.5 eV | 10⁻¹⁶ cm² | 10¹²-10¹³ cm⁻³ | **Primary charge trap** |
| **Oxygen-related (if oxynitride)** | E_c - 3.0 eV | 10⁻¹⁶ cm² | 10¹¹-10¹² cm⁻³ | Secondary trap (parasitic) |
| **Si dangling bond (≡Si•)** | E_c - 2.0 eV | 10⁻¹⁵ cm² | 10¹⁰ cm⁻³ | Surface states; mobile |

#### Charge Storage and Retention

**Electron capture into traps:**

$$\text{e}^- + \text{Trap} \rightarrow \text{Trap}^- \text{(filled)}$$

**Retention timescale:** At room temperature, trap-bound electrons have hold time:

$$\tau = \tau_0 e^{E_t / k_B T}$$

Where E_t = trap depth below conduction band (typically 2-4 eV for deep traps).

**Numerical example:**
- Deep trap: E_t = 3.0 eV
- Room temperature: T = 300 K, k_B·T = 26 meV
- τ = τ₀ · exp(3.0 eV / 0.026 eV) = τ₀ · exp(115) ≈ τ₀ · 10⁵⁰

Even with small prefactor (τ₀ ~ 10⁻¹³ s), total retention time >> 10 years.

**Result:** Electrons trapped in deep Si₃N₄ traps are stable for years at room temperature.

---

## Part 2: Si₃N₄ Deposition Methods

### 2.1 PECVD Si₃N₄

**Precursors:**
- SiH₄ (silane)
- NH₃ (ammonia)
- H₂ (hydrogen; dilute, reduce deposition rate and defects)

**Reaction (simplified):**

$$\text{SiH}_4 + 4\text{NH}_3 + \text{plasma} \rightarrow \text{Si}_3\text{N}_4 + 12\text{H}_2$$

**PECVD conditions:**

| Parameter | Typical Value | Effect |
|---|---|---|
| **Temperature** | 300-500°C | Higher T → higher quality, but substrate damage risk |
| **Pressure** | 500-2000 Pa | Higher P → conformal, slower; Lower P → faster, less conformal |
| **RF Power** | 50-500 W | Higher power → faster deposition, more defects |
| **SiH₄/NH₃ ratio** | 1:5 to 1:20 | Higher NH₃ → higher N content (less Si-rich) |
| **Deposition rate** | 50-300 nm/min | Depends on power and pressure |

**Resulting Si₃N₄ properties:**

| Property | PECVD Value |
|---|---|
| **Stoichiometry** | Si₃N₃.₅ to Si₃N₄ (slightly N-rich) |
| **Density** | 2.8-3.0 g/cm³ (lower than crystalline, due to amorphous structure) |
| **Etch rate (in CF₄)** | 50-100 nm/min (lower than SiO₂) |
| **Trap density** | 10¹²-10¹³ cm⁻³ (suitable for memory) |
| **Defect density** | 10¹⁰-10¹² cm⁻³ (acceptable) |
| **Thermal stress** | Tensile (100-400 MPa) |

**Advantages:**
- Fast deposition
- Conformal coverage (good step coverage)
- Cost-effective

**Disadvantages:**
- More defects than LPCVD/ALD
- Higher hydrogen content (can outgas later)
- Stress management required

---

### 2.2 LPCVD Si₃N₄

**Precursors:**
- SiCl₄ or SiH₄
- NH₃
- (H₂ sometimes, to improve quality)

**Reaction (simplified):**

$$3\text{SiH}_4 + 4\text{NH}_3 \rightarrow \text{Si}_3\text{N}_4 + 12\text{H}_2$$

**LPCVD conditions:**

| Parameter | Typical Value |
|---|---|
| **Temperature** | 700-900°C |
| **Pressure** | 100-500 Pa (ultra-low pressure) |
| **Deposition rate** | 10-50 nm/min (slow) |

**Properties:**

| Property | LPCVD Value |
|---|---|
| **Stoichiometry** | Si₃N₄ (stoichiometric) |
| **Density** | 3.1-3.2 g/cm³ (closer to bulk) |
| **Trap density** | 10¹²-10¹³ cm⁻³ (similar to PECVD) |
| **Defect density** | 10⁹-10¹⁰ cm⁻³ (lower than PECVD) |
| **Stress** | Compressive (200-500 MPa) |

**Advantages:**
- Higher quality (fewer defects)
- Stoichiometric
- Uniform deposition (slow = better control)

**Disadvantages:**
- Much slower (PECVD ~10× faster)
- Higher temperature (substrate compatibility issues)
- Higher equipment cost

---

### 2.3 ALD Si₃N₄ (Emerging Technology)

**Precursors:** Multiple options:
- Si(NH)₂ precursor + N₂H₄ (uncommon, slow)
- SiCl₄ + NH₃ (reactive precursor approach)
- Newer Si-N precursor molecules (Lam, Applied Materials)

**ALD characteristics:**
- **Temperature:** 200-400°C
- **Deposition rate:** 0.1-0.5 nm/cycle (very slow, but precise)
- **Saturation:** Excellent self-limiting reaction
- **Conformality:** Outstanding (fills high-AR features easily)

**Properties:**

| Property | ALD Si₃N₄ |
|---|---|
| **Stoichiometry** | Si₃N₄ to Si₂N₂O (excellent control) |
| **Density** | 3.0-3.2 g/cm³ |
| **Defect density** | 10⁸-10⁹ cm⁻³ (lowest of all methods) |
| **Stress** | Minimal (can be tuned) |

**Disadvantages:**
- **Extremely slow** (hours to deposit µm-thick films)
- **Only practical for thin layers** (<50 nm in production)
- High equipment cost

**CTO stack use:** ALD increasingly used for **blocking oxide** and **tunneling oxide** in advanced 3D NAND (better uniformity, lower defects). Si₃N₄ charge-trap layer often remains PECVD or LPCVD due to speed requirements.

---

## Part 3: Oxidation of Si₃N₄

### 3.1 Thermal Oxidation of Nitride

#### Dry Oxidation in O₂

Si₃N₄ can be oxidized at high temperature (~900-1100°C) in oxygen atmosphere:

$$\text{Si}_3\text{N}_4 + 3\text{O}_2 \rightarrow 3\text{SiO}_2 + 2\text{N}_2$$

**Kinetics (Deal-Grove model adapted):**

Like SiO₂ growth on silicon, oxidation of Si₃N₄ is **diffusion-limited**:

$$\frac{d x}{dt} = \frac{D(C_s - C_0)}{x}$$

**Key difference from Si oxidation:** Si₃N₄ oxidation is **much slower** than Si oxidation:

| Substrate | 900°C, 1 hour, dry O₂ |
|---|---|
| Silicon (Si) | ~15 nm SiO₂ formed |
| Si₃N₄ | ~1-2 nm SiO₂ formed |

**Why slower?** Si-N bond is stronger than Si-Si bond; harder for oxygen to penetrate and break bonds.

**Activation energy for Si₃N₄ oxidation:** E_a ≈ 2.5-3.0 eV (vs. 2.0-2.5 eV for Si)

#### Wet Oxidation in Steam

Wet oxidation (steam) dramatically accelerates Si₃N₄ oxidation:

| Condition | Rate of SiO₂ growth |
|---|---|
| Dry oxidation (O₂) @ 900°C | ~1-2 nm / hour |
| Wet oxidation (H₂O) @ 900°C | ~20-50 nm / hour |
| **Speed advantage:** | **10-50×** |

**Mechanism:** Water (H₂O) reacts with Si₃N₄ more readily than O₂:

$$\text{Si}_3\text{N}_4 + 6\text{H}_2\text{O} \rightarrow 3\text{SiO}_2 + 4\text{NH}_3$$

---

### 3.2 Oxidation During CTO Etch Post-Etch Cleaning

#### Critical Concern: Re-oxidation of Si₃N₄ Surface

**Problem scenario:**

1. CTO etch removes SiO₂ layers selectively, **exposing Si₃N₄ charge-trap layer**
2. Post-etch residue removal uses **oxidizing plasma** (O₂ plasma, or oxidizing fluorocarbon plasma) to burn off carbon-based residues
3. Si₃N₄ surface re-oxidizes: $\text{Si}_3\text{N}_4 + \text{O (from plasma)} \rightarrow \text{SiO}_2 + \text{N}_2$
4. **Result:** A new oxide layer forms on top of charge-trap nitride, preventing subsequent etch steps or device function

#### Oxidation Rate in Plasma

In oxidizing plasmas (O₂ plasma, remote plasma):

**At room temperature:**
- Negligible oxidation (O radicals are weak oxidant at low T)

**At 100-200°C:**
- Significant oxidation (1-5 nm/min possible)

**At 300°C+:**
- Rapid oxidation (10+ nm/min; can form ~nm-thick oxide layer in seconds)

#### Prevention Strategies

1. **Avoid oxidizing conditions post-etch**
   - Use reducing plasmas (H₂, CHF₃ in reduction mode)
   - Or use purge steps instead of active plasma cleaning
   
2. **Minimize exposure time**
   - Shorter in-situ cleaning duration
   - Avoid air exposure between etch and clean
   
3. **Careful temperature management**
   - Keep wafer temperature <100°C during any post-etch oxidizing steps
   - Prevents fast oxidation kinetics
   
4. **Alternative: Selective re-oxidation**
   - Some processes intentionally create thin (~2-3 nm) oxide layer on Si₃N₄
   - This "protective oxide" prevents charge loss and improves device reliability
   - Subsequent etch steps remove this protective oxide if needed

---

## Part 4: Si₃N₄ in CTO Etch Context

### 4.1 Selectivity SiO₂/Si₃N₄ and Its Control

#### Baseline Selectivity in Fluorine Plasma

In standard CF₄ or SF₆ plasma at 25°C:

| Chemistry | SiO₂ etch rate | Si₃N₄ etch rate | Selectivity SiO₂/Si₃N₄ |
|---|---|---|---|
| **CF₄** | ~250 nm/min | ~40-60 nm/min | **4-6:1** |
| **SF₆** | ~150 nm/min | ~30-50 nm/min | **3-5:1** |
| **C₄F₈** | ~100 nm/min | ~10-20 nm/min | **5-10:1** |

**Selectivity mechanism:**

- SiO₂ etches fast because:
  1. Si-O bond is relatively weak (smaller barrier to F• attack)
  2. Product (SiF₄, volatile) easily desorbs
  3. Oxide surface less "protected" by polymerization

- Si₃N₄ etches slower because:
  1. Si-N bond is stronger (harder to break)
  2. Nitrogen creates a "passivation effect" (N-based radicals or polymers form protective layer)
  3. Reaction cross section with F radicals lower

#### Selectivity Control Knobs

**To enhance SiO₂/Si₃N₄ selectivity (make it higher):**

1. **Reduce temperature** (-20 to +10°C): Slows Si₃N₄ etch more than SiO₂ → selectivity increases
2. **Increase pressure** (50-100 mTorr): More collisions → F• lifetime decreases → Si₃N₄ protected more
3. **Add polymerizing agent** (C₄F₈, CHF₃): Forms polymer passivation on Si₃N₄ preferentially → increases selectivity to 10-20:1
4. **Reduce RF power:** Lower plasma density → fewer F• → selectivity improves slightly

**To reduce selectivity (make SiO₂/Si₃N₄ ratio lower):**

1. **Increase temperature** (+30 to +50°C): Thermal activation favors Si₃N₄ etch → selectivity decreases
2. **Reduce pressure** (5-20 mTorr): F• mean free path increases → higher F• flux to Si₃N₄ → selectivity decreases
3. **Increase RF power:** More F• available for Si₃N₄ attack → selectivity decreases slightly

#### Selectivity Drift During CTO Etch

**Critical observation:** Selectivity can **shift significantly** during a single ~20-minute CTO etch process:

**Mechanism:**

1. **Initial etch (top layers, 0-5 min):** High selectivity (SiO₂/Si₃N₄ = 4:1 typical)
2. **Mid-etch (5-15 min):** Selectivity degrades slightly as:
   - Chamber walls accumulate fluorocarbon polymer
   - Temperature rises (heat accumulation)
   - Ion impact on Si₃N₄ layers increases (as they become more exposed)
3. **Final etch (15-20 min):** Selectivity can drop to 2-3:1 or lower

**Consequence:** Bottom CTO layers (deep in trench) experience lower selectivity than top layers. Risk of **over-etching Si₃N₄** at depth.

**Mitigation:** Real-time optical monitoring; feedback-controlled power/pressure adjustments to maintain constant etch rate and selectivity.

---

### 4.2 Trap Density Optimization in CTO

#### Device Requirements for Trap Density

3D NAND charge-trap device performance depends on trap density:

**Too low trap density:**
- Threshold voltage (V_th) distribution broadens (large standard deviation)
- Reduced program/erase speed (fewer traps to capture/release)
- Higher bit error rate (trap resolution poor)

**Optimal trap density:** 10¹²-10¹³ cm⁻³
- Tight V_th distribution
- Adequate program/erase speed
- Low bit error rate

**Too high trap density:**
- Lateral spread of charge to neighboring cells (cross-talk)
- Increased parasitic capacitance
- Difficult to achieve by deposition (would require non-standard Si₃N₄ or ion implantation)

#### Trap Density Tuning During Deposition

**PECVD parameters that affect trap density:**

| Parameter Change | Effect on Trap Density |
|---|---|
| Increase temperature | Slightly decreases (fewer point defects) |
| Decrease SiH₄/NH₃ ratio | Increases (more nitrogen vacancy formation) |
| Increase RF power | Increases (more plasma-induced defects) |
| Add Ar dilution | Affects slightly (depends on exact conditions) |

**After deposition, trap density is relatively fixed**. Limited options to modify it post-deposition without damaging device.

---

## Summary: Si₃N₄ as Charge-Storage Medium for CTO

| Aspect | Impact on CTO Etch |
|---|---|
| **Trap states (N vacancies)** | Are the active charge-storage element; must be preserved during etch |
| **Strong Si-N bonding** | Makes Si₃N₄ harder to etch than SiO₂; selective etch possible |
| **Oxidation during cleaning** | Critical risk; must prevent or control re-oxidation post-etch |
| **Trap density optimization** | Device performance depends on trap density; etch selectivity must protect it |
| **Deposition method (PECVD, LPCVD, ALD)** | Determines defect density, stoichiometry, and how nitride responds to etch/clean |

Silicon nitride is not merely a dielectric in CTO—it is the **functional device element**. Preserving its integrity during etch and post-etch processing is critical to device success.

---

[Continue to Chapter 4: Plasma Chemistry for CTO Etch →](./04-cto-etch-chemistry.md)
