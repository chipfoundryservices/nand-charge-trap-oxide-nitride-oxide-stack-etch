# Chapter 1: Introduction to 3D NAND Architecture & CTO Layer Stack

## Executive Summary

Three-dimensional NAND flash memory represents the most significant architectural innovation in semiconductor memory since the floating-gate transistor. By stacking transistor layers vertically rather than expanding horizontally, 3D NAND overcomes the area-scaling limitations that plagued 2D planar NAND at the 15-nm node and below. The charge-trap-oxide (CTO) stack—a multilayer dielectric structure of alternating silicon dioxide and silicon nitride—is the enabling technology for this vertical scaling. This chapter establishes the architectural context for CTO etch: why the CTO stack exists, how it differs from floating-gate memory, what etch challenges it presents, and how CTO etch integrates into the broader 3D NAND manufacturing flow. Readers will gain understanding of the physical structure of 3D NAND, the rationale for the CTO stack composition, the etch sequences required to form vertical strings and define gate segments, and the critical success factors that make CTO etch a central technology differentiator for NAND manufacturers.

---

## Part 1: From Floating-Gate to Charge-Trap Flash

### 1.1 The Floating-Gate Transistor (FG-NAND)

#### Historical Context
Floating-gate (FG) NAND emerged in the 1980s as the dominant NAND flash architecture, achieving commercial scale in the 1990s and scaling to the 40-nm node by 2010. The FG cell is conceptually simple:

- **Two coupled gates:** A "floating gate" (FG, electrically isolated) and a "control gate" (CG, connected to word line)
- **Oxide sandwich:** Thin tunneling oxide (5-10 nm) between FG and silicon channel, thicker control oxide (10-20 nm) between FG and CG
- **Charge storage:** Electrons injected onto FG via Fowler-Nordheim (FN) tunneling; persist due to oxide insulation

#### Scaling Success
FG NAND scaled magnificently:

| Technology Node | Year | Linewidth | Layers | Key Achievement |
|---|---|---|---|---|
| 1 µm | 1989 | 1000 nm | 1 | First FG production |
| 500 nm | 1995 | 500 nm | 1 | Mainstream NAND |
| 90 nm | 2004 | 90 nm | 1 | 1 Gbit+ density |
| 40 nm | 2010 | 40 nm | 1 | 2D NAND scaling limit |
| 15 nm | 2014 | 15 nm | 1 | Last generation 2D NAND |

The scaling path relied on:
1. **Lithography shrinkage** (photolithography improvements from 365 nm to ArF 193 nm)
2. **Oxide thickness control** (gate oxide remained 7-10 nm for charge confinement)
3. **Cell architecture optimization** (split-gate to shared-gate, string architecture)

#### Fundamental Limits: Why FG Stops at 15nm

Two physical limits constrain further FG scaling:

**Limit 1: Tunneling Oxide Thickness**

The tunneling oxide cannot be scaled thinner without incurring unacceptable charge leakage. Consider:

- **Fowler-Nordheim (FN) tunneling probability:** Scales exponentially with oxide thickness: $P_{FN} \propto e^{-2\sqrt{2m^*}\phi^{3/2}t_{ox}/3\hbar eE}$
  - φ = barrier height (~3.1 eV for SiO₂)
  - t_ox = oxide thickness
  - E = electric field

- **Charge retention requirement:** 10-year retention (typical NAND spec) requires <1 bit error per 10^12 cycles
  - Leak time constant: τ ∝ e^{2\sqrt{...}t_{ox}}
  - Scaling t_ox by 1 nm increases leak current by ~10×

**At 15 nm node:**
- Tunneling oxide: ~6-8 nm (minimum achievable)
- 10-year retention becomes marginal without temperature reduction or charge re-equilibration schemes
- **Result:** Further thickness reduction unacceptable

**Limit 2: Gate-to-Gate Capacitive Coupling**

As linewidth shrinks, neighboring floating gates couple capacitively. The coupling ratio C_couple/C_total increases, making cell programming and sensing unreliable:

$$C_{couple} = \frac{\epsilon_0 \epsilon_r A}{t_{inter}}$$

Where t_inter is inter-cell spacing. At 15 nm, t_inter ≈ 20-30 nm, and coupling becomes significant.

---

### 1.2 Introduction to Charge-Trap Flash (CTF)

#### Core Concept

Charge-Trap Flash (CTF) replaces the discrete floating gate with a **distributed trap layer**—silicon nitride (Si₃N₄) embedded within the gate dielectric stack. Electrons are trapped directly within the nitride's band gap states rather than on an isolated conductor.

**CTO Stack (Typical Modern 3D NAND):**

```
Word Line (Polysilicon)
    ↓
Blocking Oxide (SiO₂, ~8 nm)
    ↓
Charge-Trap Layer (Si₃N₄, ~6 nm) ← ELECTRONS STORED HERE
    ↓
Tunneling Oxide (SiO₂, ~6 nm)
    ↓
Silicon Channel (pillar)
```

#### Why Charge-Trap is Superior for Scaling

**Advantage 1: Oxide Thickness Decoupling**

In FG cells, the tunneling oxide must be thin (for fast programming) yet thick enough to retain charge. These requirements compete. In CTF:
- Tunneling oxide thickness optimized for electron injection kinetics, not charge confinement
- Charge retention depends on trap state energy depth in Si₃N₄, not on oxide barrier thickness
- Result: **Thinner oxides become possible** → smaller vertical footprint → better density

**Advantage 2: Distributed Charge Storage**

Floating gates store charge on a discrete, isolated conductor. A single leakage path can cause catastrophic charge loss. Charge-trap stores electrons **throughout the Si₃N₄ layer**:

```
Floating-Gate Model:
    FG Conductor (isolated):  ████████ ← ALL CHARGE HERE
    Oxide:                     ░░░░░░░░
    
Charge-Trap Model:
    Si₃N₄ layer:              • • • • • • ← CHARGE DISTRIBUTED
    Oxide:                     ░ ░ ░ ░ ░
```

**Consequence:** Loss of a single trap site (1 electron) affects total charge by only 1/N, where N = total trap density (~10^12-10^13 traps/cm²). Charge loss is gradual and recoverable with periodic refresh, not catastrophic.

**Advantage 3: Scalability to Extreme Feature Sizes**

Charge-trap materials are inherently less sensitive to:
- Defects in the trap layer
- Small variations in oxide thickness (±10% thickness variation acceptable; FG would require ±5%)
- Coupling to neighbors (distributed trap density less sensitive to neighbor interference)

**Result:** 3D NAND feature scaling becomes possible to extreme aspect ratios and tight spacing.

**Advantage 4: Temperature Stability**

Trap states in Si₃N₄ are deeper than FG charge loss mechanisms in oxide, enabling:
- Higher operating temperatures (100°C+ vs. 70°C FG limit)
- Better high-temp data retention
- Reduced need for charge refresh cycles

---

## Part 2: 3D NAND Architecture

### 2.1 Planar vs. 3D: The Vertical Scaling Transition

#### Planar (2D) NAND Scaling Limits

2D planar NAND scaled horizontally: shrinking linewidth to increase bit density. By 2010:

- **Area per cell:** 50 nm × 50 nm (2D NAND at 40 nm node) = 2500 nm²/cell
- **Cell cost:** Decreasing with node progression (lithography improves)
- **Scaling path:** Well-understood—continue shrinking linewidth

**However, fundamental limits emerged:**

1. **Lithography Cost:** Extreme UV (EUV) lithography, required below 15 nm, was expensive and low-yield
2. **Process Complexity:** Managing isolation between closely spaced floating gates became difficult
3. **Bit Cost:** At 15 nm, bit cost stopped decreasing as lithography costs exploded
4. **Device Density Plateau:** 2D NAND stalled at ~1 Tb/cm² (40-50 billion transistors per die)

**Result by 2015:** NAND manufacturers collectively abandoned 2D NAND scaling and pivoted to 3D NAND.

#### 3D NAND: Vertical Scaling

3D NAND stacks transistor layers vertically:

**Density Improvement:**
- 32-layer 3D NAND (2013): ~32× more transistors per die than 2D at same linewidth
- 64-layer 3D NAND (2015): ~64× more transistors
- Modern 3D NAND (2024): 176-232 layers reported by major manufacturers
- **Result:** ~176-232× bit density increase from vertical stacking alone

**Key Insight:** A 232-layer 3D NAND with 50 nm minimum linewidth (same as 2D NAND at 15 nm) achieves:
- **Cell area:** 50 nm × 50 nm × 1 (single physical layer in 2D sense) × 232 (layers) = equivalent area
- **Bit cost:** ↓↓ (no extreme lithography, mature 50 nm tools sufficient)
- **Density:** ↑↑ (232× from vertical stacking)

**Result:** Economics improved dramatically, and NAND bit cost decreased for the first time since 2D scaling plateaued.

### 2.2 3D NAND String Architecture

#### Vertical String Concept

A 3D NAND string is a **vertical stack of transistors** connected in series, with one transistor per layer. Each layer has its own gate (control gate).

**Schematic (Simplified, 4-layer example):**

```
      BL (Bit Line, vertical pillar)
         ↓
    ╔════════════╗
    ║ Layer 4    ║
    ║ CG4, TR4   ║  ← Transistor 4
    ╚════════════╝
         │ (channel connection)
    ╔════════════╗
    ║ Layer 3    ║
    ║ CG3, TR3   ║  ← Transistor 3
    ╚════════════╝
         │
    ╔════════════╗
    ║ Layer 2    ║
    ║ CG2, TR2   ║  ← Transistor 2
    ╚════════════╝
         │
    ╔════════════╗
    ║ Layer 1    ║
    ║ CG1, TR1   ║  ← Transistor 1
    ╚════════════╝
         │
        SL (Source Line)
```

**Key elements:**

- **Bit Line (BL):** Vertical silicon pillar (channel)
- **Source Line (SL):** Connection to source at base
- **Control Gates (CG1-CG4):** Horizontal gate structures encircling the pillar
- **Inter-layer Spacing:** Insulation between gates (spacing layers of dielectric)
- **Gate Stack:** Multi-layer CTO dielectric beneath each gate (enables charge storage)

#### Gate Stack and CTO Placement

Each control gate sits atop a **gate stack** that includes the CTO layers:

```
CG4 (Polysilicon)
────────────────── ← Metal interconnect
CTO4 (SiO₂/Si₃N₄/SiO₂)  ← Charge-trap stack for CG4 transistor
────────────────── ← Spacing layer (SiO₂)
CG3 (Polysilicon)
────────────────── ← Metal interconnect
CTO3 (SiO₂/Si₃N₄/SiO₂)  ← Charge-trap stack for CG3 transistor
────────────────── ← Spacing layer (SiO₂)
... and so on
```

**Vertical stack composition (for 64-layer NAND):**

| Layer | Thickness | Repeat | Total |
|-------|-----------|--------|-------|
| Gate (polysilicon) | 50 nm | 64 | 3.2 µm |
| CTO stack | 20 nm | 64 | 1.3 µm |
| Spacing layer | 10 nm | 64 | 0.64 µm |
| **Total height** | — | — | **~5-8 µm** |

**Total trench depth for string formation:** 5-8 µm (64 layers) to 20-40 µm (232 layers in advanced 3D NAND)

---

### 2.3 CTO Stack Composition Details

#### Layer-by-Layer Breakdown

The CTO stack repeats vertically 64+ times. Each CTO unit (20 nm thick) consists of:

```
Blocking Oxide Layer (BO)
  Material: SiO₂ (silicon dioxide)
  Thickness: ~8-10 nm
  Function: Prevents charge leakage to gate (high resistance to tunneling)
  Quality: High-density, high-purity oxide
  
Charge-Trap Layer (CT)
  Material: Si₃N₄ (silicon nitride)
  Thickness: ~5-8 nm
  Function: Hosts trapped electrons; trap state density ~10^12-10^13 traps/cm²
  Quality: Stoichiometric nitride; defect-free preferred
  
Tunneling Oxide Layer (TU)
  Material: SiO₂ (silicon dioxide)
  Thickness: ~5-7 nm
  Function: Electron injection/removal via FN tunneling; controls programming speed
  Quality: Ultra-thin, high-quality oxide for controlled tunneling
```

#### Selectivity Requirements During CTO Etch

When etching the CTO stack vertically:

1. **Etch SiO₂ layers selectively** to eventually expose Si₃N₄
   - SiO₂ must etch faster than Si₃N₄ in classical recipes
   - But cannot over-etch into underlying Si₃N₄ (charge-trap layer)
   - Selectivity required: SiO₂/Si₃N₄ ≥ 3:1 minimum

2. **Control layer erosion precision**
   - Each SiO₂ layer is only 8-10 nm thick
   - Variation in etch depth across 300mm wafer must be <1-2 nm (±10-20% target)
   - Deep in the trench (50+ µm down), etch rate slowing due to ARDE
   - Bottom layers must etch at same rate as top layers → severe uniformity challenge

3. **Stop-on-Si₃N₄ layer** (for intermediate etches)
   - Some processes require etching SiO₂ while stopping on Si₃N₄
   - Selectivity SiO₂/Si₃N₄ must be >5:1 to guarantee no Si₃N₄ erosion
   - But selectivity too high risks under-etch of final SiO₂ layer

---

## Part 3: Manufacturing Sequences and Etch Role

### 3.1 Simplified 3D NAND Flow

**Step 1: Blanket Deposition**
- Alternate deposition of SiO₂ and Si₃N₄ layers
- 64+ repeats for 64-layer NAND
- Final stack height: 5-8 µm
- Total deposited material: SiO₂ + Si₃N₄ + spacing layers

**Step 2: Lithography**
- Photoresist patterning for pillar locations
- Typical pillar diameter: 30-50 nm
- Pillar pitch: 60-100 nm (distance between pillar centers)

**Step 3: Deep Trench Etch (VERTICAL PILLAR FORMATION)**
- **Purpose:** Etch through all 64 CTO stack layers + all spacing layers
- **Depth:** 5-8 µm (for 64 layers)
- **Linewidth:** 30-50 nm
- **Aspect Ratio:** 100:1 to 250:1
- **Challenge:** CTO stack etch dominates this step; extremely high aspect ratio requires HAR-specific chemistry and chamber design
- **Duration:** 15-30 minutes (long etch times = significant thermal load on chamber)

**Step 4: Spacer Formation (Optional)**
- Deposition of thin spacer layer (Si₃N₄ or SiO₂)
- Etch-back to create spacers on pillar walls
- Function: Isolate adjacent gates

**Step 5: Channel Deposition**
- Epitaxial or polycrystalline silicon deposition into pillar core
- Fills remaining pillar volume after gate stack formation

**Step 6: Additional Etch Sequences**
- Removal of specific oxide/nitride layers for gate segmentation
- Further CTO etch to define gate boundaries (horizontal etch sequences)

### 3.2 Why CTO Etch is the Bottleneck

CTO etch is the manufacturing step that **most critically defines 3D NAND success metrics:**

| Metric | Requirement | Impact if Failed |
|--------|-------------|------------------|
| **Selectivity** | SiO₂/Si₃N₄ > 3:1 | Over-etch damages charge-trap layer; charge loss; read errors |
| **Uniformity** | ±5% etch depth across 300mm | Top-layer transistors vs. bottom-layer transistors have different characteristics; yield loss |
| **Residue Control** | <100 nm particle size | Residue bridges between pillars; shorts strings; device failure |
| **Etch Duration** | <20 minutes target | Thermal transients; chamber wall temperature drift; repeatability loss |
| **Aspect Ratio Capability** | Support 100:1+ AR | Inability to etch deep pillars → cannot achieve high layer count → density loss |

**Bottom line:** A single 10% selectivity loss during CTO etch can destroy the charge-trap layer, rendering the entire wafer non-functional. CTO etch process window and tool reliability are first-order manufacturing constraints.

---

## Part 4: CTO Etch Integration into the Semiconductor Supply Chain

### 4.1 CTO Etch Tool Requirements

CTO etch is **not** a standard etch tool application. Compared to conventional polysilicon or dielectric etch:

- **Plasma source:** ICP (Inductive Coupling Plasma) preferred over CCP for extreme aspect ratios (ion flux control critical)
- **Chamber pressure:** Lower pressure (20-50 mTorr vs. 100+ mTorr for standard etch) for radical diffusion into deep features
- **RF power:** Higher RF density (100-500 W) to sustain plasma at low pressure
- **Thermal load:** High thermal dissipation required (CTO etch generates 500+ W in 200 mm chamber)
- **Process chamber:** Dedicated chamber (not shared with other etch types) to avoid contamination
- **Cost:** ~$5-8 million USD per chamber (premium vs. standard etch tools)

### 4.2 Equipment Suppliers and Competitive Landscape

**Major suppliers of 3D NAND CTO etch tools:**

| Supplier | Primary Customers | Technology Advantages |
|----------|-------------------|----------------------|
| Lam Research | Samsung, SK Hynix, Micron | HAR-ADE compensation, dual-frequency RF |
| Applied Materials | Intel, KIOXIA | Thermal management, residue control |
| Tokyo Electron | Micron, manufacturers | Chamber uniformity |

**Competitive factors:**
- HAR-ADE uniformity (±3-5% across wafer)
- Selectivity stability (±2% over 100-wafer batch)
- Endpoint detection accuracy in deep trenches
- Residue removal effectiveness (in-situ clean efficacy)

---

## Summary: From Architecture to Etch Challenge

| Aspect | Impact on CTO Etch |
|--------|------------------|
| **64+ layer stack** | Each layer must be etched sequentially with precision; selectivity maintained over hours of etch time |
| **Vertical pillar formation (5-8 µm depth)** | Extreme aspect ratios demand specialized plasma chemistry and chamber design |
| **Charge-trap layer (Si₃N₄)** | Cannot be over-etched; selectivity failure = device failure |
| **Tight pitch (30-50 nm)** | Gas diffusion limited in confined spaces; uniformity challenges |
| **High-temperature operation** | Residue neutralization requires precise thermal control |

**Result:** CTO etch is a specialized, high-value, high-complexity process that represents significant technology differentiation in 3D NAND manufacturing.

---

## Conclusion

The transition from floating-gate to charge-trap flash, and from 2D to 3D NAND, fundamentally changed the economics of NAND memory. 3D NAND architecture trades horizontal scaling complexity for vertical stacking simplicity, but this simplicity comes with new etch challenges. The CTO stack—repeated 64+ times vertically—demands plasma etch processes that simultaneously achieve layer-by-layer selectivity, extreme aspect ratio capability, and residue control. Understanding these architectural constraints is the foundation for understanding why CTO etch technology matters and why it commands significant engineering resources and capital investment in NAND manufacturing.

The chapters that follow develop the chemistry, plasma physics, chamber design, and manufacturing integration required to master CTO etch.

---

[Continue to Chapter 2: Silicon Oxide Properties & Thermal Oxidation Kinetics →](./02-silicon-oxide-properties.md)
