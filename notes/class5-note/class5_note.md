# Note: class5
## 大模型部署背景
存在的问题
- 内存开销大
- 请求数不固定，生成的token逐个生成且不固定
- LLM相对视觉模型，结构较为简单，大部分是decoder-only（token逐个生成是最大的缺点）

大模型部署挑战
- 设备（消费级显卡和手机）存储问题？
- 稳定快速推理问题，如何有效管理和利用内存？
- 如何提高系统吞吐量？对于个体用户，如何降低响应时间？

## LMDeploy
### 简介
- 是在N卡上部署的全流程解决方案

    ![Alt text](image.png)

### 核心功能
- 量化：为什么要做weights-only的量化？

    ![Alt text](image-1.png)

- 推理服务API Server

    ![Alt text](image-2.png)

## 实践：安装、部署、量化
### 环境配置
### 服务部署
- 经由LMDeploy部署的服务是经典的C/S架构
    
    ![Alt text](image-3.png)

#### 模型转换
使用 TurboMind 推理模型需要先将模型转化为 TurboMind 的格式，目前支持在线转换和离线转换两种形式。在线转换可以直接加载 Huggingface 模型，离线转换需需要先保存模型再加载。

- 实现多卡并行运算的原理

    ![Alt text](image-4.png)

    - 列并行：将多张卡上的运算结果进行横向拼接
    - 行并行：将多张卡上的运算结果进行矩阵加法运算

#### TurboMind 推理+命令行本地对话
```bash
# Turbomind + Bash Local Chat
lmdeploy chat turbomind ./workspace
```

![Alt text](image-5.png)

#### TurboMind 推理+API服务
```

```
### 模型量化
#### KV Cache量化
#### W4A16量化