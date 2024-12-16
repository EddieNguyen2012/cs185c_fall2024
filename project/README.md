# Impact of Southeast Asian Monsoons and La Nina/El Nino on Ocean Stratification and Circulation using MITgcm

The goal of this project is to model and analyze the impact of the Southeast Asian monsoon system 
(both the Southwest and Northeast monsoons) together with El Nino/La Nina on ocean stratification and circulation patterns,
particularly in the South China Sea and adjacent regions.

## Project Description
How do seasonal monsoons in southeast Asia impact ocean stratification?

In this project, my region of interest will be from 99-122E and 2-25N, which includes South China Sea and Gulf of Thailand. My model will
run with the duration of 1 year but two times: one simulate the year with El Nino and another during La Nina year. Specifically, I will use ECCO Version 5 2015
data to simulate the El Nino model as this is one of the strongest El Nino events in
recent years. Then the La Nina after that in 2017 will be chosen for the other model. I expect the El Nino model to have
weaker trade wind, higher temperature and lower salinity due to the effect of the event. 

As of right now, I expect to create a timeseries model to represent the output temperature and salinity from both models then comparing
them to see the difference between the 2 models. I want to investigate seasonal variations in ocean stratification, particularly
changes in temperature and salinity profiles. Then, Analyze the differences in vertical temperature and salinity profiles between the El Nino
conditions in 2015 and the La Nina conditions in 2017, focusing on changes in stratification and mixed layer depth during each monsoon season.

## Reproducing Model Results

The following steps outline how to construct the model files, configure and run the model, and assess the model results.

### Step 1: Create the Model Files
Several input files need to be created to run the model. Generate the following list of files using the notebooks indicated in paratheses:
- Model Grid (Creating the Model Grid.ipynb)
- Bathymetry (Creating the Bathymetry.ipynb)
- Initial Conditions (Creating the Initial Conditions.ipynb)
- External Forcing Conditions (Creating the External Forcing Conditions.ipynb)
- Boundary Conditions (Creating the Boundary Conditions.ipynb)
The model files should be placed into the  `input` directory.

### Step 2: Add files to the computing cluster
Once the input files have been created, the model files can be transferred to the computing cluster. Begin by cloning a copy of [MITgcm](https://github.com/MITgcm/MITgcm) into your scratch directory and make a folder for the configuration, .e.g.
```
mkdir MITgcm/configurations/ca_upwelling
```
Then, use the `scp` command to send the `code`, `input`, and `namelist` directories to your configuration directory. 

### Step 3: Compile the model
Once all of the files are on the computing cluster, the model can be compiled. Make a `build` directory in the configuration directory and run the following lines:
```
../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make
```

### Step 4.1: Run the model for 2015
After the compilation is complete, run the model using the 2015 data. Move to the `run` directory, link everything from `input` and `code`, and the submit the job script:
```
sbatch cs185c.slm
```

### Step 4.2: Run the model for 2017
Again, link everything from `input` and `code` to a directory called `run_2017`. Then, edit the `data.cal` file to change the `startDate_1` to `20170115`. Then, submit the job script again to rerun the model.

### Step 5: Analyze the Results

All the analysis steps and results are in `Result Visualization.ipynb`. It also generate a video in `frames` folder to visualize the
change of stratification.
