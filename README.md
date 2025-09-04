# Extracting Weights: Breaking Taylor Unswift Obfuscation

This repository contains the implementation accompanying the paper:
**“Extracting Original Weights Post-Model Obfuscation: An Attack on Taylor Unswift.”**

We demonstrate that the [Taylor Unswift method](https://arxiv.org/pdf/2410.05331), which uses a truncated Taylor expansion to mask weight matrices in Transformer-style MLP layers, can be inverted. Our attack reconstructs the original weights with near-perfect accuracy using only inputs, outputs, and partial knowledge of the model.

---

## 📖 Overview

* **Taylor Unswift**: A technique that obfuscates the down-projection matrix $W_{d2}$ in Transformer MLPs by embedding it into a Taylor series expansion of the activation function.
* **Our Contribution**: We show that this obfuscation is *reversible*. By rearranging the forward equations and applying the Moore–Penrose pseudoinverse, we can directly solve for $W_{d2}$.
* **Result**: The recovered weights match the original with extremely high fidelity.

> **Average entry-wise distance between true and recovered weights:**
> **0.0000016806**

---

## 🚀 Features

* Implementation of the **forward obfuscated MLP** (Taylor Unswift).
* Attack pipeline to **reconstruct weights** from input–output pairs.
* Utilities for measuring recovery accuracy (L2 error, entry-wise distance).
* Example scripts demonstrating full recovery on LLaMA-style MLP layers.

---

## 🔬 Method

The core recovery equation is:

$$
W_{d2} = Z^{+} \, \tilde{Y}, \quad Z = \sigma(X W_{d1})
$$

where

* $X$ = input batch,
* $W_{d1}$ = encoder matrix,
* $\tilde{Y}$ = observed obfuscated output,
* $Z^{+}$ = pseudoinverse of the activation-transformed input.

This linear inversion bypasses the obfuscation and recovers the original $W_{d2}$.

---

## 📊 Results

* Average entry-wise distance between recovered and original weights:

  ```
  0.0000016806
  ```
* Recovery requires only moderate computation and does not degrade performance on benchmarked inference.

---

## 📂 Repository Structure

```
Extracting-Weights/
│── protection/                 # Appendix script for Taylor Unswift Core
│── taylor_expansion/         # Scripts to run Taylor Unswift
│── AttackSample.ipynb       # Attack sample
│── README.md            # Project documentation
```

---

## ⚠️ Disclaimer

This code is released for **academic and research purposes only**.
It is intended to evaluate the robustness of weight obfuscation methods and highlight potential vulnerabilities.

---

## 📜 Citation

If you use this work, please cite:

```
@article{taylorunswift_attack,
  title={Breaking Taylor Unswift: Extracting Original Weights Post Model Obfuscation},
  author={Nguyen, Ethan},
  year={2025},
  note={arXiv preprint}
}
```
