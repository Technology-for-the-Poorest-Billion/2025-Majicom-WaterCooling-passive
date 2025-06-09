# Modelling Methodology

The numerical model provided an initial means of investigating the behaviour of different materials and conditions. Although it lacks the real world nuanced provided by the experimental method, it allows for you to map how lab conditions translate to real world conditions, as well as providing further insight that can be used to inform further design. This document will provide a detailed breakdown of how the model was constructed.

## Air properties 

The first aspect of the model is determining the transport properties of air. This has been achieved using the "CoolProp" library (http://www.coolprop.org/). 

@article{doi:10.1021/ie4033999,
    author = {Bell, Ian H. and Wronski, Jorrit and Quoilin, Sylvain and Lemort, Vincent},
    title = {Pure and Pseudo-pure Fluid Thermophysical Property Evaluation and
             the Open-Source Thermophysical Property Library CoolProp},
    journal = {Industrial \& Engineering Chemistry Research},
    volume = {53},
    number = {6},
    pages = {2498--2508},
    year = {2014},
    doi = {10.1021/ie4033999},
    URL = {http://pubs.acs.org/doi/abs/10.1021/ie4033999},
    eprint = {http://pubs.acs.org/doi/pdf/10.1021/ie4033999}
    }
