---
layout: retrospective
title:  Markov games that people play
date:   2019-09-02
original_paper: Markov games as a framework for multi-agent reinforcement learning
original_paper_link: https://students.cs.byu.edu/~cs670ta/Fall2009/MinimaxQLearning.pdf
original_paper_authors: Michael L. Littman
retrospective_author: Michael L. Littman
---

### Paper TL;DR

The paper introduced Markov games, a model from game theory, to the
AI/ML community as a way of thinking about multi-agent RL. It also
provided a concrete algorithm for solving such problems---minimax
Q-learning. It provided empirical results showing advantages of this
approach over standard Q-learning.

### Overall Outlook

I'm glad I wrote the paper. At the time, I was enthralled by the idea
of reinforcement learning and wanted to apply the ideas to a kind of
video game called "sumo" that my mentor David Ackley had
designed. Thinking about the game, it became clear to me that
Q-learning, which was still young, wouldn't be able to generate a good
strategy for the game---some random behavior is needed to fake out the
opponent. That insight led me to learning about game theory and
ultimately I saw that a natural extension of the Markov decision
process (MDP) model---so popular for understanding RL environments---could
capture this kind of problem quite well. The basic idea of the model
is simple to conceptualize if you are already familiar with MDPs. An
MDP consists of a set of states, a set of actions, a transition
function describing the impact of the selection of an action on the
current state, and a reward function associated with states and
actions that should be maximized. A Markov game adds a *second* set of
actions under the control of a second agent. One agent is selecting
actions to maximize reward and the other is selecting actions to
minimize it. Any MDP is just a Markov game where the minimizer has
only one choice in every state. Classic zero-sum matrix games are
Markov games where there is only one state. Any standard board-game
where the players take turns can be viewed as a Markov game, but the
model can also express games where the players must make their choices
simultaneously. The paper described these connections and also
provided a Q-learning-like algorithm for learning optimal decisions in
these games. I thought it was useful to broaden the standard MDP model
to allow for more decision makers.

Looking back, I'm heartened that other people found this idea useful
as well.

I learned a few things about the problem in the years that followed
publication:
* I couldn't prove that minimax-Q converged, although it sure seemed
like it should. Later, I connected with Csaba Szespvari, who helped me
articulate specific conditions for convergence, which minimax-Q
satisfied (whew!). Those conditions were helpful for proving
convergence of a bunch of other learning rules, so I'm glad we did
that.
* I later learned that the Markov games model was better known by a
different name---"stochastic games". I wish I had used that name. I
also found out that some convergence results were known about the
model (1953) from BEFORE MDPs were even invented (1957). Specifically,
the value-iteration algorithm for computing optimal policies for MDPs
was already proven to converge for the more general stochastic games
model. I was thinking that Markov games were a generalization of MDPs,
but, really, MDPs are a restriction of Markov/stochastic games!
* I was really interested in the general-sum version of the problem,
but couldn't figure out anything concrete in time for the paper. I
kind of brushed it off, saying "Only the specific case of two-player
zero-sum games is addressed...", thinking I'd have something more to
say by the next deadline. Turns out, the general sum case is really
really really subtle. I got to write several more papers about it and
there's still plenty more to say because it's not really clear that
the general sum setting can be meaningfully solved. So, that's been
good and bad.

### Opportunities for Improvement

I wish I had gotten more into general sum games in the paper. There
was a followup paper later that addressed general sum games in a way
that I think is unsatisfactory. That paper led to two other papers
pointing out its shortcomings, so I won't belabor the point here. But,
I might have been able to save a lot of people a lot of trouble if I
had clarified what was known about general sum games in this paper.

You know, or not. Maybe this explicit back and forth was needed to
explore the idea.

But, apart from the general sum games issue, I think one major
improvement over this paper was the work on "R-Max", which showed how
a polynomial bound on the number of suboptimal actions could be made
when learning in Markov games.  (Link:
http://www.jmlr.org/papers/v3/brafman02a.html .)  It's still useful to
have a model-free method like minimax-Q, but the guarantees for R-Max
are so much nicer. In particular, the R-Max algorithm is model
based---it uses its experience to build an approximate version of the
Markov game it is in. For states that have not been visited
sufficiently, it substitutes in an artificial large reward that is the
maximum possible reward. That's where the name "R-Max" comes
from. This choice means that learners are drawn to states they haven't
visited many times, leading to improvements to their model. These days,
people use R-Max as an approach for learning in MDPs. But, the paper
presents it in the context of zero-sum games and shows that it results in 
near optimal behavior in all but a polynomial number of steps.

The paper did get some criticism. In the experiments presented in the
paper, there was a separation between training and testing. That is,
after having a chance to learn, the agent's behavior was frozen, then
it had to face new learners. So, the goal was to learn a policy that
was robust---hard to exploit. Some later work asked, why not just
continue learning? In particular, a feature of minimax-Q is that it
learns a stochastic policy, but it's not clear a stochastic policy is
needed if the agent is allowed to continue to adapt. If it starts
choosing one action too often and that makes it exploitable, a
continually-adapting agent could then make the necessary adjustments.

I suppose that's ok and I agree that the artificial separation between
training and testing is awkward. But, I still think it's very
reasonable to want the learning algorithm to produce a high-quality
non-learning artifact. That's standard in supervised learning and
single agent RL. It's not obvious why multiagent RL should be
considered fundamentally different. One could argue that both
continual learning and train/test have their place.

It was also pointed out that the train/test setup I used has an
important flaw in that the behavior of the opponent during testing has
a big influence on what the agent is able to learn. If the opponent is
uncooperative (and why would an opponent in a zero-sum game be
cooperative?), minimax-Q might only experience a limited fraction of
the state space and therefore play extremely poorly in the testing
phase. The R-Max work provides an account for this issue by NOT
separating training and testing and instead measuring the number of
mistakes made lifelong. However, R-Max at least learns the target
stochastic policy, so it is arguably a better way of looking at things
than either train/test OR continual re-learning.

I haven't found it in print, but the dynamics of the soccer game also
got some criticism. Uther proposed playing on a hexagonal grid, and I
think he argued that this topology uses the field more
effectively---for the rectangular grid I proposed, play ends up being
restricted to just the middle of the field.

### New Perspectives

Looking back, the paper was very much a product of its time. The
reinforcement-learning community was still pretty young and Q-learning
was almost the only game in town. People were interested in using RL
to learn about games. In fact, Tesauro's TD-gammon work, which helped
launch the first big wave of interest in reinforcement learning and
temporal difference learning, was contemporary with this paper and
also focused on learning in a zero-sum game. Providing information
about how these two items---games and Q-learning---combine seemed like
a clarifying step.

But, it could also be seen as somewhat naive. The experiments were
small scale and there was no theoretical guarantees provided. Those
steps had to wait until later.
