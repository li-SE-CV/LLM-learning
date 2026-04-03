# 一、底层基础（必须会）
## 1. 机器学习 ML
- 损失函数：交叉熵、MSE、KL 散度、NLL 损失
- 优化：梯度下降、SGD、Adam、AdamW
- 过拟合 & 欠拟合、正则化 L1/L2、Dropout
- 评价指标：准确率、F1、PPL、BLEU、ROUGE
- 极大似然估计 MLE

## 2. 深度学习 DL
- 前向传播、反向传播、链式法则
- 梯度消失 / 梯度爆炸
- 激活函数：ReLU、GELU、SwiGLU
- 归一化：LayerNorm、RMSNorm
- 初始化、梯度累积、混合精度 FP16/BF16

---

# 二、核心骨架：Transformer（重中之重）
- 整体结构：Encoder / Decoder / Encoder-Decoder
- **多头注意力机制（手撕）**
  Q/K/V 计算 → 注意力分数 → 加权求和
- 为什么要除以 √dₖ：方差归一化，防止梯度消失
- 位置编码：绝对、相对、**RoPE、ALiBi**
- 结构改进：SwiGLU、RMSNorm、GQA/MQA

---

# 三、两大学习范式（面试核心）
## 1. 迁移学习（大模型的灵魂）
思想：把预训练的通用知识，迁移到下游任务
- 预训练 + 微调
- 全参数微调
- **PEFT 高效微调**
  - LoRA、QLoRA、AdaLoRA
  - Adapter、Prefix/Prompt Tuning
  - IA3、VeRA
- 知识蒸馏（大模型 → 小模型）

## 2. 强化学习（大模型对齐人类）
思想：通过奖励/偏好，让模型更听话、更安全
- RLHF 流程：SFT → Reward Model → PPO
- **PPO**：近端策略优化，稳定训练
- **DPO**：直接偏好优化，不用 RM，不用 RL
- 变种：**GRPO、DAPO、ORPO、KTO、IPO、SPIN**

---

# 四、大模型训练全流程
1. **预训练 Pre-training**
   目标：Next Token Prediction（Decoder-only）
2. **SFT 有监督微调**
   让模型会跟着指令走
3. **偏好对齐**
   PPO / DPO 系列，让模型更符合人类偏好
4. **后处理**
   蒸馏、量化、长上下文扩展

---

# 五、RAG 检索增强生成（高频必问）
1. 文档加载 → **语义切分**
2. 向量化 Embedding
3. 检索：
   - 稀疏：BM25
   - 稠密：Qwen-Emb、BGE-M3
4. **RRF 排序融合**
5. 重排 Reranker
6. 送入 LLM 生成
7. 进阶：**GraphRAG**（实体+关系+社区检索）

> 用户输入不是直接召回，要先：查询改写、意图识别、纠错、增强。

---

# 六、推理加速 & 工程优化
- **KV Cache**：缓存键值，加速生成
- **vLLM**：核心 PagedAttention，分页管理 KV
- 量化：INT4/INT8、GPTQ、AWQ
- 解码策略：Greedy、Beam、Top-k、Top-p、Temperature
- OOM 解决方案：减小 bs / seq_len、LoRA、量化、FSDP/DeepSpeed

---

# 七、模型架构 & 多模态
- 主流架构：Decoder-only（GPT、Qwen、Llama）
- 为什么用 Decoder-only：适合自回归生成
- 多模态架构：ViT 图像编码 + 投影层 + LLM
- 感受野：CNN 区域 / Transformer 注意力覆盖范围
- Qwen 等改进：RoPE、GQA、长上下文、多语言

---

# 超精简一句话总复习
- **机器学习**：基础损失、优化、评估
- **深度学习**：网络训练与梯度
- **Transformer**：大模型的结构核心
- **迁移学习**：预训练+微调（LoRA 等）
- **强化学习**：PPO/DPO 对齐人类
- **RAG**：检索+生成，解决幻觉
- **推理加速**：KV Cache + vLLM + 量化
