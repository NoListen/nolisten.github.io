---
title: 'PPO in Particle Environment'
date: 2018-05-17
permalink: /posts/2018/05/ppo-particle/
excerpt: Personal understandings about RL's problems and PPO
tags:
  - reinforcement learning
  - ppo
---

As we know, the reinforcement learning(RL) suffers from large variance and doesn't have stable learning signals like supervised learning.
The learning process appears like a seasaw to me that may make old things worse when learn about new things. I previously wrote a [demo](https://github.com/NoListen/DeepWhat/tree/master/pi) to learn
to recite the infinite non-repeating decimals $\pi$ sequentially with hidden size 64 and can only recite only up to 1700 digits. The recurrent neural network(RNN) predicts 10 digits at one time and is trained with those 10 digits at each time step.
If the network predicts the results correctly then we move to the next 10 digits. Otherwise, the network has 90 percents chance to predict it again after trained with the labels and 10 percents to predict from the beginning again. In the test time, RNN recites $\pi$ from the beginning until it outputs the wrong results.
Though the training procedure applies supervised learning, it's also a Markov Decision Process and has something similar to RL.
If the network changes its parameters, then the memory passed by the RNN can also varies accordingly but the changes in memory are not considered in current time step and can influence RNN's predictions in test time.
Though this kind of problems can be alleviated by offline learning and large batch size training, how to balance the reinforcement learning data still remains as one problem.

PPO serves as the basic reinforcement learning algorithm of Open AI. I'd like to interpret PPO in an intuitive ways.
The PPO equation is $L^{CLIP}(\theta)min(r_t(\theta)\hat{A}_t, clip(r_t(\theta), 1-\epsilon, 1+\epsilon)\hat{A}_t)$. Further information about PPO please refer to the [paper](https://arxiv.org/pdf/1707.06347.pdf).
Assume $A_t$ is greater than zero, then if we don't clip the ratio $r_t(\theta)$, the