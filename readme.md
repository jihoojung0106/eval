# Environment Setup

## 1. Python Environment
- Use **Python 3.9**
- Install required packages:
```
pip install -r requirements.txt
```

---

# Evaluation on MER2023 Dataset

## 1. Download Model
- **Base model:**  
  https://huggingface.co/meta-llama/Llama-2-7b-chat-hf  
  → Set `llama_model` in `eval_emotion.yaml` to the path, e.g.:  
  ```
  llama_model: "/mnt/bear3/users/jungji/ckpt/Llama-2-7b-chat-hf"
  ```

- **Finetuned checkpoint (`checkpoint_best.pth`):**  
  https://drive.google.com/file/d/1NoPZDj5_392zBtVK1IHO8bepA4910iI_/view  
  → Set `ckpt` in `eval_emotion.yaml` to the downloaded checkpoint path.

---

## 2. Download Data

### MER2023 Features
- `features_of_MER2023-SEMI.zip`:  
  https://drive.google.com/file/d/1DJJ8wP3g4yLT0ZFZ_-H4izJHAGJx2AJ_/view

- `relative_test3_NCEV.txt`:  
  https://drive.google.com/file/d/1YyoWabWtAJuFI6ylMM220i_kh_0Nagv9/view

Set the paths in **eval_emotion.yaml**:
```
feature_face_caption:
    eval_file_path: mer2023/features_of_MER2023/relative_test3_NCEV.txt     # MER2023
    img_path: mer2023/features_of_MER2023-SEMI/first_frames_MER2023-SEMI
```
relative_test3_NCEV.txt가 first_frames_MER2023-SEMI 이 폴더의 바로 상위 폴더에 있도록 해주길
---


## 3. Run Evaluation
Run the evaluation script with torchrun:

```
torchrun --nproc_per_node 1 eval_emotion.py --cfg-path eval_configs/eval_emotion.yaml --dataset feature_face_caption
```

---

## Reference
For more details, see the official Emotion-LLaMA repository:
https://github.com/ZebangCheng/Emotion-LLaMA
