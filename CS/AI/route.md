
# 机器学习基础

需要掌握的知识框架：

## 监督学习
- 线性回归
- 逻辑回归
- 决策树
- 随机森林
- GBDT、XGBoost、LightGBM
- SVM
- KNN
- 朴素贝叶斯

## 无监督学习
- K-Means
- 层次聚类
- DBSCAN
- PCA
- NMF
- 异常检测

## 训练与评价

- 训练集、验证集、测试集
- 交叉验证
- 过拟合与欠拟合
- 正则化
- 数据泄漏
- 类别不平衡
- 超参数搜索
- Pipeline
    

常见指标：
- 分类：Accuracy、Precision、Recall、F1、ROC-AUC、PR-AUC
- 回归：MAE、MSE、RMSE、R²
- 聚类：NMI、ARI、轮廓系数
- 排序与推荐：Recall@K、NDCG@K、MRR

这一阶段建议统一使用 `scikit-learn`，其官方文档覆盖预处理、模型选择、指标、Pipeline 和大量示例。([Scikit-learn](https://scikit-learn.org/stable/getting_started.html?utm_source=chatgpt.com "Getting Started — scikit-learn 1.9.0 documentation"))

---

# 深度学习与 PyTorch

理论部分：

- 神经元与多层感知机
- 前向传播
- 损失函数
- 反向传播
- 梯度下降
- Batch、Epoch、Learning Rate
- SGD、Momentum、Adam
- Dropout、BatchNorm
- 权重初始化
- 学习率调度
- 过拟合与正则化

PyTorch 部分：
- Tensor
- Dataset、DataLoader
- `nn.Module`
- 损失函数
- Optimizer
- 自动求导 Autograd
- 训练循环
- 验证循环
- 模型保存与加载
- GPU 使用
- TensorBoard
- 混合精度训练
    

PyTorch 官方基础路线本身就是按照 Tensor、Dataset/DataLoader、模型、自动求导、优化循环和模型保存展开的，适合作为你的代码主线。https://docs.pytorch.org/tutorials/intro.html?utm_source=chatgpt.com

三类模型：
- CNN：图像分类基础
- RNN/LSTM：理解序列模型即可
- Transformer：后续重点



# 大模型基础与应用

## 大模型基本原理
- Token 与 Tokenizer
- Embedding
- Self-Attention
- Multi-Head Attention
- Transformer
- Encoder 与 Decoder
- 预训练、指令微调、对齐
- 上下文窗口
- Temperature、Top-p
- 幻觉和知识截止
- 推理模型基本概念

## 模型调用
- 调用大模型 API
- 多轮对话
- System Prompt
- Structured Output
- Function Calling / Tool Calling
- 流式输出
- 多模态输入
- 错误重试和限流

## RAG
- 文档加载
- 文本切分
- Embedding
- 向量检索
- 关键词检索
- 混合检索
- Rerank
- Prompt 拼接
- 引用溯源
- RAG 评估

常用组件：
- Transformers
- Hugging Face Hub
- Sentence Transformers
- FAISS
- Chroma、Milvus 或 pgvector
- LangChain、LlamaIndex

## 微调

先了解，再根据需要实践：
- SFT
- LoRA
- QLoRA
- PEFT
- 量化
- 数据构造
- 模型评估
- 推理部署

Hugging Face 当前官方 LLM 课程已经覆盖 Transformer、Transformers 库、Datasets、Tokenizers、模型微调、数据构造和推理模型等主题，可以作为这一阶段的主教材。([Hugging Face](https://huggingface.co/learn/llm-course/en/chapter1/1?utm_source=chatgpt.com "Introduction · Hugging Face"))

---

# Agent 技术

不要一开始就学复杂多智能体系统。推荐顺序是：

## 单 Agent 基础
- LLM
- Prompt
- Tool Calling
- Memory
- 状态管理
- ReAct
- 任务规划
- 结果验证
- Human-in-the-loop

## 工作流 Agent
- 顺序执行
- 条件分支
- 循环与重试
- 并行节点
- 审核节点
- 状态持久化
- 长任务恢复

## 多 Agent
- Supervisor 模式
- Planner–Executor
- Researcher–Writer–Reviewer
- Agent 通信
- 冲突处理
- 权限控制
- 成本与延迟控制

技术选择：
- 简单应用：直接用原生模型 SDK
- 快速开发：LangChain
- 状态化工作流：LangGraph
- 知识库/RAG：LlamaIndex
- 多 Agent 实验：AutoGen、CrewAI 等

LangGraph 当前定位偏向低层的 Agent 编排和运行时，适合需要确定性流程、状态控制和 Agent 行为混合的项目。([Docs by LangChain](https://docs.langchain.com/oss/python/langgraph/overview?utm_source=chatgpt.com "LangGraph overview - Docs by LangChain"))

需要注意：
> Agent 的核心不是“会调用框架”，而是把任务拆分成状态、节点、工具、判断条件和失败恢复机制。

---

### 7. AI 工程化与部署

#### 后端
- FastAPI
- REST API
- Pydantic 数据校验
- 异步请求
- 文件上传
- WebSocket 或流式输出
- JWT 鉴权
- Redis 缓存
- PostgreSQL/MySQL

FastAPI 官方教程采用逐步构建方式，基础教程已经足够搭建完整 API 应用。([FastAPI](https://fastapi.tiangolo.com/tutorial/?utm_source=chatgpt.com "Tutorial - User Guide - FastAPI"))

#### 部署

- Docker
- Dockerfile
- Docker Compose
- Nginx
- Linux 服务器
- 环境变量
- 日志
- HTTPS
- GPU 环境
- 基础云服务器部署

Docker 官方入门内容覆盖容器、镜像、仓库、镜像构建及 Compose 等核心概念。([Docker Documentation](https://docs.docker.com/get-started/introduction/?utm_source=chatgpt.com "Introduction | Docker Docs"))

#### MLOps 基础
- 实验记录
- 参数与指标管理
- 模型版本管理
- 数据版本
- 模型注册
- 线上监控
- CI/CD
- 自动测试

先掌握：
- MLflow
- Git
- Docker
- GitHub Actions

MLflow 可用于记录实验参数、指标、模型产物，以及管理模型生命周期和模型注册。([MLflow AI Platform](https://mlflow.org/docs/latest/tracking?utm_source=chatgpt.com "ML Experiment Tracking | MLflow AI Platform"))


# 数学学习路线

## 线性代数
- 向量和矩阵
- 矩阵乘法
- 转置
- 逆矩阵
- 秩
- 特征值和特征向量
- 正交
- 范数
- SVD
- PCA 的矩阵解释

学习标准：

> 能看懂模型公式中的矩阵维度，并能用 NumPy 实现。

## 概率统计

重点：
- 随机变量
- 条件概率
- 贝叶斯公式
- 常见概率分布
- 期望、方差
- 最大似然估计
- 假设检验
- 置信区间
- 采样
- 偏差与方差

## 微积分与优化

重点：
- 导数
- 偏导数
- 梯度
- 链式法则
- 梯度下降
- 凸函数基本概念
- 拉格朗日乘子

不需要一开始深入证明，先解决三个问题：
1. 公式在表达什么
2. 每个变量维度是什么
3. 公式如何转化成代码