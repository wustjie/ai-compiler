# TVM

ai编译器与传统编译器结构相似：  
·编译器前端：接收C/C++/Java等不同语言，进行代码生成，吐出IR  
·编译器中端：接收IR，进行不同编译器后端可以共享的优化，如常量替换，死代码消除，循环优化等，吐出优化后的IR  
·编译器后端：接收优化后的IR，进行不同硬件的平台相关优化与硬件指令生成，吐出目标文件  

环境配置/docker
```
docker pull tvmai/demo-gpu
nvidia-docker run --rm -it tvmai/demo-gpu bash
```
环境配置/ubuntu
```
git clone --recursive https://github.com/apache/tvm tvm
cd tvm
mkdir build
cp cmake/config.cmake build
cd build
cmake ..
make -j4
export TVM_HOME=/path/to/tvm
export PYTHONPATH=$TVM_HOME/python:${PYTHONPATH}
```

使用样例（将torchvision中的ResNet18 Pytorch模型通过Relay构建TVM中的计算图并进行图优化，再通过LLVM编译到Intel CPU上进行执行，比直接使用Pytorch推理快2倍）：
https://github.com/BBuf/tvm_learn


TVM的思想可以总结为表示和调度分离，所谓表示就是IR，调度就是schedule

scheduler是一系列优化方法的集合，不影响结果，只影响性能。

![image](https://github.com/wustjie/ai-compiler/assets/34996802/a555e5d7-6a5d-4c15-8d83-1a356e8944aa)

tvm.schedule当中的API例程：https://github.com/StrongSpoon/tvm.schedule





