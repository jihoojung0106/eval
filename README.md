# README — MER2023 Evaluation Guide

## 🚀 Environment Setup

### **1. Python Environment**
- Use **Python 3.9**
- Install all dependencies:
```bash
pip install -r requirements.txt
```

---

## 🎯 Evaluation on the MER2023 Dataset

### **1. Download Model Weights**

#### **Base Model**
- LLaMA-2 7B Chat:  
  https://huggingface.co/meta-llama/Llama-2-7b-chat-hf  

After downloading, set the path in `eval_emotion.yaml`:
```yaml
llama_model: "/mnt/bear3/users/jungji/ckpt/Llama-2-7b-chat-hf"
```

#### **Finetuned Checkpoint**
- `checkpoint_best.pth`:  
  https://drive.google.com/file/d/1NoPZDj5_392zBtVK1IHO8bepA4910iI_/view  

Set the checkpoint path in `eval_emotion.yaml`:
```yaml
ckpt: "/path/to/checkpoint_best.pth"
```

---

### **2. Download Data**

#### **MER2023 Feature Files**
- `features_of_MER2023-SEMI.zip`  
  https://drive.google.com/file/d/1DJJ8wP3g4yLT0ZFZ_-H4izJHAGJx2AJ_/view

- `relative_test3_NCEV.txt`  
  https://drive.google.com/file/d/1YyoWabWtAJuFI6ylMM220i_kh_0Nagv9/view

After extracting the features, **your directory should look like this**:

```
mer2023/
│── features_of_MER2023-SEMI/
      └── first_frames_MER2023-SEMI/
      └── relative_test3_NCEV.txt     ← Must be placed here
```

#### **Configure paths in `eval_emotion.yaml`:**
```yaml
feature_face_caption:
    eval_file_path: mer2023/features_of_MER2023-SEMI/relative_test3_NCEV.txt
    img_path: mer2023/features_of_MER2023-SEMI/first_frames_MER2023-SEMI
```

---

### **3. Run Evaluation**

Execute the evaluation using `torchrun`:

```bash
torchrun --nproc_per_node 1 eval_emotion.py --cfg-path eval_configs/eval_emotion.yaml --dataset feature_face_caption
```

---


### 📚 Reference

For more details, please refer to the official Emotion-LLaMA repository:  
https://github.com/ZebangCheng/Emotion-LLaMA
