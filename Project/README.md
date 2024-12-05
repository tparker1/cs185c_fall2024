# Numerical Analysis: How resolution changes output. 

## Project Description
In this project, I will investigate the effects of resolution on a global numerical ocean model. Specifically, I will compare the output after one year for a grid of size SIZEXSIZE to a grid of size SIZE X SIZE.
 
_How much can changing the grid resolution effect the model output?_
This experiment will explore how much the model output is altered by simply changing the grid resolution of the model. 
To investigate this question, I will run a model simulation beginning in 2008 for 1 year, using MITgcm. I will run models at different grid resolutions: 1 degree and 11 degree. 

I anticipate no major changes or instability from changing the grid resolution. 

For initial conditions, I will use the state of the ECCO Version 5 Model in January of 2008. Similarly, 

For the external forcing conditions, I use the ECCO Version 5 model output and turn on MITgcm interpolation. To analyze the results, I will create a time series of the temperature at arbitrary points, and a video of the velocity magnitudes over time for each grid resolution. 

Limitations: Due to time and computing restraints the model will be run on a very coarse grid. Furthermore, this experiment does not consider the effects of underwater wave turbines on on coastal ecosystems or surfer well-being. 


## Creating the model grid
The grid for my model will be a coarse grid of the entire planet, with a grid spacing of 2 covering a grid of 180 columns and 90 rows. This coarse grid will enable me to run the model for longer. The code for the grid can be found in `notebooks/9-1 Creating Model Grid`.

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


