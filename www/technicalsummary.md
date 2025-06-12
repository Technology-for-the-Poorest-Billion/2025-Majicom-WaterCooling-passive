---
title: Technical Summary
---


## Numerical Model 

The first aspect of our project was to code a virtual simulation of the Majicom Kiosk. The aim of this code was to predict how the water would behave as the environment or the design of the kiosk was changed and evolved. As the code was produced we found that we could also use this to try and replicate the experimental results by treating it as a scaled down version of the kiosk. The full annotated code can be found [here](https://colab.research.google.com/drive/1D8jrgBWuxRUjkXFdTaMW2er6YYpis4Rj?authuser=1#scrollTo=mpWEDmWmkx8X)

We used a simple heat exchange model shown below to understand all of the different sources of energy in and out of the water: Heat from the air, radiation from the tank walls and energy taken away by the evaporative cooling. These all have a complex interplay that are affected by the design of the rest of the tank. Being able to test how changing the tank quickly through this model makes it much faster to test different cooling jackets, and helped to provide some early insight into our ideas. 

<img width="600" alt="Tank Diagram" src="https://raw.githubusercontent.com/Technology-for-the-Poorest-Billion/2025-Majicom-WaterCooling-passive/refs/heads/main/finalassets/TankDiagram.png">

To show a small demonstration of this, we attempted to simulate the water temperature inside the tank for two different coating materials: Cotton & Linen. These results can be seen below, and show clearly how this can be used to estimate the final temperature of the water and how quickly it is able to cool the water down.

<img width="600" alt="Model Result" src="https://raw.githubusercontent.com/Technology-for-the-Poorest-Billion/2025-Majicom-WaterCooling-passive/refs/heads/main/finalassets/modelData.png">



## Additional Data

One of the main benefits of trying to simulate the system as a whole is that it allows us to control a very broad range of inputs to get different results. As well as controlling material, we can control how the air temperature or other important conditions affect the water temperature. 



This graph is an example of this. It looks at how the temperature and humiditiy affects the temperature of the water. This is vital for determining how cooling varies from the wet to dry season. We find, for example, in the dry season when the air temperature increases and the humidity decreases, we achieve a more effective cooling than we do during the wet season. This value is marked on the graph above. This also helps Majicom inform any future decisions, such as whether it is worth putting in additional energy to dry out the air further, even if that means heating it up 




## Future Development

The main part of this model that, given more time, we would have liked to develop is allowing it to more accurately distinguish between different materials. Material properties are very complex to model, so the next step of development would be to use our experimental results to inform the code and give more accurate numbers to exactly how different materials behave. This extends beyond just different materials, and also includes how different weaves and types of fabric behave. 


