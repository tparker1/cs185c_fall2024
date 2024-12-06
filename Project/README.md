# Numerical Analysis: How resolution changes output. 

## Project Description
In this project, I will investigate the effects of resolution on a global numerical ocean model. Specifically, I will compare the output after one year for a global model with 1-degree resolution to a global model with 0.5-degree resolution, each with a 60s time step. 
 
_How much can changing the grid resolution effect the model output?_
This experiment will explore how much the model output is altered by simply changing the grid resolution of the model. 
To investigate this question, I will run a model simulation beginning in 2008 for 1 year, using MITgcm. I will run the same model at a higher grid resolutions. Specifically, I will compare the 1-degree model to a 0.5-degree mode. 

I anticipate no major changes or instability from changing the grid resolution. I hope that grid refinement resolves some vertical artifcats found in the more coarse grid.  

For initial conditions, I will use the state of the ECCO Version 5 Model in January of 2008. 

For the external forcing conditions, I use the ECCO Version 5 model output and turn on MITgcm interpolation. To analyze the results, I will create a time series of the temperature at arbitrary points, and a video of the velocity magnitudes over time for each grid resolution.  


## Step 1: Create the Model Files
Several input files need to be created to run the model. Generate the following list of files using the notebooks indicated in paratheses:

- Model Grid (notebooks/9-1 Creating Model Grid.ipynb)
- Bathymetry (notebooks/9-2 Creating Bathymetry.ipynb)
- Initial Conditions (notebooks/10-2 Creating Initial Conditions.ipynb)
- Grid Prepping for MITgcm Interpolation (notebooks/Converting XC Range.ipynb)

### Creating the model grid
The code for create my grids can be found in `notebooks/9-1 Creating Model Grid`.

My experiement will require two grids: 
- A coarse grid of the entire planet, with a grid spacing of 1 (1-degree resolution) covering a grid of 360 columns and 180 rows. 
- A medium grid of the entire planet, with a grid spacing of 1/2 (0.5-dregree resolution) covering a grid of 720 columns and 90 rows. 

In the data file for my model, I will specifiy the following parameters in the `PARM04` namelist in the `data` file:

COARSE GRID
```
usingSphericalPolarGrid=.TRUE., 
delX = 1  
delY = 1  
xgOrigin = 0  
ygOrigin = -90   
```

MEDIUM GRID
```
usingSphericalPolarGrid=.TRUE., 
delX = 0.5  
delY = 0.5  
xgOrigin = 0  
ygOrigin = -90   
```

### Creating the bathymetry file
The code to create my bathymetry file can be found in `notebooks/9-2 Creating Bathymetry`. 

By running this notebook, we prepare the input bathymetry by smoothing and filling the land. 

This bathymetry will be implemented into the model by editing the `PARM05` dataset of the `data` file as follows:
```
 &PARM05
 bathyFile = 'global_bathymetry.bin,
 &
```

### Creating the Initial Conditions
The code to create my initial condition files can be found in `notebooks/10-2 Creating Initial Conditions`. 

This notebook will guide you through creating the initial condition grids for each resolution. 

These initial condition grids will be implemented into the model by editing `PARM05` in the `data` file as follows:
```
hydrogThetaFile = 'THETA_IC.bin',
hydrogSaltFile = 'SALT_IC.bin',
uVelInitFile = 'UVEL_IC.bin',
vVelInitFile = 'VVEL_IC.bin',
pSurfInitFile = 'ETAN_IC.bin',
```

### Prepping Grids for MITgcm Interpolation
The code to prepare the initial condition and bathymetry grids can be found in `noteboke/Converting XC Range.ipynb`

This notebook will shift input grids with `xgOrigin, ygOrigin = -180, -90` to `xgOrigin, ygOrigin = 0, -90` to align with MITgcm's built-in interpolation expectations. 


## Step 2: Add files to the computing cluster

Once the input files have been created, the model files can be transferred to the computing cluster. Begin by cloning a copy of MITgcm into your scratch directory and make a folder for each configuration, .e.g.

`mkdir MITgcm/configurations/global_ocean_coarse`

`mkdir MITgcm/configurations/global_ocean_medium`

Then, use the scp command to send the code, input, and namelist directories to the respective configuration directory.

## Step 3: Compile the model

Once all of the files are on the computing cluster, the model can be compiled. Make a build directory in each of the configuration directories and run the following lines:

../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make


## Step 4: Run the two models
### 4.1: Run the coarse grid model

After the compilation is complete, run the coarse grid model. Move to the respective run directory, link everything from input and code, and the submit the job script:

`sbatch cs185c_parker.slm`

### 4.2: Run the medium grid model

Next, run the medium grid model to complete the experiment. For this one, go to the medium grid configuration file, link everything from input and code, and the submit the job script:

`sbatch cs185c_m_parker.slm`

## Step 5: Analyze the Results

There are two notebooks provided for analysis:

[comment]    Analyzing Model Results

[comment]    This notebook is provided to have a quick look at spatial and temporal variations in the temperature field in the model with wind. It also generates the visualization provided in the figures directory.

[comment]  Answering the Science Question

[comment]    This notebooks provided some analysis plot to address the science question posed above.


