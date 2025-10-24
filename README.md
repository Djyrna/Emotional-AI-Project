# EmotionAI – Emotion-Aware Story and Image Generation


## Overview

**EmotionAI** is an artificial intelligence system designed to support the emotional well-being of children — particularly orphans — through personalized visual storytelling.

The system:
1. Detects a child’s facial emotion from an image.
2. Extracts additional attributes (age, gender, glasses, clothing color).
3. Generates a therapeutic **story** tailored to the detected emotion.
4. Produces a matching **illustration** in an anime art style.

The result is an **emotionally intelligent AI companion** that provides empathy and comfort in a nonverbal, visually engaging way.


## Pipeline Overview

### Emotion Detection  
- Dataset: **FER2013**  
- Models tested:  
  - **ResNet18** – stable and efficient  
  - **DenseNet121** – best generalization performance  
  - **Vision Transformer (ViT)** – explored, but limited by dataset size  

**Best model:** DenseNet121 (Test Accuracy ≈ 65%)  

---

### Story Generation  
- Emotion classification (0–6 → Angry, Disgust, Fear, Happy, Sad, Surprise, Neutral)  
- Detected traits (age, gender, glasses, color) are used to craft a **personalized prompt**.  

**Language Models used:**  
| Model | Params | Description |
|--------|---------|-------------|
| Pythia-410M | 0.4B | Lightweight, fast inference |
| OPT-1.3B | 1.3B | Fluent, coherent generation |
| Phi-3 Mini | 3.8B | Best balance between empathy and fluency |

Example prompt:
> *"A child with big emotions learns that anger transforms into strength when..."*



### Image Generation  
- Models:  
  - **Counterfeit-V2.5** – fine-tuned Stable Diffusion for anime visuals  
  - **Waifu Diffusion** – smooth, colorful, expressive style  

- Parameters explored:  
  - `num_inference_steps`: 25 → 70  
  - `guidance_scale`: 7.5 → 15  

Negative prompts were used to remove undesired features for better control.

---

### Evaluation  
- **Emotion Alignment:** The generated story’s emotion is compared with the detected facial emotion.  
- **CLIPScore:** Measures semantic coherence between the generated story and image.  

Example results:  
| Image | Steps | Guidance | Dominant Emotion |
|--------|--------|-----------|------------------|
| Fig. 4 | 50 | 7.5 | Neutral |
| Fig. 7 | 70 | 7.5 | Happy |

---

## Results Summary

| Model | Train Acc. | Test Acc. | Notes |
|--------|-------------|-----------|-------|
| ResNet18 | 99.5% | 59.8% | Strong baseline |
| DenseNet121 | 99.5% | **65.1%** | Best test results |
| ViT | – | 47% | Resource-limited |

Emotion recognition achieved solid accuracy.  
Generated stories reflect emotional tone (verified via external models).  
Anime-style images enhance emotional engagement.  

---

##  Conclusion

**EmotionAI** demonstrates how deep learning and multimodal generation can be combined to create emotionally adaptive, human-centered AI experiences.

Although the system works effectively, future improvements include:
- Multi-image story generation (series of scenes).  
- Audio narration or animation for richer interaction.  
- More advanced prompts incorporating visual similarity with the child’s photo.

