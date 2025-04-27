---
layout: post
title: Key Insights from Professor Yann LeCun's Talk on "Shaping the Future of AI Innovations" at NUS120 Distinguished Speaker Series
category:
    - "Artificial Intelligence (AI)"
    - "Deep Learning"
    - "Machine Learning"
    - "Natural Language Processing (NLP)"
    - "Future of AI"
    - "Talk"
---
It was a privilege to attend today's NUS120 Distinguished Speaker Series at the National University of Singapore, where Professor Yann LeCun shared some truly insightful perspectives on AI and it's future. In this post, I'll try to summarize some key insights I learned from his talk.

![alt text](/images/yunn-lecun-imran-nus120.jpg "Professor Yunn LeCun")

---

### **Key Argument**

Professor LeCun's central argument is that current approaches, especially relying heavily on Auto-Regressive Large Language Models (LLMs), are fundamentally limited and will not lead to true Advanced Machine Intelligence (AMI) or systems with human-level understanding. He advocates for a necessary paradigm shift towards models capable of learning world models directly from sensory input.

Notably, Professor LeCun expressed his preference for the term `Advanced Machine Intelligence (AMI)` over `Artificial General Intelligence (AGI)`.

He points out the misconception that LLMs could soon reach PhD-level capabilities, comparing it to a recurring mistake in AI history. For example, Newell and Simon’s belief in systematic search as the path to intelligence failed due to the overwhelming complexity of real-world problems. Similarly, today’s focus on pattern recognition falls short. In his view, true intelligence involves non-trivial problem-solving in open-ended, unpredictable environments, which cannot be reduced to brute-force search or shallow pattern recognition.

He emphasizes that achieving human-level AI demands **novel paradigms** beyond today’s LLMs, addressing gaps in world modeling, reasoning, and safety.

---

### **The Future of Human-Digital Interaction**

**AI Assistants as Mediators**: All interactions with the digital world will soon be mediated by AI systems that understand, reason, and plan.

**Human-Level Intelligence Requirements**:

- Machines must **understand the physical world** (intuitive physics, object manipulation).
- Systems need **persistent memory**, **reasoning/planning abilities**, and **controllability/safety by design**.

---

### **Critique of Current Approaches**

**Auto-Regressive LLMs Are Flawed**:

- **Fundamental Limitations**: LLMs cannot be made fully factual, non-toxic, or controllable. Errors compound exponentially with token generation.
- **Lack of World Understanding**: LLMs process text as discrete tokens but fail to grasp the physical world (e.g., no domestic robots match a house cat’s basic intelligence).
- **Regurgitation vs. Innovation**: LLMs primarily regurgitate training data and cannot invent novel solutions to unseen problems.

**The Moravec Paradox**:

- AI excels at complex tasks (e.g., chess) but struggles with "simple" human/animal skills (e.g., object manipulation, basic planning).
- **Root Cause**: Language is simpler than physical-world modeling. LLMs lack sensory experience and intuitive physics.

**Data Limitations**:

- **LLMs vs. Human Children**: A 4-year-old processes $~1.1E14$ bytes of visual data (via optical nerves), surpassing even the largest LLMs (trained on $~0.9E14$ bytes of text).
- **Sensory Learning Gap**: LLMs miss the rich, continuous sensory input humans use to build mental models.

**Scaling and Probabilistic Models:**

- **Scaling Alone is Insufficient:** Simply scaling up current LLM architectures will not inherently lead to the desired level of intelligence or address fundamental flaws.
- **Inherent Instability of Auto-Regressive Prediction:** As the sequence length increases, the probability of deviating from coherent and correct outputs grows exponentially in auto-regressive models.
- **Generative Models Inadequate for Continuous Domains:** Generative models, which aim to predict every detail, are not well-suited for the partially predictable and high-dimensional continuous nature of the real world.
- **Intractability of Probabilistic Models:** Probabilistic models become computationally infeasible in high-dimensional continuous domains.

---

### **Desiderata for Advanced Machine Intelligence (AMI)**

Professor LeCun outlines the following essential characteristics for future AI systems:

- **Learning World Models from Sensory Inputs:** Systems should learn intuitive physics and how the world works directly from sensory data like video.
- **Persistent Memory:** The ability to retain and access information over time.
- **Large-Scale Associative Memories:** Mechanisms for efficiently linking and retrieving related information.
- **Planning Actions:** Systems must be able to devise sequences of actions to achieve specific objectives.
- **Reasoning:** The capacity to infer and deduce, leading to the invention of new solutions to unseen problems (zero-shot learning).
- **Controllability and Safety by Design:** Ensuring that AI systems operate within defined boundaries and for intended purposes, not as an afterthought through fine-tuning.

---

### **Recommended Architectural Shifts**

**Replace Generative Models**

- **Joint-Embedding Predictive Architecture (JEPA):** Investigate and develop models based on joint embedding. Predict abstract representations of inputs rather than pixels/tokens, enabling handling of partially predictable environments. This is presented as a potential solution to overcome the limitations of generative models.
- **Energy-Based Models (EBMs):** Utilize models that learn an energy function representing the compatibility between inputs and outputs, enabling inference through optimization, enabling complex inference/planning (superior to fixed feed-forward networks).

**Key Recommendations**:

- **Abandon Generative Models:** Shift focus away from purely generative approaches. Abandon **auto-regressive LLMs**, **probabilistic models**, and **contrastive learning**.
- **Move Beyond Contrastive Methods:** Adopt **regularized methods**, **model-predictive control**, and use RL only to refine world models.
- **Re-evaluate Reinforcement Learning (RL):** Primarily use model-predictive control for planning and reserve RL for adjusting the world model or critic when planning fails.
- **Focus Research Away from LLMs (for Human-Level AI):** If the goal is human-level intelligence, resources should be directed towards alternative architectures and approaches.

---

### **Open Research Challenges**

- **World-Model Training**: Train models on multimodal data (video, text, code, interactions) at scale. Develop **JEPA with latent variables** to handle non-deterministic environments.
- **Planning & Optimization**: Gradient-based/combinatorial algorithms for hierarchical planning under uncertainty. Large-scale **differentiable associative memories** for efficient reasoning.
- **Safety & Robustness**: Regularize latent variables to prevent model collapse. Ensure systems act predictably in novel scenarios.

---

### **Provocative Conclusion**

`"IF YOU ARE INTERESTED IN HUMAN-LEVEL AI, DON'T WORK ON LLMS"`

- **Scaling LLMs Is Not Enough**: Human-level AI requires new paradigms emphasizing **world modeling**, **sensory learning**, and **optimization-based reasoning**.
- **Call to Action**: Shift research focus to architectures like JEPA and EBMs, prioritizing physical-world understanding and safety.

---

In essence, Professor LeCun advocates for a fundamental rethinking of AI architectures, moving away from the dominant paradigm of auto-regressive language models towards systems that learn rich, continuous world models from sensory experience and perform inference through optimization rather than simple feed-forward propagation.

Professor LeCun referred to his paper "[A Path Towards Autonomous Machine Intelligence](https://openreview.net/forum?id=BZ5a1r-kVsf)" where he distilled many of his ideas on AI and Advanced Machine Intelligence (AMI).
