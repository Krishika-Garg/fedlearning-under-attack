# Federated Learning Under Data Poisoning Attacks

This project studies the **security vulnerabilities of Federated Learning (FL)** systems under **data poisoning and backdoor attacks**, and evaluates the effectiveness of **robust aggregation techniques** in defending against malicious clients.

Using a simulated federated environment, the project demonstrates how adversarial participants can compromise a global model — and how alternative aggregation strategies can significantly reduce attack success while preserving model performance.

---

## Key Highlights
- Simulated Federated Learning setup using **Flower (FLwr)**
- Implementation of **label-flip** and **backdoor poisoning attacks**
- Comparative analysis of **FedAvg**, **Trimmed Mean**, **Krum**, and **FoolsGold**
- Evaluation based on **Accuracy** and **Attack Success Rate (ASR)**
- Focus on **security–accuracy trade-offs** in decentralized learning

---

## Background

Federated Learning enables multiple clients to collaboratively train a shared model **without exchanging raw data**, making it well-suited for privacy-sensitive applications such as healthcare and finance.

However, the decentralized nature of FL introduces security risks. Malicious clients can manipulate local updates to:
- Corrupt the global model
- Introduce hidden backdoors
- Degrade system reliability without noticeable accuracy loss

This project explores these vulnerabilities and evaluates defense mechanisms through controlled experimentation.

---

## Objectives
- Analyze the impact of data poisoning attacks in Federated Learning
- Simulate adversarial client behavior in a federated environment
- Implement and compare robust aggregation strategies
- Identify methods that balance **robustness** and **model accuracy**

---

## System Overview

### Federated Workflow
1. MNIST dataset distributed across multiple clients (IID setup)
2. Clients perform local training on a CNN model
3. Malicious clients inject poisoned data or backdoor triggers
4. Server aggregates model updates using different strategies
5. Global model evaluated over multiple training rounds

---

## Attacks Implemented

### Label Flip Attack
Malicious clients deliberately flip class labels (e.g., `0 → 1`) during local training, introducing bias into the aggregated model.

### Backdoor Attack
Attackers inject specific pixel patterns into input samples, causing targeted misclassification when the trigger is present, while maintaining normal accuracy on clean data.

---

## Defense Mechanisms

| Aggregation Method | Description |
|------------------|-------------|
| **FedAvg** | Standard aggregation baseline, vulnerable to attacks |
| **Trimmed Mean** | Removes extreme updates before aggregation |
| **Krum** | Selects updates closest to the majority of clients |
| **FoolsGold** | Detects colluding attackers using gradient similarity |

---

## Experimental Results

| Aggregator | Accuracy (%) | ASR (%) | Observation |
|----------|--------------|---------|-------------|
| FedAvg | 95.97 | 36.90 | Highly vulnerable |
| Trimmed Mean | 95.25 | 10.13 | Best accuracy–security trade-off |
| Krum | 91.75 | 9.87 | Strong defense with accuracy drop |
| FoolsGold | 95.85 | 28.78 | Partial protection |
| FedAvg (No Attack) | 94.80 | 0.00 | Clean baseline |

**Key Insight:**  
Trimmed Mean achieved the most effective balance between reducing attack success and maintaining overall accuracy.

---

## Tech Stack
- **Language:** Python
- **Machine Learning:** PyTorch
- **Federated Learning:** Flower (FLwr)
- **Dataset:** MNIST
- **Visualization:** Matplotlib, Pandas
- **Execution Environment:** Google Colab
- **Distributed Simulation:** Ray
