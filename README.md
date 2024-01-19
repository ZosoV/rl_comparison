# RL Comparison

Over time, I intend to compare the functionality and implement well known RL algorithm. I'm going to focus on the model-free domain, but over time I would like to cover the whole following map.

![](./assets/rl_algorithms_9_15.svg)


**NOTE:** I intend to write only small implementations of the algorithms when possible and based on other sources on the Internet. I don't intend to do hard detailed implementations of the algorithms. This source is only for understanding.


| **Algorithm** | **Type** | **Description** | **Policy Formula** | **Algorithm Key Points** | **Other Formulas** |
|---------------|----------|-----------------|--------------------|--------------------------|--------------------|
| Q-Learning | Value-based | Model-free algorithm learning the value of an action in a state. | $\pi(s) = \arg\max_a Q(s, a)$ | Learns a Q-function for action-value estimation using the Bellman equation. Updates Q-values via: $Q(s, a) \leftarrow Q(s, a) + \alpha [R(s, a) + \gamma \max_{a'} Q(s', a') - Q(s, a)]$. | TD Error: $\delta = R(s, a) + \gamma \max_{a'} Q(s', a') - Q(s, a)$ |
| Deep Q-Learning (DQN) | Value-based | Extension of Q-learning using deep neural networks for Q-function. | Same as Q-Learning | Uses deep neural networks for Q-function approximation. Implements experience replay and fixed Q-targets. Loss Function: $L(\theta) = \mathbb{E} \left[ \left( R(s, a) + \gamma \max_{a'} Q(s', a'; \theta^-) - Q(s, a; \theta) \right)^2 \right]$. | Loss Function: $L(\theta)$ |
| REINFORCE | Policy-based | Monte Carlo policy gradient method using full episodes for policy update. | $\pi_\theta(a\|s)$ | Directly learns a stochastic policy using full episode returns. Policy update proportional to the gradient of log probability of the policy weighted by return. | Policy Gradient: $\nabla_\theta J(\theta) = \mathbb{E} \left[ \sum_t G_t \nabla_\theta \log \pi_\theta(A_t \| S_t) \right]$ |
| Advantage Actor-Critic (A2C) | Actor-Critic | Combines value and policy methods, with an actor for actions and a critic for evaluation. | Actor: $\pi(a\|s, \theta)$, Critic: $V(s, \phi)$ | Actor updates policy based on critic's advice. Critic evaluates action based on current policy. Uses advantage function to reduce update variance. | Advantage Function: $A(s, a) = Q(s, a) - V(s)$, Critic Update via TD Error |


## Paper Reviews

- [] Q-Learning: 
- [x] DQN: [Code](001_dqn.ipynb) | [Summary]() | [Playing Atari with Deep Reinforcement Learning](https://arxiv.org/abs/1312.5602) | There is another version in Nature.
- [x] REINFORCE: [Summary]() | [Intro to Policy Optimization](https://spinningup.openai.com/en/latest/spinningup/rl_intro3.html)
- [x] A2C / A3C: [Summary](002_A2C_A3C.md) | [Asynchronous Methods for Deep Reinforcement Learning](https://arxiv.org/abs/1602.01783)

## Extra Sources

- https://github.com/eemlcommunity/PracticalSessions2022/tree/main/rl
- https://www.youtube.com/live/-PxTOolYPzQ?si=X-8lBKmBUr3Kxma8&t=26323
- https://deeplearning.neuromatch.io/_images/lunar_lander.svg
- https://www.youtube.com/live/KUaoh2I5H88?si=-S-LcZvglrrPT6SC&t=25049
