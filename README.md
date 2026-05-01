# 🚀 GRPO Fine-Tuning with Structured Outputs (XML CoT)

This repository demonstrates how to fine-tune a Large Language Model (LLM) using **GRPO (Group Relative Policy Optimization)** with **structured outputs** and **reward shaping**.

We train the model to:

* Produce **step-by-step reasoning**
* Output answers in a strict **XML format**
* Optimize for correctness using reward functions

---

## 🧠 What is GRPO?

GRPO (Group Relative Policy Optimization) is a reinforcement learning method designed for LLM fine-tuning.

Instead of relying on a value function (like PPO), GRPO:

* Samples multiple outputs per prompt
* Compares them **within a group**
* Updates the model based on **relative ranking**

👉 This makes training:

* More stable
* Memory efficient
* Simpler to implement

---

## 📌 Key Features

* ✅ GRPO-based fine-tuning
* ✅ XML structured output enforcement
* ✅ Chain-of-thought (CoT) reasoning
* ✅ Reward-based optimization
* ✅ GSM8K math reasoning dataset
* ✅ Format + correctness rewards

---

## 🏗️ Output Format

The model is trained to respond strictly in this format:

```xml
<reasoning>
Step-by-step reasoning...
</reasoning>
<answer>
Final answer
</answer>
```
---


## 📊 Dataset

We use the GSM8K dataset for math reasoning:

* Each sample:

  * Input: Question
  * Output: Numeric answer
* Ground truth is extracted using:

  ```python
  #### final_answer
  ```

---

## 🧪 Training

Run training:

```bash
python train.py
```

---

## 🎯 Reward Functions

The model is optimized using multiple reward signals:

### 1. ✅ Correctness Reward

* Matches extracted `<answer>` with ground truth

### 2. 🔢 Integer Reward

* Encourages numeric outputs

### 3. 🧾 Format Reward (Strict)

* Enforces exact XML structure

### 4. 🧾 Format Reward (Soft)

* Allows flexible but valid XML

### 5. 📏 XML Structure Score

* Rewards properly formatted tags
* Penalizes extra text

---

## 🔍 Example

### Input:

```
What is 12 + 7?
```

### Model Output:

```xml
<reasoning>
12 + 7 = 19
</reasoning>
<answer>
19
</answer>
```

---

## 🧩 Why XML Format?

We use XML-style tags because:

* Easy to parse (`<answer>...</answer>`)
* Robust compared to JSON in LLM outputs
* Enables clean separation of:

  * reasoning
  * final answer

---

## 🧠 Key Insight

We are not just training for accuracy.

We are training the model to:

* Think step-by-step
* Follow strict structure
* Produce machine-readable outputs

---

## 📈 Evaluation

Evaluation is based on:

* Exact match accuracy
* Format compliance
* Reward scores

---

## 🚀 Pushing to Hugging Face

After training:

```python
model.push_to_hub("your-username/grpo-model")
tokenizer.push_to_hub("your-username/grpo-model")
```

---

## ⚠️ Notes

* The model **expects XML format prompts**
* Outputs may degrade if format is not enforced
* Works best with structured reasoning tasks

---
