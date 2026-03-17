# OpenEMMA VLM Model Comparison

## Overview

OpenEMMA employs a Chain-of-Thought (CoT) pipeline with a Vision-Language Model (VLM) for autonomous driving in CARLA 0.9.16. The VLM performs a four-step reasoning process: Scene Description → Critical Object Identification → Driving Intent → Motion Prediction.

The VLM functions as an **advisory system**, while actual vehicle control is handled by a route-based pure-pursuit controller. The VLM’s outputs are visualized in the UI and can influence speed through intent modulation.

Four VLM backends were evaluated under identical conditions: **Town01, same route, and same traffic environment**.

---

## 1. Model Specifications

| | LLaVA-v1.5-7B | LLaMA-3.2-11B-Vision | Qwen2-VL-7B | GPT-4o (API) |
|---|---|---|---|---|
| **Parameters** | 7B | 11B | 7B | Unknown (closed) |
| **Type** | Local | Local | Local | Cloud API |
| **VRAM (fp16)** | ~14 GB | ~22 GB | ~16 GB | 0 GB |
| **Conda Env** | `openemma` or `avllm` | `openemma` | `openemma` | `openemma` |
| **transformers** | 4.36.2+ | 4.46.2+ | 4.46.2+ | N/A |
| **Cost** | Free | Free | Free | ~$0.01/frame |

---

## 2. Quantitative Performance (GPT-4o — 4,341 Frames)

> Note: Quantitative data were extracted from GPT-4o debug CSV logs. Other models were compared qualitatively based on CoT logs due to the absence of saved CSV data.

| Metric | Value |
|---|---|
| Total frames | 4,341 |
| Avg speed | 8.9 km/h |
| Max speed | 17.0 km/h |
| Zero speed frames | 1,279 / 4,341 (29.5%) |
| Avg absolute steer | 0.0377 |
| Brake frames | 31 / 4,341 (0.7%) |
| VLM "red light" detected | 453 / 4,217 (10.7%) |
| VLM "stop" intent | 1,367 / 4,120 (33.2%) |
| VLM speed = 0 | 1,360 / 4,103 (33.1%) |

**GPT-4o Intent Distribution:**

| Intent | Count | % |
|---|---|---|
| Go straight and maintain speed | 2,142 | 52.0% |
| Go straight and stop | 1,207 | 29.3% |
| Go straight and slow down | 311 | 7.5% |
| Go straight and speed up | 300 | 7.3% |
| Other | 160 | 3.9% |

---

## 3. Qualitative CoT Comparison

### 3.1 Scene Description (CoT Step 1)

| Model | Quality | Example |
|---|---|---|
| **LLaVA** | Poor | "The driving scene in the virtual city includes traffic lights, other vehicles, pedestrians, and lane markings." (repeated every frame) |
| **LLaMA** | Good | "A virtual city street with a long, straight road and no other vehicles." / "A yellow line down the center..." |
| **Qwen** | Decent | "A straight road with yellow lane markings. The road is wide..." |
| **GPT-4o** | Excellent | "A straight road with a wet surface reflecting the setting sun." / "Double yellow lane markings, indicating two-way traffic." |

**Analysis:**

- LLaVA: Repeats fixed templates → fails to capture actual scene variation  
- LLaMA: Generates frame-dependent descriptions, capturing road geometry and object presence  
- Qwen: Better than LLaVA but limited variation  
- GPT-4o: Captures fine-grained details such as surface conditions, lighting, and lane semantics  

---

### 3.2 Critical Objects (CoT Step 2)

| Model | Hallucination Rate | Primary Issue |
|---|---|---|
| **LLaVA** | ~95%+ | Always hallucinates "Red traffic light" |
| **LLaMA** | ~5% | Occasionally includes irrelevant objects |
| **Qwen** | ~70% | Frequent "Red traffic light" hallucination |
| **GPT-4o** | ~10% | Detects only valid objects with diversity |

**Key Findings:**

- LLaVA & Qwen: Strong dataset bias toward "red traffic light" → hallucinations even in empty scenes  
- LLaMA: Lowest hallucination rate among local models  
- GPT-4o: Minimal hallucination with broader object diversity  

---

### 3.3 Driving Intent (CoT Step 3)

| Model | Estimated Stop Ratio | Intent Diversity | Accuracy |
|---|---|---|---|
| **LLaVA** | ~5% | Very low ("Go straight" repetition) | Low |
| **LLaMA** | ~15% | High (speed up / maintain / slow down) | High |
| **Qwen** | ~60% | Low (excessive "Stop") | Low |
| **GPT-4o** | ~33% | High (balanced distribution) | High |

**Analysis:**

- Qwen: Red-light hallucination leads to excessive stopping → degraded driving performance  
- GPT-4o: Balanced intent distribution reflecting real scenarios  
- LLaMA: Similar pattern to GPT-4o with reliable situational awareness  

---

### 3.4 Motion Prediction (CoT Step 4)

| Model | Format | Parsing Success | Speed Profile |
|---|---|---|---|
| **LLaVA** | Unstable | ~60% | Frequent numerical hallucination |
| **LLaMA** | `5,0; 5.5,0; 6,0` | ~95% | Gradual acceleration |
| **Qwen** | `0,0; 0,0; 0,0` | ~90% | Often stuck at zero (stop bias) |
| **GPT-4o** | `3.8,0; 3.8,0; 3.8,0` | ~98% | Smooth acceleration/deceleration profiles |

---

## 4. Overall Summary

| Criteria | LLaVA-v1.5-7B | LLaMA-3.2-11B | Qwen2-VL-7B | GPT-4o |
|---|---|---|---|---|
| **Scene Quality** | ★☆☆☆☆ | ★★★★☆ | ★★★☆☆ | ★★★★★ |
| **Hallucination** | ★☆☆☆☆ (severe) | ★★★★☆ (minimal) | ★★☆☆☆ (moderate) | ★★★★★ (minimal) |
| **Intent Accuracy** | ★★☆☆☆ | ★★★★☆ | ★★☆☆☆ | ★★★★★ |
| **Motion Quality** | ★★☆☆☆ | ★★★★☆ | ★★★☆☆ | ★★★★★ |
| **Inference Speed** | ★★★★★ (~2s) | ★★★☆☆ (~4s) | ★★★★☆ (~3s) | ★★★★★ (~1–2s) |
| **VRAM** | ★★★★☆ (14GB) | ★★★☆☆ (22GB) | ★★★★☆ (16GB) | ★★★★★ (0GB) |
| **Cost** | ★★★★★ | ★★★★★ | ★★★★★ | ★★☆☆☆ |
| **Overall** | ★★☆☆☆ | ★★★★☆ | ★★★☆☆ | ★★★★★ |

---

## 5. Ranking & Recommendation

| Rank | Model | Strengths | Weaknesses |
|---|---|---|---|
| 1 | **GPT-4o** | Best scene understanding, minimal hallucination, smooth motion planning | API cost (~$0.01/frame), requires internet |
| 2 | **LLaMA-3.2-11B** | Strongest local model, low hallucination, diverse intent | Requires ~22GB VRAM, slower inference |
| 3 | **Qwen2-VL-7B** | Decent scene description, clean output format | Red-light hallucination → excessive stopping |
| 4 | **LLaVA-v1.5-7B** | Lightweight and fast | Severe hallucination, generic responses |

**Research Recommendations:**

- **For papers**: Use GPT-4o (best performance baseline) + LLaMA-3.2-11B (best local baseline)  
- **For real-time demos**: LLaMA-3.2-11B (free, sufficient performance)  
- **For cost-constrained setups**: LLaMA-3.2-11B only  

---

## 6. Run Commands

```bash
# GPT-4o (API — best quality)
OPENAI_API_KEY=sk-... conda run -n openemma python openemmaUI.py --gpt

# LLaMA-3.2-11B (local — best free option)
conda run -n openemma python openemmaUI.py --llama

# Qwen2-VL-7B (local)
conda run -n openemma python openemmaUI.py --qwen

# LLaVA-v1.5-7B (local — not recommended)
conda run -n openemma python openemmaUI.py --llava
```

## 7. Notes

All models use the same route-based pure-pursuit controller (VLM is advisory only)

All four models are supported in the openemma conda environment (transformers 5.3.0+)

The avllm environment (transformers 4.36.2) supports only LLaVA

GPT-4o requires the OPENAI_API_KEY environment variable

For proper quantitative comparison, debug CSV logging for all models should be implemented (TODO)
