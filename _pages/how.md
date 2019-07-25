---
layout: page
permalink: /how/
title: How it works
---

## Getting started

We’ve tried to make writing and submitting a retrospective as simple as possible. There are three steps:

**Step 1:**  *Pick a past paper of yours*, where you have something to say beyond what’s already in the paper. 

**Step 2:**  *Write your retrospective!* You can use our retrospectives template, or write it from scratch. If you’re not sure what to write, see our ‘What to write’ section below, or look at some examples of previous retrospectives. There is no minimum or maximum page limit for retrospectives --- you can write a short update in 20 minutes, or a long article with additional results, graphs, and new perspectives. 

**Step 3:**  *Submit your retrospective* by submitting a pull request to our GitHub repository here, using the pull request template. Once we confirm that the retrospective was written by an author of the original paper, it’ll be listed on the website! We strongly recommend that you update your paper on arXiv (if possible) to include a link to your retrospective as a footnote on the first page. 

Retrospectives are written in markdown, which is very simple to use and supports both images and code snippets. If you’re unfamiliar with markdown, see a quick cheat sheet [here](https://en.support.wordpress.com/markdown-quick-reference/) or a longer intro [here](https://www.markdownguide.org/getting-started/). If you’re not sure how to make a pull request, there are many tutorials online, for example [here](https://help.github.com/en/articles/creating-a-pull-request). 


## What to write

What are things you can write about in a retrospective? In short, you can write about anything that’s relevant to your original paper, but that is not actually contained in the paper. See some examples of previous retrospectives here. 

To give more concrete guidance, below we list three categories of topics that can be considered for writing a retrospective. A retrospective can talk about all or none of these things. Retrospectives can also be accompanied by updates to the original paper; we particularly recommend this if serious flaws were found in the paper. 

1. **Flaws or mistakes in the paper’s methodology.** 
For example, you discovered a bias in your dataset, or there was accidentally some overlap between validation and test, or there’s a weird bug that you don’t know the cause of and didn’t really figure out. Maybe you didn’t run enough seeds, and when you run more seeds your method isn’t actually that much better. *Basically, any way in which your scientific methodology was flawed or lacking.* 

2. **Limitations in the applicability of the work.**
For example, you have reason to believe your approach doesn’t generalize well to other datasets, or your results are not robust to small changes in the experimental set-up. Maybe you tried switching from MLPs to LSTMs and everything broke. Maybe your classification model works better, but is less robust to adversarial attacks. *Basically, any way in which your approach was limited that you didn’t realize or acknowledge at the time. *

3. **Changes in understanding or intuition.** 
For example, you have a simpler way to motivate your idea, or your intuition for why your model or approach works has changed. Maybe there are new aspects of your idea that you didn’t explore in the paper, but want to talk about, or new visualizations that improve understanding. These can be accompanied by additional (informal) results. You can also point to new work by others that is relevant to the paper. *Basically, anything that you’ve learned since writing the original paper that would be useful for others to know.*


## Reviewing process

We want to make retrospectives open to everyone, and to require minimal oversight. As such, retrospectives submitted to the GitHub repository will not be officially peer-reviewed. We will judge a retrospective on two factors:

1. The retrospective is written by an author of the original paper, and is relevant to the content of the original paper.
2. The retrospective complies with our code of conduct.

Note that the criteria for acceptance of the retrospective to the NeurIPS 2019 workshop may be more stringent. If there is sufficient interest, we will consider starting an alternate publication for high-quality retrospectives, which will be reviewed more thoroughly. 

