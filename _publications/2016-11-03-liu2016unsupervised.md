---
title: "Unsupervised deep domain adaptation for pedestrian detection"
collection: publications
permalink: /publication/2016-11-03-liu2016unsupervised
excerpt: 'Lihang Liu, Weiyao Lin, **Lisheng Wu**, Yong Yu, Michael Ying Yang. Accepted by ECCV Workshop 2016.'
date: 2016-11-03
venue: 'ECCV'
paperurl: 'https://arxiv.org/pdf/1802.03269.pdf'
---

[Arxiv](https://arxiv.org/pdf/1802.03269.pdf)

# Abstract

This paper addresses the problem of unsupervised domain
adaptation on the task of pedestrian detection in crowded scenes. First,
we utilize an iterative algorithm to iteratively select and auto-annotate
positive pedestrian samples with high confidence as the training samples
for the target domain. Meanwhile, we also reuse negative samples from
the source domain to compensate for the imbalance between the amount
of positive samples and negative samples. Second, based on the deep
network we also design an unsupervised regularizer to mitigate influence
from data noise. More specifically, we transform the last fully connected
layer into two sub-layers — an element-wise multiply layer and a
sum layer, and add the unsupervised regularizer to further improve the
domain adaptation accuracy. In experiments for pedestrian detection,
the proposed method boosts the recall value by nearly 30% while the
precision stays almost the same. Furthermore, we perform our method
on standard domain adaptation benchmarks on both supervised and
unsupervised settings and also achieve state-of-the-art results.
