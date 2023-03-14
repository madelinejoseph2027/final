# THE FINAL

## In a nutshell
"Educational" Video: https://www.youtube.com/watch?v=7oJAp_oXcQE

**Cartoon here**


## Usage

Please make sure all of the attending files from this repository are present in your working directory (e.g., by cloning this repo to your local system).

Run the following in the command line:

```bash
python3 search.py
```

## Output

For computational efficiency, the algorithm is set to evolve 50 generations of "horses" from an initial population of 1 random parent. The initial parent (generation 0) will be displayed in the pybullet GUI. After the evolution process completes, the single best individual will be displayed in the GUI. The number of generations and the population size can be changed in ```constants.py``` as desired.

**The text file "BestFitnesses.txt" contains a comma-separated list of the fitnesses of the best individual in a population for each generation.**


## Algorithm Details
**Add corresponding code for each part**

The hillClimbingHorse is a set of pybullet/pyrosim-based functions that evolves a 3-dimensional robot, comprised of randomly sized, sensorized, and motorized rectangular pieces, that moves to the right.

The algorithm generates a "horse" by pre-defining a thoracic length of 2 to 5 links. The links' dimensions can range in size from 0.1 to 3.0 units. The algorithm then adds "limbs" into x, y, and z directions. These segments are random in size, but are **bilaterally symmetric** (to mimic most animals), such that if a "limb" exists on one side of the horse, its mirror image exists on the other. Sensors, motors, and synaptic weights are assigned at random based on a coin toss (boolean variable randomly set to 0 or 1).

The following diagram shows an example "horse." Green links are sensorized, while blue are unsensorized. Green joints are motorized, while blue are unmotorized (this wouldn't actually be reflected in the output – joints are not colored). Synapses are active if they connect to a sensorized link with a motorized joint. A synapse that connect a unsensorized and/or unmotorized joints are inactive. The mirror plane, which defines the bilateral symmetry of the "horse," runs perpendicular to the viewer's line of vision. 

![Body-Brain Diagram](https://user-images.githubusercontent.com/122245493/220243994-f18b9ff8-2993-41eb-a7e1-76335d226b88.jpg)


The algorithm evolves horses optimized for locomotion using the parallel hillclimber model. In brief, an initial random parent is generated and then cloned. The cloned child will be mutated in one way. To prevent confounding changes (i.e., combinations of changes whose effects' origin can not be deconvoluted from the multiple changes), **either** the body or brain of the child is mutated. A coin toss determines if the brain or body is varied. If the brain is varied, a secondary coin toss determines if a sensor or synaptic weight is changed. If the body is varied, that secondary coin toss determines if a section is added or removed. The parent and mutated child are then "competed" against each other based on some metric of fitness. Whichever individual has the superior fitness is preserved for further mutation and competition, while the other is discarded. In this instance, locomotion to the right (measured as average x-position of the leftmost legs) is the fitness function. The following diagram shows the basic scheme of the evolutionary algorithm. 

![EvAlgo](https://user-images.githubusercontent.com/122245493/221730155-d7553383-cfa0-45ff-8c91-202135178db7.jpg)


## Sample Results

A selection of 4 unevolved vs. 4 evolved robots:

![MJ_FinalTrailer](https://user-images.githubusercontent.com/122245493/225088909-6dc0739b-2c02-40d6-b38b-9bcea8ea876c.gif)


The following curves show the results of 5 runs of the evolutionary algorithm. This plot represents 100 generations of populations of 10 individuals which were evolved and competed. The diagram tracks the fitness of the best individual of the 10 across those 100 generations. 

![FitnessCurve](https://user-images.githubusercontent.com/122245493/221730753-45c95812-b2ba-484c-9754-fe268de0dd6c.png)



## Citations
Bongard, J. [u/DrJosh]. “Education in Evolutionary Robotics” Reddit, 6 Feb. 2023, https://www.reddit.com/r/ludobots/.

Kriegman, S. Artificial Life, Northwestern University, Evanston, Illinois, Winter 2023.
