# Strain Wave Interference Logic (SWIL) Simulation

This repository contains LTspice electrical-equivalent simulations of **Strain Wave Interference Logic (SWIL)**, a novel computing architecture that replaces silicon transistors with propagating Surface Acoustic Waves (SAWs) on piezoelectric substrates.

This project specifically models the physical challenges of designing an acoustic XOR gate, including global propagation delays, geometric race conditions, and phase transition nulls.

## Project Structure

*   `LTspice_Simulations/`
    *   `01_swil_xor_race_condition.asc`: The original geometric design. Uses unequal path lengths ($\lambda/2$ difference) to create a 180° phase shift for XOR destruction. Demonstrates the **Acoustic Race Condition** where the wave on the longer path arrives late, creating a logic glitch.
    *   `02_swil_xor_equal_path.asc`: Fixes the race condition using exactly equal path lengths and an inverted IDT to instantly launch a 180° wave. Demonstrates the **Phase Transition Null**, a mechanical ring-down artifact caused by crossing the zero-amplitude point when switching phases.
    *   `03_swil_xor_ideal_math.asc`: Uses mathematical ultra-wideband IDT parameters (impossible in reality, $Q=0.5$) to completely eliminate all mechanical glitches, outputting a textbook-perfect truth table.
*   `Docs/`
    *   `Presentation_Outline.md`: A structured markdown presentation detailing SWIL components, physics, drawbacks, and a comparison against modern CMOS Full Adders.

## How to Run

1.  Install [LTspice](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html).
2.  Open any `.asc` file in the `LTspice_Simulations` folder.
3.  Press **F9** (or `Simulate -> Run`).
4.  Add the following traces to the waveform viewer to observe the logic:
    *   `V(va)` (Input A Envelope)
    *   `V(vb)` (Input B Envelope)
    *   `V(int)` (Raw Acoustic Interference Wave)
    *   `V(xor_out)` (Digital Output)

## Physical Parameters Used
*   **Substrate:** Lithium Niobate (LiNbO₃) 128° Y-X cut
*   **Carrier Frequency:** 10 MHz
*   **Acoustic Velocity:** 3979 m/s
*   **Wavelength ($\lambda$):** 397.9 µm
*   **IDT Model:** Butterworth-Van Dyke (BVD) resonant circuit

## Key Findings

Unlike electrons in CMOS which travel near the speed of light, acoustic waves travel at the speed of sound. This project proves that utilizing geometric path lengths to manipulate wave phase creates inherent timing mismatches (race conditions). The simulations prove that SWIL architecture must utilize equal-length waveguides combined with IDT polarity inversion and synchronous clocked readouts to achieve stable logic.
