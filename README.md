# LW-PLA Delta UAV — Version 1

**A 3D-printed, modular fixed-wing UAV platform. Designed as the foundation for a progressively autonomous aerial system.**

![Status](https://img.shields.io/badge/status-in%20development-orange)
![Version](https://img.shields.io/badge/version-1.0-blue)
![Stage](https://img.shields.io/badge/stage-manufacturing%20prep-yellow)

<p align="center">
  <img src="CAD/Isometric%20View.png" alt="Isometric view of the LW-PLA delta wing UAV" width="850"/>
</p>

> **Project status:** Version 1 is currently in the design-validation and manufacturing-preparation phase. The airframe design, 2D aerodynamic analysis, and CG/stability calculations are complete. Printing, assembly, and flight testing are the next milestones. This README doubles as the live project plan — sections marked 🔄 or 🔜 are actively being worked on or planned.

---

## Mission

Version 1 is not about maximum performance — it is about **validating everything at once**: the airframe geometry, the LW-PLA manufacturing process, the propulsion system, the control architecture, and the systems integration needed for future autonomy. Every design decision was made with a systems-engineering mindset rather than a purely aerodynamic one, so that later versions can add autonomous navigation, onboard perception, and target tracking **without redesigning the aircraft**.

The long-term goal: a compact, fast, rapidly manufacturable UAV that serves as a research platform for autonomous guidance, embedded computing, and computer vision — with a human always in the loop.

---

## Why LW-PLA?

Lightweight foaming PLA expands during printing, producing parts at roughly half the density of standard PLA — light enough for a flying airframe while still printable on a consumer machine. It allows complex aerodynamic geometry that would be impractical to build from foam board or costly in composites, and any damaged section can be reprinted in hours for pennies. For an iterative test platform, that trade — some stiffness (recovered with carbon-fiber spars) in exchange for weight, geometric freedom, and near-instant repairability — is exactly the right one.

---

## Design at a Glance

<p align="center">
  <img src="CAD/Top%20view.png" alt="Top view" width="420"/>
  <img src="CAD/Side%20view.png" alt="Side view" width="420"/>
</p>

| Parameter | Value |
|---|---|
| Configuration | Tailless tapered delta (flying wing) |
| Wingspan | ~850 mm |
| Airfoil | MH60 (full span, single incidence) |
| Reference area | 219,160 mm² |
| Mean aerodynamic chord (MAC) | 275.19 mm |
| Wing aerodynamic centre | 245.51 mm |
| First-flight CG range | 273–287 mm |
| Control surfaces | Elevons only |
| Stabilizers | Dual fixed vertical fins (yaw stability + prop protection on belly landings) |
| Propulsion | 2× A2807 1700 KV brushless, rear-mounted |
| Battery | 6S 3000 mAh LiPo |
| Flight controller | SpeedyBee F405 Wing |
| Radio link | ExpressLRS (ELRS) |
| Primary structure | Lightweight foaming PLA (LW-PLA) + carbon-fiber spars |
| Launch method (V1) | Hand launch |

---

## Aerodynamic Analysis ✅

Two interactive analysis reports are published via GitHub Pages:

### 📊 [2D Aerodynamic Report — MH60 Airfoil (XFOIL)](https://morakah-hub.github.io/LWPLA-Aircraft/Calculations/2D_Aerodynamic_analysis_%28XFOIL%29.html)

XFOIL 6.99 polar study of the MH60 section at **Re = 200k, 300k, and 400k** (Mach 0, Ncrit 9), covering the hand-launch, cruise, and high-speed flight regimes.

Key results:

| Metric | Value |
|---|---|
| Peak L/D @ Re 200k | 61.9 (α = 6.5°) |
| Peak L/D @ Re 300k | 70.8 (α = 6.0°) |
| Peak L/D @ Re 400k | 77.7 (α = 6.0°) |
| CLmax @ Re 400k | 1.22 (α = 12°) |

### 📐 [Wing MAC & Aerodynamic Centre Analysis](https://morakah-hub.github.io/LWPLA-Aircraft/Calculations/mac_analysis.html)

Full-lifting-surface MAC derivation, aerodynamic centre location, and the first-flight CG envelope for the tailless configuration. Because the aircraft has no horizontal tail, CG placement relative to the wing AC is the single most safety-critical number for first flight — this report documents exactly how the 273–287 mm range was derived.

<p align="center">
  <img src="Calculations/CG_mass_properties.png" alt="CG location from Onshape mass properties" width="850"/>
</p>

*CG location verified in CAD using Onshape mass properties — the modeled centre of gravity is checked directly against the calculated 273–287 mm first-flight envelope before anything is printed.*

---

## Airframe & CAD ✅

The complete airframe is modeled for additive manufacturing, with the internal layout organized around a modular electronics bay sized for future avionics (companion computer, GPS, airspeed sensor, camera) from day one.

<p align="center">
  <img src="CAD/Exploded%20view.png" alt="Exploded view showing modular airframe sections" width="850"/>
</p>

*Exploded view — the airframe splits into printable sections joined by carbon-fiber spars, so damaged components can be reprinted and replaced individually rather than rebuilding the aircraft.*

<p align="center">
  <img src="CAD/Transparent%20view.png" alt="Transparent view showing internal layout" width="850"/>
</p>

*Transparent view — internal volume reserved for the flight controller, ESCs, 6S battery, and future companion computing hardware. Autonomy is designed in, not bolted on.*

📄 Full engineering drawing: [`CAD/Drawing.pdf`](CAD/Drawing.pdf)

**Design philosophy highlights:**
- **LW-PLA everywhere possible** — foaming PLA cuts structural mass dramatically while allowing complex aerodynamic geometry on a consumer printer.
- **Engineering plastics where it matters** — motor mounts and high-stress joints will be printed in stronger materials.
- **Repairability as a feature** — any section of the aircraft can be reprinted in hours, which fundamentally changes the risk calculus for flight testing.

---

## Manufacturing 🔄 *(in progress)*

Print-profile development and fabrication of the first airframe. LW-PLA is notoriously sensitive to temperature, flow rate, and foaming ratio, so this phase includes:

- [ ] LW-PLA foaming calibration (flow %, temperature towers, density tuning)
- [ ] Test prints of wing sections — surface quality vs. weight trade study
- [ ] Spar integration and bonding method validation
- [ ] Motor mount prints in engineering plastic
- [ ] Full airframe print + assembly
- [ ] **Weight & balance report** — as-built mass budget vs. design estimates, and final CG verification against the [calculated envelope](https://morakah-hub.github.io/LWPLA-Aircraft/Calculations/mac_analysis.html)

📁 Documentation will live in [`/Manufacturing`](Manufacturing) — *coming soon.*

---

## Avionics 🔜 *(coming soon)*

Full documentation of the electronics architecture — treated as its own subsystem rather than an afterthought:

- **System wiring diagram** — SpeedyBee F405 Wing, dual ESCs, ELRS receiver, servos
- **Power budget** — 6S main bus, regulated rails, and headroom reserved for the future companion computer (Raspberry Pi), GPS, airspeed sensor, and camera
- **Bench-test results** — servo/elevon calibration, motor direction and failsafe verification before the airframe ever leaves the ground

📁 Diagrams and documentation will live in [`/Avionics`](Avionics) — *coming soon.*

---

## Flight Testing 🔜 *(planned)*

Structured, incremental test campaign. Manual RC control remains the safety backbone throughout.

**Planned test sequence:**
1. **Ground tests** — control surface checks, motor/ESC thrust verification, failsafe validation, range test
2. **Glide/trim tests** — hand-launch glides to verify CG placement and elevon trim
3. **First powered flight** — stability, control authority, trim documentation
4. **Envelope expansion** — speed runs, stall characterization, turn performance
5. **Data-logged flights** — flight-controller blackbox review, comparing real performance against the XFOIL predictions

📁 Flight logs, blackbox data, and video will live in [`/Flight-Tests`](Flight-Tests) — *coming soon.*

---

## Roadmap

### Version 1 — *Foundation* (current)
| Milestone | Status |
|---|---|
| Concept & configuration selection | ✅ Complete |
| CAD design | ✅ Complete |
| 2D aerodynamic analysis (XFOIL) | ✅ Complete |
| MAC / CG / stability calculations | ✅ Complete |
| 3D CFD analysis — will validate the full 3D flow field and directly inform design decisions for future versions | 🔜 Planned |
| LW-PLA print calibration | 🔄 In progress |
| Airframe manufacturing | 🔜 Planned |
| Avionics integration & bench testing | 🔜 Planned |
| Ground testing | 🔜 Planned |
| First flight | 🔜 Planned |
| Flight test campaign & report | 🔜 Planned |

### Version 2+ — *Toward Autonomy*
- **Assisted stabilization → autonomous waypoint navigation** (GPS + airspeed sensor integration)
- **Companion computer integration** (Raspberry Pi — volume, power, and cooling already reserved in V1)
- **Onboard camera + computer vision** — perception, and eventually detection/tracking of dynamic aerial objects
- **Portable launch station** — repeatable launches, reduced operator workload
- **Propulsion optimization** — thrust stand data, efficiency mapping

---

## Repository Structure

```
LWPLA-Aircraft/
├── CAD/                  ✅ Airframe model, engineering drawing, rendered views
├── Calculations/         ✅ XFOIL 2D analysis + MAC/CG reports (GitHub Pages)
├── Manufacturing/        🔄 Print profiles, build log, weight & balance
├── Avionics/             🔜 Wiring diagram, power budget, bench tests
├── Flight-Tests/         🔜 Test cards, blackbox logs, flight video
├── Images/               📷 Build and flight photography
└── README.md
```

---

## About

Designed and built by **Mohamed-Essadak Rakah** — Mechanical Engineering @ UMass Amherst.

This project integrates mechanical design, additive manufacturing, aerodynamics, embedded systems, and (eventually) autonomous robotics into a single evolving research vehicle. Each iteration keeps what worked, fixes what didn't, and documents both.

📫 [mrakah@umass.edu](mailto:mrakah@umass.edu) · [GitHub Profile](https://github.com/morakah-hub)
