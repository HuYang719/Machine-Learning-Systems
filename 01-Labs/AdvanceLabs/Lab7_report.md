## 实验报告

### 实验环境

|          |                                 |                    |
| -------- | ------------------------------- | ------------------ |
| 硬件环境 | 服务器数目                      | G4dn.12xlarge X  1 |
|          | 网卡型号、数目                  | ENA X 1            |
|          | GPU型号、数目                   | T4 X 4             |
|          | GPU连接方式                     | PCIe + MPI         |
| 软件环境 | OS版本                          | Ubuntu 18.04       |
|          | GPU driver、(opt. NIC driver)   | Nvidia-smi 450     |
|          | 深度学习框架 python包名称及版本 | PyTorch 15.0       |
|          | CUDA版本                        | CUDA 11.0          |
|          | NCCL版本                        |                    |
|          |                                 |                    |

### 实验结果

1. 测试服务器内多显卡加速比

   |          |            |                    |                                                              |                     |        |         |
   | -------- | ---------- | ------------------ | ------------------------------------------------------------ | ------------------- | ------ | ------- |
   | 通信后端 | 服务器数量 | 每台服务器显卡数量 | 耗时                                                         | 平均吞吐率          | 加速比 | Devices |
   | MPI      | 1          | 1                  | real	2m53.341s<br/>user	2m50.806s<br/>sys	0m3.649s  | 346.82 images/sec   |        | CPU     |
   | MPI      | 1          | 2                  | real	1m38.953s<br/>user	3m44.813s<br/>sys	0m8.718s  |                     |        | CPU     |
   | MPI      | 1          | 4                  | real	0m53.875s<br/>user	3m34.885s<br/>sys	0m9.433s  |                     |        | CPU     |
   |          |            |                    |                                                              |                     |        |         |
   | MPI      | 1          | 1                  | real	1m53.525s<br/>user	0m29.322s<br/>sys	0m4.397s  | 530.97 images/sec   | 1      | GPU     |
   | MPI      | 1          | 2                  | real	1m8.494s<br/>user	1m30.942s<br/>sys	0m17.767s  | 882.35 images/sec   | 1.66   | GPU     |
   | MPI      | 1          | 3                  | real	0m55.322s<br/>user	2m3.882s<br/>sys	0m23.796s  | 1,084.56 images/sec | 2.04   | GPU     |
   | MPI      | 1          | 4                  | real	0m48.933s<br/>user	3m5.696s<br/>sys	0m30.887s  | 1,226.99 images/sec | 2.31   | GPU     |
   |          |            |                    |                                                              |                     |        |         |
   | Gloo     | 1          | 1                  | real	2m55.241s<br/>user	2m53.243s<br/>sys	0m4.006s  |                     |        | CPU     |
   | Gloo     | 1          | 2                  | real	1m42.106s<br/>user	3m21.320s<br/>sys	0m21.370s |                     |        |         |
   | Gloo     | 1          | 4                  | real	0m56.182s<br/>user	3m44.350s<br/>sys	0m42.000s |                     |        |         |
   |          |            |                    |                                                              |                     |        |         |
   | Gloo     | 1          | 1                  | real	1m53.752s<br/>user	0m30.322s<br/>sys	0m4.645s  |                     |        | GPU     |
   | Gloo     | 1          | 2                  | real	1m10.358s<br/>user	1m11.627s<br/>sys	0m28.830s |                     |        | GPU     |
   | Gloo     | 1          | 4                  | real	0m49.046s<br/>user	1m35.980s<br/>sys	0m59.422s |                     |        | GPU     |
   |          |            |                    |                                                              |                     |        |         |
   | NCCL     | 1          | 1                  | real	1m52.536s<br/>user	0m29.208s<br/>sys	0m4.673s  |                     |        | GPU     |
   | NCCL     | 1          | 2                  | real	1m8.814s<br/>user	2m1.194s<br/>sys	0m22.052s   |                     |        | GPU     |
   | NCCL     | 1          | 4                  | real	0m48.482s<br/>user	3m32.790s<br/>sys	0m34.929s |                     |        | GPU     |

2. 测试服务器间加速比

   （暂时还没钱开多个服务器.jpg）

   |          |            |                    |              |            |        |
   | -------- | ---------- | ------------------ | ------------ | ---------- | ------ |
   | 通信后端 | 服务器数量 | 每台服务器显卡数量 | 平均每步耗时 | 平均吞吐率 | 加速比 |
   | MPI      |            | 1                  |              |            |        |
   | MPI      |            | 1                  |              |            |        |
   | Gloo     |            | 1                  |              |            |        |
   | Gloo     |            | 1                  |              |            |        |
   | NCCL     |            | 1                  |              |            |        |
   | NCCL     |            | 1                  |              |            |        |
   |          |            |                    |              |            |        |

3. 总结加速比的图表、比较不同通信后端的性能差异、分析可能的原因



CPU训练时，使用MPI性能稍好于GLOO

使用单机两个GPU通信时，GLOO和NCCL都明显优于MPI；但四个GPU时，三者差别不大，怀疑时通信量造成的影响







## 

```
HOROVOD_GPU_OPERATIONS=NCCL pip install --no-cache-dir horovod
```

