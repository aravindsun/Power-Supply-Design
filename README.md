# Power-Supply-Design
Power Supply Design focusses on building reliable low‑voltage regulated supplies for custom electronics. The repo explores both traditional and modern approaches — from transformer‑rectifier‑LDO topologies to efficient switch‑mode designs — with emphasis on practical implementation, noise performance, and reproducibility.

# Objective
The objective here is to create 3.3V power supply for a microcontroller sitting on a custom pcb board. The first approach would be to use a low frequency transformer with a full bridge rectifier as a separate unit. This will be fed to an LDO on the pcb to give regulated 3.3V supply. The second approach would be to use high frequency transformer with switched mode converters which are efficient and compact and can be added onto the pcb.

# Topology
<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/7b61c72b-b1b4-44dd-993b-ac20144846ea" />
The above image shows the front end of power conversion i.e., coverting 230V AC to unregulated DC voltage for the LDO input.

# Requirements
  1) Input Voltage - 230V +/- 10%
  2) Output Voltage(min) - 5V  // This is required so that the regulator will not stop even if the supply goes to the min value
  3) Output Voltage ripple - 0.5Vp-p
  4) Load Current(max) - 200mA

# Design Calculation
1) Calculate Transformer Turns Ratio:
  * Step down 230 V AC to suitable secondary RMS voltage.
  * Target DC after rectifier ≈ 7–9 V (to allow LDO dropout)
  * Required secondary RMS ≈ 6 V AC (since VDC ≈ 1.414 × Vrms − 2 × Vdiode)
Turns ratio ≈ 230:6 ≈ 38:1

2) Select Rectifier Diodes :
  * Choose diodes that can handle current and reverse voltage.
  * Load current: 200 mA → choose ≥ 1 A rated diodes
  * Reverse voltage: secondary peak ≈ 8.5 V → choose ≥ 50 V PIV
Common choice: 1N4001–1N4007 series

3) Size Filter Capacitor :  
  * Reduce ripple to within 0.5 Vp-p at load current.
  * Ripple ΔV ≈ Iload / (f × C)
  * For 200 mA, f = 100 Hz (full bridge on 50 Hz mains)
  * C ≈ I / (f × ΔV) = 0.2 / (100 × 0.5) = 4000 µF
Choose standard value: 4700 µF, 16 V rating

4) Determine Transformer Current Rating
  * Ensure secondary winding can supply required current.
  * DC load power ≈ 5 V × 0.2 A = 1 W
  * Accounting for rectifier and LDO losses, secondary ≈ 2 W
  * At 6 V AC, current ≈ 2 W / 6 V ≈ 0.33 A
Choose transformer rated ≥ 500 mA at 6 V AC for margin
     
