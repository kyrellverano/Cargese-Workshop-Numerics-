# Cargese-Workshop-Numerics-

This repository is for the Numerical Simulations Workshop during the Summer School in Cargese: Frontiers of Mixing.
More information about the summer school can be seen here: https://www.copermix-itn.eu/frontiers-of-mixing/

# Part 2: Finite-State-Controller
We approach a navigation problem as a memory augmented partially observable Markov decision process but highlighting the fact that we only use a low-dimensional finite memory. These memory states are the finite state controllers in optimizing the search process. In simple words, we derive an optimal searching behavior using an optimal strategy of updating memory states.
## Algorithm
We frame a source-tracking problem as a gridworld where a searcher (agent) navigates through an environment where the odor source (target) emits intermittent and uncorrelated signals. The searcher does not have any knowledge of its spatial position. The agent then uses these signals (odors) as cues to reach the target. The idea is that the more cues an agent receives, the closer it is to the source. Our task is to answer the question: how are these intermittent cues exploited to formulate an efficient strategy to locate an odor source? The set-up is a 2-dimensional grid wherein the target is at a fixed position and the agent starts downwind from the target. The state of the agent is an ordered pair of its x and y positions. Actions of the agent are: left, right, up, down (the code also working for an additional action:stay). From either a model of odor detection or from data, we derive a probability distribution of signals (observations) received given a state. A model of the environment is known: state position of the agent after an action and what is the reward to be received. In the set-up, we set a negative reward for each step until it reaches a target range centered at the source. In this way, maximizing the rewards also minimize the time it takes to reach the target. The policy is how the agent acts given a memory state and observation. It is also embedded here how the agent updates its memory thus it is a mapping from the current memory state, observation received to the action and memory update. This policy is parameterized and we implement a policy gradient to maximize the average rewards given a distribution of signals or observations. 
## Conda Environment
You have two options: Notebooks or Python Scripts. The first step is to download the folder FSC_NB (Notebooks) or FSC_PS (Python Scripts), depending on your choice. For both modes, there are some preliminary steps to create an environment which have the required versions of packages. The implementation of the algorithm makes use of a fortran code which needs to be compiled. 
```
conda create -n fmc python=3.8.5
conda activate fmc
conda install numpy=1.19.2
conda install scipy=1.5.2
conda install -c jmcmurray os
conda install -c jmcmurray json
conda install -c jmcmurray matplotlib
``` 
Download the python notebooks and utils.py then compile the fortran script by running the following:
```
f2py -c fast_sparce_multiplications_2D.f90 -m fast_sparce_multiplications_2D
```
After doing the installation/compilation above, you just need to activate the environment every time you use it again: `conda activate fmc` .

## Pre-saved policies and environment
