---
layout: retrospective
title:  Lessons Learned from The Lottery Ticket Hypothesis
date:   2019-11-27
original_paper: The Lottery Ticket Hypothesis: Finding Sparse, Trainable Neural Networks
original_paper_link: https://arxiv.org/abs/1803.03635
original_paper_authors: Jonathan Frankle, Michael Carbin
retrospective_author: Jonathan Frankle
---

### Introduction

I published a paper entitled [_The Lottery Ticket Hypothesis_](https://openreview.net/forum?id=rJl-b3RcF7) in ICLR this past spring. The paper, in brief, shows that small vision networks have subnetworks that can train from the start to full accuracy with many fewer parameters. It was my first machine learning publication, and I learned many lessons over the course of developing the project from idea to completed paper. In this retrospective, I record many of the lessons that I learned along the way in hopes they might prove useful to others.


As context, although I am new to machine learning, I am not new to computer science research. During other parts of my PhD and my time as an undergraduate, I aspired to research cryptography, computer security, technology policy, and programming language theory. I intend these lessons to reflect this broader perspective.

### Technical Lessons

I’ll begin with simple technical facts that I learned along the way. These lessons may seem basic, but that’s entirely the point. I came into this field as a novice, and I hope that other newcomers will feel solidarity in the steepness of the learning curve.

**Basic vision networks and datasets.** I performed the initial experiments for this project on a two-neuron network for XOR. (See Section 2 of the [original arxiv posting](https://arxiv.org/abs/1803.03635v1).) I knew about MNIST, and I made up a fully-connected network that seemed to work reasonably well. From that point forward, it is possible to read all of the Arxiv postings that followed as saying, "Jonathan learned about a new network or technique." I eventually learned about CIFAR-10 and convolutions, and I made up a few networks ([Arxiv v2](https://arxiv.org/abs/1803.03635v2)). Someone recommended I try Resnet-18, so I implemented Resnet-20 and inadvertently called it Resnet-18 ([Arxiv v3](https://arxiv.org/abs/1803.03635v3), although the mistake is still in the [published version](https://openreview.net/forum?id=rJl-b3RcF7)). When another paper used VGG-19, I scrambled to implement it and add it to the paper ([Arxiv v4](https://arxiv.org/abs/1803.03635v4)). By now, I've read enough papers to understand the canonical tasks, networks, and expected performance, but it took months as a working researcher to gather that knowledge.

**Good engineering pays off.** This point likely reflects the entirely empirical nature of my paper. I have never regretted taking extra time to ensure that my research codebases are carefully designed, well-maintained, and flexible enough to support adaptation for new uses. That upfront investment pays for itself many times over. The alternative involves wading through messy code to write new experiments and wondering whether your experiment failed for scientific reasons or due to bugs.

**Good experiment management pays off.** The same is true for experiment management. I've built experiment management into my research frameworks, meaning that I don't need to worry about keeping track of which data is stored where or which naming scheme I decided to use. My typical strategy is to write the hyperparameters for each experiment in a standardized way and store the experiment in a diretory whose name is the MD5-hash of those hyperparameters. That way, when I later need to retrieve those results, I describe the experiment I want by its hyperparameters and my framework finds the results automatically. This has saved me countless hours of manual experiment tracking and searching for data that must be _somewhere_.

**Infrastructure matters, to a point.** In the first version of the paper, I performed all experiments on my laptop. Afterwards, I gained access to a few old K80s that made it possible for me to collect data on small networks for CIFAR-10. This infrastructure was sufficient nearly all of the core experiments in the published version of the paper. This isn't to say the experience wasn't painful, and I spent months begging for infrastructure from any lab or company with whom I was in contact. (I gained access to industrial-scale infrastructure later on, which made it possible to fill the appendices with hyperparameter sweeps.) The lesson here is that you can get a large amount of mileage with small amounts of infrastructure, and that you don't need to work at a major tech company to do productive empirical research.

### Lessons about Research in Machine Learning

This was my first machine learning publication, and I have a number of reflections on the machine learning community as a newcomer.

**The community values empirical work on understanding deep learning.** I often receive advice that, if the paper doesn't show an obvious, practical win over previous work, it is unlikely to be published. Indeed, this work is often easier to publish, since it shows tangible progression on a well-established problem of some sort. It's the kind of work that seems to be most common at research conferences these days. However (and with the caveat that my experience may not be representative), my paper was entirely empirical and scientific with no direct applications. To the contrary, my methods are gratuitously inefficient. To that end, I take the interest that my paper received as evidence that members of the community do find this work valuable, even if it's sometimes harder to publish.

**Reviews and acceptances are a lottery.** The original version of my paper was submitted to NeurIPS 2018; it was rejected. I submitted a largely similar to ICLR 2019 (with a little more polish and a large number of hyperparameter sweeps), and it received a _best paper_ award. Variance is high, and reviews are almost always valuable feedback even if the paper isn't accepted.

**The community is skeptical and values rigor.** The key difference between the NeurIPS and ICLR versions? Thirty pages of hyperparameter sweeps showing that the effects I observed were not due to cherry-picked hyperparameters of some kind. NeurIPS reviewers expressed deep concern that I had hand-selected hyperparameters to make my experiments work. This was a particularly valid concern considering that I was mainly using networks that I had made up out of ignorance for standard benchmarks. In the ICLR version, I worked hard to demonstrate that this was _not_ the case, and I believe the reviewers rewarded the paper for doing so.

**We should question assumptions and received wisdom.** The basis of my paper was to question the received wisdom that the kind of overparameterization we see in practice is necessary for neural networks to learn. It stemmed from a naive question I asked myself after reading some papers on pruning. There are numerous opportunities in the field to similarly question received wisdom of all sorts. Moreover, these are exactly the sorts of questions someone new ot the field can ask after reading a few papers.

### Personal Lessons

The fifteen months from the original idea (in February of 2018) to its presentation at ICLR (in May of 2019) were stressful. At every moment during that time, I felt as if the future of the project was on the line, and hours spent away from lab were an opportunity wasted.

**The fast pace of research is a source of stress.** Paper cycles are short and the papers themselves are quite thin compared to other communities. The standard publishable unit is smaller in machine learning than in other venues where I've published (e.g., POPL or Usenix Security), creating time pressure to release small advances quickly rather than to see an idea through with the time and thought it deserves. The field is moving quickly, so there is pressure to release ideas as quickly as possible (see [Arxiv v1](https://arxiv.org/abs/1803.03635v1)). We tend to reward first-movers almost exclusively, despite the fact that many ideas have lengthy lineages and there are often near-simultaneous discoveries. All told, I felt a rush to get each new idea completed and posted as quickly as possible, which was a continuous source of pressure and stress for the entire length of the project.

**We have created winner-take-all environments.** For any number of reasons---be it celebrity, hype, or money---contemporary machine learning is filled with winner-take-all circumstances. Take ICLR as an example. Out of a few hundred accepted papers, only 24 were given oral presentations and two were selected for _best paper_ awards. Many of these papers probably deserved some degree of recognition, but the minuscule number of papers to receive such recognition creates a winner-take-all environment that makes competition unnecessarily intense. In other research communities I have published in, every paper receives an oral presentation and there is no _best paper_ award. If there are any awards at all, they are _test of time_ awards that recognize papers with a decade of perspective.

**Attention is a double-edged sword.** From the first Arxiv release onward, the paper received attention from the broader community. It appeared on Reddit/Hackernews, it was featured in blog posts, and I received many emails from interested researchers. This attention is certainly good for my scientific career and for the long-term success of the paper---I've received offers to give talks, and senior reseachers have been interested in speaking to me. However, it created an enormous amount of pre-publication pressure. Personally, attention/celebrity are not my motivations for pursuing research in machine learning, and it was a challenge to manage the pressure that accompanied these aspects.

