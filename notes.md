ML Assignment Notebook - WAT.ai W25

what is a seed?
- control randomness of proceesses to ensure reproducability
- random seeds ensure that processes produce the same results whenever scripts run:
    - in NNs: initilaizing weights, shuffling datasets, splitting data into test and train 
- reproducibility:
    - same results
- fair model comparisons:
    - testing diff models, we want fair comparison by keeping data split and initialzation consistent
- unexpected varibaility: 
    - w/o seeds, all changes can durastically lead to inconsistent results

issues with seeds:
- does not guarantee identical results across hardwares (specifically GPU-based computation)
- some operations willl introduce randomness beyond seed control

why use 42 for seeds?
- 42 is “the answer to life, the universe, and everything.”
- normally should be fixed

THERMAL DIFFUSIVITY
what is thermal diffusivity?
- how quickly heat spreads through a substance
- high -> heat spreads quickly
- low -> heat spreads slowly

parameters
- n_samples=1000 → Number of heat equation simulations (data points) to generate.
- nx=50 → Number of spatial grid points (dividing the material into 50 sections).
- nt=20 → Number of time steps (how many time intervals the simulation runs for).
- dx=0.02 → Spatial step size (distance between consecutive grid points, e.g., 0.02 meters).
- dt=0.001 → Time step size (how much time passes between each step, e.g., 0.001 seconds).


what is the split people usually do for datasets?
- 80 / 20 

TASK 1:
- goal:
    - take an initial temperature distribution (50 spatial points) and predict evolution over 20 epochs

- input:
    - a vector of size 50 (initial temps at 50 positons on a 1D rod)
- output:
    - a maxtrix (20 x 50), 50 positions over 20 epochs
- batch processing 

- what is a spatial point?
    - context: 1d heat equation
    - discrete positions along a 1d rod or material where temp is measured
- why use spatial points?
    - we are solving the equaition numerically 
    - dividing the rod into small sections using grid points (spatial points)
- how is a spatial point calculated?
    - dx = len(rod) / (num of points - 1)