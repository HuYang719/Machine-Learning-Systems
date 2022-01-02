# FedNLP: Benchmarking Federated Learning Methods for Natural Language Processing Tasks



## Summary

A benchmark for federated learning algorithm on NLP tasks. Evaluated FedAvg, FedOPT, FedProx on Text Classification, Sequence Tagging, QA, Seq2Seq (translation) tasks. 





## Experiments



![image-20220102133007493](/Users/lucyyang/Library/Application Support/typora-user-images/image-20220102133007493.png)



#### How do popular FL methods perform differently under the same settings?

FedOpt performs better than the other two methods, with only exception being in the seq2seq generation task.

May be the difference in terms of the loss functions have a great impact on FL performance.



#### How do different non-IID partitions of the same data influence FL performance?

Non-IID and label distribution shift have large impact, but quantity skew does not introduce a greate challenge for FL when the label distribution is closer to the uniform one.

Personalized FL may mitigate the data heterogeneity. 

Comment: Interesting, devices heterogeneity, network heterogeneity, data heterogeneity, 

#### Are compact model DistillBERT adequate for FL+NLP?

BERT has 2X larger communication cost than DistilBERT 

![image-20220102134913247](/Users/lucyyang/Library/Application Support/typora-user-images/image-20220102134913247.png)

## Future Direction





## Comments

