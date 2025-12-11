<!-- PROJECT BANNER -->
<p align="center">
  <img src="https://via.placeholder.com/900x200.png?text=Rock–Paper–Scissors+RNN+%7C+Online+Learning+Neural+Network" />
</p>

<h1 align="center">🤖 Rock–Paper–Scissors RNN (Online Learning AI)</h1>

<p align="center">
  <strong>A self-learning interactive game where an RNN predicts your next move.</strong>
</p>

<p align="center">
  <!-- BADGES -->
  <img src="https://img.shields.io/badge/Python-3.10-blue" />
  <img src="https://img.shields.io/badge/TensorFlow-RNN-orange" />
  <img src="https://img.shields.io/badge/Keras-Online--Learning-green" />
  <img src="https://img.shields.io/badge/Run%20in-Colab-yellow" />
  <img src="https://img.shields.io/badge/License-MIT-brightgreen" />
</p>

---
## 📌 Overview

This project implements an **interactive Rock–Paper–Scissors game** where the computer uses a **Recurrent Neural Network (RNN)** to learn and **predict your moves in real time**.  

It actively updates its weights **after every round**, making the computer smarter the more you play. If you repeat patterns (consciously or unconsciously), the RNN learns them and begins beating you consistently.

---

## 🚀 Features

### ✔ **Live Online Learning**
- The RNN updates after every round using `train_on_batch()`.
- Learns user patterns like:  
  - *rock → rock → paper → rock → rock → paper*  
  - *alternating sequences*  
  - *biases (always start with rock)*  

### ✔ **Stats Tracking**
- Total rounds  
- User wins  
- Computer wins  
- Ties  
- Computer win rate  

### ✔ **Interactive UI (Colab)**
Uses **ipywidgets**:
- Buttons for rock/paper/scissors  
- Reset button  
- Live scoreboard  

### ✔ **Smart Counter Strategy**
The model predicts your next move → computer plays the winning move.

---

## 🧠 How It Works (Deep Dive)

### 🔹 1. One-Hot Encoding
Each move is mapped to a 3-dimensional vector:

| Move      | Vector     |
|-----------|------------|
| rock      | [1, 0, 0]  |
| paper     | [0, 1, 0]  |
| scissors  | [0, 0, 1]  |

---

### 🔹 2. Sliding Window of Last 5 Moves
The last **5 user moves** are stored in a sequence buffer:
[
[1,0,0],
[0,1,0],
[1,0,0],
[1,0,0],
[0,1,0]
]



This becomes the **RNN input**.

---

### 🔹 3. RNN Architecture
    A[User Move History] --> B[One-Hot Encoding];
    B --> C{Sequence Buffer<br/>(length = 5)};
    C --> D[SimpleRNN Layer<br/>32 units];
    D --> E[Dense Layer<br/>16 units];
    E --> F[Softmax Output<br/>rock/paper/scissors];
    F --> G[Prediction of User Next Move];
    G --> H[Counter Move Selection];
