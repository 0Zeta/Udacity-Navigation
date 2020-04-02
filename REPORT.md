# Report

## Implementation
The environment was solved using a deep reinforcement learning agent. The implementation can be found in the `navigation`-directory.
`agent.py` contains the rl-agent and `model.py` contains the neural network used as an estimator.

### Learning algorithm
Double DQN was used as the learning algorithm for the agent.
Each training episode the experience (state, action, reward, next state) the agent gained following an epsilon-greedy policy was stored.
Then every four training steps the agent learned from a random sample from the stored experience. It learned by approximating the optimal
q-value function (mapping a state to the expected returns of each possible action). The [Double DQN](https://arxiv.org/abs/1509.06461)
algorithm was used instead of the normal DQN approach to improve the results of the agent. Therefore the estimate of the action expected to be optimal
for the next state that is used in the Q-learning formula is made by a fixed target network while the action itself is chosen
by the local network.

### hyperparameters
The following hyperparameters were used:
* replay buffer size: 1e6
* minibatch size: 128
* discount factor: 0.99
* tau (soft update for target network factor): 1e-3
* learning rate: 4e-4
* update interval (how often to learn): 4
* epsilon start (probability to choose a random action): 1.0
* min epsilon: 0.01
* epsilon decay factor: 0.995

### Neural network
The model used as the q-value function estimator is a simple feedforward fully-connected neural network with 4 layers with
37, 196, 128 and 64 neurons.

## Results
The agent was able to solve the environment after 440 episodes achieving an average score of 13.08 over the last 100 episodes
of the training.
![score per episode](https://user-images.githubusercontent.com/9535190/78250207-cfc4ac00-74ef-11ea-9a9e-40d93d9e1953.png)

## possible future improvements
The algorithm could be improved in many ways. For example one could implement some DQN improvements, for example Prioritized Experience Replays
which would improve the learning effect gained from the saved experience. Also a variant where only the screen pixels of the
simulation are used as the input for the algorithm could be tried out using convolutional neural networks. One would have to
use multiple frames as the input though as the agent has no way to determine the current velocity with only one frame. 