## Reviewers



## Writing

1. However, large-scale models are too **compute- or memory-intensive** for resource-constrained edge devices.
2. Prior works **on** parallel and distributed execution **primarily** focus on training---rather than inference---using homogeneous accelerators in data centers.
3. We propose EdgePipe, a distributed framework for edge systems that uses pipeline parallelism to **both speed up** inference and enable runing larger (and more accurate) models that **otherwise cannot fit on** single edge devices.
4. EdgePipe improves throughput **by** aX **over** a 4-node baseline using 16 edge devices, which **independently cannot fit the model in memory**.
5. We show up to aX throughput improvement over the **state-of-the-art** PipeDream when using **a heterogeneous set of** devices.