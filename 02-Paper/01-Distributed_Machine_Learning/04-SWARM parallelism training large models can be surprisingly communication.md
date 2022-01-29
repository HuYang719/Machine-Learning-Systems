# SWARM Parallelism: Training Large Models Can Be Surprisingly Communication-efficient



## Problem，Motivation， Importance

- Problem: Training large models (13B parameters) for unreliable devices under low bandwidth (400mbps)

- Motivation: HPC in data center is notoriously expensive for researchers. Use more cost-efficient distributed training /the help of volunteers to train large models
- Importance: let everyone has the ability to train large-scale model!  

## Method

- Suqire-cube law
- Pipeline parallelism for unrealiable connection
- Compression-aware architectures: maxout method on the partitionable layer in every stage (now not sure the results)
- 

## Experiments



## Reviewer Comments

1. A lthough large model can increase computation efficiency, the author does not justify **learning quality** and **time-to-solution**

   > It will be nice to see if the authors could get comparable results to an existing Transformer model only using the maxout trick.

   > Ans: we argue that SWARM is more cost-efficient than strategies for training large models

2. The background and related work section lacks detail in the field of model-parallelism, see e.g. Ben-Nun, T., & Hoefler, T. (2019). Demystifying parallel and distributed deep learning: An in-depth concurrency analysis. ACM Computing Surveys (CSUR), 52(4), 1-43. On the other hand, the section on data-parallelism is quite extensive even though not really relevant for this paper. Moreover, some of the work in this section is comparably old and not state-of-the-art any mor

3. O(n^3) and O(n^2) are theoritical and are upper bound (consider highly parallelism on GPU for computation and all reduce techniques for communication). **Compare upper bound is meaningless**

4. Not demonstrate how to handle leaving or joining

   >  One can easily think of situation where all peers in one swarm are idle and hence all leave to an other stage, leaving the swarm empty? How do you avoid such deadlocks?

   Motivation, not cheap the devices! 

5. > One of the main motivations of their work is that highly specialized hardware is expensive and hence not available to many researchers in developing countries. Yet all experiments are run on T4 cloud devices and A100s. This is not cheap hardware! The argument is that one could use many cheap devices instead of fewer high-end ones. How many of these devices would I actually need? And what about the connections between those devices? Would the cost of the network not outweigh the saving for compute devices?

## Writing



## My Comments

**In fact, we can estimate the training time with joining users and the model and data size.**

The compression and decompression parameters need to be training

1. it is too early for us to consider adaptive scheduling?
2. pipeline parallelism with model compression, but the problem leaves in the increased stages, when the stages increases 
3. Stages 多长才好，怎么去分配stage和data parallelism的比例？
4. 异构情况下，他们怎么决定stage的长度呢？

#### Evaluation (Novelty, Effective, Problem Size )

Problem Size: 100

- Solve this can make more internet-based devices join in training
- Different from the data center scenario

Novelty: 1

- Random wire seems werid 
- Compression model is a common technique

Effective: 



#### What I can Learn

#### Which part could be improved

#### Future directions

