# Extreme Coastal Wave Harvesting

## Project Description
In this project, I will investigate the effects of excessive wave energy harvesting on global ocean currents. That is:
 
_How would harvesting coastal wave energy impact ocean currents?_
For example, imagine if all of Earth’s shores were lined with underwater wave turbines. 

This experiment will explore how much of the ocean’s energy is contained in shore waves, and the long-term consequences of converting shorelines to energy sinks. 
To investigate this question, I will create a very coarse model of Earth and run the model simulation for approximately 10+ years (hopefully 50+), beginning in 1980. I anticipate that if the model can run for a sufficiently long time, we will see a slowing of ocean currents. 

For initial conditions, I will use the state of the ECCO Version 5 Model in January of 2008. Similarly, I will construct boundary and external forcing conditions for this model from the ECCO Version 5 model output. To analyze the results, I will create a time series of mean velocity magnitudes. For visualization, I will create two movies of velocities: one with the shore velocity sinks and one without. 

Limitations: Due to time and computing restraints the model will be run on a very coarse grid. Furthermore, this experiment does not consider the effects of underwater wave turbines on on coastal ecosystems or surfer well-being. 


## Creating the model grid
The grid for my model will be a coarse grid of the entire planet, with a grid spacing of 1/2 covering a grid of 360 columns and 180 rows. This coarse grid will enable me to run the model for longer. The code for the grid can be found in `notebooks/9-1 Creating Model Grid`.

In the data file for my model, I will specifiy the following parameters in the `PARM04` namelist in the `data` file:

```
usingSphericalPolarGrid=.TRUE., 
delX = 2  
delY = 2  
xgOrigin = -180  
ygOrigin = -90   
```

## Creating the bathymetry file
The code to create my bathymetry file can be found in `notebooks/9-2 Creating Bathymetry`. 

This bathymetry will be implemented into the model by editing the `PARM05` dataset of the `data` file as follows:
```
 &PARM05
 bathyFile = 'global_bathymetry.bin,
 &
```


