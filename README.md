# Reinforcement Learning in Custom Grid-World Environments

This repository presents a comprehensive study of tabular reinforcement learning algorithms applied to custom-designed Grid-World environments. The work focuses on environment design, policy learning, algorithm comparison, and visualization.

The project explores:
- Markov Decision Process (MDP) formulation
- On-policy learning using SARSA
- Multi-step off-policy learning using n-step Double Q-learning
- Visualization-driven environment interpretation
- A logistics-inspired warehouse robot environment

---

## Key Contributions

- Design of multiple custom Grid-World environments following a Gym-style interface
- Implementation of SARSA from first principles using epsilon-greedy exploration
- Implementation of n-step Double Q-learning with n ranging from 1 to 5
- Empirical hyperparameter analysis and optimization
- Development of dynamic visualizations for agent behavior
- Evaluation of learning stability, convergence speed, and reward dynamics

---

## Algorithms Implemented

### SARSA (On-Policy Temporal Difference Control)

- Tabular Q-learning structure
- Epsilon-greedy exploration strategy
- Decaying exploration rate
- Empirical convergence analysis using episode reward curves

### n-step Double Q-Learning

- Dual Q-table architecture to reduce maximization bias
- Generalized n-step return formulation
- Comparative evaluation for n values in the range 1 to 5
- Improved learning stability compared to SARSA

---

## Environments

### Custom Grid-World Environment

- Discrete state space with obstacles, hazards, and reward zones
- Four-directional agent movement
- Explicit reward shaping for learning efficiency
- Grid visualization using Matplotlib

### Warehouse Robot Environment

- 6x6 grid representing a warehouse layout
- Static obstacles acting as shelves
- Object pickup and delivery mechanics
- Extended action space including movement, pick-up, and drop-off
- Augmented state representation combining agent position and object possession
- Sparse terminal reward for successful delivery

---

## Evaluation and Analysis

Evaluation metrics include:
- Episode-wise total reward tracking
- Exploration rate decay visualization
- Comparison of initial and trained Q-tables
- Greedy policy rollouts after training
- Cross-algorithm performance comparison

Experimental results demonstrate stable convergence using SARSA and faster, more stable learning using n-step Double Q-learning. Optimal performance is achieved with moderate n-step values, typically between 2 and 3.

---


