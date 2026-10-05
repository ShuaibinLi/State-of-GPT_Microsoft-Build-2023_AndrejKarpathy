# State of GPT — Microsoft Build 2023 (By Andrej Karpathy)

This repository contains the presentation slides from the landmark talk **"State of GPT"** given by **Andrej Karpathy** (former OpenAI Chief Scientist and former Director of AI at Tesla) at Microsoft Build 2023. As one of the foundational primers in the Large Language Model (LLM) domain, it systematically covers the complete lifecycle of LLMs—from core training pipelines and pretraining architectures to practical Prompt Engineering and deployment strategies.

---

## 📌 Overview

- **Speaker**: Andrej Karpathy (OpenAI / Former Tesla AI)
- **Talk Title**: State of GPT
- **Event**: Microsoft Build 2023
- **Primary Goal**: Demystify how GPT models are trained and operate under the hood, while providing developers with engineering best practices for utilizing LLMs effectively.

---

## 🛠️ Key Topics & Takeaways

### 1. The 4-Stage GPT Training Pipeline

The document breaks down the end-to-end training process into four standardized stages:

| Stage                                     | Input Data                          | Learning Approach & Objective                     | Key Output                        |
| :---------------------------------------- | :---------------------------------- | :------------------------------------------------ | :-------------------------------- |
| **1. Pretraining**                  | Massive unannotated web text        | Unsupervised next-token prediction                | Base Model                        |
| **2. Supervised Fine-Tuning (SFT)** | High-quality Q&A / Instruction sets | Supervised learning for instruction following     | SFT Model (Assistant)             |
| **3. Reward Modeling (RM)**         | Ranked model outputs                | Train a scalar scoring model for response quality | Reward Model                      |
| **4. RLHF / PPO**                   | Prompts                             | Proximal Policy Optimization using RM feedback    | Aligned Assistant (e.g., ChatGPT) |

### 2. Base Model Comparison & Training Dynamics (Pretraining)

The presentation compares key milestone foundation models:

- **GPT-3 (2020)**: 50,257 Vocabulary Size | 2,048 Token Context | 175B Parameters | Trained on 300B Tokens | ~1,000–10,000 V100 GPUs for ~1 month (~$1M–$10M)
- **LLaMA (2023)**: 32,000 Vocabulary Size | 2,048 Token Context | 6.7B–65B Parameters | Trained on 1T–1.4T Tokens | 65B model trained on 2,048 A100 GPUs for 21 days (~$5M)
- **Data Organization**: Transformer inputs are formatted as $(B, T)$ tensors (Batch Size, Sequence Length). Multiple documents are concatenated into rows using special `<|endoftext|>` tokens as delimiters.

### 3. Practical Prompt Engineering & LLM Optimization

To maximize model performance, Karpathy outlines several key operational strategies:

- **Allocate Compute Budget (Chain of Thought)**: GPT assigns a fixed amount of compute per token. For complex reasoning, guide the model to "think step by step" to express its reasoning across more tokens.
- **System Prompts**: Establish explicit roles, constraints, and target output formats (e.g., JSON schemas).
- **Few-Shot Prompting**: Provide 2–3 high-quality input-output examples directly in the prompt to significantly improve output consistency.
- **Augment with System 2 Tools**: Combine LLMs with Retrieval-Augmented Generation (RAG), code interpreters, and external APIs to overcome limitations in knowledge recency and calculation precision.
