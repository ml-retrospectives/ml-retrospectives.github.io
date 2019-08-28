---
name: Submit Retrospective
about: Use this template to submit your retrospective
title: "[Retrospective]"
labels: ''
assignees: jzf2101, bouthilx, ryan-lowe, koustuvsinha

---

---
layout: retrospective
title:  A Quick Template for Writing Retrospectives
date:   2099-01-01
original_paper: A Quick Template for Writing Retrospectives
original_paper_link: https://ml-retrospectives.github.io/published_retrospectives/2099/retro-template/
original_paper_authors: Alfred Einstein, Mary Curry
retrospective_author: Alfred Einstein
---

### Paper TL;DR

Give a short description of the original paper. What claims did you make? What were the main results?


### Overall Outlook

Looking back on your paper, what are your thoughts about it now? What's been the impact of the paper in the community (if any)? Give an overview of the things you've learned about your paper since it's been published.


### Opportunities for Improvement

As described on the [how it works](https://ml-retrospectives.github.io/retrospectives/how/) page, there are many things you can talk about in a retrospective. We list three of them below, but you can write about all or none of these.  


1. **Flaws or mistakes in the paper’s methodology.**
For example, you discovered a bias in your dataset, or there was accidentally some overlap between validation and test, or there’s a weird bug that you don’t know the cause of and didn’t really figure out. Maybe you didn’t run enough seeds, and when you run more seeds your method isn’t actually that much better. *Basically, any way in which your scientific methodology was flawed or lacking.*

2. **Limitations in the applicability of the work.**
For example, you have reason to believe your approach doesn’t generalize well to other datasets, or your results are not robust to small changes in the experimental set-up. Maybe you tried switching from MLPs to LSTMs and everything broke. Maybe your classification model works better, but is less robust to adversarial attacks. *Basically, any way in which your approach was limited that you didn’t realize or acknowledge at the time.*

3. **Changes in understanding or intuition.**
For example, you have a simpler way to motivate your idea, or your intuition for why your model or approach works has changed. Maybe there are new aspects of your idea that you didn’t explore in the paper, but want to talk about, or new visualizations that improve understanding. These can be accompanied by additional (informal) results. You can also point to new work by others that is relevant to the paper. *Basically, anything that you’ve learned since writing the original paper that would be useful for others to know.*"

This *Opportunities for Improvement* section is a way to combine your thoughts about points 1) and 2). What could have been improved about your paper's methodology? What are some limitations of your work that you've learned since publishing? The more honest you can be about your thoughts, the more the community will benefit.  


#### Subsection

This is a subsection where you could describe one of the opportunities for improvement. It's nice to separate each opportunity for improvement by a different subsection, since this makes your retrospective more readable.

For example, I could have written some code like this, which would have made my approach more reproducible:

```python
for thing in range(list_of_things):
    if thing > other_thing:
        print("I'm inside a print statement!")
```

**Adding Photos**

You can add a photo by writing:

`![Image Description](Image_URL)`

e.g.

![Gaussians](https://upload.wikimedia.org/wikipedia/commons/9/9b/Gaussian_training_data.png)

Custom sizing and alignment can be included by adding the image using HTML:

`<p align=center><img src="image_url" width="x%"></p>`


<p align=center><img src="https://upload.wikimedia.org/wikipedia/commons/9/9b/Gaussian_training_data.png" width="30%"></p>

To upload an image, you can use services such as Dropbox or in a GitHub repo, using a path to your image.

- **Dropbox:** 

Create a [shared link](https://help.dropbox.com/files-folders/share/view-only-access) to your image and [replace the characters](https://support.zendesk.com/hc/en-us/articles/232005968-Embed-Dropbox-images-on-Help-Center-articles) `?dl=0` with `?raw=1`

`http://www.dropbox.com/{path_to_your_image}?raw=1`

- **GitHub:** 

Please include a link the the repo in the following format

`https://raw.github.com/{username}/{repository}/{branch}/{path}`
