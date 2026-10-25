# CS 370 Pirate Intelligent Agent Portfolio

**Russell Chimunya**  
Southern New Hampshire University

## Project Overview

This project applies deep Q-learning to a pirate-themed pathfinding problem. The pirate must navigate an 8 × 8 maze, avoid blocked cells, and reach the treasure. A neural network estimates the future value of moving left, up, right, or down. The project demonstrates how reinforcement learning can turn feedback from an environment into a learned navigation policy.

The main portfolio artifact is [my Project Two Jupyter Notebook](Chimunya_Russell_ProjectTwo.ipynb). It includes the training code, explanatory comments, executed results, and evaluation checks.

## Provided Code and My Project Work

I was given the maze layout, the `TreasureMaze.py` environment, the `GameExperience.py` replay class, and a notebook containing model-building and game-testing functions. The environment handles movement, observations, rewards, and game status. The replay class stores transitions and prepares training targets. The supplied neural network uses two 64-unit dense layers with PReLU activations and four action-value outputs.

My project work focused on completing and refining the notebook's Q-training algorithm. This included resetting games at random free cells, selecting actions with an epsilon-greedy strategy, storing transitions, sampling replay batches, updating the network, and periodically synchronizing a target network. I also refined the training helper so each model uses its own optimizer, added bounded loops and explicit verification, and documented the logic with inline comments. I preserved both supplied Python helper files unchanged.

An important correction was passing Boolean terminal flags to the replay class. A nonempty status string such as `not_over` is true in a Python condition. Passing that string would incorrectly treat a continuing transition as terminal and omit its future-reward estimate. This showed me why understanding the interface between components matters as much as writing the training loop.

## What Computer Scientists Do and Why It Matters

Computer scientists turn problems into representations, algorithms, and systems whose behavior can be tested. Their work includes identifying requirements, selecting suitable data structures, evaluating computational costs, and explaining the limits of a solution. This matters because people and organizations rely on software to make decisions and carry out tasks consistently.

In this project, the maze became a numerical observation, movement became a discrete action space, and navigation quality became a reward signal. The project connected programming, probability, numerical optimization, and experimental evaluation. It also showed me that a sophisticated technique is not automatically the best practical choice: breadth-first search is simpler for a known, small, unweighted maze, while deep Q-learning demonstrates how an agent can learn decisions through interaction.

## How I Approach Problems as a Computer Scientist

I begin by defining the goal, constraints, inputs, and evidence that would count as success. I then break the problem into components and verify those components before interpreting the behavior of the whole system. For the pirate agent, this meant examining the environment and replay interfaces, implementing the training process, and evaluating the frozen greedy policy separately from exploratory training behavior.

The recorded seed-42 run first satisfied the full 32-game perfect training window and every-start completion check at zero-based epoch 274, after 275 games. The resulting policy reached the treasure from all 50 non-target free starting positions. I also reloaded the saved model in a separate process and confirmed the same 50 successful starts. However, the top-left route took 26 moves compared with a shortest-path distance of 24, and only 28 of the 50 routes matched shortest-path distances. Those measurements support successful navigation on this maze, not a claim that every route is optimal.

Instructor feedback helped me improve how I interpret experiments. When learning rate, discount factor, and other settings change together, I cannot attribute a reward change to learning rate alone. Short runs with high exploration also provide limited evidence about the learned greedy policy. For a controlled comparison, I would vary one setting at a time, keep the remaining settings and evaluation budget fixed, repeat matched seeds, and compare success rates, returns, and path lengths. I would document unexpected results rather than assume they support my original explanation.

## My Ethical Responsibilities to Users and the Organization

My responsibility to end users is to build systems that behave predictably within their stated limits and to communicate those limits honestly. A high training win rate alone is not enough to justify a claim of reliable performance. In this project, I distinguished training outcomes from evaluation, successful routes from shortest routes, and results on a fixed maze from generalization to a new environment. The implementation also does not simulate a human competitor, so I cannot claim that it proves the pirate will beat a person.

My responsibility to the organization includes maintainable code, reproducible evidence, accurate attribution, and clear reporting of defects. I should distinguish supplied code from my project contributions, preserve required interfaces, and avoid presenting unperformed experiments as results. I documented that the supplied environment's penalty behavior differs from the written specification and that its observation omits visit history even though rewards depend on revisits. Reporting those limitations helps future developers understand what must be reviewed before reusing the agent.

For systems involving real people, these responsibilities also include protecting personal information, checking whether outcomes disadvantage particular users, and matching testing and human oversight to the consequences of failure. A reward function represents what a developer chooses to optimize; it does not automatically capture fairness, safety, or the user's full goals. I need to question that objective as well as measure the model's performance.

## Repository Files

| File | Purpose |
| --- | --- |
| `Chimunya_Russell_ProjectTwo.ipynb` | Executed project notebook with training code and evaluation |
| `TreasureMaze.py` | Supplied environment, unchanged |
| `GameExperience.py` | Supplied replay helper, unchanged |
| `requirements.txt` | Dependency versions used for the recorded execution |

## Running the Notebook

The recorded execution used Python 3.13, TensorFlow 2.21.0, Keras 3.15.1, NumPy 2.5.4, and ml_dtypes 0.6.0 on macOS. These exact package versions may need adjustment on other platforms. Keep both helper modules beside the notebook, use a dedicated Python environment, and run the notebook cells in order. The saved notebook uses a generic Python kernel name so it is not tied to a kernel installed on my computer.

The notebook's seed helps reproducibility, but different library versions and hardware can change the stopping epoch. Package installation should be performed in the chosen environment before starting the notebook; the original starter's older dependency pins should not be installed into an incompatible modern environment.
