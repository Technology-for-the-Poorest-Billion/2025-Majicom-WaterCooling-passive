---
title: Technical Summary
---


## Numerical Model 

The first aspect of our project was to code a virtual simulation of the Majicom Kiosk. The aim of this code was to predict how the water would behave as the environment or the design of the kiosk was changed and evolved. As the code was produced we found that we could also use this to try and replicate the experimental results by treating it as a scaled down version of the kiosk. The full annotated code can be found [here](https://colab.research.google.com/drive/1D8jrgBWuxRUjkXFdTaMW2er6YYpis4Rj?authuser=1#scrollTo=mpWEDmWmkx8X)

We used a simple heat exchange model shown below to understand all of the different sources of energy in and out of the water: Heat from the air, radiation from the tank walls and energy taken away by the evaporative cooling. These all have a complex interplay that are affected by the design of the rest of the tank. Being able to test how changing the tank quickly through this model makes it much faster to test different cooling jackets, and helped to provide some early insight into our ideas. 

<img width="600" alt="Tank Diagram" src="https://raw.githubusercontent.com/Technology-for-the-Poorest-Billion/2025-Majicom-WaterCooling-passive/refs/heads/main/finalassets/TankDiagram.png">

To show a small demonstration of this, we attempted to simulate the water temperature inside the tank for two different coating materials: Cotton & Linen. These results can be seen below, and show clearly how this can be used to estimate the final temperature of the water and how quickly it is able to cool the water down.

<img width="600" alt="Tank Diagram" src="https://raw.githubusercontent.com/Technology-for-the-Poorest-Billion/2025-Majicom-WaterCooling-passive/refs/heads/main/finalassets/modelData.png">

## Future Development

The main part of this model that, given more time, we would have liked to develop is allowing it to more accurately distinguish between different materials. Material properties are very complex to model, so the next step of development would be to use our experimental results to inform the code and give more accurate numbers to exactly how different materials behave. This extends beyond just different materials, and also includes how different weaves and types of fabric behave. 


## Analysis of results

placeholder

## Further applications

placeholder
