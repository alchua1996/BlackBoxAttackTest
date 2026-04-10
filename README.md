# Zeroth-Order Black-Box Adversarial Attacks (ZO-AdaBound)

## Overview

This project implements **black-box adversarial attacks** on deep learning models using **zeroth-order (gradient-free) optimization methods**. The focus is on attacking models where gradients are not accessible, such as deployed APIs or production systems.

The core contribution is the implementation and evaluation of **ZO-AdaBound**, an adaptive zeroth-order optimizer designed to improve stability and performance in high-dimensional, query-limited settings.

This work was completed as part of a **graduate-level class project** focused on optimization and machine learning, and is my portion of the work.

---

## Key Features

* Black-box adversarial attack pipeline for image classification models
* Zeroth-order gradient estimation via:

  * Random direction sampling
  * Coordinate-wise estimation
  * Natural Evolution Strategies (NES)

* Evaluation metrics:

  * Attack success rate
  * L2 distortion
  * Iterations / query efficiency

---

## My Contribution

This repository builds on an existing implementation of **ZO-AdaMM** and related zeroth-order optimization methods.

My primary contributions include:

* Implementing **ZO-AdaBound**, an adaptive zeroth-order optimizer with bounded learning rates
* Integrating ZO-AdaBound into a black-box adversarial attack pipeline
* Designing and running experiments to evaluate:

  * Convergence behavior
  * Stability vs. baseline optimizers
  * Attack effectiveness under query constraints
* Extending the framework to support multiple gradient estimation strategies

---

## Theoretical Analysis (Proofs)

In addition to implementation, I developed **formal theoretical guarantees** for the proposed method.

* Derived **convergence results for nonconvex optimization settings**
* Established **regret bounds in convex settings**
* Analyzed the behavior of zeroth-order adaptive methods under noisy gradient estimates

Full proofs and derivations are provided in the accompanying PDF:

📄 `ZO-AdaBound-Proofs.pdf`

---

## Methodology

### Black-Box Attack Setting

We assume:

* No access to model gradients or internal parameters
* Only query access to model outputs (probabilities or logits)

Attacks are performed by iteratively estimating gradients using **function evaluations only**, then updating perturbations to induce misclassification.

---

### Zeroth-Order Gradient Estimation

Gradients are approximated using random direction sampling:

* Sample random direction vectors
* Evaluate function differences
* Construct gradient estimates from directional derivatives

This enables optimization in high-dimensional spaces without backpropagation.

---

### ZO-AdaBound

ZO-AdaBound extends adaptive optimization to the zeroth-order setting by:

* Maintaining first and second moment estimates of gradient approximations
* Applying **dynamic bounds on learning rates** to stabilize updates
* Combining:

  * Fast convergence (adaptive methods)
  * Stability (bounded step sizes)

---

## Code Structure

```id="code_structure"
.
├── imagenet_blackBox_attack2.py   # Main attack script
├── Utils.py                       # Helper functions (model queries, preprocessing)
├── setup_inception.py             # Model and dataset setup (ImageNet / Inception)
├── ZOAdaBound_Final.pdf         # Theoretical analysis and proofs
```

---

## Usage

1. Configure parameters in the `args` dictionary:

   * Dataset (e.g., ImageNet)
   * Number of iterations
   * Learning rate
   * Number of query directions (`q`)
   * Optimization method (`mode = "ZOAdaBound"`)

2. Run:

```id="run_command"
python imagenet_blackBox_attack2.py
```

---

## Notes

* This code is adapted from a baseline implementation of **ZO-AdaMM** and related zeroth-order optimization methods
* The current structure reflects academic-oriented experimentation rather than production-level engineering
* Some dependencies (e.g., dataset loaders, model wrappers) may require additional setup


---

## Disclaimer

This project is intended for **research and educational purposes only**, specifically to study the robustness and security of machine learning models.

---

