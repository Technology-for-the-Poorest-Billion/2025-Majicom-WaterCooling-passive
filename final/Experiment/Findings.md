Oishi: 

## Results Summary

Six tests were carried out to observe cooling behaviour under different airflow configurations and voltages, comparing three evaporative materials (jute, cotton, linen) and a control (no wrap). The main measure used was **temperature drop from baseline**, normalised using ambient conditions.

### Key Trends:
- **12V Bottom Fan** produced the highest cooling overall, with **cotton and jute** consistently outperforming linen and control.
- **Side Fans (Dual) at 12V** also showed strong performance, particularly for **jute**, which had consistent cooling without significant fluctuation.
- **9V Top Fan** was the weakest setup overall — cooling was minimal, and temperature gains were seen in some trials, especially for linen.
- **Control** samples showed negligible change across all trials, validating that cooling was due to the fabric and airflow, not ambient fluctuation alone.

---

## Discussion

These results confirm that **fan placement and power are critical** for effective evaporative cooling. The best results came from **directional bottom airflow at 12V**, likely due to increased turbulence and forced convection directly across the wet fabric surface.

### Material Performance:
- **Cotton** consistently achieved the most cooling under strong airflow (particularly in 12V setups), aligning with its high absorbency and porous structure.
- **Jute** showed stable cooling, likely due to its thicker weave holding water longer and evaporating more steadily.
- **Linen** underperformed in most conditions — likely due to lower water retention and faster drying, which reduces sustained evaporative effect.

### Dual Fan Setups:
While more energy intensive, the **side fan ×2 (12V)** configuration resulted in the **most consistent and rapid cooling**. However, gains over the 12V bottom fan were modest, suggesting diminishing returns.

### Voltage Sensitivity:
Moving from 9V to 12V **significantly increased cooling**, especially for high-retention materials. In practical deployment, this could justify using short bursts of 12V airflow for rapid cooling before passive maintenance kicks in.

---

## Limitations & Future Work

### Limitations:
- UK testing conditions mean some humidity variability — though ambient-adjusted calculations accounted for this.
- Manual fabric wringing may introduce slight inconsistencies in retained water mass.
- Some fan setups had limited space for airflow dispersion, which may not fully reflect open-air kiosk conditions.

### Opportunities:
- Add mass tracking (weight of fabric before/after) to study evaporation rates directly.
- Test in open outdoor conditions to validate real-world performance.
- Investigate fan timing (pulsed vs continuous) to reduce power draw while maintaining cooling.
- Test material combinations (e.g. inner absorbent + outer breathable layer) for hybrid cooling systems.

---

## Final Handover Notes

This test rig is fully modular and low-cost. To replicate or extend this work:

- Use `data/` files to re-analyse or verify results.
- Review `plots/` for clear comparisons across configurations.
- Adjust fan speed, duration, or material thickness as needed.
- If adding new materials, follow the same soaking/wrapping method to ensure consistency.

This data can now inform Majicom’s material and fan selection in Tanzania - particularly when balancing cost, cooling rate, and energy use. The setup is transferrable, tweakable, and field-ready.

