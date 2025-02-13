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

- what is a spatial point?
    - context: 1d heat equation
    - discrete positions along a 1d rod or material where temp is measured
- why use spatial points?
    - we are solving the equaition numerically 
    - dividing the rod into small sections using grid points (spatial points)
- how is a spatial point calculated?
    - dx = len(rod) / (num of points - 1)

- fully connected layers:
    1. 50 spatial points (neurons) to 128 neuerons
        - allows the model to learn complex spatial features
        - extracts sptaial relationships in the input (temp distribution)
    2. 128 neurons to 256 neurons
        - increases learning capactity yielding complex dependecies
    3. 256 neurons to 1000 neurons
        - output should have 1000 neurons (20 x 50) 

- forward pass
    - using ReLU
    1. passes x thru fc1 (fully connected layer 1) maps 50 to 128
        - ReLU introduces non-linearity to capture complex patterns
    2. passes x thru fc2 (fully connected layer 1) maps 50 to 256
    3. maps 256 to 1000 
        - no activation since predicting continuous temp vals (regression task)
    4. retval is reshaping output to be 20 x 50

TASK 2:
- loss fcn and optimizer
    - MSE (loss): since this a regression task (predicting cts values)
    - ADAM (optimizer): updates the weights efficiently
    - learning rate: updates how much weights adjust per step
- data -> pytorch tensors
    - reshaping data 
- iterating for 100 epochs
    - zero gradients: clear previous gradients to acoid accumiulation from past updates
    - fwd pass: make predictions
        - output shape is (batch, 20, 50)
    - computing loss: uses the MSE to compare predictions to actual vals
    - bckwd pass: computes gradients (how much weights shld be adjusted)
    - update weights: uses gradeints from bckwd pass to update weights

TASK 3: 
- set model to evaluation mode
    - ensures dropout layers wld be disabled
    - batch normalization wldnt update during inference
    - allows consistent predcitions
- convert test data to tensors (from numpy arrays)
- predict without gradients
    - reduced memory
    - speeds up inference
- use MSE to measure deviation between prediction and actual
    - flatten so it can be used across all vals
- randomly choose a test sample to visualize 