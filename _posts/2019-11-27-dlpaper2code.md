---
layout: retrospective
title:  DLPaper2Code: Auto-Generation of Code from Deep Learning Research Papers
date:   2019-11-27
original_paper: DLPaper2Code: Auto-Generation of Code from Deep Learning Research Papers
original_paper_link: https://www.aaai.org/ocs/index.php/AAAI/AAAI18/paper/download/17100/16330
original_paper_authors: Akshay Sethi, Anush Sankaran, Naveen Panwar, Shreya Khare, Senthil Mani
retrospective_author: Anush Sankaran
---

### Paper TL;DR 

Given the PDF research paper of a deep learning model as input, we aim to automatically parse the figures and text in the research paper, and generate a production ready implementation of the deep learning in Keras, Tensorflow, PyTorch, or Caffe.

### Overall Outlook

This paper addresses an important issue faced by most of the researchers and software developers. The number of papers in deep learning were growing tremendously fast and it was difficult to keep track of the literature growth, even in selective niche topics. We started with an ambitious idea completely automating this task by implementing research papers from the PDF paper. The paper gained lots of media attention and people talking about it:
* François Chollet's Tweet and the discussion: https://twitter.com/fchollet/status/930492131780714496?lang=en
* Blog: https://medium.com/breathe-publication/capsule-networks-and-dlpaper2code-ec3af0ec185b
* Influencing other papers: "Deep learning-assisted literature mining for in vitro radiosensitivity data"

### Opportunities for Improvement

However, thinking in retrospective, we did not reach the ambitious end goal that we started off with. I discuss some of the aspects where we missed out:

1. **Are our Experiments Sufficient to Withhold our Claims?**
We had two basic modules: (i) Given a figure, classify whether it explains a DL model architecture or not, (ii) If it is a DL model architecture, then extract content and flow from it. Due to lack of any golden dataset, it is very difficult to evaluate our methodology. Hence, we created a simulated dataset of CAFFE and Keras model visualizations with ground truth code. However, the visual variations in these figures are very limited and our method was highly fine-tuned to these kind of figures, achieving 98%+ accuracy in classification and content extraction. However, when we hand picked a few actual research papers, the content extraction performed poorly, giving as low as 18% accuracy in a small hand-annotated set of 10 papers. The primary reason was the visual diversity of the images available in research papers. Though, we highlighted this in the discussion section of our original paper, in retrospective, our actual aim was to improve that 18% to a higher number, which this paper did not achieve!

2. **Is our Solution Practically Usable?**
What could we have done, if we actually had a perfect DLpaper2Code? Download all the arXiv and other published papers in deep learning domain, and create a catalog of research papers along with their implementation ready code. Practically, make the code of every research paper publicly available. Though, we aimed at achieving it and started building such a catalog system, we were not able to achieve the kind of accuracy in building the model catalog. Although our research paper created a buzz and showed promise, the practical applicability and usability of the methodology was very less that we would have ideally wanted it to be!

3. **Could we have made the Dataset and Code available from Community's Benefit?** 
We came up with a novel grammar and definition of simulating and generating any kind of a valid deep learning model. We generated more than 2,00,000 deep learning models, along with their visualizations, and code in Keras and Caffe. Also, we downloaded more than 10k arXiv research papers in DL and manually annotated more than 27,000 figures from research papers, as DL model figures or not. We additionally demonstrated the capabilities of our systems as a [Demo Paper](https://aaai.org/ocs/index.php/AAAI/AAAI18/paper/view/16795) in AAAI 2018. However, because of internal compliance policies and data/code sharing constraints in industry, we could not share the data nor the code of this paper to the community. In retrospective, I still strongly believe that sharing both the code and the data, would have ave really positively impacted the community and also the community could have pushed the limits of this challenging problem to better solutions. It feels like that all the hard work and manual labour of the research went unnoticed and unused because of the copyright and compliance policies.

#### An Improved Method, Maybe?

We consumed a deep learning model's research paper as output, and generated code in different deep learning libraries such as Keras, Tensorflow, Caffe, and PyTorch. However, the methodology that we proposed was not deep learning based. It was an OpenCV based shape detection using morphological operations and basic OCR. In retrospective, could we have made a generalizable solution using some state-of-art deep learning algorithms. Over the last year, after the original paper got published, I have come across some DL based approaches, that I could have used to maybe better solve my content extraction problem:

* Deep Segmentation of Shapes: `Tags2Parts: Discovering semantic regions from shape tags`
* Semantic flow segmentation using Shapes: `BAE-NET: Branched Autoencoder for Shape Co-Segmentation`

PS: However, on a different note, we are happy that we adopted a non-DL approach to solve the problem and saved some carbon footprint in this world, by saving extensive computational and hyperparameter search time!

### Wait! What's the actual problem that we wanted to solve?
In retrospective, the biggest realization I had, is when I realized what is the actual problem we are trying to solve. The aim is to extract content from research papers and the challenge is that the research papers are written crazily with so much complexity and diversity, that trying to extract specific information from text/figures is practically next to impossible!

Thus, instead of trying to better our algorithms to this hard task, why not bring in some standardization in writing research papers? Design and define a standard for drawing figures in research papers and insist that research should express model architectures only using this definition, else the papers will not get accepted. If we can enforce a (latex) styling condition and page limit on submitted papers, we could as well enforce a figure representation constraint. 

In this regard, I recently came across this paper: [The Diagrammatic AI Language (DIAL): Version 0.1](https://arxiv.org/abs/1812.11142).

They actually enforce a defintion on how a deep learning model architecture could be visually shown in a research paper. This ensures that there is very little diversity in research papers, and our methodology could be focussed towards this visual variation alone!

With this solution, we could achieved better accuracies and in turn, more practical applicability. In retrospective, I would have ideally wanted to solve our actual problem using this DIAL kind of a definition. My special kudos the authors of the DIAL paper! 

