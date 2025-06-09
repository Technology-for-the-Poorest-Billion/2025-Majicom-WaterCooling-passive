# Modelling Methodology

The numerical model provided an initial means of investigating the behaviour of different materials and conditions. Although it lacks the real world nuanced provided by the experimental method, it allows for you to map how lab conditions translate to real world conditions, as well as providing further insight that can be used to inform further design. This document will provide a detailed breakdown of how the model was constructed.

## Air properties 

The first aspect of the model is determining the transport properties of air. This has been achieved using the "CoolProp" library (http://www.coolprop.org/) by Bell et al.  (http://pubs.acs.org/doi/abs/10.1021/ie4033999). The air property class uses this library, taking the dry bulb temperature (environmental temperature) and the local relative humidity to determine density, thermal conductivity and other critical attributes. The Diffusion Coefficient of water in air is being determined by an empirical relationship from Yaws, Carl. (2009). Diffusion Coefficient in Air - Inorganic Compounds. Transport Properties of Chemicals and Hydrocarbons. 497-501. 10.1016/B978-0-8155-2039-9.50016-8. 

$D = A + BT + CT^2$

$A = -10.298, B = -180.06, C =$ FILL OUT THESE NUMBERS


## Modelling heat transfer

The core of this model is a resistive analogy for convective, conductive and radiative heat transfer. The system can be described as a series of thermal exchanges between the air, the fabric and the water itself. This is shown pictographically below, alongside an equivalent circuit diagram for the system. Convective and conductive heat transfers are modelled as resistors, whilst the body of water is treated as a capacitor, using a lumped parameter model to assume uniform internal temperature distribution. There are three main routes of convective / conductive heat exchange. Firstly, there is a heat transfer between the air and the fabric. This is then followed by conductive heat transfer between the fabric and the water (these are broken into two separate steps to allow for the removal of energy by evaporation). Additionally, there will be some direct heat transfer between the air and water via the uncovered surfaces on the top and bottom of the tank. 

The model also accounts for radiative heat transfer between the outer wall of the kiosk and the fabric. Radiative heat transfer can be modelled as a separate circuit that can be used to solve for the power exchange between the two grey bodies. This subsequently forms a current source into the fabric node as an additional source of energy into the system. The loss of energy due to the evaporation of water in the fabric is also modelled as a current source. The process of calculating the power draw is a more involved process that will be discussed subsequently.


## Determining thermal resistances

The process of modelling thermal resistance of porous fabric involves considering the fabric to be a three phase composition of air, water and the fibres themselves. Air and water have the capacity to drastically reduce or increase the thermal conductivity respectively, and as such it is vital to understand how the saturation ratio affects the conductivity of the fabric as a whole. This is done by considering how porous (via a porosity ratio ranging from 0 to 1) the fabric is. 

When the fabric contains a smaller volume of water than there are pores, the thermal conductivity can be calculated as:

$k_{total} = (V_{material}k_{material} + V_{air}k_{air} + V_{water}k_{water})/V_{total}$

$V_{material} = (1-\phi)V_{total}$ 

$V_{water} = S*m_{sat}*V_{material}\rho_{material} / \rho_{water}$ 

$V_{air} = \phi *V_{total}-V_{water}$

Where $\phi$ is the porosity, S is the saturation ratio (fraction of maximum water mass currently in the material) and $m_{sat}$ is the maximum amount of water that 1kg of fabric can absorb.

$k_{air}$ is a parameter provided by CoolProp. $k_{water}$ and $k_{fabric}$ are given by INSERT SOURCES HERE respectively. 

Porosity is not the limiting factor for governing how much water the fabric can absorb. Organic fibres can swell to accomodate a greater volume of water. Pure unwoven cotton, for example can absorb 27x its own weight through this method. In order to account for this phenomenon, I have assumed that no swelling occurs in the first case where $V_{water} < V_{pore}$ until the point where all air is fully displaced from the pores. After this point the conductivity can be modelled as 

$k_{total} = V_{water}k_{water} + V_{material}k_{material} / V_{material} + V_{water}$

A similar process is applied for estimating the emissivity of the fabric, again using this linear method of handling a three phase mixture. 

The convective heat transfer coefficient can be determined by considering the Nusselt's number, a dimensionless coefficient that describes heat transfer into a convective flow. Specifically, the correlations used to calculate Nusselt's number are the same as those used below for Sherwood number (see next section), with the Schmidt number replaced with the Prandtl number,

$Pr = \nu/\alpha$

$Nu = hL/k$

## Calculating evaporative rates

Mass transfer in a forced convection system is governed by the Sherwood Number (Sh). Sh is a non dimensional group that is analagous to the Nusselts Number (Nu) for heat transfer convective systems and describes how mass from a surface diffuses into a moving stream of fluid. Typically the Sherwood number can be determined through a set of empirical relationships that are derived experimentally for a specific geometry. The sherwood number is defined more specifically as 

$Sh = h/(D/L)$

Where h is the mass transfer coefficient, D is the diffusion coefficient and L is a characteristic length (either height or diameter depending on whether the flow is axial or crossflow)

With the flow in the Majicom kiosk, there are two configurations of interest. Firstly is the top down / bottom up configuration, in which the fan faces along the axis of the cylinder. There is no standard approach for this type of flow, so the approximation being made is that the edge effects( the deflection of flow due to the ends of the cylinder) are negligible, thus meaning that flow can be considered to be purely axial and thus can be modelled as a flat plate. In reality, the aspect ratio of the tank likely does not lend itself well to this approximation, with a relatively large tank diameter contributing to the radial deflection of air. In this case I am arguing that the presence of the outer sheath helps to redirect flow as it is pushed out radially, ensuring that the flow is approximately axial.

The second configuration has two fans positioned on either side of the tank, facing normally inwards. In this case we consider the flow to be cross flow over a cylinder, which has its own empirical relationship. The primary source of inaccuracy with the model in this instance is the area over which the air flows across the tank. Currently it is being assumed to be over the entire height of the tank, however depending on the fan size it may be less than this.

The empirical formulae for the Sherwood Number are give by https://studylib.net/doc/7272115/4-convective-mass-transfer---chemical-engineering-learning and https://wwwcourses.sens.buffalo.edu/ce407/notes/ce407_notes_mass_transfer_correlations.pdf as 

$Sh = 0.664 Re_L^{1/2} Sc^{1/3}$ Laminar Plate Flow

$Sh = 0.036 Re_L^{0.8} Sc^{1/3}$ Turbulent Plate Flow

$Sh =  0.61 Re_D^{1/2} Sc^{1/3}$ Cylindrical Cross Flow 

Where Re is the Reynold's number with respect to the height (L) or diameter (D), defined as $uL/\nu$ and Sc is the Schmidt Number, defined as $\nu/D$

The key takeaway from the Sherwood Number is the mass transfer coefficient h. h determines the rate of evaporation as 

$\dot m = S*h_m(P_v - P_a)$

Where $P_v$ is the saturated vapour pressure at the fabric temperature and $P_a$ is the partial vapour pressure of water vapour in air

The S is added as an additional coefficient to model the impact of the fabric drying. As the fabric dries, less water is able to be drawn to the surface of the fabric to continue evaporation, and as a result the rate of evaporation slows down. In a more fully developed model this would occur in multiple stages. For large values of S, drying has a negligible impact on the rate of evaporation as liquid is drawn to the surface via capillary action. As water is increasingly removed from the system however, and more voids form in pores, this action becomes increasingly inhibited, resulting in a transition where saturation does impact evaporation profiles. 

Gonçalves M et all  discuss this in the context of droplets on the surface of the fabric, and how porosity and material behaviours impact evaporation rates. (Droplet evaporation on porous fabric materials. Sci Rep. 2022 Jan 20;12(1):1087. doi: 10.1038/s41598-022-04877-w. PMID: 35058506; PMCID: PMC8776847)

Knowing the rate of evaporation, the power removed from the system can be easily calculated as

$\dot q = L_v\dot m$

Where L is the latent heat of vapourisation of water.

## Temperature Calculation

Having now determined all of the thermal resistances and the net power into the system (as a function of the fabric temperature which is currently unknown), the next step in the process is to calculate the water and the fabric temperature.
This proved difficult to achieve analytically for two reasons. Firstly, the temperature of the fabric is unknown. This is important and cannot simply be assumed to be the same as the air temperature due to the cooling it experiences. The second complication is how to account for the time varying behaviour of the bulk of water.

### Solving for Fabric Temperature

In order to solve for the fabric temperature, an energy balance was considered at the fabric node. There are four sources of power in / out of the fabric: evaporative cooling, radiative heating, conductive transfer from the water and convective transfer from the air. For a starting arbitrary guess at Tf it is possible to calculate the energy balance at the node, provided that Tw is also known. Based on the resistive analogy, we would expect the sum of power in / out of the node to be 0. Therefore by determining an error in net power give as

$e = q_{air-fabic} + q_{water - fabric} - q_{evap} + q_{rad}$

We can iteratively solve for the value of Tf that gives a power balance using a Newton-Raphson scheme.


### Solving for Water Temperature

Solving for the temperature of the water is equivalent to modelling the discharging of a capacitor. An initial starting temperature is defined (by default is the temperature of the air, but can be changed in the event that cold tap water is being used such as in the experimental testing). Using the above methods the temperature of the fabric at this starting temperature can be evaluated. This allows us to then determine the power flow through the capacitor via an energy balance at the water node

$q_{cap} = q_{air-water} + q_{fabric - water}$

The time dependent behaviour of capacitors is given as 

$I(t) = CdV/dt$ Where I is analogous to q and V is analagous to T. Using a numerical difference scheme, the time evolution of the water temperature can then be determined. The "steady state" condition is reached either when a maximum time is reached, or when the rate of change of temperature crosses a minimum threshold. 

## Drying Characteristics

The final aspect of the model is a drying characteristic. This was initially implemented in the function coolingTime, but was subsequently integrated into the core simulation function, meaning either can be used to physically consistent results (although returning different values). In the numerical difference scheme this is achieved by considering the rate of evaporation and therefore the mass loss within that interval of time. This can then be used to recalculate S and hence determine the amount of time it would take for a sample to fully dry (or to transition between any two arbitrary saturation ratios)


## Glossary 

$Re$ = Reynold's Number (Advective vs Viscous non-dimensional number)

$Sc$ = Schmidt Number (Momentum Diffusivity non-dimensional number)

$Pr$ = Prandtl Number (Thermal Diffusivity non-dimensional number)

$Sh$ = Sherwood Number (Convective Mass Transfer non-dimensional number)

$Nu$ = Nusselts' Number (Convective Thermal Transfer non-dimensional number)

$h$ or $h_m$ = Mass Transfer Coefficient 

$S$ = Saturation Ratio (mass of water / maximum absorbable mass of water)

$m_sat$ = Saturated Water Mass (maximum absorbable mass of water per unit mass of fabric)

$\phi$ = Porosity (volume fraction of fabric weave occupied by voids)

$\epsilon$ = emissivity (radiative property)

$L_v$ = Latent heat of vapourisation 












