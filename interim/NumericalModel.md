
# Proposal Summary

In order to produce deliverable results within the required timeframe, the below condensed propsal has been produced. The aim of this is to outline what we feel is realistically achievable over the short period of the next three weeks. The previous proposal explored three different assisted passive cooling methods: evaporative cooling, PCM and radiative cooling. The scope of the project is now being narrowed down to focus predominantly on evaporative cooling. The aims of the project (in priority order) are as follows:

1. To identify the optimal material to coat or construct the storage tank in to maximise evaporative cooling
2. To calculate air speeds and fan powers required to achieve the desired cooling
3. To experimentally validate these results through the application of a small scale model
4. To explore experimentally how different spray methods or fan placements affect the results quality (low priority)


## Numerical Model

https://colab.research.google.com/drive/1D8jrgBWuxRUjkXFdTaMW2er6YYpis4Rj?authuser=1

The numerical model is the first focus of the project and ideally will take 1 - 1.5 weeks to construct sufficiently accurately to inform experimental results. Over the latter half of the project, further refinement can take place alongside the experimental method. 

****Aim****
The aim of the model is to identify the temperature drop in the body of water as we vary a range of different conditions. The conditions that we wish to be able to vary are:

1. Material
2. Material thickness
3. Material saturation
4. Fan power

Keeping variables such as tank / kiosk geometry controlled, and making a series of assumptions to simplify parts of the analysis. 

### Transport Properties of moist air

In order to be able to accurately model the airflow. It is important to be able to determine the transport properties of air.

Inputs:
- Temperature
- Pressure
- Humidity

Outputs:

- Saturation Pressure
- Vapour partial pressure
- dynamic / kinematic viscosity
- thermal conductivity
- density / specific volume

Investigating how to determine these properties, as well as a review of IB thermofluids content lead me to https://www.scribd.com/document/628245606/Qpedia-Nov08-Estimating-the-Effect-of-Moist-Air-on-Natural-Convection-Heat-Transfer
Which breaks down numerical solutions to determine critical transport properties of humid air.

Further investigation revealed that these features had already been built into python by http://www.coolprop.org/



### Air Speed Calculation

- Using fan properties to calculate the airspeed. This can be achieved either through analytic approximations for air speed based on fan power, or by using different fan specifications (using its CFM - cubic feet per minute, i.e volumetric flow rate)

Input:
- Fan power / efficiency OR Fan model and CFM

Output:
- Air speed 

### Evaporation Rate Calculation 


!(interim/interimassets/gm2alex.jpg)

- This is likely the most complicated part of code. This will attempt to calculate the rate of evaporation based off of a number of high order approximations. The primary governing equation for this is

$\dot{m}_{\text{evap}} = S \cdot h_m \cdot A \cdot (P_s - P_a)$

This equation needs to be verified against literature and may end up being different in the final model, however acts as a starting point for identifying relevant variables:

$P_s$ = Saturation Pressure (function of the ambient temperature)
$P_a$ = Partial pressure of vapour in air (function of ambient temperature and humidity)
S = Saturation coefficient - ratio of the amount of water saturated in the material and total mass that can be absorbed
Need some further research into how the saturation coefficient effects mass flow, and also how the total wet mass at maximum saturation affects the equation (as this is subtly different from saturation ratio)
$h_m$ = evaporation coefficient - need more research into exactly how this is calculated, but fundamentally it is a function of air properties at the known temperature / humidity and the airflow speed. Likely this will be defined through a series of high order approximations 

Inputs:
- Air Temp
- Air Humidity
- Airflow speed
- Material saturated mass
- Saturation coefficient (how soaked the material is)

Output: 
- rate of evaporation


Modelling Evaporation Rates:

The main area of contention for this model is determining $h_m$, which is a mass transfer coefficient between the surface of the wrapping and the air flowing over the body. This field of study can often be considered as analagous to both heat transfer processes and also diffusive mass transfer between a solid and a fluid flowing over the body. This analogy leads us to look at comparing nondimensional expressions between these equivalent systems.

Specifically, this leads us to look at the **Sherwood Number**, which is a nondimensional measure of convective mass diffusion. It is the mass flow equivalent of the Nusselts number.
Sherwood Number is defined as 

$Sh = h_m L/D$

Where D is the mass diffusivity and L is a characteristic length.

In order to calculate the Sherwood number,we can look at applying empirical relationships that very with the geometry of the system. This is the particular area where high order assumptions will likely need to be made. Commonly well understood geometries include:

- Flow over a flat plate
- Flow across a cylinder
- Cross-flow over a cylinder
- Pipe / Annular Flow
- Flow through a stream of spheres

Given that none of these accurately model the system we are looking at, a decision needs to be made as to which most accurately models our system. Initially, our tank/kiosk structure looks similar to an annular structure. However, in our situation evaporative mass transfer is only occuring from the external surface of the inner ring. The empirical relationships used for pipe flow look at internal flow through a cylinder and an annulus assumes that mass transfer occurs both through the inner and outer cylinder.

The other option is to consider the inner cylinder as a flat plate. Typically this is only possible for slender cylinders, where edge effects caused by deflection of air over the flat face over the cylinder is negligible. In these scenarios a boundary layer is able to develop as on a flat plate. Given that there is negiglbe variation radially, and the system is axisymmetric, it can be considered as a flat plate. In our scenario, the aspect ratio of our tank is likely outside of the range where we can make these assumptions. However, we are arguing that the presence of the outer kiosk will act as a sheath, counteracting any radial deflection and meaning that the flow can very approximately be modelled used a flat plate analogy. Given that this is the case, the following empirical relationship can be said to apply 

$Sh = 0.0664 Re_L^{1/2}Sc{1/3}$ For laminar flow

$Sh = 0.0366Re_L^{0.8}Sc^{1/3}$ For turbulent flow

**Alternatively** Beddingford & Drew (FIND SOURCE from https://studylib.net/doc/7272115/4-convective-mass-transfer---chemical-engineering-learning) found a correlation for axial flow over a cylinder as being modelled as approximately 

$k_GPSc^{0.56}/{G_m} = 0.281(Re_D)^{-0.4}$

On further review **this is not applicable** it is for flow **normal to the axis**

https://studylib.net/doc/7272115/4-convective-mass-transfer---chemical-engineering-learning

https://www.tmt.unze.ba/zbornik/TMT2015/TMT_2015_084.pdf

https://wwwcourses.sens.buffalo.edu/ce407/notes/ce407_notes_mass_transfer_correlations.pdf

https://link.springer.com/content/pdf/10.1007/s40032-014-0098-0.pdf

https://link.springer.com/article/10.1007/s11242-022-01775-7

### Evaporation Rate Calculation Challenges 

There have been a broad number of challenges assocaited with calculating the mass transfer and the heat transfer. The details of which and possible methods to overcome them are detailed below:

Saturated Vapour Pressure:

In order to find the mass flow, I need to know the temperature of the fabric at the equilibrium point. In order to determine this I need to know the energy removed from the system and so the argument becomes circular.
In order to calculate a stable equillibrium point I am considering an energy balance between the energy conducted through the tank, the energy convected into the air and the energy lost through latent heat.
Iterating over this balance numerically from a reasonable starting point (via Newton-Raphson or another numerical scheme) I can identify a stable solution. This is assuming that the tank of water is well mixed and therefore at a uniform temperature. This is not an unreasonable assumption, as the tank will likely be sitting full, with small amounts of additional water added periodically that are small in comparison to the bulk volume of the tank.  As such the tank will have had sufficient time for transient thermal gradients to decay and therefore have a roughly uniform temperature profile.

Saturation Ratio:

Modelling the saturation ratio is slightly more complex than initially anticipated. it is important to be able to do this so that I can estimate the thermal conductivity of the coating material. For thermal conductivity it is the volume ratio that matters and it is a three phase system - water, fibre and air (although I may be able to neglect the effects of air if its volume fraction is very small). There is some important distinction here to be made about exaclty how much water can be absorbed by the fabric and then also how much air is within the fabric. When the material is totally soaked, it holds water not just in its pores, but also by swelling to absorb water. As such, it is possible that at a high saturation (say 0.8-0.9) that there is no air at all present (rather than the 0.1-0.2 that you might expect). As such I need to make a decision as to how to account for the air. 

One possible option is that air is accounted for below a certain threshold, where I assume all the water to be held in pores, and above which i switch to the assumption that there is no air and it is all due to water swell. 


### Energy exchange 

The final part of this is to use thermal conductivity models to estimate the temperature change in the water:

Main issues / research areas:

- Where in the tank do we take the temperature? at the outer surface of the tank (max temp drop), the middle (min temp drop) or is there a preexisitng more complicated model we can implement to give a more accurate average temperature drop
- How much of the energy goes into the tank versus the air (can this be determined with a resistive model for heat transfer)

The main appraoch here is to use IB heat transfer techniques to estimate based on the energy loss what temperature change is induced in the water. The main area of contention is in the working out how to consider temperature gradients in the large body of water.

To calculate the energy from the rate of evaporation, consider the latent heat capacity of water.

Inputs:
- Water properties
- Rate of evaporation
- Material thickness and layering (to find combined thermal conductivity - need to consider how to account for saturation in this possibly?)

Output:
- Temperature of water


Throughout this process, the parameters of interest (as discussed above) can be varied to explore how they may affect the end result. 
Much of this may be based on simplification, and more complicated aspects, like capillary action in the material may be too complicated to implement. 
Also worth exploring whether it is possible to adapt this model to consider a clay vessel that passively leaks water - zero outer layer thickness and mass of water availble to evaporate given by porosity of clay, always at S = 1.

