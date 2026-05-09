## VIBE: Disentangling Social Dynamics via Kinematics-Informed Variational Inference for Behavioral Emotion 

**VIBE** is a kinematics-aware framework designed for Group Emotion Recognition (GER). Unlike current AI models that act as black boxes and get distracted by background environments , VIBE utilizes causal structuring and mathematical constraints to filter out background noise and isolate the genuine emotions and sociological mechanics of a crowd.

---

## Key Innovations

* **Causal Disentanglement**: Employs a Dual-Stream Variational Information Bottleneck (VIB) to strictly separate affective signals from environmental confounders.


* **Orthogonality Constraint**: Introduces a soft constraint that geometrically forces the "Agent" and "Context" latent spaces to remain disjoint, ensuring the model focuses on agent dynamics rather than background noise.


* **Gamma-Gated Transformer**: Features a Transformer equipped with Decoupled Adaptive Layer Normalization (AdaLN). This modulates neural attention based on a raw physical synchrony metric ($\gamma$), allowing the model to dynamically adapt based on the crowd's physical state.


* **Text-Guided Semantic Alignment**: Projects learned features into a shared embedding space to enforce cosine similarity with pre-trained textual anchors, explicitly grounding abstract visual dynamics in human interpretability.



---

## Architecture & Modalities

VIBE integrates audio, video, and text modalities through specialized pre-trained backbones:

* **Global Context ($X_{glob}$)**: Captured using VideoMAE V2 to process scene-level dynamics.


* **Local Agent Tubes ($X_{loc}$)**: Visual tubes are extracted for tracked agents and processed via DINOv2 to represent raw actor dynamics.


* **Acoustic Prosody ($X_{aud}$)**: Paralinguistic cues (like pitch and energy) are extracted using HuBERT.


* **Textual Context ($X_{text}$)**: Crowd-level descriptions are encoded using RoBERTa to serve as linguistic anchors for the semantic alignment objective.



---

## Performance Benchmarks

VIBE sets a new benchmark for group affect prediction, consistently outperforming state-of-the-art methods on "in-the-wild" datasets:

| Dataset | Accuracy | F1 Score |
| --- | --- | --- |
| **VGAF** | <br>**70.17%** 

 | 0.701 

 |
| **GECV** | <br>**91.85%** 

 | 0.915 

 |

Performance consistently peaks when the model tracks around 8 agents ($K=8$), effectively capturing the primary affective circle.

---

## Implementation Setup

* **Hardware Environment**: Conducted on a workstation equipped with an NVIDIA A2000 GPU (12GB VRAM), an Intel® Xeon® W-2265 CPU, and 64 GB of RAM.


* **Optimization**: Trained using the AdamW optimizer with a weight decay of $1\times10^{-3}$ and a Cosine Annealing learning rate scheduler.


* **Hyperparameters**: Utilizes a batch size of 16, an initial learning rate of $1\times10^{-4}$, and a latent dimension (D) of 512, trained over 30 epochs.


* **Data Processing**: Video streams are temporally decimated to 6 Hz, and raw trajectory coordinates are stabilized using a Gaussian smoothing kernel to mitigate detector jitter.



---

## Impact

By effectively separating human behavior from the surrounding environment, VIBE mitigates "shortcut learning," preventing models from making biased guesses based on background details. This helps build more transparent, accountable, and responsible AI systems for emotion recognition that are robust across diverse, real-world locations.
