# Readme file for Passive Cooling (Evaporative Cooling)
Placeholder
## **Objective**
- Identify the **most effective, low-cost, material-airflow combination** for evaporative cooling with **minimal water and power use**.
- Prepare implementation proposal for **real-world kiosk integration**

<!-- I have selected sustainable materials, designing the experimental setup, and building a testing framework to compare passive and fan-assisted evaporative cooling performance. I’ve also developed a detailed **risk assessment** to ensure safety throughout testing. -->

<!-- While T1 is exploring a **heat pump-based system**, our work focuses on an **assisted passive cooling solution** that avoids high power demands. This approach could operate independently or in parallel with active systems, offering a more affordable and energy-efficient alternative. -->

---

## Experimental Method

This part of the project focused on designing and building a low-cost, scalable experimental setup to test evaporative cooling performance using Jute, Cotton, and Linen wraps.
To test evaporative cooling performance, a developed **controlled model** is used:

- 500mL plastic bottles (representing kiosk containers)
- A small 3–5L bucket acting as an airflow chamber
- Fabric materials soaked and wrapped around each bottle
- PC fans (~12V) to generate controlled airflow

The fan is placed **5–10 cm away** from the bottle to ensure measurable airflow across the surface. The bottle is suspended inside the bucket secured by a 3D printed clamp or placed centrally to standardise airflow exposure. We are also using cold tap water to mimic the temperature they could get in Tanzania (around 15 degrees).

- Multiple fan placements (bottom, top, side ×2) and voltages (9V, 12V) were tested
- Cooling was measured via temperature difference (ΔT) over 40 minutes
- Cotton with a 12V bottom fan yielded the highest cooling (~6.8°C)
- Jute and Linen showed strength in low-power or long-duration configurations

All processed data, graphs, and detailed analysis can be found in the '(/final/experimentaldata/) folder.  
➡ [Read the full experimental README](/final/experimentaldata/README.md)
