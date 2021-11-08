## Reference

[2017 ICLR]

@misc{papernot2017semisupervised,
      title={Semi-supervised Knowledge Transfer for Deep Learning from Private Training Data}, 
      author={Nicolas Papernot and Martín Abadi and Úlfar Erlingsson and Ian Goodfellow and Kunal Talwar},
      year={2017},
      eprint={1610.05755},
      archivePrefix={arXiv},
      primaryClass={stat.ML}
}



## Summary

Motivation: privacy--- avoid using user's model/activation/dataset to train server's model.

Method: Use multiple teacher model and their ensmble to train the student model. Adopt dfferential privacy to anlysis the private loss, which is a good analysis

Evaluation: Only on MNIST and SVHN dataset. 

Repo: (unofficial) https://github.com/kamathhrishi/PATE



Limitation: More focus on privacy anlysis, dataset is relatively small, do not sure on the larger datset, whether the accuracy has a huge lost.

What we can learn? I do not undertant their differential privacy anlaysis, but I am sure it is a useful tool and  I should learn it.



## Writing

1. A model may inadvertently and implicitly store some of  its training data; careful analysis of the model may therefore reveal sensitive information.
2. Recent attacks exploiting this implicit memorization in machine learning have demonstrated that private, sensitive training data can be recovered from models.
3.  Such attackes can proceed directly, byanalyzing internal model parameters, but also indirectly, by repeatedly querying opaque models to dather data for the attack's analysis. 
4. In this strategy, first, an ensemble, of teacher models is trained on disjoint subsets of the sensitive data.
5. Then, using auxiliary, unlabeled non-sensitive data, a student model is trained on the aggregate output of the ensemble, such that the student learns to accurately mimic the ensemble.