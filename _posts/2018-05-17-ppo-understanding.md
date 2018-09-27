---
title: 'PPO in Particle Environment'
date: 2018-05-17
permalink: /posts/2018/05/ppo-particle/
tags:
  - reinforcement learning
  - ppo
---

As we know, the reinforcement learning suffers from large variance and doesn't have stable learning signals like supervised learning.

PPO serves as the basic reinforcement learning algorithm of Open AI. I'd like to interpret PPO in an intuitive ways.
The PPO equation is $min(r_t(\theta)\hat{A}_t, clip(r_t(\theta), 1-\epsilon, 1+\epsilon)\hat{A}_t)$.