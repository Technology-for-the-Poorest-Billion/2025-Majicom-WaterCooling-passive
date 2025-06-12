Author: Oishi

## 1. Results Summary

The following section presents a detailed breakdown of cooling behaviour observed under various experimental configurations. Cooling performance was assessed based on the temperature difference between the water bottle and the ambient chamber after 40 minutes. Each setup tested three materials (Cotton, Jute, Linen) and a control (no wrap) using different fan placements (Bottom, Top, Side ×2) and voltages (9V, 12V).

All readings were normalised to account for ambient temperature shifts and reported as ΔT (Temp diff from ambient). The results allow comparison of not just absolute cooling, but stability over time and responsiveness to airflow changes.

---

### 1.1 Bottom Fan, 9V

![Cooling 9V Bottom Fan](/finalassets/experimentaldata/plots/botfan9V.png)

- **Linen** demonstrated the highest cooling (~6°C), achieving a smooth upward curve. Its slower moisture release rate may have helped sustain evaporation over 40 minutes.
- **Jute** showed an initial dip then gradual rise, indicating delayed but stable evaporation. Likely due to thickness retaining water for longer.
- **Cotton** rose consistently, but peaked slightly lower than Linen. This matches expectations that cotton, while quick to absorb, also dries faster.
- **Control** exhibited a brief cooling drop (likely due to temperature lag) before plateauing at ~2.3°C.

**Interpretation:** Bottom fan placement is effective even at low voltage, as the airflow directly hits the moistest section of the wrap (lower half of bottle). Linen's success here supports the idea that at low airflow, slower-drying fabrics perform better.

---

### 1.2 Bottom Fan, 12V

![Cooling 12V Bottom Fan](/finalassets/experimentaldata/plots/botfan12V.png)

- **Cotton** was clearly the top performer, rising steadily to ~6.8°C.
- **Jute** and **Linen** showed solid performance (~5.3°C), slightly lower but still effective.
- **Control** cooled only to ~1.6°C, again validating that the fabrics are the active component.

**Interpretation:** At higher voltages, cotton thrives due to its fast capillary action and high evaporation rate. However, the fact that linen and jute still held decent performance suggests that water retention under high airflow can still deliver long-term cooling. This setup is highly transferable to real-world kiosk conditions.

---

### 1.3 Top Fan, 9V

![Cooling 9V Top Fan](/finalassets/experimentaldata/plots/topfan9V.png)

- **Cotton** performed best (~5.3°C), again showing strong early and steady gains.
- **Jute** trailed slightly (~4°C), but showed consistent performance.
- **Linen** improved slowly but was stable.
- **Control** remained near-flat (~0.6°C).

**Interpretation:** Top fans likely have lower direct contact with saturated surfaces. Despite this, the fabric’s ability to wick moisture upwards helps. Cotton again outperforms due to its lightweight nature and vertical wickability. The result validates that even weak airflow setups have potential, particularly for resource-constrained deployments.

---

### 1.4 Side Fans ×2, 9V

![Cooling 9V Side Fans](/finalassets/experimentaldata/plots/sidefan9V.png)

- **Jute** peaked (~3.2°C) mid-way but dropped after 25 mins. Likely dried too quickly.
- **Cotton** was relatively flat but stable, ending ~3°C.
- **Linen** climbed slowly, overtaking others near the end (~3.1°C).
- **Control** declined to ~1.2°C.

**Interpretation:** With lower power and high exposure (side vents), fabrics that dry out fast suffer late-phase drop-offs. Linen’s dense weave appears to retain just enough water to benefit late in the cycle. This result suggests **side fans at low voltage may be inefficient unless paired with fabric that retains water well.**

---

### 1.5 Side Fans ×2, 12V

![Cooling 12V Side Fans](/finalassets/experimentaldata/plots/sidefan12V.png)

- **Cotton** sustained the highest cooling (~6.4°C).
- **Jute** hovered consistently around ~5.3°C.
- **Linen** improved steadily and caught up (~4.1°C).
- **Control** stayed under 2°C.

**Interpretation:** This is the most aggressive configuration tested. High exposure on two sides combined with high voltage pushes evaporation to peak levels. Cotton’s performance supports numerical predictions on airflow-driven evaporation. Linen’s late surge validates that slower-release materials can complement higher airflow.

---

## 2. Discussion & Interpretation

### 2.1 Fabric Behaviour Summary

| Material | Water Holding | Wicking Speed | Cooling Stability | Best At                |
|----------|----------------|----------------|--------------------|------------------------|
| Cotton   | Medium         | Fast           | Excellent @ 12V    | High airflow setups    |
| Jute     | High           | Medium         | Stable             | Low/moderate airflow   |
| Linen    | Medium-Low     | Slow           | Improves over time | Long-duration cooling  |

- **Cotton** dominates high-speed airflow conditions, especially bottom and side 12V. Its rapid water release makes it optimal for quick cooling but may need re-wetting.
- **Jute** shines in low-airflow settings where it can slowly release water without drying too fast.
- **Linen** is a slow starter but catches up, making it great for sustained use where rapid spikes aren’t needed.

---

### 2.2 Fan Placement vs Performance

| Fan Setup | Performance | Notes                                              |
|-----------|-------------|----------------------------------------------------|
| Bottom    | High        | Direct contact with saturated zone, most consistent |
| Top       | Medium      | Less effective but lightweight fabrics perform okay |
| Side x2   | Variable    | Depends heavily on fabric drying rate and voltage   |

- **Bottom placement consistently yielded best results** regardless of material.
- **Top airflow** is limited by airflow distribution.
- **Side fans** at 12V rival bottom fans, but at 9V they underperform due to fabric drying prematurely.

---

### 2.3 Numerical Model Tie-in

The trends align well with heat transfer and mass diffusion models:
- Evaporation rate ∝ surface temp difference × air velocity × humidity gradient
- High velocity improves rate but reduces duration unless moisture is resupplied
- Fabrics with high capillarity (cotton) suit burst cooling; jute/linen provide longer-lasting stability

**Diminishing returns** were observed as expected in dual fan 12V setup. Side fans at 12V increased evaporation, but overall advantage over 12V bottom fan was marginal, suggesting energy inefficiency.

---

### 2.4 Deployment Considerations

- **Power vs Performance:** 12V is effective but may strain solar systems. 9V bottom fan with jute or linen is more energy-efficient.
- **Cost of Materials:** Cotton is cheaper and widely available but may require more frequent wetting.
- **User Behaviour:** If users frequently open the kiosk, airflow refreshes naturally. Bottom fans can act as assistive rather than primary cooling.
- **Environmental Variability:** Humid days will reduce effectiveness. Outdoor testing will help validate robustness.

---

## 3. Recommendations

- **Best All-Round Setup:** Bottom fan, 12V, Cotton wrap
- **Most Efficient Low-Energy Setup:** Bottom fan, 9V, Jute
- **For Sustained Cooling:** Linen with side fans at 12V, or combined wrap
- **Innovation Opportunity:** Dual-layer wraps (cotton outside, jute inside) or wick-fed fabric reservoirs
- **Testing Extension:** Include fan pulsing and material rehydration cycles to simulate real use

This data now serves as a validated baseline for field deployment testing and numerical simulation comparisons. The rig, materials, and method are robust, adaptable, and transferrable to real-world settings.



