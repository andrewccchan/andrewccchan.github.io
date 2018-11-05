---
layout: post
title: Mathematics behind Reinforcement Learning
summary: Reinforcement learning (RL), though recently regarded as a branch a deep learing, has a long history of study and has a lot of math behind it. However, while learning RL, most people focus on applicaitons and neglect the theory. Unfortunately, to truly understand RL and apply it to a new problem, one must have a decent knowledge of the theory and the awareness of the assumptions behind RL. This article aims at demystifying some mathematics behind RL and pointnig out its key assumptions of the theory.
---

# Mathematics behind Reinforcement Learning

Reinforcement learning (RL), though recently regarded as a branch a deep learing, has a long history of study and has a lot of math behind it. However, while learning RL, most people focus on applicaitons and neglect the theory. Unfortunately, to truly understand RL and apply it to a new problem, one must have a decent knowledge of the theory and the awareness of the assumptions behind RL. This article aims at demystifying some mathematics behind RL and pointnig out its key assumptions of the theory.

## The Stochastic Process

### What is stochastic and what is not in RL?



## Reward Function

There are two types of reward functions in RL. The first one is $R_s$, which is the **expected** future return starting from state $s$, and the second is $R_s^a$, which is the **expected** future return starting from state $s$ and taking action $a$. Before discussing the relation between these two reward functions, we should first pay attention to the word "expected" in the definition of the both reward functions. This word means that the future return is represented by a random variable in a stocastic process — that is, there is a distribution of future return, instead of a scalar value. In other words, we start from the state state (and take the same action), but we may end up in having different return in different trials of an experiment.

Then let's turn to the definition of the two reward function and derive a formula relating these two functions:


$$
R_s = \mathbb{E}[R_{t+1} | S_t = s]
$$

$$
R_s^a = \mathbb{E}[R_{t+1} | S_t = s, A_t = a]
$$


An intuitive way to understand the relation between the two functions is that the former one is the average of the latter over all the action space. Indeed, as we will see in the following equation, this intuition is almost correct.  

<div align="center">
$$
\begin{align*}
R_s  &= \mathbb{E}[R_{t+1} | S_t = s] \\
	&= \sum_{r_{t+1}} r_{t+1} \cdot f[r_{t+1} | s] \\
	&= \sum_{r_{t+1}} r_{t+1} \sum_{a} f[r_{t+1}, a | s] \\
	&= \sum_{r_{t+1}} \sum_{a} r_{t+1} \frac{f[r_{t+1}, a, s]}{f[s]} \\
	&= \sum_{r_{t+1}} \sum_{a} r_{t+1} \frac{f[r_{t+1}, a, s]}{f[a|s]\cdot f[s]}f[a|s] \\
	&= \sum_{a} \sum_{r_{t+1}} r_{t+1} \frac{f[r_{t+1}, a, s]}{f[a,s]}f[a|s] \\
	&= \sum_{a} \sum_{r_{t+1}} r_{t+1} \cdot f[r_{t+1} | a, s] \cdot f[a|s] \\
	&= \sum_{a} R^a_s \cdot f[a|s] \\
\end{align*}
$$
</div>

Eq. (3) says that $R_s$ is equal to the weighted sum of $R_s^a$, and the weight equals to the probability of taking action $a$ given state $s$.

Furthermore, if the agent following the policy $\pi (a|s) = \mathbb{P}[A_t =a | S_t =s]  = f[a|s]$,  the expected return starting from state $s$ and following policy $\pi$ can expressed by the following equation
$$
R_s^{\pi} = \sum_{a} R^a_s \cdot \pi[a|s]
$$


## State-value Function

The state-value function $v_\pi (s)$ is the expected return starting from state $s$ and following policy $\pi$. It is defined as follows:
$$
v_\pi (s)  = \mathbb{E}_\pi [G_t | S_t=s]
$$
Note that the notation $\mathbb{E}_\pi$ does not mean the expectation over policy; it means the expectation over $G_t$ when following policy $\pi$.

We can expand Eq. (4) as follows:
$$
\begin{align*}
v_\pi (s) &=  \mathbb{E}_\pi [G_t | S_t=s]\\
	     &=  \mathbb{E}_\pi [R_{t+1} + \gamma R_{t+2} + ... | S_t=s] \\
	     &=  \mathbb{E}_\pi [R_{t+1} + \gamma G_{t+1} | S_t=s] \\
	     &= \mathbb{E}_\pi [R_{t+1} | S_t=s] + \gamma \mathbb{E}_\pi [G_{t+1} | S_t = s]
\end{align*}
$$


## Softmax Policy

I only show the math part for now

Definition:
$$
\pi_\theta (s,a) \propto e^{\phi(s,a)^t\theta}
$$
We first determine the proportional coefficient $k(\theta)$, which s a function of $\theta$:
$$
\pi_\theta(a|s) = k(\theta) e^{\phi(s,a)^t\theta}
$$
Since of summation of $\pi_\theta(a|s)​$ over $a​$ equals to $1​$, we have:
$$
\sum_a k(\theta) e^{\phi(s,a)^t\theta} = 1
$$
Or equivalently,
$$
\frac{1}{k(\theta)} = \sum_a e^{\phi(s,a)^t \theta}
$$
Then consider the score function
$$
\nabla_\theta \log\pi_\theta (s,a) = \frac{1}{k(\theta)}\frac{\partial k(\theta)}{\partial \theta} + \phi(s,a)
$$
Then we calculate the partial derivative of $k(\theta)$ with respect to $\theta$. By Eq. (8), we have:
$$
\begin{align*}
\frac{\partial k(\theta)}{\partial \theta} &= \frac{\partial }{\partial \theta}(\frac{1}{\sum_a e^{\phi(s,a)^t \theta}}) \\
&= \frac{-\sum_a e^{\phi (s,a)^t \theta}\cdot \phi(s,a)}{(\sum_a e^{\phi(s,a)^t \theta})^2} \\
\end{align*}
$$
Combining the above equation along  with Eq. (9) and Eq. (8), we have:
$$
\begin{align*}
\nabla_\theta \log\pi_\theta (s,a)  &= \phi(s,a) - \frac{\sum_a  e^{\phi(s,a)^t \theta}\phi(s,a)}{\sum_a  e^{\phi(s,a)^t \theta}} \\
&= \phi(s,a) - \sum_a  k(\theta)e^{\phi(s,a)^t \theta}\phi(s,a)\\
&= \phi(s,a) - \sum_a  \pi_\theta(a|s)\phi(s,a)\\
\end{align*}
$$
Notice that the $\sum_a  \pi_\theta(a|s)\phi(s,a)$ equals to $\mathbb{E}_{\pi_\theta}[\phi(s,\cdot)]$. Therefore, we have:
$$
\nabla_\theta \log\pi_\theta (s,a)  = \phi(s,a) - \mathbb{E}_{\pi_\theta}[\phi(s,\cdot)]
$$



## On-policy and Off-policy learning

The



Deterministic policy gradient: expected gradient of the action-value function.

## Optimization formula for actor-critic

When I first implemented the actor-critic algorithm, I tried to understand how the algorithm works by looking at how other people implemented the algorithm. However, I got confused about  the way most people implement the algorithm. I often found that what people implemented is different from the algorithm describes in the paper. Only later when I got more experiences with the mathematics behind actor-critic and started to implemented my variant of actor-critic, that I started to realized that is just a math trick!

Let's start with the RDPG algorithm and take a look at how the paper describes the algorithm. The critic is updated after each episode by the following formula:
$$
\Delta \omega = \frac{1}{NT} \sum_{i} \sum_{t} (y^i_t -Q^\omega(h^i_t, a^i_t))\frac{\partial Q(h^i_t, a^i_t)}{\partial \omega}
$$
The actor is then updated by the following formula:
$$
\Delta \omega = \frac{1}{NT}\sum_i \sum_t \frac{\partial Q^\omega(h^i_t, \mu^\theta(h^i_t))}{\partial a}\frac{\mu^\theta(h^i_t)}{\theta}
$$
Then, let's look at how people implement the algorithm:

```python
target_action, (target_hx, target_cx) = self.agent.actor_target(to_tensor(state1, volatile=True), (target_hx, target_cx))

next_q_value = self.agent.critic_target([
    to_tensor(state1, volatile=True),
    target_action
])
next_q_value.volatile=False

target_q = to_tensor(reward) + self.discount*next_q_value

# Critic update
current_q = self.agent.critic([ to_tensor(state0), to_tensor(action) ])

# value_loss = criterion(q_batch, target_q_batch)
value_loss = F.smooth_l1_loss(current_q, target_q)
value_loss /= len(experiences) # divide by trajectory length
value_loss_total += value_loss

# Actor update
action, (hx, cx) = self.agent.actor(to_tensor(state0), (hx, cx))
policy_loss = -self.agent.critic([
    to_tensor(state0),
    action
])
policy_loss /= len(experiences) # divide by trajectory length
policy_loss_total += policy_loss.mean()

# update per trajectory
self.agent.critic.zero_grad()
value_loss.backward()
self.critic_optim.step()

self.agent.actor.zero_grad()
policy_loss = policy_loss.mean()
policy_loss.backward()
self.actor_optim.step()
```

In this above implementation, the critic is updated by minimizing the TD error and the actor is updated by minimizing the negative the critic's evaluation of the current action. Though this implementation looks quite different from the theory, they are in fact the same!

First, what the program does is taking the partial derivation of the square of the TD error, or $\frac{\partial (y^i_t - Q^\omega(h^i_t,a^i_t))^2}{\partial \omega}$.

By simple calculus, we have:
$$
\frac{\partial (y^i_t - Q^\omega(h^i_t,a^i_t))^2}{\partial \omega} = -2(y^i_t - Q^\omega(h^i_t,a^i_t))\frac{\partial (y^i_t - Q^\omega(h^i_t,a^i_t))}{\partial \omega}
$$
Isn't the right hand side of the equation (almost) the same as the formula on the paper?

Then, consider the actor, what the program does is taking the derivative of the critic's output w.r.t to actor's parameter, or $\frac{\partial Q^\omega(h^i_t, \mu^\theta(h^i_t))}{\partial \theta}$

By chain rule, we have:
$$
\frac{\partial Q^\omega(h^i_t, \mu^\theta(h^i_t))}{\partial a} =\frac{\partial Q^\omega(h^i_t, \mu^\theta(h^i_t))}{\partial \mu^\theta(h^i_t))}\frac{\partial \mu^\theta(h^i_t))}{\partial \theta}
$$
Again, the right hand side of the equation is exactly the same as the formula on the paper. Therefore, this implementation is correct and much easier to implement.
