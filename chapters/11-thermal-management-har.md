# Chapter 11: Thermal Management in High-Aspect-Ratio Etch

## Executive Summary

High-aspect-ratio CTO etch of deep 25-µm pillars generates significant heat in confined spaces, creating extreme **temperature gradients** from the plasma-facing surface (70-100°C) to the pillar bottom (0-20°C), with gradients as steep as 10-20°C per micrometer. This chapter develops the detailed thermal physics of HAR-CTO etch: how heat is generated from plasma collisions and ion bombardment, how that heat conducts through narrow trenches and across insulating SiO₂/Si₃N₄ layers, and what thermal consequences arise for etch rate, selectivity, and oxide stability. Three primary thermal challenges are addressed: **(1) thermal gradients creating localized etch rate variations** (top hotter, etches faster; bottom cooler, etches slower—opposite to ARDE compensation needed), **(2) reactive species temperature dependence** leading to activation-energy-driven etch variations, and **(3) thermal-induced oxidation and stress** that can damage the charge-trap layer. The chapter concludes with practical thermal management strategies used in production: aggressive chuck cooling, thermal coatings on chamber walls, optimized gas injection patterns, and pulsed-RF techniques that reduce average power dissipation.

---

## Part 1: Heat Generation in Plasma Etching

### 1.1 Plasma Power and Heat Dissipation

#### Total RF Power Dissipation

**In typical CTO etch (100-500 W RF input):**

| Power Level | RF Input | Heat to Wafer | Heat to Walls |
|---|---|---|---|
| **100 W** | 100 W | 20-30 W | 70-80 W |
| **300 W** | 300 W | 80-120 W | 180-220 W |
| **500 W** | 500 W | 150-200 W | 300-350 W |

**Where does RF power go?**

1. **Ionization and excitation** (35-45%): Electrons gain energy, ionize gas molecules → remains as thermal energy in plasma
2. **Ion bombardment of wafer** (20-30%): Direct energy transfer to surface
3. **Ion bombardment of chamber** (15-25%): Electrode, walls, thermal loads
4. **Radiative losses** (5-10%): Photons escape chamber
5. **Inefficiencies** (5-10%): Reflected power, matching network losses

#### Heat Flux to Wafer

**At 300 W RF power → ~100 W to wafer:**

**Wafer area (300 mm): A = π(150)² = 70,650 mm² = 706.5 cm²**

$$\text{Heat flux} = \frac{100 \text{ W}}{706.5 \text{ cm}^2} = 0.14 \text{ W/cm}^2 = \mathbf{1400 \text{ mW/cm}^2}$$

**For comparison:**
- Summer sunlight on Earth: ~1000 mW/cm²
- CTO etch: **1.4× sunlight intensity!**
- **Result:** Intense heating of wafer surface

---

### 1.2 Heat Conduction Through CTO Stack

#### Thermal Conductivity of CTO Materials

| Material | Thermal Conductivity κ (W/m·K) | Relative to SiO₂ |
|---|---|---|
| **Silicon (bulk)** | 150 | 107× |
| **SiO₂** | 1.4 | 1× |
| **Si₃N₄** | 10-15 | 7-11× |
| **Fluorocarbon polymer** | 0.2-0.5 | 0.15-0.36× |

**Key insight:** CTO stack is **extremely insulating** (κ_SiO₂ = 1.4 W/m·K) → poor heat conduction to cool substrate below

#### Temperature Profile Through CTO Stack

**During CTO etch with 300 W RF, 150 W to wafer:**

```
Temperature vs. Depth in CTO Stack

T (°C)
^
| 80 ──────────  Surface (hot, plasma-facing)
|
| 60 ──────      Within top SiO₂ layers
|          \
| 40 ──────  \     Mid-depth (CTO layers)
|            \
| 20 ──────   \    Deep layers (cold)
|             \
|  0 ────────  \   Bottom (pillar core)
|_________________________> Depth (µm)
0             5       10      15      20
```

**Temperature gradient:** ~3-4°C per micrometer at top; ~1-2°C per micrometer at depth

#### Heat Conduction Calculation

**Using Fourier heat law:**

$$q = -\kappa \frac{dT}{dz}$$

**In CTO stack (κ ≈ 2 W/m·K average, accounting for 50/50 SiO₂/Si₃N₄):**

$$\text{Temperature gradient} = \frac{q}{\kappa} = \frac{1400 \text{ W/m}^2}{2 \text{ W/m·K}} = 700 \text{ K/m} = 7°C \text{ per µm}$$

**For 25 µm deep feature:**

$$\Delta T = 7°C/\mu m \times 25 \mu m = 175°C$$

**But wait—measured gradient is only 30-40°C, not 175°C. Why?**

**Answer:** The chuck cooling (liquid N₂ or chiller at -10°C) and larger-scale heat spreading in the chamber mean:
- **Effective heat sinking location:** Not at bottom of pillar, but at wafer back-side chuck
- **Effective stack thickness for thermal conduction:** Not 25 µm, but ~200 µm (including wafer substrate and chuck interface)
- **Revised gradient:** ΔT = (1400 W/m² × 0.2 m) / 2 W/m·K = 140 K... still high!

**Reality:** Active cooling dramatically reduces gradient; wafer is kept at ~0-20°C, limiting top gradient to ~30-50°C despite high power.

---

## Part 2: Thermal Effects on Etch Rate and Selectivity

### 2.1 Temperature Dependence of Etch Rate

#### Arrhenius Scaling (from Chapter 5)

**Etch rate follows Arrhenius behavior:**

$$R(T) = R_0 e^{-E_a / k_B T}$$

**With activation energy E_a ≈ 10-20 kJ/mol:**

**Temperature scaling (verified experimentally):**

| Temperature | Relative Etch Rate | Change Factor |
|---|---|---|
| **-10°C (263 K)** | 1.0× | Baseline |
| **+10°C (283 K)** | 1.7× | 70% faster |
| **+30°C (303 K)** | 2.8× | 180% faster |
| **+50°C (323 K)** | 4.5× | 350% faster |

**Rough rule of thumb:** Etch rate **doubles for every 10-15°C increase**

#### Thermal Gradient Effect on Uniformity

**In deep CTO trench with thermal gradient (top hot, bottom cool):**

```
Depth      Temperature    Etch Rate
(µm)       (°C)           (nm/min)

0-2 µm     +40°C          300 nm/min (hot, fast)
5-10 µm    +25°C          200 nm/min
10-15 µm   +15°C          140 nm/min
20-25 µm   +5°C           100 nm/min  (cool, slow)
```

**Etch rate ratio (top/bottom): 300/100 = 3:1** (due to thermal gradient alone)

**This is **opposite** to ARDE compensation needed!**
- ARDE wants to speed up bottom to compensate for radical starvation
- Thermal gradient wants to slow down bottom (it's already cool)
- **Competing effects make recipe optimization difficult**

---

### 2.2 Selectivity Changes with Temperature

#### SiO₂ vs. Si₃N₄ Temperature Scaling

**Both materials have temperature-dependent etch rates, but with slightly different activation energies:**

| Material | E_a (kJ/mol) | Scaling per 10°C |
|---|---|---|
| **SiO₂** | 15 | ~1.6× |
| **Si₃N₄** | 18 | ~1.5× |

**Result:** E_a values **similar**, so selectivity is relatively **stable** to temperature changes

**Selectivity SiO₂/Si₃N₄ vs. temperature:**

| Temperature | Selectivity |
|---|---|
| **-10°C** | 5.2:1 |
| **+10°C** | 5.1:1 |
| **+30°C** | 5.0:1 |
| **+50°C** | 4.9:1 |

**Conclusion:** Temperature changes **minimally affect selectivity** (unlike etch rate)

---

## Part 3: Thermal Stress and Oxide Integrity

### 3.1 Thermal Expansion Mismatches

#### CTE (Coefficient of Thermal Expansion) Differences

| Material | CTE (ppm/K) |
|---|---|
| **Silicon** | 2.6 |
| **SiO₂** | 0.5 |
| **Si₃N₄** | 3.0-3.5 |

**During etch (temperature rises from -10°C to +40°C, ΔT = 50 K):**

**Linear expansion:**
- Silicon: ΔL/L = 2.6 × 10⁻⁶ × 50 = 1.3 × 10⁻⁴ = 0.013%
- SiO₂: ΔL/L = 0.5 × 10⁻⁶ × 50 = 2.5 × 10⁻⁵ = 0.0025%
- **Differential:** Si expands ~5× more than SiO₂

**Thermal stress at Si-SiO₂ interface:**

$$\sigma_{thermal} = E \times \Delta \epsilon = E \times (CTE_{Si} - CTE_{SiO_2}) \times \Delta T$$

**Where E_Si ≈ 170 GPa:**

$$\sigma = 170 \text{ GPa} \times (2.1 \times 10^{-5}) \times 50 \text{ K} = \mathbf{180 \text{ MPa}}$$

**Consequence:** Thermal stress **comparable to or exceeding** mechanical stress in CTO layers

#### Oxide Cracking Risk

**SiO₂ fracture strength:** ~50-100 MPa (in thin films)

**Thermal stress:** 180 MPa (calculated above)

**Risk:** Thermal stress can **exceed fracture strength**, creating microcracks in oxide

**If oxide cracks during etch:**
- Leakage current increases
- Charge-trap protection compromised
- Device failure possible

---

### 3.2 Thermal Oxidation During In-Situ Cleaning

#### Re-oxidation at Elevated Temperature

**During post-etch in-situ cleaning (O₂ plasma at 25-50°C):**

**Oxidation rate of Si₃N₄ (from Chapter 6):**

$$R_{oxidation} = R_0 e^{-E_a^{ox} / k_B T}$$

**With E_a^ox ≈ 2.5-3.0 eV:**

| Temperature | Oxidation Rate |
|---|---|
| **+10°C** | 0.5 nm/min |
| **+25°C** | 1.5 nm/min |
| **+50°C** | 5 nm/min |

**Over a 5-minute clean:**
- At +10°C: 2.5 nm oxide forms (acceptable)
- At +50°C: 25 nm oxide forms (**dangerous**, too thick)

**Result:** Thermal management during cleaning is **critical** to prevent charge-trap oxidation

---

## Part 4: Thermal Management Strategies

### 4.1 Chuck Cooling and Temperature Control

#### Liquid-Cooled Electrode Chuck

**Typical production chamber setup:**

```
Plasma
  ↓ (100-300 W RF)
   ═════════════════════  Powered electrode
   |  300mm Wafer        |
   |  (heated by plasma) |
   ═════════════════════
   |   Aluminum chuck    |  Actively cooled
   | (with cooling lines)|  via liquid chiller
   ═════════════════════
   |  Liquid N₂ or       |
   | -10°C chiller       |
```

**Cooling capacity:** 10-50 kW (for large production chambers)

**Target wafer temperature:** -10 to +20°C (tunable)

#### Temperature Uniformity Across Wafer

**In ideal scenario (with active cooling):**
- Center of wafer: 0°C (closest to chuck)
- Edge of wafer: +15-20°C (farther from chuck, more plasma heating)
- **Radial temperature variation:** ~20°C

**Consequence:** Etch rate varies radially (center ~2× faster than edge)

**Mitigation:** 
- Adjust gas flow patterns (higher flow at edge → cooler edge)
- RF power distribution (asymmetric to preferentially heat edge)
- Multiple cooling zones in chuck

---

### 4.2 Pulsed-RF Power for Thermal Control

#### Power Pulsing Reduces Peak Temperature

**Continuous RF power:**
- Average power: 300 W
- Peak temperature rise: +40°C

**Pulsed RF power (30 sec on / 10 sec off):**
- Average power: 300 W × (30/(30+10)) = 225 W
- Peak temperature rise: +30°C (lower due to thermal dissipation during off-time)
- **Benefit:** 10°C cooler

**More aggressive pulsing (20 sec on / 20 sec off):**
- Average power: 300 W × (20/40) = 150 W
- Peak temperature: +20°C
- **Tradeoff:** Lower average power → slower etch rate (mitigated by optimization)

#### Thermal Transient Timescale

**Wafer thermal time constant (RC-like):**

$$\tau_{thermal} = \frac{C_{wafer}}{h \times A}$$

Where:
- C_wafer = heat capacity of wafer (~1000 J/K)
- h = heat transfer coefficient (chuck + conduction; ~100 W/m²·K effective)
- A = wafer area (~0.07 m²)
- τ ≈ 140 seconds

**Consequence:** Wafer temperature changes **slowly** (100+ second timescale)

**Pulsing benefit:** If pulse period << τ_thermal, pulsed power averages out smoothly, reducing peak temperature without inducing rapid oscillations

---

### 4.3 Thermal Management in Three-Phase Recipe

#### Temperature Targets by Phase

**Modern production recipe with thermal optimization:**

| Phase | Duration | Avg Power | Target T | Selectivity | Etch Rate |
|---|---|---|---|---|---|
| **1 (top)** | 0-3 min | 200 W | -5°C | 10:1 | 100 nm/min |
| **2 (mid)** | 3-12 min | 280 W | +10°C | 5-6:1 | 180 nm/min |
| **3 (deep)** | 12-20 min | 300 W | +20°C | 4-5:1 | 250 nm/min |

**Rationale:**
- Phase 1: Cold (high selectivity priority) → reduce power, cool chuck aggressively
- Phase 2: Moderate warmth (balance) → increase power, allow slight temperature rise
- Phase 3: Warmer (etch rate priority, depth less critical for selectivity) → higher power, accept +20°C

**Net result:** Temperature-induced etch rate variation ≈ 30% (manageable with optical feedback)

---

## Summary: Thermal Management in HAR-CTO Etch

| Thermal Issue | Magnitude | Impact | Mitigation |
|---|---|---|---|
| **Heat flux to wafer** | 1400 mW/cm² (1.4× sunlight) | Significant heating | Active chuck cooling |
| **Thermal gradient (top-bottom)** | 30-50°C across 25 µm | Etch rate nonuniformity | Pulsed RF, optimized gas flow |
| **Etch rate temperature scaling** | 2-3× per 20°C | Selectivity maintained, rate varies | Multi-phase recipe with temperature targets |
| **Thermal stress at Si-SiO₂** | ~180 MPa (near fracture) | Oxide cracking risk | Keep T < +50°C; minimize stress cycles |
| **Re-oxidation during cleaning** | 5 nm/min at +50°C | Charge-trap protection loss | Cool to <20°C before cleaning |
| **Wafer thermal time constant** | ~140 seconds | Slow temperature response | Pulsing helpful only if period << 140 s |

**Key Design Principle:** Thermal management is a **primary constraint** on 3D NAND CTO etch recipe design. Every process parameter (power, pressure, gas composition) has both plasma-chemistry and thermal consequences. Production recipes carefully balance these: achieving adequate etch rate and selectivity while keeping wafer temperature in safe range (-10 to +30°C) to avoid thermal damage, stress cracking, or unwanted oxidation.

---

[Continue to Chapter 12: Residue Neutralization & In-Situ Cleaning →](./12-residue-neutralization.md)
