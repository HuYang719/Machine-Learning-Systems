# DAPPLE: A Pipelined Data Parallel Approach for Training Large Models

## Problem，Motivation， importance

pipeline parallelsim for heterogeneous network and synchronization training

PipeDream solve for async but in practice, sync is important for convergence  

## Method

Pivot stage: the stage with the least bubble overhead

The key idea of pivot stage is to find the bottlenect (cannot be optimized) stage for pipeline parallelism

Include communication as a stage and also follows the equation (1)



## Experiments



## Reviewer Comments



## Writing



## My Comments

1. the equation (1) for T_s (steady phase) is not suitable for steady phase when communication large than computation
   $$
   T_s = (M-1)(F_Q+B_Q)
   $$
   

2. Two problems are very interesting:
   1. low bandwidth and high latency, how the pipeline changed
   2. When the network becomes dynamic, how to cope? 

#### Evaluation (Novelty, Effective, Problem Size )

10,>10,10

#### What I can Learn

#### Which part could be improved

#### Future directions

