# Modelling Methodology

The numerical model provided an initial means of investigating the behaviour of different materials and conditions. Although it lacks the real world nuanced provided by the experimental method, it allows for you to map how lab conditions translate to real world conditions, as well as providing further insight that can be used to inform further design. This document will provide a detailed breakdown of how the model was constructed.

## Air properties 

The first aspect of the model is determining the transport properties of air. This has been achieved using the "CoolProp" library (http://www.coolprop.org/) by Bell et al.  (http://pubs.acs.org/doi/abs/10.1021/ie4033999). The air property class uses this library, taking the dry bulb temperature (environmental temperature) and the local relative humidity to determine density, thermal conductivity and other critical attributes. The Diffusion Coefficient of water in air is being determined by an empirical relationship from Yaws, Carl. (2009). Diffusion Coefficient in Air - Inorganic Compounds. Transport Properties of Chemicals and Hydrocarbons. 497-501. 10.1016/B978-0-8155-2039-9.50016-8. 


@article{article,
author = {Yaws, Carl},
year = {2009},
month = {12},
pages = {497-501},
title = {Diffusion Coefficient in Air - Inorganic Compounds},
isbn = {9780815520399},
journal = {Transport Properties of Chemicals and Hydrocarbons},
doi = {10.1016/B978-0-8155-2039-9.50016-8}
}

$ln(D) = A + B/T + Cln(T)$

$A = -10.298, B = -180.06, C =
