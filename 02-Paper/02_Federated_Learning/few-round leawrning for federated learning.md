## Motivation

1.FL needs a large number of communication rounds

2.Cause a significant challenge in (i) bandwidth-limited or (ii) time-sensitive applications (connected vehicles or drones)

(i) bandwidth-limited: cause slow transmission, but there is no quantative results to evaluate the relationship between bandwidth and the transmission data size; furthermore, do we have anyother methods to improve (e.g. data/gradients compression?)

(ii) time-sensitive applicaitons, why cannot start learning process when they stop? We only need data and they could store data after finishing moving.



3. Clients can have unseen data compared to the preparation in the server, current method cannot tacle with this.

## Method

meta-train an initial model 

![img](https://pic4.zhimg.com/80/v2-23b952fb974edeffa4e28d0065440227_720w.jpg)





## Experiments



Compare with R-round FedAvg algorithm on CIFAR-100, miniImageNet, FEMNIST. 



## Rebuttal

#### Reviewer 1

- Larger datasets: author conduct on tinyImageNet. + explain we used **FEMNIST** and CIFAR 100 with more classes.
- [-] No real testbed, only simulation. author: focus on accuracy, and other work like FedAVG FedProx also only have simulation



#### Reviewer 3

1. **Comment regarding our non-IID scenario:** We stress that the non-IID scenario that we considered (which is also adopted in [McMahan17], [Sattler20]) is a strong model of non-IIDness; each client has data samples of only one or two classes (among 64 classes for CIFAR-100 and miniImageNet), making the local data of each client significantly biased and leading to a strong non-IID scenario. As the number of classes in the local dataset increases, we have a weaker non-IID scenario; in an IID setup, each client has all 64 classes in its local data.

   [McMahan17] H. B. McMahan et al., “Communication-efficient learning of deep networks from decentralized data,” AISTATS 2017.

   [Sattler20] F. Sattler et al., "Robust and communication-efficient federated learning from non-iid data," IEEE Transactions on Neural Networks and Learning Systems, 2020.

## Summary

[  ]  Meta Learning

Motivation and problem should be the key of one paper.









