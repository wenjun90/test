# Multi-Agent Assistant Dispatcher

This repository implements a multi-agent system to optimize the power grid dispatching operations. The system integrates several agents for topology management, reconnection, and optimization, leveraging reinforcement learning and optimization techniques.

## Table of Contents
- [Installation](#installation)
- [Repository Structure](#repository-structure)
- [Configuration](#configuration)
- [Usage](#usage)
- [Testing](#testing)
- [Evaluation](#evaluation)

## Installation

Follow these steps to set up the environment and install required dependencies:

1. Create the conda environment:

    ```bash
    conda env create -f environment.yml
    ```

2. Activate the environment:

    ```bash
    conda activate dispatching
    ```

3. Install the additional required package:

    ```bash
    pip install torch-scatter -f https://data.pyg.org/whl/torch-2.1.0+cu121.html
    ```

## Repository Structure

```plaintext
├── Agent
│   ├── AgentReconnection.py        # Agent that reconnects disrupted lines in case of an attack.
│   ├── AgentRecoverTopo.py         # Agent to recover the original topology when grid is safe.
│   ├── AgentImitationTopk.py       # Imitation model to predict top-k actions as input for AgentTopology.
│   ├── AgentTopology.py            # Agent to search topology actions using greedy or full simulation.
│   └── DispatcherAgent.py          # Dispatcher agent optimizing grid operations via DCOPF optimization.
├── Imitation_model                 # Directory containing the imitation learning models.
│   ├── model                       # Pre-trained model for predicting top-k actions.
│   ├── src                         # Script for training the imitation model.
│   └── config                      # Config for the imitation models.
├── Env_test_challenge_L2RPN_IDF_2023
│   └── (dataset files for testing and evaluation)
├── config.json                     # Configuration file for agent parameters.
├── run_agent.py                    # Main script to run the agents.
```

## Key Python Files

The repository contains the following key Python files, each serving a specific purpose in the multi-agent system:

| File Name                      | Description                                                                                     |
|---------------------------------|-------------------------------------------------------------------------------------------------|
| `AgentReconnection.py`          | Agent responsible for reconnecting disrupted lines in case of an attack.                        |
| `AgentRecoverTopo.py`           | Agent to recover the original topology when the grid is safe.                                   |
| `AgentImitationTopk.py`         | Imitation model to predict top-k actions as input for the AgentTopology.                        |
| `AgentTopology.py`              | Agent to search topology actions using either greedy or full simulation methods.                 |
| `DispatcherAgent.py`            | Dispatcher agent optimizing grid operations via DCOPF optimization.                             |
| `run_agent.py`                  | Main script to run the agents and simulate decision-making in the power grid.                   |
| `train.py`                      | Script for training the imitation learning model.                                               |
| `evaluation.py`                 | Script for evaluating the performance of the imitation learning model.                          |
| `test_eval.py`                  | Script for testing specific scenarios and evaluating performance on predefined datasets.        |


## Configuration

The agent configurations are stored in the `config.json` file. Below are the key parameters:

| Parameter                    | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| algo                          | Specifies the algorithm, options include greedy search or full simulation.   |
| dispatching                   | Determines if the dispatcher module should be used (true or false).          |
| search_method                 | Options: multi_agent_dependent, multi_agent_independent, or single_agent.    |
| imitation                     | Set to true to use the Imitation model for top-k action predictions.         |
| topk                          | The number of top-k actions predicted by the Imitation model (e.g., 15).     |
| multiple_parades              | The number of best choices (e.g., 5) after reranking top-k actions.          |
| min_rho                       | Specifies the threshold for actions that reduce rho below the default value. |
| penalty_curtailment_unsafe     | Penalty for unsafe curtailment actions.                                      |
| penalty_redispatching_unsafe   | Penalty for unsafe redispatching actions.                                    |
| penalty_storage_unsafe         | Penalty for unsafe storage usage.                                            |



## Usage

### Testing

To run the agent and simulate decision-making in the power grid, execute the `run_agent.py` script:

```bash
python run_agent.py
```


## Testing Scenarios

Test Scenarios: Test specific scenarios using the test_eval.py script for various situations:

```bash
python test_eval.py
```

## Evaluation score for agent

Evaluate the Model: Evaluate the model's performance and score on the provided dataset:

```bash
python eval_score.py
```


