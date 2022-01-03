# Lab2 Report



|          |               |               |
| -------- | ------------- | ------------- |
| Hardware | CPU（# vCPU） | 2             |
|          | GPU           | /             |
| Software | OS Version    | macOS Mojave  |
|          | Package       | PyTorch-1.9.0 |
|          | CUDA Version  | /             |
|          |               |               |

 

## Custom Linear Operator

 

| Method (Linear) | Peformance (3 epochs)                                        |
| --------------- | ------------------------------------------------------------ |
| Original        | Test set: Average loss: 0.0349, Accuracy: 9887/10000 (99%)<br/><br/>python ../Lab1/mnist_basic.py  454.80s |
| Python Custom   | Test set: Average loss: 0.0334, Accuracy: 9890/10000 (99%)<br/><br/>python mnist_custom_linear.py  468.49s |
| Cpp Custom      | Test set: Average loss: 0.0334, Accuracy: 9890/10000 (99%)<br/><br/>python mnist_custom_linear_cpp.py  456.92s |



## Additional Experiments

