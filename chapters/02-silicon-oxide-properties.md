# Chapter 2: Silicon Oxide Properties & Thermal Oxidation Kinetics

## Executive Summary

Silicon dioxide (SiO₂) is the most abundant material in semiconductor etching. It is the primary insulator in gate oxides, interlayer dielectrics, and the charge-trap-oxide (CTO) stack. Understanding SiO₂ etch behavior requires first understanding SiO₂ itself: its structure, its thermal properties, its oxidation kinetics, and its relationship to the silicon substrate. This chapter establishes the material science foundation for SiO₂ in CTO etch contexts. Special attention is paid to native oxide formation, the Deal-Grove oxidation model (which predicts how SiO₂ grows on silicon and how oxide thickness varies), the structure of thermally-grown oxides versus deposited oxides, and the role of hydroxyl (OH) groups and trace water in oxide properties. These material details directly impact etch selectivity (SiO₂ vs. Si₃N₄), residue formation (SiO₂-based residues), and process window margins for CTO etch.

---

## Part 1: Silicon Dioxide Fundamentals

### 1.1 Crystal Structure and Bonding

#### SiO₂ in Nature and Semiconductor Processing

Silicon dioxide exists in multiple crystalline forms in nature (quartz, cristobalite, tridymite) and as amorphous SiO₂ (used in semiconductor processing). In semiconductor devices, **amorphous SiO₂** dominates because:

1. **Isotropic properties:** No grain boundaries or directional etch anisotropy
2. **Controllable stoichiometry:** Precise Si:O ratio tunable through deposition conditions
3. **Defect minimization:** Amorphous structure reduces long-range ordering defects

#### Amorphous SiO₂ Structure (Random Coil Network)

Unlike crystalline SiO₂ (rigid Si-O-Si bridges arranged in perfect lattice), amorphous SiO₂ is a **random three-dimensional network** of Si-O bonds:

```
Crystalline SiO₂ (quartz):
    O
    ║
Si—O—Si—O—Si  (regular, repeating network)
    ║   ║
    O   O

Amorphous SiO₂ (semiconductor oxide):
         Si
        /  \
       O    O
      / \  / \
     Si  Si  Si  (random, three-dimensional network)
      \ /  \ /
       O    O
        \  /
         Si
```

**Key properties of amorphous SiO₂:**

| Property | Value | Significance |
|----------|-------|---|
| **Si-O bond length** | 1.62 Å | Compared to C-C (1.54 Å), Si-O is slightly longer |
| **Si-O bond energy** | 466 kJ/mol | Strong covalent bond; requires high-energy plasma to break |
| **Coordination number** | 4 (Si), 2 (O) | Each Si bonded to 4 O; each O bonded to 2 Si |
| **Density (thermal oxide)** | 2.27 g/cm³ | Lower than silicon (2.33 g/cm³) due to open network structure |
| **Refractive index** | 1.46 (@ 550 nm) | Used for optical thickness measurement |
| **Thermal conductivity** | 1.4 W/m·K | ~170× lower than silicon (237 W/m·K); thermal isolation excellent |

#### Bonding in SiO₂

**Primary Si-O-Si bonds:**
- Covalent bonds
- Very strong (466 kJ/mol dissociation energy)
- Require high activation energy to break

**Secondary OH groups (defects):**
- Si-OH and Si-O-H groups occur at oxide surfaces and within the oxide
- Water (H₂O) can be incorporated during deposition or thermal oxidation
- OH concentration: typically 10^17-10^19 cm⁻³ in thermal oxides

**Trace impurities (depending on deposition method):**
- Nitrogen (if from PECVD nitride process cross-contamination)
- Carbon (if from CVD precursor gases)
- Chlorine (if oxide grown in HCl-containing ambient)

---

### 1.2 Thermal Oxidation: The Deal-Grove Model

#### Historical Context and Importance

"Thermal oxidation" refers to growing SiO₂ on silicon by exposing silicon to oxygen at elevated temperature (>800°C). The process is controlled, reproducible, and produces ultra-high-quality oxide. For CTO etch, thermal oxide is the baseline reference.

**Thermal oxidation timeline:**

| Date | Achievement |
|------|-------------|
| 1957 | Thermal oxidation discovered |
| 1960 | Deal and Grove publish oxidation model |
| 1965 | Thermal oxide used in integrated circuits |
| 1970s-1980s | Gate oxide scaling enabled by controlled thermal oxidation |
| 1990s+ | Atomic-layer understanding of oxide growth |

#### Deal-Grove Oxidation Model

The **Deal-Grove Model** predicts oxide thickness growth rate as a function of:
- Temperature (T)
- Ambient oxygen partial pressure
- Oxidation time (t)
- Oxide thickness already grown (x)

**Physics:** Oxidation proceeds by diffusion of oxygen through the growing oxide to the Si-SiO₂ interface, where oxygen reacts with silicon:

$$\text{Si} + \text{O}_2 \rightarrow \text{SiO}_2$$

**Reaction rate equation:**

$$\frac{dx}{dt} = \frac{D(C_s - C_0)}{x}$$

Where:
- x = oxide thickness
- D = oxygen diffusion coefficient through oxide
- C_s = oxygen concentration at oxide surface
- C_0 = oxygen concentration at Si-oxide interface
- t = time

**Solution (Deal-Grove):**

$$x^2 + Ax = B(t + \tau)$$

Where:
- A, B = constants dependent on temperature and oxidation ambient
- τ = effective time offset (accounts for pre-existing native oxide)

**Simplified forms:**

For short times (thin oxide, <100 nm): **Reaction-limited regime**
$$x \approx kt_r t$$

For long times (thick oxide, >100 nm): **Diffusion-limited regime**
$$x \approx \sqrt{D_\text{eff} \cdot t}$$

#### Oxidation Parameters for Common Conditions

| Condition | Temperature | Duration | Final Oxide | Note |
|-----------|---|---|---|---|
| **Dry oxidation (O₂)** | 900°C | 1 hour | ~15 nm | Slow, high-quality |
| **Wet oxidation (steam)** | 900°C | 1 hour | ~150 nm | 10× faster than dry |
| **Native oxide (room temp)** | 25°C | 1 year | ~1-3 nm | Automatic on Si surface |
| **Rapid thermal oxidation** | 1000°C | 30 sec | ~50 nm | Fast, widely used |

**Arrhenius dependence of growth rate:**

$$B = B_0 e^{-E_a / k_B T}$$

Typical activation energy for thermal oxidation: **E_a ≈ 2.0-2.5 eV**

**Result:** Oxidation rate doubles for every ~20°C temperature increase in the 800-1100°C range.

---

### 1.3 Native Oxide and Oxide Regrowth

#### Native Oxide Formation

Silicon exposed to air spontaneously forms a **native oxide layer** due to reaction with atmospheric oxygen and water:

$$2\text{Si} + \text{O}_2 \rightarrow 2\text{SiO}$$
$$2\text{SiO} + \text{O}_2 \rightarrow 2\text{SiO}_2$$

**Native oxide properties:**

| Property | Value |
|----------|-------|
| **Thickness (room temperature, 1 year)** | 1-3 nm |
| **Growth rate** | Slows exponentially; negligible after a few nm |
| **Quality** | Moderate (defects, pinholes common) |
| **Density** | Lower than thermal oxide (incorporates water, OH groups) |

**Mechanism (Cabrera-Mott Model):**

Growth slows because:
1. Initial oxygen reacts readily → rapid oxide formation
2. As oxide thickens, electron tunneling must cross the oxide layer to reach silicon
3. Tunneling probability decreases exponentially with distance
4. Transport becomes rate-limiting → growth rate drops

$$\text{Growth rate} \propto e^{-x/\lambda}$$

where λ ≈ 0.5-1 nm is the tunneling decay length.

**Result:** Native oxide growth essentially stops after ~2-3 nm; further oxidation requires thermal activation.

#### Oxide Regrowth During CTO Etch and Post-Etch Cleaning

**Critical issue in CTO etch:** During post-etch residue removal (in-situ cleaning), oxide can **regrow** on freshly-etched SiO₂ surfaces if oxygen is present:

- Fresh SiO₂ surface (from etch) is reactive
- Addition of oxidizing plasma (O₂ plasma) or thermal oxidation (heat in air) causes regrowth
- Regrowth can be fast (~1-5 nm per minute in oxygen plasma at 200-300°C)

**Consequence:** If oxide regrows during cleaning, the CTO stack is not properly exposed, and subsequent etch steps fail or exhibit poor selectivity.

**Mitigation:** Post-etch cleaning must:
1. Use *reducing* plasmas (H₂, reducing fluorocarbon) for residue removal, or
2. Carefully control temperature to prevent oxidation
3. Minimize time between etch and cleaning
4. Avoid air exposure of freshly-etched CTO stack

---

## Part 2: Thermal Properties of SiO₂

### 2.1 Thermal Conductivity and Its Impact on CTO Etch

#### Thermal Conductivity Values

SiO₂ is a **thermal insulator**:

| Material | Thermal Conductivity (W/m·K) | Relative to SiO₂ |
|----------|---|---|
| Silicon | 237 | 170× |
| Aluminum | 237 | 170× |
| Copper | 385 | 275× |
| **Silicon Dioxide** | **1.4** | **1×** |
| Silicon Nitride | 10-15 | 7-11× |
| Photoresist | 0.2-0.3 | 0.2× |

**Temperature dependence of SiO₂ thermal conductivity:**

κ(T) ≈ κ₀ · (T₀/T)^α, where α ≈ 1.0-1.2 for amorphous SiO₂

Result: Thermal conductivity *increases* as temperature *decreases*. At cryogenic temperatures (4 K), κ drops significantly; at high temperatures (>500 K), κ continues decreasing.

#### Implications for CTO Etch Chamber Design

**Thermal management challenge:** CTO etch deposits ~100-500 W into the 300mm wafer and surrounding chamber. The SiO₂-rich CTO stack provides **thermal resistance** between:
- Heat generation site (plasma, electrode)
- Wafer back-side chuck (where cooling water flows)

**Result:**
- Wafer temperature rises despite active cooling (target: -10 to +50°C; often +30-40°C in production)
- CTO stack top (electrode side) is hotter than stack bottom (silicon channel side)
- Temperature gradients can be significant (10-20°C across 5-8 µm stack thickness)

**Thermal transient behavior:** When RF power switches on, wafer temperature rises on timescale of 1-5 seconds (due to low SiO₂ thermal conductivity). This slow transient makes power switching difficult for endpoint control.

---

### 2.2 Thermal Expansion and Stress in CTO Layers

#### Coefficient of Thermal Expansion (CTE)

| Material | CTE (ppm/K) |
|----------|---|
| Silicon | 2.6 |
| SiO₂ (amorphous) | 0.5 |
| Si₃N₄ | 3.0-3.5 |
| Photoresist | 50-100 |

**Consequence:** During CTO etch (temperature rise from 25°C to 40°C, ΔT ≈ 15°C):

- Si expands: ΔL/L = 2.6 × 10⁻⁶ × 15 = 3.9 × 10⁻⁵ = 0.004%
- SiO₂ expands: ΔL/L = 0.5 × 10⁻⁶ × 15 = 0.75 × 10⁻⁵ = 0.0008%
- **Differential expansion:** Si expands ~5× more than SiO₂

**Result:** Thermal stress at Si-SiO₂ interface; in deep CTO stacks, this can create:
- Stress-induced defects in oxide
- Enhanced charge leakage at interface
- Pillar bending or warping (in extreme cases)

**Mitigation:** Careful thermal control; keep wafer temperature below ~50°C to minimize CTE-induced stress.

---

## Part 3: Chemical Reactivity of SiO₂ in Plasma Etch

### 3.1 Etch Chemistry Basics

#### SiO₂ Etch Reactions with Fluorine

SiO₂ is etched by fluorine-containing plasmas via reactions with fluorine radicals (F•) and fluorine ions (F⁺):

**Primary reactions:**

1. **SiO₂ + F → SiF⁺ + O⁻** (ion-assisted; requires ion impact)
2. **SiO₂ + F → SiF + O** (neutral radical attack; slower)
3. **SiF⁺ + H₂O → SiF·H + OH⁻** (surface hydration)

**Product species (volatile, exit chamber):**
- SiF₄ (silicon tetrafluoride; **volatile**)
- SiF₂ (silicon difluoride; **volatile**)
- CO₂, CO (from carbon source in some chemistries)
- H₂O (water vapor)

#### Etch Rate Dependence on Plasma Parameters

**Fluorine radical concentration [F•]:**
$$\text{R}_\text{etch} \propto [\text{F}^\bullet]^{0.5-1.0}$$

Typical etch rate dependence on process parameters:

| Parameter | Effect on Etch Rate | Reason |
|---|---|---|
| **RF Power** | Increases | More plasma dissociation → more F• production |
| **Pressure** | Decreases | Higher pressure → more collisions → shorter F• mean free path |
| **Temperature** | Increases | Faster reaction kinetics; surface processes accelerate |
| **[CF₄] or [SF₆]** | Increases | Direct source of fluorine |

**Typical etch rates for SiO₂:**
- CF₄ plasma (100 W, 20 mTorr, 25°C): ~200-300 nm/min
- SF₆ plasma (100 W, 20 mTorr, 25°C): ~100-200 nm/min (lower because SF₆ is slower source)
- C₄F₈ plasma (100 W, 20 mTorr, 25°C): ~50-100 nm/min (passivation layer limits rate)

---

### 3.2 Stoichiometry and Oxidation State Effects

#### SiO₂ Variations: Fully Oxidized vs. Sub-Oxides

In plasma or under extreme conditions, partially oxidized silicon ("sub-oxides") can form:

| Composition | Formula | Properties | Etch Rate |
|---|---|---|---|
| **Fully oxidized (stoichiometric)** | SiO₂ | Insulating; dense | Reference (1.0×) |
| **Sub-oxide** | SiO₁.₅ | Intermediate; less dense | ~1.2-1.5× faster |
| **Sub-oxide** | SiO | Semi-metallic; low resistance | ~2-3× faster |
| **Silicon** | Si | Metallic; conducts electricity | 100-1000× faster (sputtering dominates) |

**Implication for CTO etch:** If oxide becomes partially reduced (SiO instead of SiO₂), its etch rate increases dramatically. This can cause:
- Selectivity loss (SiO₂/Si₃N₄ ratio changes)
- Etch rate runaway (less oxide → faster etch → more heat → more oxide reduction)

**Prevention:** Maintain oxidizing conditions throughout CTO etch; avoid plasma conditions that reduce oxide (high ion energy + low fluorine flux).

---

## Part 4: SiO₂ in CTO Stack Context

### 4.1 Thermal Oxide vs. Deposited Oxide in CTO Layers

CTO stacks use both **thermal oxide** (grown) and **deposited oxide** (PECVD or ALD):

| Characteristic | Thermal SiO₂ | Deposited SiO₂ |
|---|---|---|
| **Quality** | Ultra-high (Si interface excellent) | Good (interface defects possible) |
| **Defect density** | Very low (~10⁸ cm⁻³) | Moderate (~10¹⁰-10¹² cm⁻³) |
| **OH groups** | Moderate (1-5% of Si-O) | Higher (1-10% of Si-O) |
| **Thickness uniformity** | Excellent (±5%) | Good (±10%) |
| **Film stress** | Compressive (~300 MPa) | Tensile (100-500 MPa) |
| **Etch rate (same plasma)** | 100 nm/min | 110-130 nm/min (10-30% faster) |

**Implication:** Deposited SiO₂ etches slightly faster than thermal SiO₂. In multi-layer CTO stacks, this can create selectivity variations if some layers are thermal and others deposited.

### 4.2 Charging Effects and Oxide Breakdown Risk

During high-aspect-ratio CTO etch, **charge accumulation** can damage SiO₂:

1. **Negative charge buildup** in deep oxide layers (from ion bombardment)
2. **Positive charge at surface** (from secondary electron emission)
3. **Electric field buildup** across thin oxide layers (100-1000 V/cm possible)
4. **Thermal breakdown** at hot spots

**Result:** Oxide breakdown (permanent short circuit) can occur. Typical breakdown fields:

| Oxide Type | Breakdown Field |
|---|---|
| **High-quality thermal SiO₂** | 6-10 MV/cm |
| **Deposited SiO₂** | 4-8 MV/cm |
| **Defective oxide** | 2-4 MV/cm |

In CTO etch with 50+ mTorr pressure and high power density, localized fields can exceed these values temporarily, risking oxide breakdown and device failure.

**Mitigation:** Control plasma potential and ion energy; use pulsed RF power to reduce peak fields.

---

## Summary: SiO₂ as Foundation for CTO Etch

| Aspect | Impact on CTO Etch |
|---|---|
| **Strong Si-O bonding** | High energy required for etch; requires energetic fluorine radicals or ions |
| **Low thermal conductivity** | Thermal management difficult; wafer temperature rises during etch |
| **Thermal expansion mismatch (Si vs. SiO₂)** | Stress at interfaces; must control temperature |
| **Etch rate dependence on stoichiometry** | Sub-oxides etch much faster; selectivity can be lost with etch rate runaway |
| **Native oxide regrowth** | Post-etch residue removal must prevent oxide regrowth |
| **Charge accumulation risk** | High-aspect-ratio etch can accumulate charge; must control voltages carefully |

Understanding SiO₂ chemistry and physics is the foundation for designing reliable CTO etch processes.

---

[Continue to Chapter 3: Silicon Nitride Properties →](./03-silicon-nitride-properties.md)
