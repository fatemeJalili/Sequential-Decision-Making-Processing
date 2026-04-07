# Sequential-Decision-Making-Processing
This repository contains the code and documentation for the Sequential Decision Making Processing course projects, including MDP-based optimization and reinforcement learning assignments. 


## Part 1 — Minimizing Age of Information (Optimal Cache Updating Policy)
**Language: MATLAB**

#### Problem Formulation
- Modeled a cache system with **N = 10 files**, each with a state defined by its **Age of Information (AoI)** X and a **freshness indicator** F (2-state Markov channel).
- Defined binary per-file actions: **update (a = 1)** or **no update (a = 0)**.
- Objective: minimize the **infinite-horizon average weighted AoI** subject to a constraint on the average number of updates M = 3, with file popularities following a **Zipf distribution**.

#### Lagrangian Decomposition & Linear Programming
- Applied **Lagrangian relaxation** to decouple the constrained MDP into N independent **per-file problems**.
- Solved each per-file problem as a **Linear Program (LP)** over state-action frequencies v(f, x, a).
- Computed the **dual function g(λ) = Σ J_n(λ) − λM** and maximized it over λ to recover the globally optimal policy.

  <img src="https://github.com/user-attachments/assets/389d8a88-1c21-41d2-aa46-92184ee1b20b" height="300">
  
#### Per-file Lagrangian Costs J_n(λ)

  <div style="display: flex; justify-content: space-between;">

    <img src="https://github.com/user-attachments/assets/015c6f21-f0ad-4eee-8aca-6e3eb242bd2b" height="220">
    <img src="https://github.com/user-attachments/assets/afe338a7-8efd-45c2-989c-821cb2b95fd6" height="220">
  </div>

#### Threshold Policy & Analysis
- Proved that the optimal stationary policy has a **threshold structure**: update file n if and only if its AoI exceeds a state-dependent threshold τ_r.
- **Popular files** (small n, Zipf rank): small thresholds → updated frequently, low AoI.
- **Unpopular files** (large n): large thresholds → AoI allowed to grow significantly before an update is triggered.
- For **q = 0.2** (correlated channel): different thresholds per channel state r, λ* = 0.60.
- For **q = 0.5** (memoryless channel): identical thresholds across channel states, λ* = 1.00.



## Part 2 — Reinforcement Learning for NOMA Resource Scheduling
**Language: Python (PyTorch)**

#### System Model
- Modeled a **2-user NOMA (Non-Orthogonal Multiple Access)** wireless resource scheduling problem.
- Each user's state is a tuple of: **data buffer occupancy**, **SNR/channel level**, and **battery level**.
- Joint action space: per-user decisions to **communicate** or remain **idle**.
- Reward is based on packet delivery throughput, penalized for **infeasible actions** (insufficient buffer, battery, or SNR).

  <img src="IMAGE_LINK_system_model" height="250">

#### Value Iteration & Policy Iteration
- Implemented classical **Dynamic Programming** methods requiring full knowledge of the transition and reward models.
- Both algorithms converge to the optimal value function and deterministic policy via the **Bellman optimality equation**.

  <div style="display: flex; justify-content: space-between;">
    <img src="IMAGE_LINK_conv_value_iteration" height="220">
    <img src="IMAGE_LINK_conv_policy_iteration" height="220">
  </div>

#### Q-Learning
- Implemented **model-free tabular Q-Learning** with **ε-greedy exploration** and optimistic initialization.
- Tracks percentage of unvisited state-action pairs to monitor exploration coverage.

  <img src="IMAGE_LINK_conv_q_learning" height="260">

#### Deep Q-Learning (DQN)
- Implemented a **Deep Q-Network** with fully-connected layers and ReLU activations (PyTorch).
- Uses an **experience replay buffer** and a separate **target network** updated periodically to stabilize training.
- Supports both **MSE** and **Huber** loss functions; ε decays over episodes.

  <img src="IMAGE_LINK_conv_deep_q_learning" height="260">
python main.py D
```

