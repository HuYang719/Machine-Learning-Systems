# CUDA Stream

## Programmer Guide

https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html

At its core are three key abstractions:

- a hierarchy of thread groups

- shared memories

-  barrier synchronization

   , that are simply exposed to the programmer as a minimal set of language extensions.

![Automatic Scalability.](../images/automatic-scalability.png)



>  A GPU is built around an array of Streaming Multiprocessors (SMs) (see [Hardware Implementation](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#hardware-implementation) for more details). A multithreaded program is partitioned into blocks of threads that execute independently from each other, so that a GPU with more multiprocessors will automatically execute the program in less time than a GPU with fewer multiprocessors.

**Comment:** Block runs on SM with multiple threads. 

> CUDA C++ extends C++ by allowing the programmer to define C++ functions, called kernels, that, when called, are executed N times in parallel by N different CUDA threads, as opposed to only once like regular C++ functions.

**Comment:** Kernel is the "function" in CUDA and will be called multiple times in parallel, but executed in different CUDA threads. You write kernel, kernel is for a thread, thread will run on core. SM consists of multiple cores (different GPU version has different cores/SM).

#### Programming Model

> Each thread that executes the kernel is given a unique thread ID that is accessible within the kernel through built-in variables.



> There is a limit to the number of threads per block, since all threads of a block are expected to reside on the same processor core and must share the limited memory resources of that core. On current GPUs, a thread block may contain up to 1024 threads.

#### Memory Hierarchy

> Each thread has private local memory. Each thread block has shared memory visible to all threads of the block and with the same lifetime as the block. All threads have access to the same global memory.

![Memory Hierarchy.](../images/memory-hierarchy.png)



## Pytorch with CUDA Stream

https://pytorch.org/docs/stable/notes/cuda.html#stream-semantics-of-backward-passes

Operations inside each stream are serialized in the order they are created, but operations from different streams can execute concurrently in any relative order, unless explicit synchronization functions (such as [`synchronize()`](https://pytorch.org/docs/stable/generated/torch.cuda.synchronize.html#torch.cuda.synchronize) or [`wait_stream()`](https://pytorch.org/docs/stable/generated/torch.cuda.Stream.html#torch.cuda.Stream.wait_stream)) are used. 

```py
## s and default stream are different
cuda = torch.device('cuda')
s = torch.cuda.Stream()  # Create a new stream.
A = torch.empty((100, 100), device=cuda).normal_(0.0, 1.0)
with torch.cuda.stream(s):
    # sum() may start execution before normal_() finishes!
    B = torch.sum(A)
```



In prior versions of PyTorch (1.9 and earlier), the autograd engine always synced the default stream with all backward ops, so the following pattern:

```
with torch.cuda.stream(s):
    loss.backward()
use grads
```



was safe as long as `use grads` happened on the default stream. In present PyTorch, that pattern is no longer safe. If `backward()` and `use grads` are in different stream contexts, you must sync the streams:

```
with torch.cuda.stream(s):
    loss.backward()
torch.cuda.current_stream().wait_stream(s)
use grads
```

even if `use grads` is on the default stream.

**Comment:** We need to sync stream before use grads for pytorch  version > 1.9



The difference between [`DistributedDataParallel`](https://pytorch.org/docs/stable/generated/torch.nn.parallel.DistributedDataParallel.html#torch.nn.parallel.DistributedDataParallel) and [`DataParallel`](https://pytorch.org/docs/stable/generated/torch.nn.DataParallel.html#torch.nn.DataParallel) is: [`DistributedDataParallel`](https://pytorch.org/docs/stable/generated/torch.nn.parallel.DistributedDataParallel.html#torch.nn.parallel.DistributedDataParallel) uses multiprocessing where a process is created for each GPU, while [`DataParallel`](https://pytorch.org/docs/stable/generated/torch.nn.DataParallel.html#torch.nn.DataParallel) uses multithreading. By using multiprocessing, each GPU has its dedicated process, this avoids the performance overhead caused by GIL of Python interpreter.



## Questions

1. Stream and hardware

   Stream is the CUDA API concept (totally different with SM!) usually use in your coding  within a single GPU context. The hardware do not have stream concept, and operations in a CUDA stream are sequential. So you can divided different stream and execute them in parallel.

   > Streams are a feature of the CUDA APIs which allow for concurrent operations within a single GPU context. Initially this was limited to overlapping copying with kernel execution, but on Fermi hardware it has been extended to permit (resources allowing) concurrent kernel execution on a GPU.
   >
   > On the GPU, a thread is the basic execution element. You write kernel code for a single thread, tell the device how you want those threads assembled into blocks and how many blocks you wish to run, and the execution model collects SIMD groupings (“warps”) of threads and schedules them on multiprocessors.

2. Send/Recv values between streams