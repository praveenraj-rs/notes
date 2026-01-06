
# Neural Networks: Classification, Theory & Usage
---
Neural Networks (NNs) are computational models inspired by the **biological brain**, designed to approximate complex, non-linear functions.

They are classified based on:

1. **Network Structure** – how neurons are connected
    
2. **Input Data Type** – spatial, temporal, graph, etc.
    
3. **Learning & Memory Behavior** – how knowledge is retained
    
4. **Functional Objective** – prediction, generation, control
    
5. **Biological Inspiration** – rate-based vs spike-based
    

---

# Classification Based on Network Structure

---

## 🔹 2.1 Feedforward Neural Network (FNN)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A-IPQlOd46dlsutIbUq1Zcw.png)

![Image](https://learnopencv.com/wp-content/uploads/2017/10/mlp-diagram.jpg)

### 📌 Core Idea

A **feedforward neural network** maps inputs to outputs using a **stack of weighted linear transformations followed by nonlinear activations**.

There are **no loops**, hence:

- No memory
    
- No temporal dependency
    

---

### 📐 Mathematical View

For a layer `l`:

[  
\mathbf{z}^{(l)} = \mathbf{W}^{(l)}\mathbf{a}^{(l-1)} + \mathbf{b}^{(l)}  
]

[  
\mathbf{a}^{(l)} = f(\mathbf{z}^{(l)})  
]

Where:

- `W` = weights
    
- `b` = bias
    
- `f` = activation (ReLU, Sigmoid, Tanh)
    

---

### 🧠 Why It Exists

FNNs were created to:

- Approximate **any continuous function** (Universal Approximation Theorem)
    
- Replace rule-based systems with **data-driven learning**
    

---

### ✅ Strengths

- Simple
    
- Fast inference
    
- Easy to deploy on microcontrollers
    

### ❌ Limitations

- No memory
    
- Cannot model sequences or time dependencies
    

---

### 📌 Typical Uses

- Regression (energy, temperature, SOC)
    
- Classification
    
- Fault detection
    

---

## 🔹 2.2 Recurrent Neural Network (RNN)

![Image](https://www.researchgate.net/publication/321811462/figure/fig2/AS%3A758310718406662%401557806772700/An-unrolled-Recurrent-Neural-Network.ppm)

![Image](https://d2l.ai/_images/rnn.svg)

### 📌 Core Idea

RNNs introduce **feedback connections**, allowing information to persist over time.

Each output depends on:

- Current input
    
- Previous hidden state (memory)
    

---

### 📐 Mathematical View

[  
h_t = f(W_x x_t + W_h h_{t-1} + b)  
]

[  
y_t = W_y h_t  
]

---

### 🧠 Why It Exists

Traditional FNNs failed on:

- Time-series
    
- Language
    
- Sequential sensor data
    

RNNs solve this by **sharing parameters across time**.

---

### ❌ Key Problem

**Vanishing / Exploding Gradients**

- Gradients shrink during backpropagation through time (BPTT)
    
- Long-term dependencies are lost
    

---

### ✅ Applications

- Time-series prediction
    
- Speech processing
    
- Vehicle speed/torque modeling
    

---

## 🔹 2.3 Long Short-Term Memory (LSTM)

![Image](https://pluralsight2.imgix.net/guides/8a8ac7c1-8bac-4e89-ace8-9e28813ab635_3.JPG)

![Image](https://d2l.ai/_images/lstm-3.svg)

### 📌 Core Idea

LSTM introduces a **cell state** that flows almost unchanged, controlled by **gates**.

This allows:

- Long-term memory retention
    
- Stable gradient flow
    

---

### 🚪 Gates Explained

|Gate|Purpose|
|---|---|
|Forget Gate|What to discard|
|Input Gate|What to store|
|Output Gate|What to reveal|

---

### 📐 Why It Works

The cell state provides a **linear path for gradients**, preventing vanishing gradients.

---

### ❌ Trade-Off

- High computational cost
    
- More parameters
    

---

### ✅ Applications

- Battery SOH/SOC prediction
    
- Regenerative braking control
    
- Predictive maintenance
    

---

## 🔹 2.4 Gated Recurrent Unit (GRU)

![Image](https://miro.medium.com/1%2Ai-yqUwAYTo2Mz-P1Ql6MbA.png)

![Image](https://image4.slideserve.com/9152372/lstm-vs-gru-l.jpg)

### 📌 Core Idea

GRU simplifies LSTM by:

- Merging forget & input gates
    
- Removing separate cell state
    

---

### 🧠 Why GRU Exists

To provide:

- Faster training
    
- Lower memory footprint
    
- Similar performance to LSTM
    

---

### ✅ Ideal For

- Embedded AI
    
- Edge devices
    
- Real-time systems
    

---

# 3️⃣ Classification Based on Input Data Type

---

## 🔹 3.1 Convolutional Neural Network (CNN)

![Image](https://miro.medium.com/1%2AQ6yA_1B_vsdGWAAwB8Z7rA.png)

![Image](https://www.researchgate.net/publication/331874666/figure/fig2/AS%3A738215627612160%401553015729189/Schematic-representation-of-a-convolution-and-pooling-layer-in-a-CNN.png)

### 📌 Core Idea

CNNs exploit **spatial locality** using shared filters.

---

### 🧠 Key Concepts

- **Convolution** → Feature extraction
    
- **Pooling** → Spatial reduction
    
- **Weight sharing** → Fewer parameters
    

---

### 📐 Why CNNs Are Powerful

- Translation invariance
    
- Hierarchical feature learning
    
- Efficient for images
    

---

### ✅ Applications

- Autonomous driving
    
- Thermal fault detection
    
- Camera-based diagnostics
    

---

## 🔹 3.2 Graph Neural Network (GNN)

![Image](https://towardsdatascience.com/wp-content/uploads/2021/06/1wtkkUZ7qAPL8Sixcs8c6vA.png)

![Image](https://media.springernature.com/full/springer-static/image/art%3A10.1038%2Fs41598-023-44224-1/MediaObjects/41598_2023_44224_Fig1_HTML.png)

### 📌 Core Idea

GNNs operate on **nodes and edges**, using **message passing**.

Each node updates its state based on neighbors.

---

### 🧠 Why GNN Exists

Traditional NNs fail when:

- Data has **no grid structure**
    
- Relationships matter more than values
    

---

### ✅ Applications

- Power grids
    
- EV charging networks
    
- Traffic & road systems
    

---

## 🔹 3.3 Transformer Neural Network

![Image](https://miro.medium.com/1%2AvrSX_Ku3EmGPyqF_E-2_Vg.png)

![Image](https://substackcdn.com/image/fetch/%24s_%21k5lk%21%2Cf_auto%2Cq_auto%3Agood%2Cfl_progressive%3Asteep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0f41a56a-8b4a-4fbb-9124-82c01f95fc35_3399x1665.png)

### 📌 Core Idea

Transformers replace recurrence with **self-attention**.

Each element attends to **all others simultaneously**.

---

### 🧠 Why Transformers Win

- Fully parallel
    
- Long-range dependency modeling
    
- Scales extremely well
    

---

### ❌ Limitation

- High memory usage
    
- Needs optimization for embedded systems
    

---

### ✅ Applications

- Language models
    
- Log analysis
    
- Multi-sensor fusion
    

---

# 4️⃣ Classification Based on Learning Behavior

---

## 🔹 4.1 Supervised Neural Networks

- Learn from labeled data
    
- Most industrial applications
    

---

## 🔹 4.2 Unsupervised Neural Networks

![Image](https://contenthub-static.grammarly.com/blog/wp-content/uploads/2024/10/6303_blog-visuals-auto-encoders_1500X800.png)

![Image](https://miro.medium.com/1%2AQG7afWQKjY3IpezhNQMzBg.png)

### 📌 Purpose

- Learn structure without labels
    

---

### 🧠 Why Useful

- Labeling is expensive
    
- Hidden patterns matter
    

---

### ✅ Applications

- Fault detection
    
- Feature extraction
    
- Compression
    

---

## 🔹 4.3 Reinforcement Learning Networks

![Image](https://www.researchgate.net/profile/Zeyuan-Yang-5/publication/339873542/figure/fig7/AS%3A868105483984923%401583983884820/a-Reinforcement-learning-architecture-b-Deep-reinforcement-learning-architecture.png)

![Image](https://www.researchgate.net/publication/353117089/figure/fig1/AS%3A1057728407543809%401629193512621/A-diagram-of-deep-Q-network-architecture.png)

### 📌 Core Idea

Agent learns by interacting with environment using **reward signals**.

---

### 🧠 Why RL Matters

- No labeled data
    
- Learns optimal control policies
    

---

### ✅ Applications

- EV energy management
    
- Robotics
    
- Autonomous systems
    

---

# 5️⃣ Special-Purpose Neural Networks

---

## 🔹 Autoencoders (AE)

- Dimensionality reduction
    
- Noise removal
    
- Fault detection
    

---

## 🔹 Generative Adversarial Networks (GAN)

- Generator vs Discriminator
    
- Synthetic data creation
    

---

## 🔹 Spiking Neural Networks (SNN)

![Image](https://www.researchgate.net/publication/342529143/figure/fig1/AS%3A11431281414771001%401746029432302/The-architecture-of-a-spiking-neural-network-SNN-The-network-consists-of-an-input.tif)

![Image](https://www.researchgate.net/publication/343269596/figure/fig2/AS%3A962207546343446%401606419564413/Mapping-of-online-learning-SNN-on-Neuromorphic-Hardware.png)

### 📌 Core Idea

Information is encoded as **spikes over time**, not continuous values.

---

### 🧠 Why SNN Exists

- Ultra-low power
    
- Brain-like computation
    

---

### ✅ Applications

- Neuromorphic chips
    
- Event-based sensors
    
- Edge AI
    

---