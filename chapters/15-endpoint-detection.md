# Chapter 15: Endpoint Detection & Optical Monitoring

## Executive Summary

Detecting when each SiO₂ layer has been completely removed in a 60+ layer CTO stack requires sophisticated **optical endpoint detection** techniques. Traditional single-wavelength approaches fail at depth (light cannot penetrate 25-µm trenches), necessitating **multi-wavelength monitoring** (UV for top layers, IR for bottom) and **complementary electrical sensing** (capacitive monitoring). This chapter develops the optical physics of thin-film interference monitoring, the signal processing algorithms that extract endpoint from noisy optical data, and the integration of optical + electrical feedback into closed-loop process control. Special emphasis is placed on the **signal-to-noise challenge**: at extreme aspect ratios, reflected light intensity drops exponentially with depth, requiring amplification and sophisticated signal processing to extract meaningful endpoint signals.

## Multi-Wavelength Optical Endpoints

Reflectance at different wavelengths:
- **248 nm (UV, CaF₂ optics):** 1-2 µm penetration; top 10-20 layers
- **405 nm (blue):** 5-10 µm penetration; mid-depth
- **532 nm (green):** 10-30 µm penetration; deeper
- **850 nm (IR, Si detector):** 50+ µm penetration; very deep

Each wavelength provides endpoint signal for different depth ranges. Combined multi-wavelength analysis covers full 25-µm stack.

## Capacitive Impedance Monitoring

Parallel approach: monitor wafer-chuck impedance.
- Fresh stack: low C (thick insulator)
- As SiO₂ removed: C increases (thinner dielectric)
- Endpoint detected by C inflection point

Advantage: depth-independent (works for all layers)
Disadvantage: cannot distinguish SiO₂ from Si₃N₄ (both contribute to C)

## Algorithm: Combined Optical + Capacitive

Production recipe:
1. **Early layers (0-10 layers):** Use UV reflectance (bright signal)
2. **Mid layers (10-40 layers):** Switch to green/IR (brighter than UV at depth)
3. **Deep layers (40-64 layers):** Capacitive sensing as backup (UV/IR signal too weak)

Result: Reliable endpoint detection for all 60+ layers in stack.

