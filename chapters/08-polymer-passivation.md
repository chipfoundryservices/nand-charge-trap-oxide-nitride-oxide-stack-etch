# Chapter 8: Polymer Formation & Surface Passivation in CTO Etch

## Executive Summary

Modern 3D NAND CTO etch relies critically on **fluorocarbon polymer deposition** to achieve the high selectivity ratios (>10:1) required to protect charge-trap nitride layers. Unlike earlier silicon etch processes where polymers were considered "bad" (unwanted byproducts requiring post-etch removal), in CTO etch **polymers are intentionally engineered as process enablers**. This chapter develops the detailed chemistry of fluorocarbon polymer formation (from C₄F₈, CHF₃, and C₅F₈ precursors), the mechanisms by which polymers selectively protect Si₃N₄ over SiO₂, and the dynamic balance between polymer **deposition** and ion **sputtering** that determines the steady-state polymer thickness. Special attention is paid to the **selectivity amplification mechanism**—how a thin polymer layer (10-50 nm) can increase effective selectivity from 5:1 to 15:1—and the **residue challenge**: post-etch polymer removal without damaging device-critical interfaces. The chapter culminates in describing modern **pulsed-plasma techniques** that exploit polymer cycling (grow-and-remove cycles) to achieve unprecedented selectivity and uniformity in 3D NAND.

---

## Part 1: Fluorocarbon Polymer Formation

### 1.1 Polymer Precursor Dissociation

#### C₄F₈ (Octafluorocyclobutane) Chemistry

**C₄F₈ molecular structure:**

```
      F F
      | |
  F—C—C—F
  | | | |
  F C—C F
    | |
    F F
```

**C₄F₈ is more polymerizing than CF₄ because:**
1. Longer carbon backbone (C₄ vs. C₁) → larger fragments after dissociation
2. More fluorine atoms attached → more available for both etch AND polymerization
3. Can dissociate into C₃, C₂ fragments (not just CF₃ monomers)

#### Dissociation Pathways

**Primary dissociation (electron impact):**

$$e^- + \text{C}_4\text{F}_8 \rightarrow \text{C}_3\text{F}_6^• + \text{CF}_2^• + e^-$$

**Secondary dissociation of fragments:**

$$e^- + \text{C}_3\text{F}_6^• \rightarrow \text{C}_2\text{F}_4^• + \text{CF}_2^• + e^-$$

$$e^- + \text{CF}_2^• \rightarrow \text{CF}^• + \text{F•} + e^-$$

#### Resulting Radical Species

| Species | Molecular Weight | Reactivity | Role in Polymer |
|---|---|---|---|
| **F•** | 19 | Very high | Etch agent; can etch polymer |
| **CF•** | 31 | Moderate | Monomer; builds polymer backbone |
| **CF₂•** | 50 | High | Key monomer for polymer chains |
| **C₂F₃•** | 81 | Moderate | Polymer chain fragment |
| **C₃F₅•** | 131 | Low | Heavier fragment; sticks to surface |
| **C₄F₇•** | 169 | Very low | Dimer precursor; high sticking coefficient |

---

### 1.2 Polymer Chain Growth Mechanism

#### Initiation: Radical Generation and Adsorption

**Step 1: CF₂ radical formation in plasma**
$$e^- + \text{C}_4\text{F}_8 \rightarrow \text{radicals including CF}_2^•$$

**Step 2: CF₂ radical approaches surface**
$$\text{CF}_2^• \rightarrow \text{surface (weak Van der Waals)}$$

**Step 3: Chemisorption to surface defects**
$$\text{CF}_2^• + \text{Si-O (surface)} \rightarrow \text{Si-O-CF}_2 \text{ (chemisorbed)}$$

#### Propagation: Chain Growth

**Step 4: Addition of next radical**

$$\text{(CF}_2)_n + \text{CF}_2^• \rightarrow \text{(CF}_2)_{n+1}$$

**Reaction rate:** Depends on:
- CF₂ radical density [CF₂•]
- Surface coverage of growing chains
- Chain termination events

#### Termination: Chain Length Stabilization

**Two termination pathways:**

**Pathway A: Radical recombination**
$$\text{(CF}_2)_n + \text{(CF}_2)_m \rightarrow \text{(CF}_2)_{n+m} \text{ (cross-linking)}$$

**Pathway B: Hydrogen capture (if H present)**
$$\text{(CF}_2)_n^• + \text{H•} \rightarrow \text{(CF}_2)_n\text{H}$$

#### Polymer Structure

**Simplified polymer composition:**

Average formula: **(CF₁.₅-CF₂)_n** (stoichiometry varies; typically fluorine-rich)

**Polymer as deposited:**

```
—CF₂—CF₂—CF—CF₂—CF₂—CF—CF—CF₂—
      |       |   |       |
      F       F   F       F
      
(typically 30-40% cross-linking between chains)
```

---

## Part 2: Selective Polymer Deposition on Si₃N₄

### 2.1 Why Polymer Deposits Preferentially on Si₃N₄

#### Surface Reactivity Differences

**On SiO₂ surface:**
- Si-O-Si (basic, oxide)
- Weakly polar
- **Low sticking coefficient** for CF₂ radicals (~10-20%)

**On Si₃N₄ surface:**
- Si-N-Si (acidic, basic nitrogen sites)
- More polarized (N is electronegative but less so than O)
- **Higher sticking coefficient** for CF₂ radicals (~30-50%)

**Why the difference?** 
- CF₂ is an electrophile (electron-deficient due to fluorine)
- N atoms in Si₃N₄ can donate electron density
- Si-N-Si sites are **more reactive** than Si-O-Si sites

#### Polymer Deposition Rate on Each Material

**Typical polymer deposition rates (C₄F₈ plasma, 100 W, 20 mTorr, 25°C):**

| Surface | Deposition Rate |
|---|---|
| **Bare Si₃N₄** | 50-80 nm/min |
| **Thin polymer on Si₃N₄** | ~40 nm/min (decreases as polymer builds up) |
| **SiO₂** | 15-25 nm/min |
| **Polymer on polymer** | ~30-40 nm/min (slower than on nitride, faster than on bare SiO₂) |
| **Aluminum (electrode)** | 100-200 nm/min (very high) |

**Selectivity of polymer deposition:**

$$S_{\text{polymer, Si3N4/SiO2}} = \frac{\text{Deposition rate on Si3N4}}{\text{Deposition rate on SiO2}} = \frac{60}{20} \approx 3:1$$

**Consequence:** Even without etch occurring, polymer preferentially accumulates on Si₃N₄.

---

### 2.2 Polymer as "Etch Mask" for Si₃N₄

#### Polymer Thickness on Si₃N₄ During Etch

**As etch proceeds with C₄F₈ in plasma:**

| Time (min) | Polymer Thickness on Si₃N₄ | Polymer Thickness on SiO₂ | Status |
|---|---|---|---|
| **0** | 0 nm | 0 nm | Start |
| **1** | 20 nm | 5 nm | Early etch; polymer building |
| **3** | 50 nm | 15 nm | Polymer reaching steady state |
| **5** | 70 nm | 25 nm | Thick polymer on Si₃N₄ |
| **10** | 100+ nm | 40 nm | Mature polymer layers |

**At steady state (> 5 min):**
- **Polymer on Si₃N₄:** ~80-120 nm (thick, protective)
- **Polymer on SiO₂:** ~30-50 nm (thin, partially protective)

#### How Polymer Reduces Si₃N₄ Etch Rate

**Bare Si₃N₄ etch:** 50 nm/min (from Chapter 6)

**With ~50 nm polymer layer:**
- Polymer is ~50% as permeable to F• as bare Si₃N₄
- Effective etch rate through polymer: ~25 nm/min
- **Etch rate reduction:** 2× (50 → 25 nm/min)

**With ~100 nm polymer layer:**
- Polymer is ~20% permeable to F•
- Effective etch rate: ~10 nm/min
- **Etch rate reduction:** 5× (50 → 10 nm/min)

#### Combined SiO₂/Si₃N₄ Selectivity Enhancement

**Without polymer (CF₄ alone):**

$$S = \frac{R_{\text{SiO2}}}{R_{\text{Si3N4}}} = \frac{200}{40} = 5:1$$

**With polymer (C₄F₈ + CF₄ blend):**

- SiO₂ etch slowed: 200 → 150 nm/min (polymer hinders access slightly)
- Si₃N₄ etch slowed more: 40 → 10 nm/min (polymer is thick, protective)

$$S = \frac{150}{10} = 15:1$$

**Selectivity improvement:** 5:1 → 15:1 (3× enhancement from polymer)

---

## Part 3: Polymer Dynamics and Steady-State Control

### 3.1 Deposition vs. Sputtering Balance

#### Polymer Deposition and Removal Rates

**Polymer deposition (from radical sticking):**
$$D_p = \alpha \times [\text{CF}_2^•] \times A_\text{available}$$

Where:
- α = sticking coefficient (~0.1-0.3)
- [CF₂•] = CF₂ radical density
- A_available = available surface area

**Polymer sputtering (from ion bombardment):**

$$E_p = \sigma \times J_\text{ion} \times E_\text{ion}$$

Where:
- σ = sputtering yield (atoms/ion) = ~0.1-1.0 for fluorocarbon polymer
- J_ion = ion flux
- E_ion = average ion energy

#### Steady-State Polymer Thickness

**At equilibrium, D_p = E_p:**

$$\alpha [\text{CF}_2^•] = \sigma J_\text{ion}$$

**Typical steady-state polymer thickness:**

| RF Power | Pressure | Temperature | Polymer Thickness |
|---|---|---|---|
| 100 W | 10 mTorr | 25°C | 50 nm |
| 200 W | 10 mTorr | 25°C | 40 nm (more ion sputtering) |
| 100 W | 30 mTorr | 25°C | 80 nm (less ion sputtering) |
| 100 W | 10 mTorr | -10°C | 60 nm (slower sputtering at low T) |

**Key insight:** Polymer thickness can be tuned via pressure (higher pressure → thicker polymer, because ions have lower mean free path).

---

### 3.2 Pulsed-Plasma Polymer Control

#### Motivation: Controlling Selectivity Drift

**Problem:** With continuous C₄F₈ plasma:
- Polymer thickness builds up over first 5-10 minutes
- Selectivity **increases over time** (as polymer thickens)
- By end of etch (20 min), selectivity can be very high, but selectivity has drifted

**Consequence:** Etch rate at bottom of stack different from top → non-uniformity

#### Pulsed-Plasma Approach

**Concept: Cyclic plasma on/off with different chemistry each cycle**

**Typical pulsed-etch recipe:**

```
Cycle 1 (30 sec on, 10 sec off):
  On:  CF₄ plasma (SiO₂ etch, minimal polymerization)
  Off: No plasma (polymer from previous cycle partially stabilizes)
  
Cycle 2 (30 sec on, 10 sec off):
  On:  C₄F₈-rich plasma (polymer deposition, selectivity enhancement)
  Off: Polymer "set" without sputtering

Repeat 10-20 times
```

#### Selectivity Stabilization via Pulsing

**With pulsed approach:**

| Phase | Plasma Chemistry | Selectivity | Polymer Thickness |
|---|---|---|---|
| **Cycle 1 (CF₄)** | Etch-dominated | 5:1 | Thin, partially eroded |
| **Cycle 1 OFF** | No plasma | — | Stabilizes |
| **Cycle 2 (C₄F₈)** | Polymerize-dominated | 8:1 | Thickens to 50 nm |
| **Cycle 2 OFF** | No plasma | — | Stabilizes |
| **Steady state** | Oscillating | **Average 6-7:1** | Oscillates 30-50 nm |

**Benefit:** Selectivity remains relatively constant over etch duration (instead of drifting from 5:1 to 10:1).

---

## Part 4: Post-Etch Residue and Cleaning

### 4.1 Polymer Residue After CTO Etch

#### Residue Quantification

**After 20-minute CTO etch with C₄F₈:**

- **Total polymer deposited on wafer:** ~2-5 µm equivalent thickness (if spread uniformly)
- **Distributed as:**
  - Top surfaces: 80-100 nm
  - Pillar walls: 50-70 nm
  - Pillar bottoms (deep features): 20-40 nm
  - Confined gaps (<50 nm wide): 10-20 nm

**Residue composition:**

| Component | Fraction | Phase |
|---|---|---|
| **Fluorocarbon polymer** | 60-70% | Solid |
| **Silicon oxyfluoride** | 10-20% | Solid/glassy |
| **Residual fluorine** | 5-10% | Absorbed |
| **Silicon monoxide** | <5% | Glassy |

**Residue thickness in critical 30-nm-wide pillar gaps:**
- ~10-20 nm polymer buildup
- Can partially or completely block gap (critical for device operation)

---

### 4.2 Residue Removal: Challenges and Solutions

#### Challenge: Confined Space Diffusion

**Pillar gaps in 3D NAND:**
- Width: 20-50 nm
- Height: 5-25 µm (deep)
- Aspect ratio: 100:1 to 1000:1

**Residue removal challenge:**
- Polymer must diffuse through narrow gap (low diffusion rate)
- Gas species must reach bottom of gap (diffusion-limited)
- Typical diffusion time for polymer removal: 5-10 minutes (slow)

#### Strategy 1: Oxidative Plasma Clean

**Use O₂ plasma to burn off polymer:**

$$\text{(CF}_x)_n + 2\text{O•} \rightarrow \text{CO}_2 + \text{CO} + \text{products}$$

**Procedure:**

1. **Etch ends** (~20 min, C₄F₈-containing plasma)
2. **Switch to O₂ plasma** (100 W, 50 mTorr, 25°C)
3. **Duration:** 3-5 minutes
4. **Expected residue removal:** 80-90% of polymer burned off

**Limitations:**
- **Re-oxidation risk:** Exposed Si₃N₄ oxidizes (see Chapter 6)
- **Ion damage:** O⁺ ions can sputter polymer AND underlying oxide
- **Incomplete removal:** Residue in deep, confined spaces may remain

#### Strategy 2: H₂-Based Reductive Clean

**Use H₂ plasma to remove polymer without oxidation:**

$$\text{(CF}_x)_n + 4\text{H•} \rightarrow \text{CH}_4 + \text{CF}_2 + ...$$

**Procedure:**

1. **H₂ plasma clean** (100 W, 30 mTorr, 50°C)
2. **Duration:** 5-10 minutes (longer than O₂ clean)
3. **Advantage:** No oxidation of Si₃N₄

**Limitations:**
- **Slower than oxidative clean** (H• less reactive than O•)
- **Hydrogen incorporation:** Some H may stick to Si₃N₄ (parasitic)

#### Strategy 3: Combination Clean (Preferred Modern Approach)

**Multi-step sequence:**

**Step 1: Brief H₂ soak (2 min)**
- Reduces polymer surface
- Prevents oxidation

**Step 2: O₂ plasma etch (3 min)**
- Oxidative burn; fast removal
- By this point, oxidation risk lower (top residue already gone)

**Step 3: Final H₂ purge (1 min)**
- Removes any residual oxide formed in Step 2
- Final cleanup

**Total time:** 6 minutes (reasonable for production)

---

## Summary: Polymer Chemistry for CTO Selectivity

| Aspect | Role in CTO Etch | Key Parameters |
|---|---|---|
| **Polymer deposition** | Enhances SiO₂/Si₃N₄ selectivity from 5:1 to 15:1 | C₄F₈ fraction, pressure, ion energy |
| **Selective Si₃N₄ coating** | Protects charge-trap layer during etch | Surface reactivity differences; polymer sticking coefficient |
| **Steady-state balance** | Maintains constant polymer thickness over etch | D_p = E_p balance; tunable by pressure/power |
| **Pulsed plasma cycling** | Stabilizes selectivity over time | On/off cycles exploit polymer deposition/stabilization |
| **Post-etch cleaning** | Removes residue without damaging Si₃N₄ | Multi-step H₂/O₂ approach |

**Design Principle:** Modern 3D NAND CTO etch is fundamentally an exercise in **polymer engineering**—carefully controlling deposition to enhance selectivity while managing residue for post-etch cleaning. Success requires integrated understanding of plasma chemistry (CF₄/C₄F₈ dissociation), surface interactions (polymer sticking), and process mechanics (sputtering, diffusion).

---

**End of Part II: Selective Etching Mechanisms ✅**

Part II covered the fundamental selectivity mechanisms and feedback control strategies that enable CTO etch. The next part (Part III: High-Aspect-Ratio Processing, Chapters 9-12) will address the extreme aspect ratios that dominate 3D NAND manufacturing and the associated challenges of etch uniformity, thermal management, and residue removal in confined 100-µm-deep pillars.

---

[Proceed to Part III: High-Aspect-Ratio Processing →](./09-arde-trenches-pillars.md)
