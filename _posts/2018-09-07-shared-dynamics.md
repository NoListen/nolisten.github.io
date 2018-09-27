---
title: 'Learn Shared Dynamics with Meta-World Models(1)'
date: 2018-09-07
permalink: /posts/2018/09/meta-world/
excerpt: Learn to unify multiple worlds' dynamics together.
tags:
  - model based
  - shared dynamics
  - consciousness
---

We often consider the features from the appearance. Sometimes, we also try to learn the features correlated to the context, like word embeddings.
 Words with similar properties can share some similarities in the word embedding space. Now, consider reinforcement learning(RL) environment states
 from this aspects. If two world environments hold different state space $\mathcal{S}_1$ and $\mathcal{S}_2$, but with the same action space $\mathcal{A}$ but
 the inner relationships between the states in each world are the same. We call the two worlds have the same dynamics.

 For example, you and 'you' in the mirror have the same dynamics but the observations are reverse horizontally.
  However, when you consider the 'you' in the mirror is yourself, you started to consider unify the representations of you and 'you' in the mirror in your mind.
  The example may aslo be one illustration of the mirror test which shows the existence of self-consciousness.

To explore the same process using machine learning, we proposed to use the shared dynamics to learn a meta-world model.
The meta-world model is based on the [world model](https://arxiv.org/pdf/1803.10122.pdf) architectures.
The world model consists of Vision(V) model and Memory(M) model. The V model is VAE and the M model is LSTM in our architecture.
Meta-World's aim is to learn the shared dynamics among multiple worlds so that one M model is shared across different world environments while each world keeps one individual V model.
 The training loss comes from the reconstruction loss of VAE and the prediction loss of LSTM.
In correspondence, the training procedure is divided into reconstruction phase R and prediction phase P.
In the R phase, we train VAE using reconstruction loss. In the P phase, we train both VAE and LSTM using prediction loss.
The reason why we don't train the models jointly because the conflicts between the two kind of losses can lead the meta-world model to a local minimum.
Moreover, the two training phases can be understood as that P phase destroys the reconstruction ability of V models to be compatible with the shared dynamics and the R phase make the V models recover
its reconstruction ability until they reach the balance.

Our experiments are carried on the variants of Atari Pong environment. Pong environment is preprocessed into binary images at first.
Then we have five kinds of variants of it which is shown in `Fig.1`. $\Gamma_o$ is the original world and five variants are $\Gamma_t$, $\Gamma_h$, $\Gamma_v$, $\Gamma_c$, $\Gamma_m$.
$\Gamma_t$ is the transpose of the original world; $\Gamma_v$ divided $\Gamma_o$ into two parts vertically and swap them and $\Gamma_h$ is obtained similarly but horizontally; $\Gamma_c$ changes the color of $\Gamma_o$;
$\Gamma_m$ is $\Gamma_o$'s mirror world. All those worlds have different state space, but with the same action space and the physical meanings of actions are the same.
<p align="center">
  <img src="{{ base_path }}/images/all_variants.png"/>
  <figcaption align="center">Fig.1 - five world variants</figcaption>
</p>

The problems appears that how can we know we have learned the shared dynamics because the network capacity allows it to learn multiple dynamics simultaneously.
We validate it indirectly by observing whether the representations of corresponding states from different worlds are unified. If corresponding states' representations are close to each other, then the transition from one state to another which is the dynamic can be considered as the same.
For the variational inference in VAE, we choose not to compare the latent vector $z$ of VAE directly. We can decode the $z$ encoded by one world's V model using another world's V model and see whether the output is the corresponding state.
If it is, then we consider we learn the shared dynamics and it also lead to the fact that the shared dynamics can unify the representations.

In our most experiments, we choose $\Gamma_o$ and one world from {$\Gamma_t$, $\Gamma_h$, $\Gamma_v$, $\Gamma_c$, $\Gamma_m$} to train the meta-world. The validation results are listed below.
Currently, the success probability is not 100% and varies from world to world. {$\Gamma_t$, $\Gamma_c$, $\Gamma_m$, $\Gamma_h$} are much easier to train the meta-world with while $\Gamma_v$ is difficult to train the meta-world with.
The reason can be that in the $\Gamma_v$ may represent the paddle in two halves and the paddle can teleport to the other end, which can be considered to have different dynamics.
<p align="center">
  <img src="{{ base_path }}/images/all_worlds.png"/>
  <figcaption align="center">Fig.2 - five world validation</figcaption>
</p>

In summary, what we only do is let the agent try to find one shared dynamics to associate itself and 'itself' in another world, then it's able to pass the mirror test.
We also try to train multiple worlds together and improve the success probability of training multiple worlds. As a result, we also find something interesting which may be updated later or delivered in a new post.