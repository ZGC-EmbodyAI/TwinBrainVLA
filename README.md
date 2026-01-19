<div align="center">

<h1>
    <span
        style="
            background: linear-gradient(90deg, #3b82f6, #8b5cf6);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            display: inline-block;
        "
    >TwinBrainVLA</span>
    <img src="./assets/TwinBrainVLA-logo.png" alt="logo" style="position: relative; top: -10px; margin-left: -2px; height: 40px;" />
    : Unleashing the Potential of Generalist VLMs for Embodied Tasks via Asymmetric Mixture-of-Transformers
</h1>

<a href="https://github.com/ZGC-EmbodyAI/TwinBrainVLA">
    <img alt="GitHub" src="https://img.shields.io/badge/GitHub-ZGC--EmbodyAI%2FTwinBrainVLA-blue?logo=github">
</a>
<a href="https://arxiv.org/">
    <img alt="arXiv" src="https://img.shields.io/badge/arXiv-2601.xxxxx-b31b1b.svg">
</a>
<a href="https://github.com/ZGC-EmbodyAI/TwinBrainVLA/blob/main/LICENSE">
    <img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-blue.svg">
</a>

**Bin Yu**<sup>1,2</sup>, **Shijie Lian**<sup>2,4</sup>, **Xiaopeng Lin**<sup>2,5</sup>, **Yuliang Wei**<sup>1</sup>, **Zhaolong Shen**<sup>2,6</sup>,<br>
**Changti Wu**<sup>2,7</sup>, **Yuzhuo Miao**<sup>1,2</sup>, **Xinming Wang**<sup>2,8</sup>, **Bailing Wang**<sup>1</sup>, **Cong Huang**<sup>2,3</sup>, **Kai Chen**<sup>2,3,9</sup>

<sup>1</sup>HIT, <sup>2</sup>ZGCA, <sup>3</sup>ZGCI, <sup>4</sup>HUST, <sup>5</sup>HKUST(GZ), <sup>6</sup>BUAA, <sup>7</sup>ECNU, <sup>8</sup>CASIA, <sup>9</sup>DeepCybo

<img src="./assets/ZGCA-logo.png" alt="ZGCA" style="vertical-align: middle; height: 16px; margin-right: 4px; position: relative; top: -2px;" />[Zhongguancun Academy](https://www.bjzgca.edu.cn/) & <img src="./assets/ZGCI-logo.png" alt="ZGCI" style="vertical-align: middle; height: 16px; margin-right: 4px; position: relative; top: -2px;" />[Zhongguancun Institute of Artificial Intelligence](https://www.zgci.ac.cn/)

</div>

---

## 📖 Abstract

Standard Vision-Language-Action (VLA) models typically fine-tune a monolithic Vision-Language Model (VLM) backbone explicitly for robotic control. However, this approach creates a critical tension between maintaining high-level general semantic understanding and learning low-level, fine-grained sensorimotor skills, often leading to "*catastrophic forgetting*" of the model's open-world capabilities. 

To resolve this conflict, we introduce **TwinBrainVLA**<img src="./assets/TwinBrainVLA-logo.png" alt="logo" style="position: relative; top: -5px; margin-left: 0px; height: 20px;" />, a novel architecture that coordinates a generalist VLM retaining universal semantic understanding and a specialist VLM dedicated to embodied proprioception for joint robotic control. TwinBrainVLA synergizes a frozen "Left Brain", which retains robust general visual reasoning, with a trainable "Right Brain", specialized for embodied perception, via a novel **Asymmetric Mixture-of-Transformers (AsyMoT)** mechanism. This design allows the Right Brain to dynamically query semantic knowledge from the frozen Left Brain and fuse it with proprioceptive states, providing rich conditioning for a Flow-Matching Action Expert to generate precise continuous controls.

Extensive experiments on SimplerEnv and RoboCasa benchmarks demonstrate that TwinBrainVLA achieves superior manipulation performance compared to state-of-the-art baselines while explicitly preserving the comprehensive visual understanding capabilities of the pre-trained VLM, offering a promising direction for building general-purpose robots that simultaneously achieve high-level semantic understanding and low-level physical dexterity.

## 🏗️ Architecture

TwinBrainVLA mimics the biological principle of hemispheric lateralization:

<div align="center">
  <img src="./assets/TwinBrainVLA-arch.svg" alt="TwinBrainVLA Framework" width="100%">
</div>

- **Left Brain (Generalist):** A frozen, pre-trained VLM (e.g., Qwen-VL) that serves as a semantic anchor, preserving open-world knowledge.
- **Right Brain (Specialist):** A trainable VLM initialized with the same weights, specialized for embodied control and proprioceptive state encoding.
- **Asymmetric MoT (AsyMoT):** A mechanism where the Right Brain attends to the frozen Key-Value (KV) pairs of the Left Brain via causal self-attention, transferring semantic knowledge without parameter pollution.
- **Action Expert:** A Flow-Matching Diffusion Transformer (DiT) that generates continuous actions based on the condition features from the Right Brain.

## 🙏 Acknowledgements

We would like to thank the [starVLA](https://github.com/starVLA/starVLA) project for its inspiring work and open-source contributions.
