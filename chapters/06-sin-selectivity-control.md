# Chapter 6: Si₃N₄ Etch Selectivity & Nitrogen Chemistry

## Executive Summary

While Chapter 5 focused on SiO₂ etch chemistry, this chapter develops the complementary view: how Si₃N₄ responds to the same fluorine plasma, why it etches slower than SiO₂, and how to manipulate its etch rate to maintain selectivity. Si₃N₄ etch selectivity is fundamentally driven by **nitrogen chemistry**—the formation of nitrogen-containing surface species (N•, NF, NF₂) that passivate the surface and slow etch. This chapter develops the detailed mechanisms of nitrogen passivation, demonstrates why Si₃N₄ is a "self-passivating" material in fluorine plasma, and shows how to exploit this chemistry for high selectivity in CTO etch. Special attention is paid to **oxidation of Si₃N₄** during post-etch cleaning (a critical failure mode), **oxynitride formation** (SiOₓNᵧ mixed phase), and the role of nitrogen vacancies (V_N) as both etch sites and charge-trap locations.

---

## Part 1: Nitrogen Passivation Chemistry

### 1.1 Surface Reactions of Fluorine with Si₃N₄

#### Initial F• Attack on Si-N Bonds

**Primary reaction with F radical:**

$$\text{Si-N} + \text{F•} \rightarrow \text{Si-F} + \text{N•}$$

**Key difference from SiO₂:** The freed nitrogen atom (N•) **remains on the surface** and participates in passivation.

#### Nitrogen-Fluorine Species Formation

**Step 1: N• radical formation**
$$\text{Si}_3\text{N}_4 + 3\text{F•} \rightarrow \text{Si}_3\text{F}_3 + 3\text{N•}$$

**Step 2: Nitrogen species formation (multiple pathways)**

**Pathway A - NF formation (common):**
$$\text{N•} + \text{F•} \rightarrow \text{NF} \text{ (surface-bound)}$$

**Pathway B - NF₂ formation:**
$$\text{N•} + 2\text{F•} \rightarrow \text{NF}_2$$

**Pathway C - N₂ formation (less common, requires collision):**
$$2\text{N•} \rightarrow \text{N}_2 \text{ (desorbs)}$$

#### Passivation Layer Buildup

**Key observation:** Unlike O• from SiO₂ etch (which desorbs as part of volatile SiF₄), N• from Si₃N₄ etch remains adsorbed on the surface:

```
Si₃N₄ surface BEFORE etch:
Si—N—Si
|   |   |
N   Si  N

After F• attack (instant):
Si—F  Si—F
|       |
NF (adsorbed passivation)
```

**Result:** A surface layer of NF and NF₂ gradually builds up, creating a **passivation layer** that slows further etch.

---

### 1.2 Passivation Layer Kinetics

#### Growth Rate of Passivation Layer

**Passivation layer thickness as function of etch time:**

$$t_p(t) = D_p(t) \times t - E_p(t) \times t$$

Where:
- t_p = passivation layer thickness
- D_p = deposition rate of N-F species (from F• attack on Si₃N₄)
- E_p = erosion rate (from ion sputtering of passivation layer)

**Typical values (CF₄ plasma, 100 W, 20 mTorr):**

| Phase | D_p (nm/min) | E_p (nm/min) | Net Growth |
|---|---|---|---|
| **Early (0-2 min)** | 50 | 10 | +40 nm/min |
| **Middle (2-10 min)** | 40 | 35 | +5 nm/min |
| **Steady state (>10 min)** | 40 | 40 | 0 (stable) |

**Steady-state thickness:** ~50-100 nm (depends on pressure, power, temperature)

#### Effect on Etch Rate

**As passivation layer grows:**

```
Time=0 min:   Etch rate = 80 nm/min (bare Si₃N₄)
Time=1 min:   Etch rate = 60 nm/min (thin passivation)
Time=5 min:   Etch rate = 25 nm/min (thick passivation)
Time=10 min:  Etch rate = 20 nm/min (steady state)
```

**Net effect:** Si₃N₄ etch rate **decreases over time** as passivation layer builds up.

**Mathematical model:**

$$R_\text{etch}(t) = R_0 e^{-t/\tau}$$

Where τ ≈ 3-5 minutes (time constant for passivation buildup)

---

### 1.3 Passivation Layer Composition and Structure

#### Chemical Composition (XPS Analysis)

**Typical passivation layer in CF₄ plasma (elemental %):**

| Element | Content | Form |
|---|---|---|
| **Si** | 20-30% | Si-F, Si-N-F |
| **N** | 10-20% | NF, NF₂ |
| **F** | 50-60% | N-F, Si-F |
| **O** | 5-10% | Si-O (adventitious) |

**Average composition:** Roughly SiN_xF_y with excess F (n-type deficient)

#### Structural Model

```
Surface of Si₃N₄ after passivation buildup:

Top layer (0-5 nm):        F-N-F
                           |   |
                        Si—N—Si (highly fluorinated)
                           |

Middle layer (5-20 nm):    Si—F
                           |   |
                        N—F   Si—N (mixed)
                           |

Bottom layer (20-50 nm):   Si—N
                           |   |
                        N—Si—N (slightly F-terminated)
```

#### Passivation Removal by Ion Bombardment

**Ion sputtering erodes passivation layer:**
- Low-energy ions (20-50 eV): Slow erosion (~2-5 nm/min)
- Medium-energy ions (100-200 eV): Fast erosion (~10-20 nm/min)
- High-energy ions (>500 eV): Very fast erosion (>50 nm/min)

**Consequence:** In ICP or CCP plasmas with significant ion energy, passivation layer reaches steady state where **deposition = sputtering**.

---

## Part 2: SiO₂/Si₃N₄ Selectivity Mechanisms

### 2.1 Why SiO₂ Etches Faster: Multi-Factor Analysis

#### Factor 1: Passivation Layer (Primary - 50-70% of selectivity)

**SiO₂ surface:**
- O• from Si-O bond breakage is weakly held
- Desorbs as volatile O₂ or as part of SiF₄
- **No passivation layer builds up**
- Continuous, fresh SiO₂ surface exposed to F•
- Etch rate: ~200 nm/min

**Si₃N₄ surface:**
- N• is strongly held on surface
- Forms NF, NF₂ passivation
- **Passivation layer slows further attack**
- Only ~10% of surface accessible for etch after passivation
- Etch rate: ~20 nm/min

**Net selectivity from passivation:** 200/20 = **10:1** (major contribution)

#### Factor 2: Product Volatility (Secondary - 20-30% of selectivity)

**From SiO₂:**
- Primary product: SiF₄ (highly volatile)
- Desorption energy: ~10 kJ/mol
- Desorption timescale: <nanoseconds

**From Si₃N₄:**
- Reaction produces Si-N-F compounds (lower volatility)
- Intermediate products: SiNF₃, Si₂NF, etc. (sticky on surface)
- Desorption energy: ~50 kJ/mol
- Desorption timescale: microseconds to milliseconds

**Consequence:** Si₃N₄ etch products linger on surface; block access to substrate.

#### Factor 3: Chemical Reactivity of Surface (Minor - <10% of selectivity)

**SiO₂ surface sites:**
- Si-O-Si bridges relatively "soft" (high electronegativity difference O ≈ 3.4)
- Polarized bonds → easier for F• to attack

**Si₃N₄ surface sites:**
- Si-N-Si bridges more "hard" (lower electronegativity difference N ≈ 3.0)
- Less polarized → harder for F• to attack

**Activation energy difference:** ~3-5 kJ/mol (minor contribution)

---

### 2.2 Selectivity Stability Across Etch Duration

#### Selectivity Drift Problem

**Observation in long CTO etch (20+ minutes):**

| Time (min) | SiO₂ Rate | Si₃N₄ Rate | Selectivity |
|---|---|---|---|
| **0-2** | 220 nm/min | 50 nm/min | 4.4:1 |
| **2-5** | 210 nm/min | 35 nm/min | 6.0:1 |
| **5-10** | 205 nm/min | 25 nm/min | 8.2:1 |
| **10-15** | 200 nm/min | 20 nm/min | 10:1 |
| **15-20** | 195 nm/min | 20 nm/min | 9.75:1 |

**Mechanism of selectivity improvement over time:**

1. **Early phase (0-2 min):** Passivation layer growing; Si₃N₄ etch rate still elevated
2. **Intermediate (5-10 min):** Passivation layer approaching steady state; Si₃N₄ rate drops rapidly
3. **Late (>10 min):** Passivation layer fully developed; selectivity stabilizes

**Consequence for CTO etch:** If etch duration is <10 minutes, selectivity is **still rising**. If etch is interrupted at wrong time, selectivity may be inadequate.

---

### 2.3 Selectivity Tuning via Nitrogen Chemistry

#### Strategy 1: Enhance Passivation (Increase Selectivity)

**Add polymerizing precursor (C₄F₈):**

C₄F₈ produces fluorocarbon radicals that:
1. Deposit polymer on Si₃N₄ surface preferentially
2. Combined with N-F passivation, creates very thick protective layer
3. Selectivity can increase from 5:1 to 15-20:1

**Mechanism:**
- CF₂•, CF₃• radicals collide with Si₃N₄ surface
- High sticking coefficient on N-reactive surface
- Polymer builds up to 50-100 nm thickness
- Underneath, N-F passivation also present
- **Double barrier** to etch

**Trade-off:** Lower absolute SiO₂ etch rate (polymer formation consumes precursor)

#### Strategy 2: Suppress Passivation (Decrease Selectivity)

**Add oxygen (O₂) to plasma:**

O₂ addition (10-20% of total gas):
- Atomic oxygen (O•) can oxidize N-F passivation: N-F + O• → N-O-F (less protective)
- Passivation layer becomes thinner
- Selectivity decreases from 5:1 to 3-4:1
- But SiO₂ etch rate increases (O helps F• production)

**Use case:** When selectivity is not critical bottleneck; prioritize etch rate.

#### Strategy 3: Ion Energy Control

**Low ion energy (<50 eV):**
- Ions can reach wafer but insufficient energy to sputter passivation
- Passivation layer remains thick
- Si₃N₄ etch rate minimized
- **Selectivity maximized** (8-12:1 achievable)

**High ion energy (>200 eV):**
- Ions easily sputter passivation layer
- Passivation layer remains thin
- Si₃N₄ etch rate elevated
- **Selectivity minimized** (3-4:1)

**Method:** Control bias voltage or RF power distribution between electrodes

---

## Part 3: Critical Issue - Si₃N₄ Oxidation During Post-Etch

### 3.1 Oxidation of Charge-Trap Layer (Failure Mode)

#### During CTO Etch

CTO etch removes SiO₂ layers sequentially. Each time an SiO₂ layer is removed, the underlying Si₃N₄ **charge-trap layer is briefly exposed** to the plasma.

#### Post-Etch Cleaning Risk

**Typical post-etch clean sequence:**

1. **Etch ends:** SiO₂ layers removed, Si₃N₄ exposed to residual F-containing plasma
2. **Clean begins:** Switch to O₂ plasma (or oxidizing fluorocarbon plasma) to burn off carbon residue
3. **Oxidation occurs:** O from plasma oxidizes exposed Si₃N₄:

$$\text{Si}_3\text{N}_4 + 6\text{O} \rightarrow 3\text{SiO}_2 + 4\text{N}_2$$

#### Oxidation Kinetics

**At room temperature:**
- Negligible oxidation (O radicals weak at low T)

**At 100-200°C (typical chamber wall temperature):**
- **Significant oxidation rate: 1-5 nm/min** possible
- Over 5-minute clean: 5-25 nm of oxide can form!

**Result:** A **newly-formed SiO₂ "barrier"** coats the charge-trap Si₃N₄ layer.

#### Consequences for Device

**If Si₃N₄ charge-trap is oxidized:**

1. **Charge storage compromised:** New SiO₂ layer on top of charge-trap acts as blocking oxide; charge stored in oxidized region instead of nitride
2. **Retention loss:** SiO₂ has lower trap density than Si₃N₄; charge leaks out
3. **Device failure:** Bit error rate increases dramatically; device unreadable

**Critical failure mode:** Post-etch oxidation of CTO charge-trap layer can destroy an entire wafer.

---

### 3.2 Prevention Strategies

#### Strategy 1: Reducing (Non-Oxidizing) Post-Etch Clean

**Use H₂-based plasma clean:**
$$\text{C residue} + 4\text{H•} \rightarrow \text{CH}_4 \text{ (desorbs)}$$

**Advantage:** No oxygen → no oxidation of Si₃N₄
**Disadvantage:** H₂ cleaning slower than O₂ cleaning; longer process time

#### Strategy 2: Temperature Control During Clean

**Keep wafer cool (<50°C) during any oxidizing clean:**
- Low temperature → slow oxidation kinetics
- Activation energy E_a ≈ 2.5 eV for Si₃N₄ oxidation
- At 25°C vs. 100°C: oxidation rate drops by ~10×

**Method:** Precool wafer to -10°C before clean step

#### Strategy 3: Protective Oxide Layer (Intentional)

**Some advanced processes intentionally create thin (~3 nm) SiO₂ on Si₃N₄:**

1. **During etch:** Final step includes controlled oxidation or exposure to oxidizing plasma
2. **This thin oxide layer:** Acts as "sacrificial" barrier
3. **Benefits:**
   - Protects charge-trap from further oxidation
   - Subsequent etch step removes this thin oxide (if needed)
   - Net result: charge-trap unaffected

**Trade-off:** Requires additional process step; adds complexity

---

## Summary: Si₃N₄ Selectivity for CTO Applications

| Aspect | Impact on Selectivity | Key Mechanism |
|---|---|---|
| **Nitrogen passivation** | Dominant (50-70% of selectivity) | N-F layer slows etch rate 5-10× |
| **Product volatility** | Secondary (20-30%) | SiF₄ vs. Si-N-F stickiness |
| **Passivation layer buildup** | Causes selectivity drift | Selectivity improves over time as passivation grows |
| **Polymerizing gas (C₄F₈)** | Enhances selectivity 2-4× | Polymer + passivation create thick barrier |
| **Ion energy** | Reduces selectivity at high E | Ions sputter passivation layer |
| **Post-etch oxidation risk** | **CRITICAL FAILURE** | Re-oxidation of charge-trap destroys device |

**Key Design Principle:** Modern 3D NAND CTO etch must balance three competing needs:
1. Maintain SiO₂/Si₃N₄ selectivity (5-10:1)
2. Achieve rapid etch rate (complete in <20 min)
3. Prevent post-etch Si₃N₄ re-oxidation (charge-trap protection)

This requires careful optimization of plasma chemistry, temperature, ion energy, and post-etch cleaning protocols.

---

[Continue to Chapter 7: Layer-by-Layer Selectivity Control →](./07-layer-selectivity-feedback.md)
