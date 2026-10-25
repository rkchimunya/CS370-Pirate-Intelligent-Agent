Project Summary
For this project, I developed a warehouse inventory application for Android devices. The application allows users to create an account, log in, view inventory records, add and remove items, and increase or decrease item quantities. It also provides optional SMS notifications when an item’s quantity reaches zero. The application addresses the need for a convenient and organized way to monitor warehouse inventory from a mobile device.
User-Centered Interface
The application includes a login screen, an inventory display, an add-item screen, and an SMS permission screen. The login screen supports both existing and first-time users. The inventory screen displays records in an organized grid and provides clear controls for adding, deleting, increasing, and decreasing inventory items.
I use consistent colors, readable typography, descriptive labels, logical navigation, and clearly placed buttons throughout the application. I also obscure passwords, validate user input, and display feedback when users enter invalid information. These design decisions make the application easier to understand and allow users to complete common tasks efficiently.
Development Approach
I divide the application into smaller components and develop each feature in logical stages. I organize the XML layouts and assign descriptive IDs before connecting them to the Java classes. I then implement user authentication, SQLite database operations, inventory controls, and SMS permission handling.
I use meaningful names, consistent formatting, small methods, and inline comments to keep the code readable and organized. Developing and testing one component at a time allows me to identify problems before integrating all the features. I can apply this structured approach to future projects because it makes larger applications easier to develop, test, and maintain.
Testing
I test the application in the Android Emulator by creating an account, logging in, adding inventory items, adjusting quantities, and deleting records. I restart the application to confirm that the SQLite database preserves user accounts and inventory information. I also test empty fields, incorrect login information, duplicate usernames, invalid quantities, and other unexpected inputs.
In addition, I test both approval and denial of SMS permission. The application continues to provide its main inventory features when a user denies permission, but it does not send notifications. Testing is essential because it confirms that the requirements function correctly and reveals problems with validation, stored information, navigation, and permission handling.
Innovation and Challenges
One challenge involves coordinating several activities with the SQLite database while keeping the inventory screen synchronized with stored information. I address this challenge by organizing database operations in a dedicated helper class and refreshing the inventory display after each change.
Another challenge involves implementing SMS notifications without making SMS permission necessary for the rest of the application. I design the application so users can decline this permission and continue managing their inventory. This approach respects the user’s decision while preserving the application’s primary functionality.
Area of Success
I am particularly successful in developing the database component of the application. The database stores account and inventory information and supports user authentication and complete inventory operations. Users can add and remove records, change item quantities, and access saved information after restarting the application. This component demonstrates my ability to connect a user-centered interface with persistent storage and functional Java code.
Reflection
This project strengthens my understanding of the complete mobile application development process, from initial planning and interface design to coding, testing, and launch preparation. I learn how important it is to evaluate an application from the user’s perspective while also maintaining organized and dependable code. The completed application demonstrates my experience with Android Studio, Java, XML layouts, SQLite databases, input validation, and Android permissions.

---

# CS 370 Pirate Intelligent Agent Portfolio

**Russell Chimunya**  
Southern New Hampshire University

## Project Overview

This project applies deep Q-learning to a pirate-themed pathfinding problem. The pirate must navigate an 8 × 8 maze, avoid blocked cells, and reach the treasure. A neural network estimates the future value of moving left, up, right, or down. The project demonstrates how reinforcement learning can turn feedback from an environment into a learned navigation policy.

The main portfolio artifact is [my Project Two Jupyter Notebook](CS370/Chimunya_Russell_ProjectTwo.ipynb). It includes the training code, explanatory comments, executed results, and evaluation checks.

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

