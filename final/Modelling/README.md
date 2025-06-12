# Modelling Overview 

This document will aim to set out an overview of how to use the code in the model provided within this repository. For more details regarding the inner design and core modelling, see final/Modelling/ModellingMethods.md. 

## Defining New Inputs

Inputs are defined through a set of different classes. New inputs should be defined in the "Input Database" section of the notebook. Currently there are three fans, two tanks, three different materials and two sets of air conditions defined there, all of which can be accessed and edited. The details of each class are included in the detailed explanation, but below are a list of classes and what parameters are required to define the class fully:

AP:

Used to define the air in the tank.

``` Ruby
air = AP(T,R)
```

Where T is the air temperature (Dry Bulb Temperature in Kelvin) and R is the relative humidity (expressed as a decimal from 0-1)

fanSpec:

Used to define behaviour of the fan. Currently only uses the CFM feature, however built in power feature means power per temperature drop can be calculated. The fan also has a "mode" setting that can either be set to "single" or "dual" currently (defaulting to single if not specified)

``` Ruby
fan = fanSpec(P, CFM, mode = 'single')
```

tankGeo:

Defines the geometry of the tank. Currently assumes a cylindrical tank in a cylindrical kiosk shell. 

``` Ruby
tank = tankGeo(Router, Rinner, tankHeight, t, k)
```
Router is the kiosk inner radius, Rinner is the tank outer radius, tankHeight is the height of the tank, t is the tank wall thickness and k is the thermal conductivity of the material the tank is made out of.

mat:

Defines the material used for the tank's evaporative jackte:

``` Ruby
material = mat(k,t,msat,density,porosity)
```
k is the thermal conductivity, t is the fabric, msat is the maximum mass of absorbable water per unit mass. Porosity refers to the proportion of volume of the fabric that is composed of voids. This parameter depends on the weave and if is not publicly available can be found easily weighing the mass of a sample and calculating its porosity when dry based on the volume of the fabric. Msat can be determined similarly if numerical data is not available by soaking a sample of fabric and dividing its mass change by its initial mass. There is an additional factor "em" used to define emissivity. This can depend on the coating of the fabric and is set by default to 0.87 as a benchmark for uncoated fabrics (https://www.thermoworks.com/emissivity-table/). 


## Using Functions

There are two functions available to be used in this script: "simulateTemp and coolingTime". Although there are other functions defined, they are primarily intermediary functions used to make the calculation process more modular. 

simulateTemp:

This is the main output function, and can be used to determine the evolution of the water tank temperature with time. It is defined as such

``` Ruby
results = simulateTemp(tank, fan, material, air, S, TwInitial, tmax = 86400, dt = 300, mode = 'constant')
```
S is the saturation ratio. It is the fraction of msat that you want to let the material absorb. Essentially it is a decimal from 0-1 that tells you how wet the fabric is, with 1 being soaked and 0 being dry. Twinit is the initial temperature of the water, whether that  is the tap water temperature or the air temperature (if the tank has been sitting outside for a while). tmax and dt set how long and over what time intervals the data is produced (in seconds). The smaller dt is, the more accurate the plot will be, but the longer the run time is. By default, it is set to simulate a day in 5 minute intervals (for full scale tank operation, dt = 1800 / 30 mins may be suitable). 

the "mode" is set to be either "constant" or "drying". Constant assumes that water is being added back as fast as it is being lost, whilst drying assumes that no water is being added back at all.

simulateTemp returns a length 3 array composed of the final temperature, the time steps which data was taken at (5 mins, 10 mins etc) and the temperatures at each of those times. An example code segment is

``` Ruby
results = simulateTemp(tank, fan, material, air, S, TwInitial, mode = 'constant')
print(results[0])
plt.plot(results[1],results[2])
plt.show()
```
Which will print the temperature at the end of the day and plot the temperature evolution across that day.

coolingTime:

Cooling time determines how long it takes for the fabric jacket to dry out from a starting saturation to a target final saturation. This takes the same parameters as the simulateTemp variable, as well as the initial and final saturation ratios. Much like with simulateTemp, it uses a time based difference method to solve for the cooling time, using time steps of dt. By default dt is set to 5 minutes, however it is recommended to change this for full scale kiosk modelling.

``` Ruby
coolingTime(tank, fan, material, air,TwInit, SInit, SFinal, dt = 300) # Retuns drying time in minutes

```

For example

``` Ruby
timetoDry = coolingTime(tankReal, fanReal, cotton, airReal, tempAvg , 1, 0, dt = 1800) # Retuns drying time in minutes
print(timetoDry)
```
tempAvg = 33 $\degree C$ (a reference temperature defined in the input database for "airReal" - based on https://www.climatestotravel.com/climate/tanzania). This will return the amount of time it takes for a cotton jacket wrapped around the full scale tank to fully dry out (taking dt = 30 minutes). 












