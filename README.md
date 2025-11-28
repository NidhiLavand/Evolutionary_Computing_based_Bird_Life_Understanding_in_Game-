# Evo Birds Life-Cycle Simulator

This repository contains the **Evo Birds Life-Cycle Simulator**, an exploratory **Reinforcement Learning (RL)** project designed to model the evolutionary and ecological dynamics of a bird population. The simulator tracks individual birds across a procedurally generated world through seasonal changes, resource constraints, and reproductive cycles.

The core goal is to use RL agents (birds) to learn survival and reproductive policies that maximize long-term viability against natural selection, seasonal hazards, and resource scarcity.

-----

## Key Features

  * **Eco-RL Sandbox:** A fully vectorized simulation environment built on NumPy, Pygame, and optionally PyTorch.
  * **Procedural World Generation:** Creates a $1024 \times 1024$ world featuring diverse habitats, synthetic elevation, and a carved river system using **Fractal Brownian Motion (FBM) noise**.
  * **Seasonal Ecology:** The simulation cycles through three seasons ("Summer," "Monsoon," "Winter"), which dynamically influence resource availability and movement costs.
  * **Vectorized Population:** Bird agents are represented by dense, state-array data structures for high-performance, vectorized updates of life stats, position, and traits.
  * **Evolutionary Traits:** Features species-specific **Traits** (mass, culmen, wing length) which are translated into foraging efficiencies, dispersal rates, and cold/heat tolerance. These traits can **mutate** across generations (Gaussian jitter).
  * **Pygame Renderer:** Provides real-time visualization with a Heads-Up Display (HUD) for tracking population metrics, reward history, and species survival.

-----

## Technical Architecture & Reinforcement Learning

### Core Technologies

The simulator is built to be flexible and efficient:

  * **Core Logic:** `numpy`
  * **Rendering:** `pygame`
  * **Parallelism:** Supports a **multiprocessing (`mp`)** backend for worker-based stepping.
  * **Deep Learning:** Optional **PyTorch** backend for accelerated computation (`torch`).

### RL Implementation

The agent logic implements classical model-free RL algorithms:

| Algorithm | CLI Flag | Mechanism |
| :--- | :--- | :--- |
| **Q-Learning** | `--algo q` (Default) | Utilizes a state-action value function for greedy policy updates. |
| **SARSA** | `--algo sarsa` | On-policy temporal difference control. |
| **Monte Carlo** | `--algo mc` | An experimental Monte Carlo control method. |

The simulation step uses **reward shaping** that factors in vital signs, nest building success, and survival against seasonal conditions to train the agents.

-----

## Simulation World & Ecology

### Geography and Habitats

The world is divided into $16 \times 16$ regions, each assigned a specific habitat type.

  * **Habitats:** Forest, Shrubland, Woodland, Grassland, Wetland, Marine, Coastal, Rock, Riverine, and Human Modified.
  * **Terrain Tiles:** T\_FLOOR, T\_WATER, T\_ROCK, T\_NEST, T\_DESERT, T\_TREE.

### Resources and Seasons

Resource availability changes based on both the habitat type and the current season.

  * **Resource Types:** Nectar, Insects, Seeds, and Vertebrate.
  * **Seasonal Cycles:** Each season (Summer, Monsoon, Winter) lasts for **250 steps**. The Monsoon season, for example, is configured to increase insect availability while introducing a **flood hazard**.

### Life Cycle Dynamics

The simulator tracks several biological states:

  * **Life Stats:** Energy, Health, Hydration, Satiety.
  * **Reproduction:** Birds must reach **Maturity Age** (350 steps) and successful mating leads to an **Incubation Period** (180 steps) before new offspring are spawned.
  * **Mortality:** Agents die when any vital stat (Energy, Health, or Hydration) reaches zero.

-----



### Running the Simulator

The project can be run directly as a script (`Evolution.ipynb`, implied by notebook analysis) or within a Jupyter/VS Code notebook environment.



**Notebook Execution:**

The notebook contains logic to safely parse command-line arguments even when run in a Jupyter or VS Code environment. The default configuration is Q-Learning (`--algo q`).
