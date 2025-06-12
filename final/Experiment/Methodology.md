# Experimental Testing of Evaporative Cooling for Water Dispensing Kiosks
Oishi: Experimental Design & Testing Lead, assisted by Timothy. 

## 1. Overview

This section documents the design, reasoning, and findings from the experimental evaporative cooling setup developed for our project with Majicom. The goal was to create a realistic, low-cost test system to help evaluate how well different fabric materials and fan configurations could cool down stored water - specifically for use in solar-powered water kiosks in Tanzania.

All tests were done using materials and methods that would be easy to replicate in real-world settings. The idea was to keep the setup simple but controlled, so that the results could guide decisions on material choice and airflow configuration in future kiosk deployments.

---

## 2. Experimental Design & Reasoning

The entire setup was built from scratch with the aim of mimicking Majicom’s use case as closely as possible. All components were chosen to be cheap, accessible, and adaptable in lower-resource environments - while still giving meaningful and consistent data.

### Bottle and Water Selection
We used 1L plastic bottles filled with 500 mL of tap water cooled to around 15°C. This was based on two key things: (1) 15°C is close to the groundwater or municipal supply temperatures expected in Tanzania, and (2) it gives enough of a starting point to track how effective each fabric is at keeping water cool over time.

### Fabric Wrapping
Each fabric sample was soaked for 5 minutes, wrung lightly, and wrapped tightly around the bottle using double sided tape as the adhesive, This method balances water retention with airflow exposure, which is key to evaporative cooling. All samples were cut to the same size and thickness to make sure comparisons were fair. As cotton is thinner, two layers of this was wrapped around the bottle to match the thickness.

The choice of fabrics was made based on local availability, cost, and previous research on material porosity and water-holding capacity (further detail in Material selection) key properties that influence how well a fabric cools via evaporation.

### Fan Configurations
Three fan placements were tested:
- Bottom-only
- Top-only
- Dual side fans (one blowing in air and one blowing out) 

Fan enclosures were made by cutting holes into plastic buckets, just large enough for airflow to pass through without letting in too much extra air from the outside. This helped us create a semi-controlled chamber -useful since room conditions in the UK are inconsistent and could skew results.
DC 12V fans from old PCs were used because they’re compatible with solar-powered systems and could be easily adjusted between low, medium, and high speeds to see what works best for each fabric.

---

## 3. Method: Step-by-Step

1. **Prep the fabric**  
   Soaked each piece in room-temp water, wrung out for ~10 seconds, and wrapped it securely around a chilled 500 mL water bottle. Secure with tape for consistency.
2. **Set up airflow**  
   Placed the wrapped bottle into a plastic bucket. Depending on the test, mount the fan at the bottom, top, or at sides. Use a second bucket /altered as a lid to create a closed chamber and minimise airflow variation. To suspend the bottle in the bucket, a 3D printed clasp was made and secured using bolts.
3. **Take measurements**  
   - Record initial water temperature and ambient chamber temperature, as well as weights of the damp and dry samples.
   - Run the fan for exactly 40 minutes.
   - Record final water and ambient temps.
   This 40-minute duration was picked because it’s a realistic waiting time between kiosk use or refills, and would give enough time for our material to actually become dry. 24 tests were done in this manner, so doing in conjunction would save much more time with more resources. 
4. **Calculate cooling**  
   Effective cooling was measured using: Cooling = Ambient Temp - Bottle water Temp. This was to make results fair across trials (since room temp in the UK varies) and normalise our data. 
This gives us a consistent way to compare setups - removing the bias of how hot or cold the room was each time.

## 4. Data & Handover Notes

All raw data is saved in the `experimentaldata/` folder in CSV format. Graphs and visuals are in `plots/`, sorted by material and fan setup. Data includes:
[Raw Data CSV](./data/raw_data_evap_cooling.csv)  
[Processed Data CSV](./data/processed_data_evap_cooling.csv)

- Fan speed
- Placement
- Initial/final water temperature
- Change in weight
- Ambient temperature
- Calculated cooling
- Normalised cooling value

### If You’re Continuing This Work:

Here’s how to quickly make sense of the data:
- Focus on the **normalised cooling** values - these tell you which setups actually worked, regardless of outside conditions.
- Filter by fan speed or material to find the most consistent performers.
- Use the bar charts and time plots (in `plots/`) to compare results visually.

### Suggestions for Further Work:
- Test more fabrics (e.g. recycled blends, plastic mesh, or double-layered systems)
- Try outdoors to evaluate real Tanzanian ambient conditions (hot, dry vs humid days)
- Introduce insulation or water-retention aids between bottle and fabric

This setup was built to be flexible. The buckets, bottles, fabric wraps and fans can all be easily swapped out without needing to rebuild the system, which means further testing or even deployment pilots can be started quickly.

### Why This Method Works

Evaporative cooling works best when:
- The material can hold moisture without drying out too fast
- There’s consistent airflow across the wet surface
- The ambient temperature is hot and dry

Everything in this setup - from soaking time to chamber enclosure - is based on making those three things happen in a reliable, controlled way. This is why the data can be trusted to reflect material and airflow performance even if it’s tested somewhere else.




