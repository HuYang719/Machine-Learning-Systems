# Ekya: Continueous Learning of Video Analytics Models on Edge Compute Servers



## Summary

- Motivation: Compressed model -> data drift -> need retraining -> need resource schedule for jointly retraining and inference -> trade off throughput, accuracy, latency, resources

- Method: Victim-Thief Scheduler 

- Comparison: Uniform Scheduler

- Implementation: PyTorch + Ray 



## Limitation

- Assume all devices are homogeneous and can hold the model

- Do not consider the network (AWS EC2), and also the dynamic change in available computation resources

- Only for one application, the constraints (throughput, latency, accuracy) are fixed

- Retraining window (time factor) is fixed and cannot changed, however, this may be different for different time period (eg. Rainy day need a small window) and different applications

- Only compare with uniform scheduler. Baseline is relatively weak

  

## Writing 

1. In fact, **with bandwidths typical in edge deployments**, cloud-based solutions are slower and **result in** lower accuracies.
2. **Advances in computer vision research** have led to high-accuracy DNN models **that** achieve high accuracy with a large number of weights, deep architechtures, and **copious training data**.
3. The most common approach to **addressing the resource constraints** on the edge is to train and deploy specialized and compressed DNNs, **which consist of** far fewer weights and shallower architecures.
4. As a result, specialized edge DNNs are **particularly vulnerable** to data drift, where live video data **diverges significantly from** the initial training data.
5. **Owing to** their ability to memorize limited amount of object variations, to maintain high accuracy, edge DNNs have to be continuously updated with the recent data and to the changing object distributions. 
6. The joint approach utilizes resources better than **statically provisioning compute** for retraining on edge servers.
7. Thus, careful selection of the configurations **considerably impacts the resource efficiency**.
8. The uncertainty of X resembles the multiarmed bandits (MAB) to maximize the expected rewards given a limited number of trails for a set of options.
9. In fact, even when we cached and reused models from prior retraining winodws with similar class distributions, the accuracy was still **substantially lower due to** other factors **that are difficult to model like** lighting, angle of objects, density of the scene, etc. Thus we adopt an online approach for edstimation by using the current retraining window's data.
10. The above insights inspired our approach, called micro-profiling, where for each video, we test various retraining configurations, but on a small subset of the retraining data and only for a small number of epochs (well before models converge).

Non-Stop! Non-Stop! Non-Stop!