<h1 align="center">LoRA Fine-Tuning for Code Generation & Reasoning</h1>

This project implements **LoRA (Low-Rank Adaptation)** fine-tuning on the  
**Qwen/Qwen2.5-Coder-1.5B-Instruct** model to improve Python code generation and reasoning performance.

Two separate training runs are performed using different datasets (**DEEP** and **DIVERSE**) and evaluated via checkpoint-based testing.

## 🎯 Project Goal
- Analyze baseline performance of a pre-trained instruct model  
- Fine-tune the model using **solution-only (code-only)** supervision  
- Compare performance between **DEEP** and **DIVERSE** datasets  
- Select the best checkpoint based on test loss  

## 🧠 Base Model
- **Model:** `Qwen/Qwen2.5-Coder-1.5B-Instruct`
- **Type:** Causal Language Model (Instruct-tuned)
- **Precision:** FP16

## 📚 Datasets
Both datasets are loaded directly from **Hugging Face** using the `datasets` library.

### 🔹 CodeGen-Deep-5K (DEEP)
- Source: `Naholav/CodeGen-Deep-5K`
- URL: https://huggingface.co/datasets/Naholav/CodeGen-Deep-5K
- Focuses on deeper algorithmic and reasoning-heavy problems

### 🔹 CodeGen-Diverse-5K (DIVERSE)
- Source: `Naholav/CodeGen-Diverse-5K`
- URL: https://huggingface.co/datasets/Naholav/CodeGen-Diverse-5K
- Focuses on diverse problem types for generalization

**Used Field for Training:** `solution` (clean code only)  
**Unused Field:** `output` (reasoning traces)

## ⚙️ Training Setup

### LoRA Configuration
- Rank (r): 32  
- Alpha: 64  
- Dropout: 0.05  
- Target Modules: Attention & MLP layers  
  (`q_proj`, `k_proj`, `v_proj`, `o_proj`, `gate_proj`, `up_proj`, `down_proj`)

### Training Hyperparameters
- Epochs: 3  
- Learning Rate: 2e-4  
- Batch Size: 2  
- Gradient Accumulation: 8 (Effective batch size: 16)  
- Optimizer: AdamW (fused)  
- Scheduler: Cosine  
- Max Context Length: 1024  
- Gradient Checkpointing: Enabled  

## 🧪 Workflow
1. Run baseline inference on the base model  
2. Load and split dataset (train / validation / test)  
3. Fine-tune using LoRA adapters  
4. Save multiple checkpoints during training  
5. Evaluate checkpoints on test set and select the best model  

## 📊 Output Image
  ![Image]( https://github.com/user-attachments/assets/7c00ad3c-7322-4616-a51b-a2deca7a0408)


## 📌 Notes
- Both trainings start **from the same base model**
- Only LoRA parameters are updated (base model frozen)
- Designed to be memory-efficient (FP16 + checkpointing)

## 🏁 Summary
This project demonstrates an efficient LoRA-based fine-tuning approach for code generation models and highlights how dataset structure impacts reasoning performance.

## 🤝 Contributing

Contributions are welcome! 

## 📡 Contact
For any queries or collaborations, feel free to reach out!

🌐 GitHub: [zeynepcol](https://github.com/zeynepcol)  
👤 LinkedIn: [zeynep-col](https://linkedin.com/in/zeynep-col/)
