ML Assignment Notebook - WAT.ai W25

SEEDS
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
