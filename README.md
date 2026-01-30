# Reinforcement Learning for Drone Delivery and Warehouse Navigation in Grid-World Environments

This repository contains an experimental study of tabular reinforcement learning methods in two custom Grid-World settings:

1) A drone parcel delivery task with hazards and goal-driven navigation
2) A warehouse robot task with obstacles, pick-up, and drop-off actions

The focus is on environment design, reward shaping, learning dynamics, and algorithm comparison using interpretable tabular methods.

---

## Project Summary

This work models each task as a Markov Decision Process (MDP) with discrete states and actions, then learns policies using:

- SARSA (on-policy temporal-difference control)
- n-step Double Q-learning (off-policy, reduced maximization bias), evaluated for n = 1 to 5

The repository includes training/evaluation plots, learned Q-tables, greedy policy rollouts, and environment visualizations.

---

## Environment 1: Drone Parcel Delivery Grid-World

The drone delivery environment is a 5x5 grid (25 states). The agent starts from a default location and must pick up a parcel and deliver it to a destination while avoiding hazardous zones.

### State Space
- 25 discrete states
- Each state is an integer in [0, 24]
- Mapping is derived from the drone’s 2D coordinates (x, y)

### Action Space
4 discrete actions:
- 0: move up
- 1: move down
- 2: move left
- 3: move right

Invalid moves outside the grid are clipped to keep the agent inside the map boundaries.

### Reward Design
The reward function is structured to encourage efficient pick-up and delivery while discouraging unsafe navigation:

- +10 for picking up the parcel (only once)
- +25 for delivering the parcel (terminal)
- -1 per step (time cost)
- -10 for entering a wind zone
- -15 for entering a no-fly zone
- -5 for entering a low-battery zone

### Objective
Starting from the default position:
1) Navigate to the parcel and pick it up
2) Avoid hazards while moving toward the delivery location
3) Deliver the parcel with maximum cumulative reward

### Environment Validation
The environment logic was verified by running a random agent for 10 timesteps. At each step, the notebook prints:
- current state
- chosen action
- received reward
- next state

A full grid visualization is displayed at every step, confirming:
- safe boundary handling (clipping)
- reward signals are triggered on correct tiles
- hazard penalties occur in the correct zones
- successful delivery terminates the episode when the parcel has been collected

---

## Environment 2: Warehouse Robot Grid-World

The warehouse environment is a 6x6 grid with static obstacles (shelves). The robot must pick up an item from a fixed pick-up location and deliver it to a drop-off location.

### State Space
- Agent position (x, y) plus a boolean flag indicating whether the agent is carrying the item
- Total observations = 2 x 36 = 72 unique states

### Action Space
6 actions:
- up, down, left, right, pick, drop

### Reward Design
- -1 per step
- -20 for attempting to move into a shelf or outside the grid
- +25 for successful pick-up (only if not already carrying)
- +100 for successful drop-off at the target while carrying (terminal)
- -5 penalty for an invalid drop action
- Additional shaping reward may be applied for moves that reduce distance to the goal, improving training efficiency

### Objective
Learn a navigation and manipulation policy that completes the pick-up and delivery task efficiently while avoiding collisions.

---

## Algorithms Implemented

### SARSA (On-Policy TD Control)
- Tabular Q(s, a)
- Epsilon-greedy exploration with decay
- Tracks total reward per episode and epsilon schedule
- Includes greedy policy evaluation after training

### n-step Double Q-learning (n = 1 to 5)
- Two Q-tables (Q_A and Q_B)
- Uses n-step returns for bootstrapping
- Reduces maximization bias compared to single-table methods
- Evaluates performance across n = 1, 2, 3, 4, 5 with reward curves and greedy rollouts

---

## Evaluation Outputs Included

Depending on the notebook, results include:
- Initial vs trained Q-tables (or partial views)
- Reward per episode plots
- Epsilon decay plots
- Greedy policy evaluation across multiple episodes
- Comparative plots across different n-step settings
- Environment rendering and visualizations

---


