# Modelling Methodology

The numerical model provided an initial means of investigating the behaviour of different materials and conditions. Although it lacks the real world nuanced provided by the experimental method, it allows for you to map how lab conditions translate to real world conditions, as well as providing further insight that can be used to inform further design. This document will provide a detailed breakdown of how the model was constructed.

## Air properties 

The first aspect of the model is determining the transport properties of air. This has been achieved using the "CoolProp" library (http://www.coolprop.org/) by Bell et al.  (http://pubs.acs.org/doi/abs/10.1021/ie4033999). The air property class uses this library, taking the dry bulb temperature (environmental temperature) and the local relative humidity to determine density, thermal conductivity and other critical attributes. The Diffusion Coefficient of water in air is being determined by an empirical relationship from the CRC Handbook of Chemistry and Physics (https://hbcp.chemnetbase.com/documents/06_40/06_40_0001.xhtml?dswid=-7014), given as

$ln(D) = A + B/T + C\dot ln(C)$
