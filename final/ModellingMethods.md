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

$m\dot = S*h_m(P_v - P_a)$

Where $P_v$ is the saturated vapour pressure at the fabric temperature and $P_a$ is the partial vapour pressure of water vapour in air






