# :book: Red Teaming Privacy-Protective Perturbation: Blind Face Restoration as an Attack Strategy

This repository contains the code for the adaptive test. 

Model weight for restoration models: [DiffBIR](https://huggingface.co/lxq007/DiffBIR/resolve/main/face_swinir_v1.ckpt), [Codeformer](https://github.com/sczhou/CodeFormer/releases/download/v0.1.0/codeformer.pth)


## :lock: Applying Adaptive Protection 

```
bash scripts/train_(codeformer/diffbir).sh %s %s'%(input_path, output_path)
```
(The codeformer weight can be automatically download while the diffbir weight should be downloaded and modify the path in DiffBIR_adapt line 858)

## :unlock: restoration attack

Please refer to [DiffBIR](https://github.com/XPixelGroup/DiffBIR), [Codeformer](https://github.com/sczhou/CodeFormer) to launch the restoration attack.

Codeformer inference:
```
python inference_codeformer.py -w 0.5 --has_aligned --input_path --output_path
```
DiffBIR inference:
```
python -u inference.py \--task face \--upscale 1 \--version v2 \--sampler spaced \--steps 50 \--captioner none \--pos_prompt \'\' \--neg_prompt \'low quality, blurry, low-resolution, noisy, unsharp, weird textures\' \--cfg_scale 4.0 \--input  --output CAAT_atkpdm_v3_wm_diffbir/%s --device cuda --precision fp32
```

## Code for the algorithms included in the experiments

### 🛡️ Protective Perturbation

- All protective perturbations use random seed `1042`.  
- We adopt the official implementations from the following repositories (default settings used):
  - [AdvDM](https://github.com/zhengyuezhao/gridpure)
  - [Anti-DreamBooth](https://github.com/VinAIResearch/Anti-DreamBooth)
  - [CAAT](https://github.com/CO2-cityao/CAAT)
  - [MetaCloak](https://github.com/liuyixin-louis/MetaCloak)
  - [DisDiff](https://github.com/riolys/DisDiff)
  - [SimAC](https://github.com/somuchtome/SimAC)

---

### 🧑‍🎨 Personalized Generation

- DreamBooth is run with random seed `10042`.  
- We use the following codebases with default settings:
  - [DreamBooth](https://github.com/VinAIResearch/Anti-DreamBooth)
  - [Custom Diffusion](https://github.com/adobe-research/custom-diffusion)

---

### 🧼 Purification-based Attack

- Official implementations are adopted with default configurations:
  - [GridPure](https://github.com/zhengyuezhao/gridpure)
  - [PDM-Pure](https://github.com/xavihart/PDM-Pure)

---

### 🧯 Restoration-based Attack

- We use the following repositories (default settings applied):
  - [CodeFormer](https://github.com/sczhou/CodeFormer)
  - [DiffBIR](https://github.com/XPixelGroup/DiffBIR)

---

### 📏 Evaluation Metrics

- Metric implementations are reused from:
  - [ISM, FDFR](https://github.com/VinAIResearch/Anti-DreamBooth)
  - [CLIP-IQAC, LIQE](https://github.com/liuyixin-louis/MetaCloak)





