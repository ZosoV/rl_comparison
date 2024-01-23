# Minimal RL: Fundamental Reinforcement Learning Algorithms Comparison

**State:** In Progress

Over time, I intend to compare the functionality and implement well known RL algorithm. I'm going to focus on the model-free domain, but over time I would like to cover the whole following map.

![](./assets/rl_algorithms_9_15.svg)


**NOTE:** I intend to write only small implementations of the algorithms when possible and based on other sources on the Internet. I don't intend to do hard detailed implementations of the algorithms. This source is only for understanding.


| **Algorithm** | **Type** | **Policy Formula** | **Algorithm Key Points** | **Other Formulas** |
|---------------|----------|-----------------------------|---------------------------------------------------|--------------------|
| Q-Learning | Value-based | $\pi(s) = \arg\max_a Q(s, a)$ | Learns a Q-function for action-value estimation using the Bellman equation. <br> Updates Q-values via: <br> $Q(s, a) \leftarrow Q(s, a) + \alpha [R(s, a) + \gamma \max_{a'} Q(s', a') - Q(s, a)]$. | TD Error: $\delta = R(s, a) + \gamma \max_{a'} Q(s', a') - Q(s, a)$ |
| Deep Q-Learning (DQN) | Value-based | $\pi(s) = \arg\max_a Q_\theta(s, a)$ | Extension of Q-learning using deep neural networks for Q-function approximation. <br> Implements experience replay and fixed Q-targets. <br> Loss Function: <br> $L(\theta) = \mathbb{E} \left[ \left( R(s, a) + \gamma \max_{a'} Q(s', a'; \theta^-) - Q(s, a; \theta) \right)^2 \right]$ <br> $\theta = \arg\max_\theta L(\theta)$ | Loss Function: $L(\theta)$ |
| REINFORCE | Policy-based | $\pi_\theta(a\|s)$ | Directly learns a stochastic policy using **full episode returns**. <br> Policy update proportional to the gradient of log probability of the policy weighted by return. <br> Policy Gradient: <br> $J\left(\pi_\theta\right)=\underset{\tau \sim \pi_\theta}{\mathrm{E}}[R(\tau)]$ <br> $\nabla_\theta J\left(\pi_\theta\right)=\underset{\tau \sim \pi_\theta}{\mathrm{E}}\left[\sum\limits_{t=0}^T \Phi_t \nabla_\theta \log \pi_\theta\left(a_t \mid s_t\right) \right]$ <br> $\theta=\arg \underset{\theta}{\min} \quad J\left(\pi_\theta\right)$ | The weight $\Phi_t$ can be: <br> $\Phi_t = R(\tau)$ <br> $\Phi_t=\sum\limits_{t^{\prime}=t}^T R\left(s_{t^{\prime}}, a_{t^{\prime}}, s_{t^{\prime}+1}\right)$ <br> $\Phi_t=\sum\limits_{t^{\prime}=t}^T R\left(s_{t^{\prime}}, a_{t^{\prime}}, s_{t^{\prime}+1}\right)-b\left(s_t\right)$ <br> others: <br> $\Phi_t = Q^{\pi_\phi}(s_t,a_t)$ <br> $\Phi_t = A^{\pi_\phi}(s_t,a_t)$ |
| Advantage Actor-Critic (A2C) | Actor-Critic | Actor: $\pi_\theta(a\|s)$ <br> Critic: $V_\phi(s)$ | Combines value and policy methods, with an actor for actions and a critic for evaluation. <br> Actor updates policy based on critic's advice. <br> Critic evaluates action based on current policy. <br> Uses advantage function to reduce update variance. <br> $\nabla_\theta J\left(\pi_\theta\right)=\underset{\tau \sim \pi_\theta}{\mathrm{E}}\left[\sum\limits_{t=0}^T \Phi_t \nabla_\theta \log \pi_\theta\left(a_t \mid s_t\right) \right]$ <br> $\theta=\arg \underset{\theta}{\min} \quad J\left(\pi_\theta\right)$ <br> <img src="assets/critic_eq.png" alt="critic_q" width="285"/> | $\Phi_t=\sum\limits_{t^{\prime}=t}^T R\left(s_{t^{\prime}}, a_{t^{\prime}}, s_{t^{\prime}+1}\right)-V_\phi\left(s_t\right)$ <br> can be seen as an estimate of the Advantage Function: <br> $A(s, a) = Q(s, a) - V(s)$ |

**NOTE:** $\hat{R}_t$ can be modeled with the infinite discounted return or finite undiscounted return.

## TODOS
- [ ] Complete note 001_DQN
- [ ] Write a short summary of 003 REINFORCE
- [ ] Code A2C
- [ ] Code REINFORCE
- [ ] Review TRPO

## Paper Reviews

- [ ] Q-Learning: 
- [x] DQN: [Code](001_dqn.ipynb) | [Summary](notes/001_DQN.md) | [Playing Atari with Deep Reinforcement Learning](https://arxiv.org/abs/1312.5602) | There is another version in Nature.
- [x] REINFORCE: [Intro to Policy Optimization](https://spinningup.openai.com/en/latest/spinningup/rl_intro3.html) | [Benchmarking Deep Reinforcement Learning for Continuous Control](https://arxiv.org/abs/1604.06778)
- [x] A2C / A3C: [Summary](notes/002_A2C_A3C.md) | [Asynchronous Methods for Deep Reinforcement Learning](https://arxiv.org/abs/1602.01783)

## Extra Sources

- https://github.com/eemlcommunity/PracticalSessions2022/tree/main/rl
- https://www.youtube.com/live/-PxTOolYPzQ?si=X-8lBKmBUr3Kxma8&t=26323
- https://deeplearning.neuromatch.io/_images/lunar_lander.svg
- https://www.youtube.com/live/KUaoh2I5H88?si=-S-LcZvglrrPT6SC&t=25049
