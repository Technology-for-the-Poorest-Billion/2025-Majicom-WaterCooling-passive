# Proposal Summary

In order to produce deliverable results within the required timeframe, the below condensed propsal has been produced. The aim of this is to outline what we feel is realistically achievable over the short period of the next three weeks. The previous proposal explored three different assisted passive cooling methods: evaporative cooling, PCM and radiative cooling. The scope of the project is now being narrowed down to focus predominantly on evaporative cooling. The aims of the project (in priority order) are as follows:

1. To identify the optimal material to coat or construct the storage tank in to maximise evaporative cooling
2. To calculate air speeds and fan powers required to achieve the desired cooling
3. To experimentally validate these results through the application of a small scale model
4. To explore experimentally how different spray methods or fan placements affect the results quality (low priority)


## Numerical Model

The numerical model is the first focus of the project and ideally will take 1 - 1.5 weeks to construct sufficiently accurately to inform experimental results. Over the latter half of the project, further refinement can take place alongside the experimental method. 

****Aim****
The aim of the model is to identify the temperature drop in the body of water as we vary a range of different conditions. The conditions that we wish to be able to vary are:

1. Material
2. Material thickness
3. Material saturation
4. Fan power

Keeping variables such as tank / kiosk geometry controlled, and making a series of assumptions to simplify parts of the analysis. 

The logic of the model will work as such:

### Air Speed Calculation

- Using fan properties to calculate the airspeed. This can be achieved either through analytic approximations for air speed based on fan power, or by using different fan specifications (using its CFM - cubic feet per minute, i.e volumetric flow rate)

Input:
- Fan power / efficiency OR Fan model and CFM

Output:
- Air speed 

### Evaporation Rate Calculation 

- This is likely the most complicated part of code. This will attempt to calculate the rate of evaporation based off of a number of high order approximations. The primary governing equation for this is

\dot{m}_{\text{evap}} = S \cdot h_m \cdot A \cdot (P_s - P_a)
