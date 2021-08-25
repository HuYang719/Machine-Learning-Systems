# Lab-1 Report



## Experimental Enviroments



|          |               |               |
| -------- | ------------- | ------------- |
| Hardware | CPU（# vCPU） | 2             |
|          | GPU           | /             |
| Software | OS Version    | macOS Mojave  |
|          | Package       | PyTorch-1.9.0 |
|          | CUDA Version  | /             |
|          |               |               |

 

## Experimental Results

###  Visualizing Models and Results

Note: use `tensorboard --logdir=logs ` 



##### Network Data Trend

<img src="/Users/lucyyang/Library/Application Support/typora-user-images/image-20210825225131760.png" alt="image-20210825225131760" style="zoom:30%;" />



<img src="/Users/lucyyang/Library/Application Support/typora-user-images/image-20210825225228704.png" alt="image-20210825225228704" style="zoom:50%;" />

##### Loss and Accuracy Trend



![image-20210825224834117](/Users/lucyyang/Library/Application Support/typora-user-images/image-20210825224834117.png)



![image-20210825224848318](/Users/lucyyang/Library/Application Support/typora-user-images/image-20210825224848318.png)



##### Operations

from profile results:

```
---------------------------------  ------------  ------------  ------------  ------------  ------------  ------------  
                             Name    Self CPU %      Self CPU   CPU total %     CPU total  CPU time avg    # of Calls  
---------------------------------  ------------  ------------  ------------  ------------  ------------  ------------  
                     aten::conv2d         0.71%     903.317us        32.73%      41.396ms      41.396ms             1  
                aten::convolution         0.01%      17.259us        32.02%      40.492ms      40.492ms             1  
               aten::_convolution         0.61%     775.225us        32.01%      40.475ms      40.475ms             1  
         aten::mkldnn_convolution        31.36%      39.654ms        31.39%      39.700ms      39.700ms             1  
                      aten::empty         0.02%      25.299us         0.02%      25.299us      25.299us             1  
                aten::as_strided_         0.02%      20.716us         0.02%      20.716us      20.716us             1  
                       aten::relu         0.47%     597.455us         1.53%       1.940ms       1.940ms             1  
                  aten::clamp_min         0.02%      27.279us         1.06%       1.343ms       1.343ms             1  
                      aten::empty         0.00%       5.226us         0.00%       5.226us       5.226us             1  
                  aten::clamp_min         1.04%       1.310ms         1.04%       1.310ms       1.310ms             1  
                     aten::conv2d         0.00%       4.681us        35.13%      44.421ms      44.421ms             1  
                aten::convolution         0.00%       4.980us        35.12%      44.416ms      44.416ms             1  
               aten::_convolution         0.01%      14.663us        35.12%      44.411ms      44.411ms             1  
         aten::mkldnn_convolution        35.09%      44.379ms        35.11%      44.397ms      44.397ms             1  
                      aten::empty         0.01%      14.540us         0.01%      14.540us      14.540us             1  
                aten::as_strided_         0.00%       3.650us         0.00%       3.650us       3.650us             1  
                       aten::relu         0.01%      15.720us         0.94%       1.183ms       1.183ms             1  
                  aten::clamp_min         0.00%       5.479us         0.92%       1.167ms       1.167ms             1  
                      aten::empty         0.00%       2.878us         0.00%       2.878us       2.878us             1  
                  aten::clamp_min         0.92%       1.159ms         0.92%       1.159ms       1.159ms             1  
                 aten::max_pool2d         1.00%       1.266ms        10.86%      13.731ms      13.731ms             1  
    aten::max_pool2d_with_indices         9.86%      12.466ms         9.86%      12.466ms      12.466ms             1  
            aten::feature_dropout         0.42%     533.460us         4.71%       5.959ms       5.959ms             1  
                      aten::empty         0.01%       9.312us         0.01%       9.312us       9.312us             1  
                 aten::bernoulli_         2.31%       2.918ms         2.34%       2.959ms       2.959ms             1  
                      aten::empty         0.03%      40.485us         0.03%      40.485us      40.485us             1  
                       aten::div_         0.04%      54.159us         0.56%     704.197us     704.197us             1  
                         aten::to         0.48%     603.033us         0.51%     650.038us     650.038us             1  
              aten::empty_strided         0.00%       3.819us         0.00%       3.819us       3.819us             1  
                      aten::copy_         0.03%      43.186us         0.03%      43.186us      43.186us             1  
                        aten::mul         1.39%       1.753ms         1.39%       1.753ms       1.753ms             1  
                    aten::flatten         0.02%      19.643us         0.03%      41.842us      41.842us             1  
                       aten::view         0.02%      22.199us         0.02%      22.199us      22.199us             1  
                     aten::linear         2.11%       2.665ms         9.68%      12.240ms      12.240ms             1  
                          aten::t         0.48%     609.637us         0.60%     757.760us     757.760us             1  
                  aten::transpose         0.11%     140.705us         0.12%     148.123us     148.123us             1  
                 aten::as_strided         0.01%       7.418us         0.01%       7.418us       7.418us             1  
                      aten::addmm         6.93%       8.767ms         6.97%       8.817ms       8.817ms             1  
                     aten::expand         0.02%      24.723us         0.02%      29.151us      29.151us             1  
                 aten::as_strided         0.00%       4.428us         0.00%       4.428us       4.428us             1  
                      aten::copy_         0.02%      21.343us         0.02%      21.343us      21.343us             1  
                       aten::relu         0.01%      12.372us         0.04%      46.287us      46.287us             1  
                  aten::clamp_min         0.01%      14.627us         0.03%      33.915us      33.915us             1  
                      aten::empty         0.00%       4.259us         0.00%       4.259us       4.259us             1  
                  aten::clamp_min         0.01%      15.029us         0.01%      15.029us      15.029us             1  
            aten::feature_dropout         0.01%      16.409us         0.18%     225.300us     225.300us             1  
                      aten::empty         0.00%       2.341us         0.00%       2.341us       2.341us             1  
                 aten::bernoulli_         0.09%     116.905us         0.09%     118.090us     118.090us             1  
                      aten::empty         0.00%       1.185us         0.00%       1.185us       1.185us             1  
                       aten::div_         0.02%      22.843us         0.03%      35.798us      35.798us             1  
                         aten::to         0.00%       4.860us         0.01%      12.955us      12.955us             1  
              aten::empty_strided         0.00%       2.912us         0.00%       2.912us       2.912us             1  
                      aten::copy_         0.00%       5.183us         0.00%       5.183us       5.183us             1  
                        aten::mul         0.04%      52.662us         0.04%      52.662us      52.662us             1  
                     aten::linear         0.00%       5.098us         0.08%      96.324us      96.324us             1  
                          aten::t         0.01%       9.217us         0.01%      17.823us      17.823us             1  
                  aten::transpose         0.00%       5.864us         0.01%       8.606us       8.606us             1  
                 aten::as_strided         0.00%       2.742us         0.00%       2.742us       2.742us             1  
                      aten::addmm         0.05%      62.877us         0.06%      73.403us      73.403us             1  
                     aten::expand         0.00%       2.922us         0.00%       3.957us       3.957us             1  
                 aten::as_strided         0.00%       1.035us         0.00%       1.035us       1.035us             1  
                      aten::copy_         0.01%       6.569us         0.01%       6.569us       6.569us             1  
                aten::log_softmax         0.51%     642.944us         4.10%       5.185ms       5.185ms             1  
               aten::_log_softmax         3.58%       4.531ms         3.59%       4.542ms       4.542ms             1  
                      aten::empty         0.01%      10.993us         0.01%      10.993us      10.993us             1  
---------------------------------  ------------  ------------  ------------  ------------  ------------  ------------  
Self CPU time total: 126.464ms
```



### Compare Different Batch Size

Training 1 epochs:

| Batch Size | Comparison                                                   |
| ---------- | ------------------------------------------------------------ |
| 1          | Self CPU time total: 51.256ms  (51.256 ms/batch)  Test set: Average loss: 0.1159, Accuracy: 9749/10000 (97%) |
| 16         | 52.227ms (3.2641875ms/batch) Test set: Average loss: 0.0586, Accuracy: 9829/10000 (98%) |
| 64         | CPU time total: 126.464ms (1.976  ms/batch) Test set:  Average loss: 0.0677, Accuracy: 9782/10000 (98%) |



