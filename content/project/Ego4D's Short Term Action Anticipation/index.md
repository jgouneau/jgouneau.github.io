---
# Documentation: https://hugoblox.com/docs/managing-content/

title: "Ego4D's Short Term Action Anticipation"
summary: "A 6 months end of studies internship on the problem of Short Term Action Anticipation on egocentric videos from the Ego4D dataset. Use of a Transformer in place of a ROI Pooling operation earning a 3rd place on the public leaderboard of the associated challenge."
authors: [admin, Lai Xing Ng]
tags: [research, internship]
categories: [research, internship]
date: 2023-09-23T21:56:49+01:00

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: "Image credit: [**Ego4D**](https://ego4d-data.org/)"
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: "https://bitbucket.org/i2r-nglx/i2r-ego4d-sta/src/master/"
url_pdf: "project/ego4d/Internship_Report_ASTAR.pdf"
url_slides: "project/ego4d/end_of_studies_internship_defense.pdf"
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

## Summary
This work was led during my last year of engineering studies' 6 months internship at [I²R](https://www.a-star.edu.sg/i2r) (within [A*STAR](https://www.a-star.edu.sg/)), Singapore, under the supervision of Lai Xing Ng.
I studied the state of the art of action prediction on egocentric (1st person POV) videos, to then take the [Short Term Object Interaction Anticipation Challenge](https://eval.ai/web/challenges/challenge-page/1623/overview) from the dataset and benchamrk suite [Ego4D](https://ego4d-data.org/). I implemented InternVideo's solution[^1] using a Visual Transformer for video features extraction and a multimodal Transformer instead the initial ROI Pooling operation for Verb/Time To Contact (TTC) features extraction, achieving 3rd place on the [public leaderboard](https://eval.ai/web/challenges/challenge-page/1623/leaderboard/3910) with the following metrics (not publicly posted):

| mAP | Noun  | Noun_Verb | TTC  | Overall |
| --- | ----- | --------- | ---- | ------- |
|     | 26.15 | 11.25     | 9.22 | 4.75    | 

I performed this work with an unexpected additional 2 months of remote setup from France because of a delay in the work pass delivery from Singapore -- happening after an expected first month in remote for the theoretical preliminaries -- and during which I managed to adapt practical tasks to the setup. 

[^1]: Grauman, Kristen et al. “Ego4D: Around the World in 3,000 Hours of Egocentric Video.” _2022 IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)_ (2021): 18973-18990. https://arxiv.org/abs/2110.07058.