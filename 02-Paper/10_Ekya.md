# Ekya: Continueous Learning of Video Analytics Models on Edge Compute Servers



## Problem

Compressed model -> data drift -> need retraining -> need resource schedule for jointly retraining and inference -> trade off throughput, accuracy, latency, resources



## Writing 

1. In fact, **with bandwidths typical in edge deployments**, cloud-based solutions are slower and **result in** lower accuracies.
2. **Advances in computer vision research** have led to high-accuracy DNN models **that** achieve high accuracy with a large number of weights, deep architechtures, and **copious training data**.
3. The most common approach to **addressing the resource constraints** on the edge is to train and deploy specialized and compressed DNNs, **which consist of** far fewer weights and shallower architecures.
4. As a result, specialized edge DNNs are **particularly vulnerable** to data drift, where live video data **diverges significantly from** the initial training data.
5. **Owing to** their ability to memorize limited amount of object variations, to maintain high accuracy, edge DNNs have to be continuously updated with the recent data and to the changing object distributions. 
6. The joint approach utilizes resources better than **statically provisioning compute** for retraining on edge servers.
7. Thus, careful selection of the configurations **considerably impacts the resource efficiency**.