# Chapter 4: Plasma Chemistry for CTO Etch: CF₄, SF₆, and Fluorocarbon Radicals

## Executive Summary

CTO etching relies on fluorine-based plasma chemistry to achieve the required SiO₂ etch rate, Si₃N₄ selectivity, and residue control. The primary etch chemistries for 3D NAND CTO stacks use molecules like CF₄ (carbon tetrafluoride), SF₆ (sulfur hexafluoride), C₄F₈ (octafluorocyclobutane), and CHF₃ (trifluoromethane). Each precursor gas dissociates in the plasma into reactive fragments—primarily fluorine radicals (F•), fluorine atoms, and various ion species. This chapter develops the plasma chemistry of CTO etch from first principles: how precursor gases dissociate in plasma, what reactive species are produced, how those species interact with SiO₂ and Si₃N₄ surfaces, and how fluorocarbon polymerization affects selectivity. Special attention is paid to the balance between radical-driven etch (isotropic, favors selectivity to SiO₂) and ion-driven etch (anisotropic, can damage selectivity). Understanding this chemistry is essential for process development, troubleshooting, and optimizing the narrow process windows required for production 3D NAND.

---

## Part 1: Fluorine Radical Production and Kinetics

### 1.1 Plasma Dissociation Mechanisms

#### Impact Dissociation

When energetic electrons collide with a fluorine-containing molecule (e.g., CF₄), they can ionize or dissociate it:

**Ionization reaction:**

$$e^- + \text{CF}_4 \rightarrow \text{CF}_4^+ + 2e^-$$

**Dissociative reaction:**

$$e^- + \text{CF}_4 \rightarrow \text{CF}_3^• + F^• + e^-$$

**Electron impact ionization cross section:** σ(E) typically peaks at electron energies of 50-200 eV.

**Threshold energy** for various CF₄ dissociation pathways:

| Dissociation Pathway | Threshold Energy |
|---|---|
| CF₄ → CF₃⁺ + F• + e⁻ | ~10 eV |
| CF₄ → CF₂⁺ + 2F• + e⁻ | ~15 eV |
| CF₄ → CF⁺ + 3F• + e⁻ | ~20 eV |
| CF₄ → C⁺ + 4F• + e⁻ | ~30 eV |

**In typical CTO etch plasma:**
- Electron temperature: T_e ≈ 2-4 eV (20,000-40,000 K)
- Mean electron energy: ≈ 3-5 × k_B × T_e ≈ 9-20 eV
- **Result:** Mix of dissociation products; primarily CF₃, CF₂, and F• are produced

#### Attachment Dissociation (Low-Energy Mechanism)

At lower electron energies, dissociative attachment can occur:

$$e^- + \text{CF}_4 \rightarrow \text{CF}_3^- + F^•$$

**Threshold energy:** ~0 eV (can occur at room temperature)
**Cross section:** Significant at energies 0-5 eV

**Implication:** Even "slow" electrons (cooler plasma regions) can contribute to F• production via attachment.

---

### 1.2 CF₄ Plasma Chemistry

#### CF₄ Precursor Gas

**CF₄ (Carbon Tetrafluoride):**
- Molecular weight: 88 amu
- Boiling point: -78°C (sublimes as solid at room temperature)
- Delivery method: Pressurized gas bottle or heated liquid container
- Typical flow: 50-200 sccm (cubic centimeters per minute at standard conditions)

#### CF₄ Dissociation Products

In a typical ICP plasma (100-500 W RF power, 20-50 mTorr pressure), CF₄ dissociates into:

| Species | Fraction | Role |
|---|---|---|
| **F• (fluorine radical)** | 30-50% | **Primary etch agent** |
| **CF₃• (trifluoromethyl radical)** | 20-30% | Etch assist; **polymerization source** |
| **CF₂• (difluoromethylene radical)** | 10-20% | Polymerization; passivation |
| **CF• (fluoromethyl radical)** | 5-10% | Minor; polymerization |
| **C• (carbon radical)** | <5% | Minority; carbonization |
| **Ions: F⁻, CF₃⁻, CF⁻, C⁻, F⁺, CF₄⁺, CF₃⁺** | ~1-5% | Ion-assisted etch; sputtering |

**Production rate:** 
$$\text{F radical production rate} \propto P_\text{RF} \times [CF_4]$$

Typical F• density in CTO etch plasma: ~10¹¹-10¹² cm⁻³

#### Fluorine Radical Lifetimes

**In the bulk plasma:**
- Lifetime: τ ~ 10-100 ms
- Consumed by collisions with other radicals, ions
- Recombination: F• + F• → F₂ (slow, requires three-body collision)

**At the wafer surface:**
- Upon contact, F• consumed instantly (reacts with Si, SiO₂, Si₃N₄)
- Reaction time: <1 nanosecond

**Mean free path in typical CTO etch plasma (30 mTorr):**
$$\lambda = \frac{k_B T}{\sqrt{2} \pi d^2 P} \approx \frac{10 \text{ mm}}{\text{cm}} \approx 1 \text{ mm}$$

**Consequence:** F• radicals diffuse ~1 mm between collisions, enabling access to features even at depths where ions cannot easily reach (ions scattered by charge accumulation).

---

### 1.3 SF₆ Plasma Chemistry

#### SF₆ Precursor

**SF₆ (Sulfur Hexafluoride):**
- Molecular weight: 146 amu
- Boiling point: -64°C
- Gas at room temperature
- Typical flow: 50-150 sccm
- **Advantage over CF₄:** Easier to dissociate (weaker S-F bonds)

#### SF₆ Dissociation

**Initial dissociation:**

$$e^- + \text{SF}_6 \rightarrow \text{SF}_5^• + F^• + e^-$$

**Further dissociation:**

$$e^- + \text{SF}_5^• \rightarrow \text{SF}_4^• + F^• + e^-$$

**Etch products in plasma:**

| Species | Fraction | Notes |
|---|---|---|
| **F• (fluorine)** | 40-60% | Primary etch agent (higher yield than CF₄) |
| **SF₅• (pentafluoride radical)** | 15-25% | Less reactive with Si/SiO₂; partial polymerization |
| **SF₄• (tetrafluoride radical)** | 10-15% | Polymerization source |
| **SO, SOF₂, etc.** | 10-20% | Sulfur-oxygen species; less etch-active |
| **Sulfur deposits** | <5% | Can accumulate on chamber walls |

**Etch rates with SF₆:**
- SiO₂: 100-200 nm/min (lower than CF₄)
- Si₃N₄: 30-50 nm/min (similar to CF₄)
- **Selectivity:** SiO₂/Si₃N₄ ≈ 3-5:1 (slightly lower than CF₄ due to SO species participation)

**Disadvantage:** Sulfur byproducts can deposit on chamber walls, requiring periodic cleaning.

---

### 1.4 C₄F₈ (Octafluorocyclobutane)

#### C₄F₈ Properties and Dissociation

**C₄F₈:**
- Molecular weight: 200 amu
- Liquid at room temperature; delivered as vapor from heated container
- Boiling point: -6°C
- Typical flow: 20-80 sccm (lower flow rates than CF₄ due to higher molecular weight)

**Molecular structure:**

```
    F F
    | |
F—C—C—F
| | | |
F C—C F
  | |
  F F
```

#### Dissociation and Polymerization

C₄F₈ is **highly polymerizing** because:
1. Larger carbon backbone (C₄ vs. C₁)
2. Produces longer-chain fluorocarbon radicals (C₄F₇•, C₃F₅•, etc.)
3. Radicals easily combine to form polymers

**Dissociation:**

$$e^- + \text{C}_4\text{F}_8 \rightarrow \text{C}_3\text{F}_6^• + \text{CF}_2^• + e^-$$

**Resulting plasma species:**

| Species | Effect |
|---|---|
| **F• and CF₂•** | Etch agents |
| **C₄F₇•, C₃F₅•, C₂F₃•** | Polymerization precursors |
| **Polymer (CF_x)_n** | Passivation layer on Si₃N₄ |

#### Selectivity Advantage with C₄F₈

**Polymerization effect:**

- C₄F₈ produces **more polymer** than CF₄
- Polymer preferentially deposits on **Si₃N₄** (more reactive surface)
- Polymer acts as "etch mask" for Si₃N₄
- SiO₂ continues to etch (polymer less stable on SiO₂)

**Result:**

| Chemistry | SiO₂/Si₃N₄ Selectivity |
|---|---|
| **CF₄** | 4-6:1 |
| **SF₆** | 3-5:1 |
| **C₄F₈** | 10-20:1 or higher |

**Trade-off:** Higher selectivity comes at cost of:
- Lower absolute SiO₂ etch rate (polymer formation consumes some precursor)
- Polymer residue on wafer (requires post-etch cleaning)
- Process complexity (managing polymer deposition)

---

## Part 2: SiO₂ and Si₃N₄ Etch Mechanisms

### 2.1 SiO₂ Etch with F• Radicals

#### Surface Reaction Mechanism

**Step 1: Fluorine radical approach and adsorption**

$$\text{F•} + \text{Si-O-Si} \text{(surface)} \rightarrow \text{F-Si•} + \text{O-Si} \text{(activated)}$$

**Step 2: Si-O bond breaking**

$$\text{F-Si•} + \text{F•} \rightarrow \text{F-Si-F} + \text{intermediate}$$

**Step 3: Product formation and desorption**

$$\text{F-Si-F} \rightarrow \text{SiF}_2 \text{ or } \text{SiF}_4 \text{ (volatile, desorbs)}$$

**Energy requirement:**
- Si-O bond breaking: ~466 kJ/mol
- Fluorine radical thermodynamic driving force: Si-F formation much more stable than Si-O
- Net reaction is **thermodynamically favorable** but kinetically limited by activation energy

#### Temperature Dependence

**Arrhenius form:**

$$R_\text{etch} = R_0 e^{-E_a / k_B T}$$

**Typical activation energy:** E_a ≈ 10-20 kJ/mol (relatively low)

**Temperature scaling:**
- At -10°C (263 K): ~100 nm/min (baseline)
- At +25°C (298 K): ~200 nm/min (2× higher)
- At +50°C (323 K): ~350 nm/min (3-4× higher)

**Consequence:** Small temperature changes create large etch rate variations. CTO etch requires tight thermal control (±5°C target).

#### Ion-Assisted Etch of SiO₂

In CCP or ICP plasmas with moderate ion energy (50-500 eV), ions contribute to SiO₂ etch:

**Ion-assisted mechanism:**

1. Ion impact creates Si-O bond damage and defects
2. Fluorine radicals more easily attack damaged bonds
3. Result: Higher etch rate than radical-only etch

**Etch rate enhancement from ions:**

$$R_\text{etch, ion-assisted} = R_\text{radical} + k_\text{ion} \times \text{Ion Flux}$$

Typical enhancement: 20-50% faster than radical-only etch.

---

### 2.2 Si₃N₄ Etch Selectivity

#### Lower Etch Rate of Si₃N₄

Si₃N₄ etches slower than SiO₂ with F• radicals because:

1. **Stronger Si-N bond** (473 kJ/mol vs. 466 kJ/mol for Si-O)
   - Marginally stronger; this alone only explains ~5% rate difference
   - **Not the main reason**

2. **Nitrogen passivation effect** (primary reason)
   - When F• attacks Si-N bonds, nitrogen species form at surface
   - Nitrogen-based radicals (N•, NH•) create a protective layer
   - This layer slows further F• attack
   - Effect: 5-10× reduction in etch rate compared to radical-only on SiO₂

3. **Product volatility**
   - SiO₂ produces SiF₄ (very volatile)
   - Si₃N₄ produces Si-N-F compounds with lower volatility
   - Slower desorption → lower apparent etch rate

#### Selectivity Mechanistic Understanding

**SiO₂ surface reaction:**

$$\text{SiO}_2 + 4\text{F•} \rightarrow \text{SiF}_4 + 2\text{O•} \text{ (fast)}$$

**Si₃N₄ surface reaction (competitive):**

$$\text{Si}_3\text{N}_4 + F• \rightarrow \text{Si}_3\text{N}_3 \text{F} + \text{N•} \text{ (slow)}$$

$$\text{N•} + \text{F•} \rightarrow \text{NF} \text{ or } \text{NF}_2 \text{ (passivation layer)}$$

**Net effect:** Passivation layer protects Si₃N₄ surface.

---

### 2.3 Polymer Passivation in C₄F₈ Etch

#### Fluorocarbon Polymer Formation

In C₄F₈-based plasmas, polymeric (CF_x)_n forms via:

**Initiation:**
$$\text{C}_4\text{F}_8 + e^- \rightarrow \text{C}_3\text{F}_6 + \text{CF}_2^•$$

**Propagation (polymer growth):**
$$\text{CF}_2^• + \text{CF}_2^• \rightarrow \text{(CF}_2)_2 \text{ (dimer)}$$

$$\text{(CF}_2)_n + \text{CF}_3^• \rightarrow \text{(CF}_2)_{n+1}\text{CF}_3 \text{ (growing chain)}$$

**Termination:**
$$\text{Polymer chain (long)} \rightarrow \text{(CF}_x)_n \text{ deposit on surface}$$

#### Polymer Deposition on Surfaces

**Deposition rate depends on surface chemistry:**

| Surface | Polymer Deposition Rate | Reason |
|---|---|---|
| **Si₃N₄** | ~50-100 nm/min | N-reactive surface attracts C_xF_y radicals; high sticking coefficient |
| **SiO₂** | ~10-30 nm/min | Less reactive; lower sticking coefficient |
| **Aluminum (electrode)** | ~100-200 nm/min | Metal surface very reactive; high sticking coefficient |
| **Polysilicon** | ~50-80 nm/min | Intermediate reactivity |

**Selectivity consequence:**
- Polymer preferentially on Si₃N₄ → acts as mask
- SiO₂ continues to etch (polymer less protective)
- **Net selectivity = ratio of bare etch rates minus polymer protection effect**

#### Polymer Thickness During Etch

**As etch proceeds (depth increases):**

1. **Early etch (top layers, 0-5 µm depth):** Polymer ~10-50 nm thick; re-etched by ions
2. **Mid-etch (5-15 µm depth):** Polymer ~50-100 nm thick; significant protection
3. **Late etch (15-25 µm depth):** Polymer can exceed 100 nm; selectivity high but polymer residue risk

**Polymer dynamics:**

$$\frac{d t_p}{dt} = D_p - E_p$$

Where:
- t_p = polymer thickness
- D_p = deposition rate
- E_p = polymer etch rate (by ions)

**Balance:** At steady state, D_p ≈ E_p; polymer thickness remains ~50-100 nm.

---

## Part 3: Etch Chemistry Design for CTO Applications

### 3.1 Process Gas Mixtures

#### Single-Gas vs. Multi-Gas Recipes

**Single-gas approaches:**
- **CF₄ alone:** Good balance of etch rate and selectivity; standard choice
- **SF₆ alone:** Similar to CF₄; slightly lower etch rate
- **C₄F₈ alone:** High selectivity; low etch rate; high polymer residue risk

**Multi-gas approaches (modern 3D NAND):**

| Gas Mixture | Effect |
|---|---|
| **CF₄ + C₄F₈** | Blended selectivity (6-10:1) without extreme polymer buildup |
| **CF₄ + CH₄ or CH₂F₂** | Controlled polymerization; improved selectivity for deep etch |
| **CF₄ + O₂** | Oxygen enhances F• production; can reduce etch rate variability |
| **CF₄ + H₂** | Reduces polymer; enhances ion-assisted etch |

**Typical production recipe:**
- **CF₄:** 60-80% of fluorine-bearing gas
- **C₄F₈:** 10-20% of fluorine-bearing gas
- **Diluent (N₂ or Ar):** 20-50% of total gas

---

### 3.2 Etch Window Optimization

#### Critical Parameters for CTO Etch Selectivity

**Selectivity vs. Etch Rate Trade-off:**

| Goal | Parameter Adjustment | Effect |
|---|---|---|
| **Increase selectivity** | Reduce temperature, add polymerizing gas (C₄F₈), reduce RF power | Selectivity ↑, etch rate ↓ |
| **Increase etch rate** | Raise temperature, increase RF power, reduce polymeric gas | Etch rate ↑, selectivity ↓ |
| **Balance** | Multi-step etch: high selectivity for top layers, higher etch rate for deep layers | Selectivity ✓, etch rate ✓ |

#### Multi-Step Etch Sequences

Advanced 3D NAND CTO etch uses **multi-step sequences**:

**Step 1: High-selectivity etch (SiO₂/Si₃N₄ = 10:1 or higher)**
- Purpose: Remove top SiO₂ layers without damaging Si₃N₄
- Conditions: Lower temperature (-5°C), higher C₄F₈ fraction, lower power
- Duration: First 3-5 minutes until Si₃N₄ exposed

**Step 2: Moderate-selectivity etch (SiO₂/Si₃N₄ = 4-6:1)**
- Purpose: Remove deeper SiO₂ with reasonable etch rate
- Conditions: Room temperature, standard CF₄/C₄F₈ mix, moderate power
- Duration: 5-15 minutes (bulk of etch)

**Step 3: High-rate etch (SiO₂/Si₃N₄ = 3:1)**
- Purpose: Rapid etch of final layers before stopping
- Conditions: Higher temperature (+20°C), higher CF₄ fraction, higher power
- Duration: Final 1-2 minutes; short duration limits selectivity loss

**Benefit:** Overall process achieves both high selectivity (top layers protected) and acceptable etch rate (completion in <20 minutes).

---

## Summary: Plasma Chemistry for CTO Etch

| Chemistry | Advantages | Disadvantages | When Used |
|---|---|---|---|
| **CF₄** | Balanced; good etch rate; moderate selectivity | Moderate selectivity (4-6:1); not ideal for deep etch | Standard choice; widely used |
| **SF₆** | High F• yield; lower polymer | Sulfur deposits; slightly lower selectivity | Alternative; less common |
| **C₄F₈** | Excellent selectivity (10-20:1); good polymer control | Lower etch rate; complex process control | Advanced 3D NAND; used in blends |
| **Blended (CF₄+C₄F₈)** | Optimized selectivity & rate | Requires multi-step recipe; equipment complexity | Modern production 3D NAND |

**Key Takeaway:** CTO etch chemistry is fundamentally a balance between:
1. **Etch rate** (F• production, temperature)
2. **Selectivity** (polymer passivation, nitrogen protection)
3. **Uniformity** (consistency across wafer and over time)
4. **Residue control** (polymer accumulation, post-etch cleaning)

Mastering this balance is central to 3D NAND manufacturing success.

---

[Continue to Chapter 5: SiO₂ Etch Chemistry & Selectivity →](./05-sio2-etch-selectivity.md)
