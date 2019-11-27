---
layout: retrospective
title:  Learning the structure of deep sparse graphical modelss
date:   2019-11-27
original_paper: A Quick Template for Writing Retrospectives
original_paper_link: http://www.jmlr.org/proceedings/papers/v9/adams10a/adams10a.pdf
original_paper_authors: Ryan Adams, Hannah Wallach, and Zoubin Ghahramani
retrospective_author: Zoubin Ghahramani
---

### **Paper TL;DR**

This paper proposed a principled answer to how to set the structure of deep belief networks or deep networks in general. In particular, the idea was to bring together Bayesian nonparametrics and deep belief networks, and apply Bayes rule to learn both the structure and activation functions of a deep belief network (a probabilistic deep learning model). A prior was used over infinitely wide and infinitely deep networks (through extending the Indian buffet stochastic process), and a Markov chain Monte Carlo method was used to perform approximate inference. We had a working implementation of the method for unsupervised learning, and demonstrated it in action  on three image datasets. 

### **Overall Outlook**

### Science as a social endeavor

A lot of papers that I’m really proud of ended up not being very much cited. And a lot of other papers, ones that were good, but not necessarily my proudest work, ended up home runs in terms of citations. It doesn’t always make that much sense to me, although it reminds me of how science is a social endeavor. There’s often a bandwagon effect underlying which papers get cited and which ones don’t. Once somebody cites a paper in some context, other people start to do the same, even if actually there might have been a better paper to cite, or one with different authors, or one with slightly different terminology.

It's interesting, even technically, because as somebody who spent a lot of time studying Bayesian nonparametrics, this rich-get-richer phenomenon basically underlies one of the most important stochastic processes in the field, the Chinese restaurant process (which is related to the Dirichlet process). These are both no longer super-fashionable but at some point were the very cutting edge of machine learning. So it's funny to see the rich-get-richer effect play itself out in the way people cite machine learning papers.

### Learning the structure of deep sparse graphical models

And speaking of Bayesian nonparametrics, and papers that I’m really proud of, but didn’t have impact in line with my excitement about them, there’s the paper that’s the subject of this retrospective. It’s a fun, really ambitious paper, published in 2010. If you think about the history of deep learning, 2010 was fairly early in the new wave of deep learning. We called the paper "Learning the structure of deep sparse graphical models." In hindsight, maybe the title could have been more catchy, like learning the “structure of deep networks,” but we called it graphical models because it was technically more correct.

At the time, there was a huge amount of excitement around deep learning and in particular deep belief networks -- back then, deep belief networks were more exciting to people than vanilla neural networks with purely-deterministic units. One of the questions people had was, how do we set a structure of deep belief networks or deep networks in general?

What this paper did was to answer that question by bringing together two totally separate branches of machine learning. One was deep learning, and the other one was Bayesian nonparametrics. And this is where it’s going to get totally wacky and ambitious. I love this paper and almost all credit goes to the other two authors, who are Ryan Adams and Hannah Wallach.

### The starting point

The starting point is that we don't know what the structure of the deep network should be. Let's use Bayes rule to learn that structure. But instead of trying out different hypotheses for the width of each layer and the depth of the network, let's go wild and define a prior over infinitely wide and infinitely deep networks --  sounds wacky enough? But Bayesian nonparametrics allows you to do that.

Before you observe the data, your prior on this is that beyond your observed units, you have infinite layers of infinitely many hidden units. And remember, this is 2010, so it sounds totally wacky. Here is what you can do: While the number of hidden units and the depth of the network is infinite, under the prior, many of those hidden units will just not get connected to the data at all. This is where the word sparse comes in. The connectivity between the hidden and observed units will be sparse, so it's not a fully connected network. With infinitely many units that are fully connected, there would be infinitely many parameters, and all hell would break loose. So you impose a sparsity structure apriori that allows you to use as many hidden units and as deep a network as the data wants.

Once you start observing the data, if the data doesn't need to use 5,000 hidden units in the first layer, we can afford to use only one or two hundred, it will do that. So this is the difference between the prior and the posterior: The prior allows you as many hidden units in every layer and as many layers as you want. But under the posterior, given the amount of data that you have, it automatically figures out how many hidden units to have in each layer, and how deep the network should be. It's this elegant framework for doing architecture search in the beginning of the deep learning revolution, and we actually implemented this.

### How it worked in practice

The way we implemented this was built on an idea Tom Griffiths and I developed, called the [Indian buffet process](http://www.jmlr.org/papers/v12/griffiths11a.html), which basically is a prior on sparse, infinite graphs. That allows you to say that the connectivity between each pair of infinitely-many layers is sparse. So there’s a distribution over how these layers are connected -- that's the prior. And we used Markov chain Monte Carlo (MCMC) to actually sample over the architectures of the networks.

Basically, the MCMC algorithm would, given a data set, sample from the number of hidden units at each layer. And it would sample over the depth of the network. So as MCMC would run, it would try out deeper and less deep networks, and wider and less wide layers. But there’s even more. We didn't want to stop just at the connectivity architecture.

In deep belief networks there’s also the question of whether to use continuous hidden units or binary hidden units. We said, to hell with that question, let's just allow the network to decide smoothly between whether any given unit should be binary or continuous. The idea was to add Gaussian noise to a unit’s activation before passing it through a sigmoid. If you take a narrow Gaussian through the linear part of the sigmoid, you get a continuous unit. But If you make the Gaussian wider or the sigmoid sharper, the unit becomes binary. So we also automatically get every unit to decide whether it prefers to be binary or linear or something in between. Essentially we were doing architecture search, activation function search, in a fully Bayesian, full non-parametric way, on infinitely wide, infinitely deep networks using totally principled Bayesian methods. So it was a little bit ambitious.

But it worked! And we ended up getting a best paper award at AISTATS. It didn't work spectacularly well in the sense that it was pretty slow, so you can’t apply it to big data sets, and we applied it towards unsupervised learning. Interestingly, at the time, supervised learning was boring -- so we thought, why not do it for unsupervised learning?

I presented it at a very small deep learning meeting in London at around 2010 or so, at the Gatsby unit, and there was a pretty good collection of early deep learning researchers there. I had been asked to give a talk about deep learning, and my talk was about how to use Bayesian nonparametrics to fully learn the structure of deep networks. And I was excited giving the talk, thinking: This is totally awesome -- it's not super practical, but conceptually it's like amazingly beautiful and we got it to work.

### **What Happened After Publication**

So then what happened afterwards? Despite the best paper award and its ambition and the fact that it worked, it had much less impact than a lot of my other papers that were mostly less interesting than it. And it’s from 2010, and most of its impact has trailed off, so these days very few people know about this paper. So why -- what went wrong? 

I think what went wrong for this paper was that *the world became very practical.* This result was something very beautiful and principled and elegant -- of course, maybe it could have been improved on. But while having that beauty and those principles were nice, people began to focus on results. This was in 2010, when people were starting to make breakthroughs, although the really big breakthroughs hadn't happened yet. 

But people were starting to beat benchmarks using traditional neural networks trained with backpropagation. And this method, elegant as it was, wasn’t going to be beating  benchmarks. First, because it was unsupervised and there are still no really good unsupervised benchmarks -- it's hard to benchmark unsupervised methods. Second, because it was slow, it can’t easily be run on big data sets. The advantage that people were leaning on at that time was from running big datasets and big networks on GPUs. Maybe we should have implemented our method to run on GPUs, and it could have been more scalable.

As implemented, the method just wasn't practical, but that’s not inherently the case -- there still may be ways to make it more practical. Certainly the ideas there are worth aspiring to and understanding: It was a very beautiful marriage between Bayesian nonparametrics (hardcore statistics), and neural nets. But it wasn't practical, so it totally missed the wave that happened afterwards, and since then it's mostly been forgotten.

### **New Perspectives**

People talk about architecture search these days, and they come up with new algorithms for it. Sometimes I think, maybe we should go back nine years or so ago, and have a look at some of the ideas in that paper. Cut some corners, because maybe you don't need to implement a fully principled MCMC. Maybe you need some tricks for it to run on a GPU. And maybe it's worth revisiting those ideas in the context of supervised learning. This is where I think there is an interesting opportunity as well as -- I almost want to say, regret -- but no, I don't regret it. Yes, we tried something crazy and ambitious, but I'm just a little sad that there were many examples of other pieces of ambitious work where I feel like the community either reinvents ideas or invents work-arounds for problems that we should know how to solve. 

There's another thing I’ve learned, and this is where working in industry has been very helpful in the last few years, which is that the best ideas are the really simple ones. Simple ideas, people understand. And if you provide the code, they can even run it without understanding it. And if it's practical, scalable, simple, and you provide the code, then that goes incredibly far.

If it's beautiful, elegant, complex, and it requires you to deeply understand two different fields of machine learning, then it's not going to go very far. Basically, this is an example of one of those things where practicality trumps beauty. So I'm not expecting this to come back in force and take over the field of machine learning, but I look at this paper fondly, and I can talk about it in a retrospective way with some amount of sadness about the fact that it didn't go that far.

