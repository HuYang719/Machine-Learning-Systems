# Throughput-Optmal Topology Design for Cross-Silo Federated Learning

## Problem，Motivation， importance

> Server-client architecture may be inefficient in cross-silo settings, as close-by data silos with high-speed access links may exchange information faster than with the orchestrator, and the orchestrator may become a communication bottleneck.
 
Topology Design for cross-silo federated learning with decentralized periodic averaging stochastic gradient descent. DPASGD 



## Method

1. Modeling the time interval d_o between the beginning of a local comptation and then receive from other nodes and update the model.
2. Modeling the cycle time, which equals the mean circuit d_o time. Minimize the cycle time equals to max the throughput.
3. Leverage known algorithm for minimal cycle time (MCT) problem:
	(1) When the network is edge-capacitated (high link capacity without congestion), MST is a solution of MCT when G_o is undirected.
	(2) When the network is edge-capacitated but the G_0 need to be digraph, Christofides' algorithm is a 3N-approximation for MCT.
	(3) When the newwork is node-capacitated (congestion at access links), Algorithm 1 is a solution when G_o is undirected and Christofides' algorithm is a 3N-approximation algorithm for MCT for digraph solution. 


## Experiments
Compared with MATCHA


## Reviewer Comments
Convergence rate?
Authors: Spectral properties of the topology do have an effect on the number of iterations to converge. But there is evidence that, in practice, this effect has been over-estimated by classic worst-case convergence bounds from [23,71,73]. The topology has a more significant effect on system throughput
than on the number of iterations to converge [5, Figs. 1b and 3] with sparser topologies achieving higher accuracy after the same time [5,Table 5]. 


## Writing
Clear.


## My Comments
1. I wonder the whether their setting is hold if there is strong data heterogeneity. Notice during the experiments, the dataset (iNaturalist) is assigned half of the **uniformly** at random. This definitely can improve the final accuracy. However, is it practical in reality? So, I feel they do not include (or only weak) data heterogeneity.
2. For theoretical part, it is a strong paper. If we only consider throughput, may be hard to compete with them.
3. This paper is still worth learning, especially their modeling method and how they cope the topology graph. 


#### Evaluation (Novelty, Effective, Problem Size )
 10, >10, > 10
#### What I can Learn
Theoretical part.
#### Which part could be improved
Feel many assumptions for these cross-silo federated learning (high-speed, stable network/ data heterogeneity)
And the final accuracy part is not well explained. 
#### Future directions
With strong data heterogeneity?

