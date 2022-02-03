
# Can Decentralized Algorithms Outperform Centralized Algorithms? A Case Study for Decentralized Parallel Stochastic Gradient Descent

## Problem，Motivation， importance

> Can decentralized algorithms be faster than its centralized counterpart
For low bandwidth and high latency, D-PSGD can outperform C-PSGD (even for multiple parameter servers)


## Method

Computation and communcaiton with neighbors can be overlap.
Model the decentralized communication topology with an undirected graph with weights: (V, W). 
V denotes the set of n nodes.
W_ij denote how much node j can affect node i.

Data:
(1) Let all distribution D_i are the same as D. Or,
(2) Let all distribution D_i are uniform.

D-PSGD is a synchronous parallel algorithm:
When the synchronization barrier is met, exchange with the neighbors and average the local variables.

## Experiments



## Reviewer Comments



## Writing



## My Comments

#### Questions
1. How does the degree of network topology affect the system performance? The whole experiments are based on ring toplogy, but without verification on more complex network.

For convergence rate, better connectivity will lower the upperbound, which is good for convergence. But for communicaiton part, that will cause more transmit traffic (increase the degree(network)), which seems a tradeoff. 



#### Evaluation (Novelty, Effective, Problem Size )

#### What I can Learn

#### Which part could be improved

#### Future directions

