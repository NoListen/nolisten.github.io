---
title: 'Tracking like a Game'
date: 2018-03-03
permalink: /posts/2018/03/rl-tracing-1/
excerpt: A new way to think about tracking.
tags:
  - reinforcement learning
  - tracking
---

I previously implemented one real time pedestrian tracking system with my colleagues which served as the basis of the MOT16 [winner](https://motchallenge.net/tracker/HT_SJTUZTE).
The tracking was realized by matching the object features extracted from CNN using ROI Pooling. It's good enough but has some disadvantages. One of them is that the features may change when the target objects change its shape.
For example, one pedestrian bend down or turn another direction. Another one can be that when two objects overlap, it's easy to mistake one for another one later.

In Atari Game, we try to obtain rewards by controlling the agents. Similarly, in tracking problems, we can also consider moving bounding boxes in one specific distance at one direction.
From this aspect, I implemented one tracking demo based on reinforce algorithm. The scenario is that one large bounding box which represents the receptive field aims at keeping the blue target rectangle around its center.
The information captured by local receptive field can help the agents to catch up with the target easily.
The code is available in my [DeepWhat](https://github.com/NoListen/DeepWhat/tree/master/rl_tracking) repository.

<div align="center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/pqewVnAjMMw" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen>
</iframe>
</div>

There are some more possible extensions.
For more complex fixed scenarios, we can try to make some simulations in the background environment to help the agents learn to distinguish those background features.
For multiple objects, Recurrent Neural Networks are necessary to keep the information of each moving object and can help to distinguish each object after they overlapped.
